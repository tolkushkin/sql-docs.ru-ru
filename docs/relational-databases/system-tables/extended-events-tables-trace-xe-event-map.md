---
title: trace_xe_event_map (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_xe_event_map_TSQL
- trace_xe_event_map
dev_langs:
- TSQL
helpviewer_keywords:
- trace_xe_event_map
- extended events [SQL Server], tables
ms.assetid: 537aa292-3540-47e8-be28-56dc01abc343
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc823459c701bd0045e594f753a803a0a092a244
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62817110"
---
# <a name="extended-events-tables---tracexeeventmap"></a>Таблицы расширенных событий — trace_xe_event_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Содержит одну строку для каждого события из числа расширенных событий, сопоставленного с классом событий трассировки SQL. Эта таблица хранится в базе данных master в схеме sys.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|trace_event_id|**smallint**|Идентификатор сопоставленного класса событий трассировки SQL.|  
|package_name|**nvarchar(60)**|Имя пакета расширенных событий, в котором находится сопоставленное событие.|  
|xe_event_name|**nvarchar(60)**|Имя события расширенных событий, которое сопоставлено с классом событий трассировки SQL.|  
  
## <a name="remarks"></a>Примечания  
 Чтобы выявить события расширенных событий, эквивалентные классам событий трассировки SQL, можно использовать следующий запрос:  
  
```  
SELECT te.name, xe.package_name, xe.xe_event_name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NOT NULL  
```  
  
 Не все классы событий имеют эквивалентные расширенные события. Для перечисления классов событий, не имеющих эквивалентных расширенных событий, можно использовать следующий запрос.  
  
```  
SELECT te.trace_event_id, te.name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NULL  
```  
  
 Большинство возвращенных в ответ на предыдущий запрос классов событий связаны с аудитом. Для аудита рекомендуется использовать [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit использует расширенные события в помощь при создании аудита. Дополнительные сведения см. в статье [Подсистема аудита SQL Server (ядро СУБД)](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>См. также  
 [trace_xe_action_map (Transact-SQL)](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)  
  
  
