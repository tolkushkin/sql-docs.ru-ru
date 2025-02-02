---
title: Поддержка распределенных транзакций | Документация Майкрософт
description: Сеансы в драйвере OLE DB для SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 97c7c4744d21697620740d2a865e5e6a66558a0f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66766115"
---
# <a name="supporting-distributed-transactions"></a>Поддержка распределенных транзакций
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Потребители драйвера OLE DB для SQL Server могут использовать метод **ITransactionJoin::JoinTransaction** для участия в распределенных транзакциях, которыми управляет координатор распределенных транзакций (Майкрософт) (служба MS DTC).  
  
 Службы MS DTC предоставляют доступ к COM-объектам, которые позволяют клиентам запускать и участвовать в координированных транзакциях через несколько соединений с различными хранилищами данных. Для инициирования транзакции, драйвер OLE DB для SQL Server Потребитель использует MS DTC **ITransactionDispenser** интерфейс. Элемент **BeginTransaction** интерфейса **ITransactionDispenser** возвращает ссылку на объект распределенной транзакции. Эта ссылка передается в драйвер OLE DB для SQL Server с помощью **JoinTransaction**.  
  
 Службы MS DTC поддерживают асинхронную фиксацию и прерывание распределенных транзакций. Для уведомления о состоянии асинхронных транзакций потребитель реализует интерфейс **ITransactionOutcomeEvents** и подключает интерфейс к объекту транзакции MS DTC.  
  
 Для распределенных транзакций драйвер OLE DB для SQL Server реализует параметры **ITransactionJoin::JoinTransaction** описанным ниже образом.  
  
|Параметр|Описание|  
|---------------|-----------------|  
|*punkTransactionCoord*|Указатель на объект транзакции MS DTC.|  
|*IsoLevel*|Игнорировать драйвера OLE DB для SQL Server. Уровень изоляции для транзакций, координируемых с использованием служб MS DTC, определяется, когда пользователь получает объект транзакции от координатора MS DTC.|  
|*IsoFlags*|Должно быть равно 0. Драйвер OLE DB для SQL Server возвращает значение XACT_E_NOISORETAIN, если указано любое другое значение объектом-получателем.|  
|*POtherOptions*|В противном случае значение NULL, драйвер OLE DB для SQL Server требует, чтобы объект параметров с помощью интерфейса. Драйвер OLE DB для SQL Server возвращает XACT_E_NOTIMEOUT, если объект параметров *ulTimeout* не равен нулю. Драйвер OLE DB для SQL Server пропускает значение *szDescription* член.|  
  
 В этом примере осуществляется координирование транзакции с использованием координатора MS DTC.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*       pIDBCreateSession   = NULL;  
ITransactionJoin*       pITransactionJoin   = NULL;  
IDBCreateCommand*       pIDBCreateCommand   = NULL;  
IRowset*                pIRowset            = NULL;  
  
// Transaction dispenser and transaction from MS DTC.  
ITransactionDispenser*  pITransactionDispenser = NULL;  
ITransaction*           pITransaction       = NULL;  
  
    HRESULT             hr;  
  
// Get the command creation interface for the session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
// Get a transaction dispenser object from MS DTC and  
// start a transaction.  
if (FAILED(hr = DtcGetTransactionManager(NULL, NULL,  
    IID_ITransactionDispenser, 0, 0, NULL,  
    (void**) &pITransactionDispenser)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
if (FAILED(hr = pITransactionDispenser->BeginTransaction(  
    NULL, ISOLATIONLEVEL_READCOMMITTED, ISOFLAG_RETAIN_DONTCARE,  
    NULL, &pITransaction)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
  
// Join the transaction.  
if (FAILED(pIDBCreateCommand->QueryInterface(IID_ITransactionJoin,  
    (void**) &pITransactionJoin)))  
    {  
    // Process failure to get an interface, release any references, and  
    // then return.  
    }  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) pITransaction, 0, 0, NULL)))  
    {  
    // Process join failure, release any references, and then return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then abort.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, 0, 0)))  
        {  
        // Get error from failed commit.  
        //  
        // If a distributed commit fails, application logic could  
        // analyze failure and retry. In this example, terminate. The   
        // consumer must resolve this somehow.  
        pITransaction->Abort(NULL, FALSE, FALSE);  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Un-enlist from the distributed transaction by setting   
// the transaction object pointer to NULL.  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) NULL, 0, 0, NULL)))  
    {  
    // Process failure, and then return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>См. также:  
 [Transactions](../../oledb/ole-db-transactions/transactions.md)  
  
  
