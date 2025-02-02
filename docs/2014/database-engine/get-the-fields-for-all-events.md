---
title: Получение полей для всех событий | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], getting fields
- xe
ms.assetid: 4e4ee03f-5bca-42ed-a37c-db1c82e3aad2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0838367ad699c1278bb6ec42f28161ba76c6fd5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064791"
---
# <a name="get-the-fields-for-all-events"></a>получить поля для всех событий
  Выполнение этой задачи предполагает использование редактора запросов в [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 После выполнения инструкций данной процедуры на вкладке **Результаты** редактора запросов будут отображены следующие столбцы.  
  
-   package_name  
  
-   event_name  
  
-   event_field  
  
-   field_type  
  
-   column_type  
  
 Можно использовать приведенные выше сведения при настройке сеансов событий, в которых используются сегментированные цели. Дополнительные сведения см. в статье [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
## <a name="before-you-begin"></a>Перед началом работы  
 Перед созданием сеанса расширенных событий [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] рекомендуется выявить поля, связанные с этими событиями.  
  
## <a name="to-get-the-fields-for-all-events-using-query-editor"></a>Получение полей для всех событий с помощью редактора запросов  
  
-   В редакторе запросов выполните следующие инструкции.  
  
    ```  
    select p.name package_name, o.name event_name, c.name event_field, c.type_name field_type, c.column_type column_type  
    from sys.dm_xe_objects o  
    join sys.dm_xe_packages p  
          on o.package_guid = p.guid  
    join sys.dm_xe_object_columns c  
          on o.name = c.object_name  
    where o.object_type = 'event'  
    order by package_name, event_name  
    ```  
  
## <a name="see-also"></a>См. также  
 [sys.dm_xe_objects (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
