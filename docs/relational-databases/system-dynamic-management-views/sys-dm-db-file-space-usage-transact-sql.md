---
title: sys.dm_db_file_space_usage (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_file_space_usage
- sys.dm_db_file_space_usage_TSQL
- sys.dm_db_file_space_usage
- dm_db_file_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_file_space_usage dynamic management view
ms.assetid: 148a5276-a8d5-49d2-8146-3c63d24c2144
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b803b86c216d877c0e056dd4892931575ca91010
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62741940"
---
# <a name="sysdmdbfilespaceusage-transact-sql"></a>sys.dm_db_file_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает сведения о пространстве, используемом каждым файлом базы данных.  
  
> [!NOTE]  
>  Вызывать его из [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] или [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], используйте имя **sys.dm_pdw_nodes_db_file_space_usage**.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|Идентификатор базы данных.|  
|file_id|**smallint**|Идентификатор файла.<br /><br /> file_id сопоставляется с file_id в [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) и с fileid в [sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md).|  
|filegroup_id|**smallint**|**Применимо к**: с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> FILEGROUP_ID.|  
|total_page_count|**bigint**|**Применимо к**: с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Общее число страниц в файле.|  
|allocated_extent_page_count|**bigint**|**Применимо к**: с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Общее количество страниц в несвободных экстентах файла.|  
|unallocated_extent_page_count|**bigint**|Общее количество страниц в свободных экстентах файла.<br /><br /> Неиспользованные страницы в размещенные экстенты не включаются.|  
|version_store_reserved_page_count|**bigint**|Общее количество страниц в однородных экстентах, размещенных для хранилища версий. Страницы хранилища версий никогда не размещаются из смешанных экстентов.<br /><br /> IAM-страницы не включаются, так как они всегда размещаются из смешанных экстентов. PFS-cтраницы включаются, если они размещаются из однородного экстента.<br /><br /> Дополнительные сведения см. в разделе [sys.dm_tran_version_store (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md).|  
|user_object_reserved_page_count|**bigint**|Общее количество страниц, выделенных из однородных экстентов для пользовательских объектов в базе данных. Неиспользуемые страницы из распределенного экстента включаются в счет.<br /><br /> IAM-страницы не включаются, так как они всегда размещаются из смешанных экстентов. PFS-cтраницы включаются, если они размещаются из однородного экстента.<br /><br /> Можно использовать столбец total_pages в [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) представления для возврата счетчика зарезервированных страниц каждой единицы распределения в пользовательском объекте каталога. Однако учтите, что столбец total_pages включает IAM-страницы.|  
|internal_object_reserved_page_count|**bigint**|Общее количество страниц в однородном экстенте, размещенных для внутренних объектов в файле. Неиспользуемые страницы из распределенного экстента включаются в счет.<br /><br /> IAM-страницы не включаются, так как они всегда размещаются из смешанных экстентов. PFS-cтраницы включаются, если они размещаются из однородного экстента.<br /><br /> Не существует представления каталога или объекта DMO, возвращающего счетчик страниц каждого внутреннего объекта.|  
|mixed_extent_page_count|**bigint**|Общее количество размещенных и освобожденных страниц в размещенном смешанном экстенте. Смешанный экстент содержит страницы, размещенные для различных объектов. Этот счетчик включает все IAM-страницы в файле.|
|modified_extent_page_count|**bigint**|**Область применения**: с [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] с пакетом обновления 2 (SP2) по [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br />Общее число страниц, измененных в размещенных экстентах файла с момента последнего полного резервного копирования. Число измененных страниц можно использовать для отслеживания объема разностных изменений в базе данных с момента последнего полного резервного копирования, чтобы решить, если разностная резервная копия требуется.|
|pdw_node_id|**int**|**Применяется к**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Идентификатор для узла, это распределение является на.|  
|distribution_id|**int**|**Применяется к**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Уникальный числовой идентификатор, связанная с распределением.|  
  
## <a name="remarks"></a>Примечания  
 Счетчики страниц всегда находятся на уровне экстента. Поэтому значения счетчиков страниц всегда будут кратными восьми. Экстенты, содержащие страницы глобальной карты распределения (GAM) и общей глобальной карты распределения (SGAM), являются размещенными однородными экстентами. Они не включаются в вышеописанные счетчики страниц. Дополнительные сведения о страницах и экстентах см. в разделе [страниц и экстентов руководство по архитектуре](../../relational-databases/pages-and-extents-architecture-guide.md). 
  
 Содержание текущего хранилища версий находится в [sys.dm_tran_version_store](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md). Страницы хранилища версий отслеживаются на уровне файла вместо уровня сеанса и уровня задачи, потому что они являются глобальными ресурсами. Сеанс может создавать версии, но версии не могут быть удалены, когда сеанс заканчивается. При очистке хранилища версий необходимо рассмотреть наиболее долго выполняющуюся транзакцию, которой нужен доступ к определенной версии. Наиболее долго выполняющаяся транзакция, связанные с очисткой хранилища версий может быть найдена путем просмотра столбца elapsed_time_seconds в [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md).  
  
 Частые изменения в столбце mixed_extent_page_count могут указывать на затрудненное использование SGAM-страниц. Когда это происходит, можно обнаружить много ожиданий PAGELATCH_UP, в которых ресурсом ожидания является SGAM-страница. Дополнительные сведения см. в разделе [sys.dm_os_waiting_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md), [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md), и [sys.dm_os_latch_ Статистика &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md).  
  
## <a name="user-objects"></a>Пользовательские объекты  
 Следующие объекты включаются в счетчики страниц пользовательских объектов.  
  
-   Пользовательские таблицы и индексы  
  
-   Системные таблицы и индексы  
  
-   Глобальные временные таблицы и индексы  
  
-   Локальные временные таблицы и индексы  
  
-   Табличные переменные  
  
-   Таблицы, возвращаемые в функциях с табличным значением  
  
## <a name="internal-objects"></a>Внутренние объекты  
 Внутренние объекты находятся только в базе данных tempdb. Следующие объекты включаются в счетчики страниц внутренних объектов:  
  
-   рабочие таблицы для выполнения операций с курсорами и буферами, а также для хранения временных больших объектов (LOB);  
  
-   рабочие файлы для таких операций, как хэш-соединение  
  
-   Сортировки  
  
## <a name="relationship-cardinalities"></a>Количество элементов связей  
  
|От|Чтобы|Связь|  
|----------|--------|------------------|  
|sys.dm_db_file_space_usage.database_id, file_id|sys.dm_io_virtual_file_stats.database_id, file_id|Один к одному|  
  
## <a name="permissions"></a>Разрешения

На [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], требуется `VIEW SERVER STATE` разрешение.   
На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], требуется `VIEW DATABASE STATE` разрешение в базе данных.   

## <a name="examples"></a>Примеры  
  
### <a name="determing-the-amount-of-free-space-in-tempdb"></a>Определение объема свободного пространства в базе данных tempdb  
 Следующий запрос возвращает общее количество свободных страниц и общий объем свободного пространства в мегабайтах (МБ) доступны во всех файлах в **tempdb**.  
  
```sql
USE tempdb;  
GO  
SELECT SUM(unallocated_extent_page_count) AS [free pages],   
(SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]  
FROM sys.dm_db_file_space_usage;  
```  

### <a name="determining-the-amount-of-space-used-by-user-objects"></a>Определение объема пространства, используемого пользовательскими объектами  
 Следующий запрос возвращает общее количество страниц, используемых пользовательскими объектами, и общее пространство в мегабайтах, используемое пользовательскими объектами в базе данных tempdb.  
  
```sql  
USE tempdb;  
GO  
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],  
(SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]  
FROM sys.dm_db_file_space_usage;
```  
  
## <a name="see-also"></a>См. также  
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Динамические административные представления, относящиеся к базе данных &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_session_space_usage (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
