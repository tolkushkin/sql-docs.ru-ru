---
title: Образец таблицы HumanResources.myTeam (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 19ac990e7288885c2fd29c8114837be24dae9a88
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2019
ms.locfileid: "64946186"
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>Образец таблицы HumanResources.myTeam (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Большинству примеров кода в разделе [Импорт и экспорт больших массивов данных](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) требуется специальная учебная таблица **myTeam**. Перед выполнением примеров необходимо создать таблицу **myTeam** в схеме **HumanResources** базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] — один из образцов баз данных в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Таблица **myTeam** содержит следующие столбцы.  
  
|Столбец|Тип данных|Допускает значения NULL|Описание|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|**smallint**|Нет|Первичный ключ для строк таблицы. Идентификатор сотрудника — члена команды.|  
|**Название**|**nvarchar(50)**|Нет|Имя члена команды.|  
|**Title**|**nvarchar(50)**|Допускает значения NULL|Должность, которую сотрудник занимает в команде.|  
|**Историческая справка**|**nvarchar(50)**|Нет|Дата и время последнего обновления строки (по умолчанию)|  
  
**Для создания таблицы HumanResources.myTeam**  
  
-   Используйте следующие инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```sql
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
**Для заполнения таблицы HumanResources.myTeam**  
  
-   Чтобы вставить в таблицу две строки, выполните следующие инструкции `INSERT` .  
  
    ```sql
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  В этих инструкциях пропущен четвертый столбец таблицы `Background`. У него есть значение по умолчанию. Если не указывать этот столбец в инструкции `INSERT` , поле останется пустым.  
  
## <a name="see-also"></a>См. также:  
 [Массовый импорт и экспорт данных (SQL Server)](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
