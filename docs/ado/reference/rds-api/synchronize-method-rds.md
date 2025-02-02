---
title: Synchronize-метод (RDS) | Документация Майкрософт
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d780c6140c1c1d09a21f7d643d7c274986b0268d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697262"
---
# <a name="synchronize-method-rds"></a>Метод Synchronize (служба удаленных рабочих столов)
Синхронизировать наборе записей с помощью базы данных, указанной в строке подключения для использования в ADO 2.5 и более поздних версий.  
  
> [!IMPORTANT]
>  Начиная с Windows 8 и Windows Server 2012, серверные компоненты служб удаленных рабочих СТОЛОВ, больше не включаются в операционной системе Windows (см. в разделе Windows 8 и [настольная книга по совместимости Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) для получения дополнительных сведений). Клиентские компоненты служб удаленных рабочих СТОЛОВ будет поддерживаться в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Приложения, использующие служб удаленных рабочих СТОЛОВ, следует перевести [WCF-сервиса данных](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>Параметры  
 *connectionString*  
 Строка, используемая для подключения к поставщику OLE DB, куда будут отправляться запрос. Если используется обработчик, обработчик может изменить или заменить строку подключения.  
  
 *HandlerString*  
 Строка определяет обработчик для использования с этого выполнения. Строка состоит из двух частей. Первая часть содержит имя (ProgID) обработчика для использования. Вторая часть строки содержит аргументы, передаваемые обработчику. Способ интерпретации строки аргументов — конкретного обработчика. Эти две части разделяются первого вхождения запятой в строку (несмотря на то, что аргументы строка может содержать дополнительные запятые). Аргументы являются необязательными.  
  
 *lSynchronizeOptions*  
 Битовая маска параметров синхронизации.  
  
 1 =*UpdateTransact* обновления базы данных, упаковываются в транзакции. Транзакция прерывается, если ни один из обновлений не подходит.  
  
 2 =*RefreshWithUpdate* причины строки состояния возвращается, когда ни одно *обновить* , ни *RefreshConflicts* имеет значение.  
  
 4 =*обновить* набор записей обновляется с использованием актуальных данных из базы данных. Ожидающие обновления не передаются в базу данных. Если этот бит не установлен, набор записей не обновляется и все имеющиеся обновления передаются в базу данных.  
  
 8 =*RefreshConflicts* все строки, содержащие ожидающие изменения не удалось обновить. Строки, которые не удалось обновить обновляются с использованием актуальных данных из базы данных.  
  
 *ppRecordset*  
 Указатель на набор записей для синхронизации.  
  
 *pStatusArray*  
 Значение variant, позволяет получить безопасный массив статусов строк для строк, затронутых при синхронизации. Не задано, если ни один из следующих параметров синхронизации заданы: *RefreshWithUpdate*, *обновить* и *RefreshConflicts*.  
  
 *lcid*  
 Код языка используется для построения все ошибки, возвращаемые в *pInformation*.  
  
 *pInformation*  
 Указатель на сведения ошибка, возвращенная **Execute**. Если значение равно NULL, возвращаются сведения об ошибке отсутствуют.  
  
## <a name="remarks"></a>Примечания  
 *HandlerString* параметр может иметь значение null. Что произойдет, в этом случае зависит от того, как настроен сервер служб удаленных рабочих СТОЛОВ. Обработчик строку «MSDFMAP.handler» указывает, что следует использовать обработчик предоставленный корпорацией Майкрософт (Msdfmap.dll). Обработчик строку «MASDFMAP.handler,sample.ini» указывает, что следует использовать обработчик Msdfmap.dll и что «sample.ini» аргумент должен передаваться обработчику. Затем Msdfmap.dll интерпретирует аргумент как направление, в которых будет производиться sample.ini Проверьте строки соединения и запроса.  
  
## <a name="applies-to"></a>Объект применения  
 [Объект DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


