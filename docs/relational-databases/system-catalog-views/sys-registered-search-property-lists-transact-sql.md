---
title: sys.registered_search_property_lists (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- registered_search_property_lists_TSQL
- sys.registered_search_property_lists
- registered_search_property_lists
- sys.registered_search_property_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- sys.registered_search_property_lists catalog view
- search property lists [SQL Server], viewing
ms.assetid: 630d4caa-9bea-4cd3-a5b1-01098b0855fc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 89636150a5925d3f1d2c77d0462666d369492010
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2019
ms.locfileid: "64946503"
---
# <a name="sysregisteredsearchpropertylists-transact-sql"></a>sys.registered_search_property_lists (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Содержит строку для каждого списка свойств поиска в текущей базе данных.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|Идентификатор списка свойств.|  
|**name**|**sysname**|Имя списка свойств.|  
|**create_date**|**datetime**|Дата создания списка свойств.|  
|**modify_date**|**datetime**|Дата последнего изменения списка свойств с помощью инструкции ALTER.|  
|**principal_id**|**int**|Владелец списка свойств.|  
  
## <a name="remarks"></a>Примечания  
 Дополнительные сведения см. в статье [Поиск свойств документа с использованием списков свойств поиска](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="permissions"></a>Разрешения  
 Видимость метаданных в списке свойств поиска ограничивается свойствами, владельцем которых пользователь является или на которые ему было предоставлено разрешение REFERENCE.  
  
> [!NOTE]  
>  Владелец списка свойств поиска может предоставить разрешения REFERENCE и CONTROL на список. Пользователи с разрешением CONTROL также могут предоставлять разрешение REFERENCE другим пользователям.  
  
## <a name="examples"></a>Примеры  
 В следующем примере отображаются идентификаторы и имена списков свойств поиска в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT property_list_id, name FROM sys.registered_search_property_lists;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
  
