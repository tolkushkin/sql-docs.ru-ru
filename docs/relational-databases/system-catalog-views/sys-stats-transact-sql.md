---
title: sys.STATS (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.stats
- stats_TSQL
- sys.stats_TSQL
- stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.stats catalog view
ms.assetid: 42605c80-126f-460a-befb-a0b7482fae6a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5150dfbccb6998c69151ca4cf02d9fe88a222830
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62856015"
---
# <a name="sysstats-transact-sql"></a>sys.stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Содержит по одной строке для каждого объекта статистики, существующего для таблиц, индексов и индексированных представлений в базе данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Каждый индекс будет иметь соответствующую строку статистики с тем же именем и Идентификатором (**index_id** = **stats_id**), но не каждая строка статистики имеет соответствующий индекс.  
  
 Представление каталога [sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) содержит статистические данные для каждого столбца в базе данных. Дополнительные сведения о статистике см. в статье [Статистика](../../relational-databases/statistics/statistics.md).  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Идентификатор объекта, которому принадлежит статистика.|  
|**name**|**sysname**|Имя статистики. Уникален в пределах объекта.|  
|**stats_id**|**int**|Идентификатор статистики. Уникален в пределах объекта.<br /><br />Если статистика соответствует индексу, *stats_id* значение совпадает со значением *index_id* значение в [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) представления каталога.|  
|**auto_created**|**bit**|Указывает, была ли статистика создана автоматически [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = статистика не была автоматически создана [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = статистика была автоматически создана [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**user_created**|**bit**|Указывает, была ли статистика создана пользователем.<br /><br /> 0 = статистика не была создана пользователем.<br /><br /> 1 = статистика была создана пользователем.|  
|**no_recompute**|**bit**|Указывает, была ли статистика создана с помощью **NORECOMPUTE** параметр.<br /><br /> 0 = статистика не была создана с помощью **NORECOMPUTE** параметр.<br /><br /> 1 = Статистика была создана с **NORECOMPUTE** параметр.|  
|**has_filter**|**bit**|0 = Статистика не имеет фильтр и рассчитывается для всех строк.<br /><br /> 1 = Статистика имеет фильтр и рассчитывается только для строк, которые удовлетворяют определению фильтра.|  
|**filter_definition**|**nvarchar(max)**|Выражение для подмножества строк, включенного в отфильтрованную статистику.<br /><br /> NULL — неотфильтрованная статистика.|  
|**is_temporary**|**bit**|**Применимо к**: с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Указывает, является ли статистика временной. Временная статистика поддерживает базы данных-получатели [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], доступные только для чтения.<br /><br /> 0 = статистика не является временной.<br /><br /> 1 = статистика является временной.|  
|**is_incremental**|**bit**|**Применимо к**: с [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Указывает, создается ли статистика в добавочном виде.<br /><br /> 0 = статистика добавочная.<br /><br /> 1 = статистика недобавочная.|  
  
## <a name="permissions"></a>Разрешения  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Примеры  
 В ходе выполнения следующих примеров возвращаются все статистические данные и статистические столбцы для таблицы `HumanResources.Employee`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT s.name AS statistics_name  
      ,c.name AS column_name  
      ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('HumanResources.Employee');  
```  
  
## <a name="see-also"></a>См. также  
 [Представления каталога объектов (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Запросив системный каталог SQL Server часто задаваемые вопросы](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Статистика](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)
 

 
