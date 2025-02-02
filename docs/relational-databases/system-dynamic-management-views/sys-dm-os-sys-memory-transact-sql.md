---
title: sys.dm_os_sys_memory (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_sys_memory
- sys.dm_os_sys_memory_TSQL
- sys.dm_os_sys_memory
- dm_os_sys_memory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_memory dynamic management view
ms.assetid: 1ca58814-1caa-44c1-b307-ff0bdcbbef62
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4cea000b63948207626298c1f0c977ba22ec3865
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62636293"
---
# <a name="sysdmossysmemory-transact-sql"></a>sys.dm_os_sys_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Возвращает информацию о распределении памяти операционной системы.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] связывает и ограничен внешним распределением памяти на уровне операционной системы и физические ограничения базового оборудования. Определение общего состояния системы является важной частью процесса распределения памяти в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Вызывать его из [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] или [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], используйте имя **sys.dm_pdw_nodes_os_sys_memory**.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**total_physical_memory_kb**|**bigint**|Общий объем физической памяти, доступной операционной системе, в килобайтах (КБ).|  
|**available_physical_memory_kb**|**bigint**|Объем доступной физической памяти, в КБ.|  
|**total_page_file_kb**|**bigint**|Максимальный объем памяти, выделяемый операционной системой, в килобайтах (КБ).|  
|**available_page_file_kb**|**bigint**|Общий объем неиспользуемой памяти файла подкачки, в КБ.|  
|**system_cache_kb**|**bigint**|Общий объем памяти системного кэша, в КБ.|  
|**kernel_paged_pool_kb**|**bigint**|Общий объем пула ядра, разбитого на страницы, в КБ.|  
|**kernel_nonpaged_pool_kb**|**bigint**|Общий объем пула ядра, не разбитого на страницы, в КБ.|  
|**system_high_memory_signal_state**|**bit**|Состояние уведомления о достаточном объеме системной памяти. Значение 1 указывает на то, что сигнал о достаточном объеме памяти был задан Windows. Дополнительные сведения см. в разделе [CreateMemoryResourceNotification](https://go.microsoft.com/fwlink/?LinkId=82427) в библиотеке MSDN.|  
|**system_low_memory_signal_state**|**bit**|Состояние уведомления о недостаточном объеме системной памяти. Значение 1 указывает на то, что сигнал памяти о недостаточном объеме памяти был задан Windows. Дополнительные сведения см. в разделе [CreateMemoryResourceNotification](https://go.microsoft.com/fwlink/?LinkId=82427) в библиотеке MSDN.|  
|**system_memory_state_desc**|**nvarchar(256)**|Описание состояния памяти. См. таблицу ниже.|  
|**pdw_node_id**|**int**|**Применяется к**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Идентификатор для узла, это распределение является на.|  
  
|Условие|Значение|  
|---------------|-----------|  
|system_high_memory_signal_state = 1<br /><br /> и<br /><br /> system_low_memory_signal_state = 0|Достаточный объем доступной физической памяти|  
|system_high_memory_signal_state = 0<br /><br /> и<br /><br /> system_low_memory_signal_state = 1|недостаточный объем доступной физической памяти|  
|system_high_memory_signal_state = 0<br /><br /> и<br /><br /> system_low_memory_signal_state = 0|Загрузка физической памяти постоянна|  
|system_high_memory_signal_state = 1<br /><br /> и<br /><br /> system_low_memory_signal_state = 1|Загрузка физической памяти непостоянна<br /><br /> Сигналы о достаточном и недостаточном объеме памяти не могут появляться одновременно. Однако быстрые изменения на уровне операционной системы могут вызвать одновременное появление обоих сигналов. При появлении обоих сигналов расценивается как сообщение о переменном состоянии.|  
  
## <a name="permissions"></a>Разрешения  
 необходимо разрешение VIEW SERVER STATE на сервере.  
  
## <a name="see-also"></a>См. также  
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Динамические административные представления, относящиеся к операционной системе SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


