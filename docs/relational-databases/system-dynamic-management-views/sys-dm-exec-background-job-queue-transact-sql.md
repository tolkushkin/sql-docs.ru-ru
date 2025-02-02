---
title: sys.dm_exec_background_job_queue (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 142329f80b55a18eb6724449f3e1ad68dfb72acb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013587"
---
# <a name="sysdmexecbackgroundjobqueue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает строку для каждого задания обработчика запросов, запланированного для асинхронного (фонового) выполнения.  
  
> **ПРИМЕЧАНИЕ.** Вызывать его из **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** или **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**, используйте имя **sys.dm_pdw_nodes_exec_background_job_queue**.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|Время добавления задания в очередь.|  
|**job_id**|**int**|Идентификатор задания.|  
|**database_id**|**int**|База данных, в которой должно быть выполнено задание.|  
|**object_id1**|**int**|Значение зависит от типа задания. Дополнительные сведения см. в разделе «Примечания».|  
|**object_id2**|**int**|Значение зависит от типа задания. Дополнительные сведения см. в разделе «Примечания».|  
|**object_id3**|**int**|Значение зависит от типа задания. Дополнительные сведения см. в разделе «Примечания».|  
|**object_id4**|**int**|Значение зависит от типа задания. Дополнительные сведения см. в разделе «Примечания».|  
|**error_code**|**int**|Код ошибки, если задание возвращается в очередь из-за сбоя. Это значение равно NULL, если задание приостановлено, не извлечено из очереди или завершено.|  
|**request_type**|**smallint**|Тип запроса задания.|  
|**retry_count**|**smallint**|Число возвратов задания в очередь из-за отсутствия ресурсов или по другим причинам.|  
|**in_progress**|**smallint**|Показывает, начато ли выполнение задания:<br /><br /> 1 = выполнение начато;<br /><br /> 0 = задание пока еще ожидает.|  
|**session_id**|**smallint**|Идентификатор сеанса.|  
|**pdw_node_id**|**int**|**Применяется к**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Идентификатор для узла, это распределение является на.|  
  
## <a name="permissions"></a>Разрешения

На [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], требуется `VIEW SERVER STATE` разрешение.   
На [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], требуется `VIEW DATABASE STATE` разрешение в базе данных.   
  
## <a name="remarks"></a>Примечания  
 Это представление возвращает сведения только для заданий асинхронного обновления статистики. Дополнительные сведения об асинхронном обновлении статистики см. в разделе [статистики](../../relational-databases/statistics/statistics.md).  
  
 Значения **object_id1** через **object_id4** зависят от типа запроса задания. Значение этих столбцов при разных типах заданий указано в следующей таблице.  
  
|Тип запроса|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|Асинхронное обновление статистики|Идентификатор таблицы или представления|Идентификатор статистики|Не используется|Не используется|  
  
## <a name="examples"></a>Примеры  
 В следующем примере возвращается целый ряд активных асинхронных заданий в фоновой очереди для каждой базы данных экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Динамические административные представления и функции, связанные с выполнением &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Статистика](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  



