---
title: sys.fulltext_index_columns (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c695997906aeb5c3d5181cc8683f8401adb5df17
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822932"
---
# <a name="sysfulltextindexcolumns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Содержит по одной строке для каждого столбца, являющегося частью полнотекстового индекса.    
 
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Идентификатор объекта, частью которого является этот столбец.|  
|**column_id**|**int**|Идентификатор столбца, который является частью полнотекстового индекса.|  
|**type_column_id**|**int**|Идентификатор столбца типа, который сохраняет предоставленные пользователем документа файл расширения — «.doc», «.xls» и так далее взятия документа в данной строке. Столбец типа указан только для тех столбцов, данные которых требуют фильтрации во время полнотекстового индексирования. Значение NULL, если не применимо. Дополнительные сведения см. в разделе [Настройка фильтров для поиска и управление ими](../../relational-databases/search/configure-and-manage-filters-for-search.md).|  
|**language_id**|**int**|Код языка, у которого средство разбиения по словам используется для индексации этого полнотекстового столбца.<br /><br /> 0 = нейтральный<br /><br /> Дополнительные сведения см. в разделе [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).|  
|**statistical_semantics**|**int**|1 = для этого столбца, помимо полнотекстового индексирования, включена статистическая семантика.|  
  
## <a name="permissions"></a>Разрешения  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Представления каталога объектов (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
