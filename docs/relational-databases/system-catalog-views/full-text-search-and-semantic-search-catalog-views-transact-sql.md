---
title: Компонент Full-Text Search и семантический поиск каталога представления (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], full-text search
- full-text search [SQL Server], catalog views
- full-text indexes [SQL Server], catalog views
ms.assetid: b08ad2fd-e3d8-458f-96f1-678217e0f419
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 2183619c0519bd170a54a0a15450d45c062d96af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945582"
---
# <a name="full-text-search-and-semantic-search-catalog-views-transact-sql"></a>Представления каталога полнотекстового и семантического поиска (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  В этом разделе описываются представления каталога, содержащие сведения о полнотекстовых и семантических индексах.  
  
## <a name="full-text-search-catalog-views"></a>Представления каталога полнотекстового поиска (Transact-SQL)  
 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)  
 Содержит по строке для каждого полнотекстового каталога.  
  
 [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)  
 Возвращает строку для каждого типа документа, который является доступным для операций полнотекстового индексирования. Каждая строка представляет **IFilter** интерфейс, который зарегистрирован в экземпляре SQL Server.  
  
 [sys.fulltext_index_catalog_usages](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)  
 Возвращает строку для каждого полнотекстового каталога, ссылающегося на полнотекстовый индекс.  
  
 [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
 Содержит по одной строке для каждого столбца, являющегося частью полнотекстового индекса.  
  
 [sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)  
 Содержит строку для каждого фрагмента полнотекстового индекса в каждой таблице, содержащей полнотекстовый индекс.  
  
 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
 Содержит по одной строке для каждого полнотекстового индекса табличного объекта.  
  
 [sys.fulltext_languages](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)  
 Содержит одну строку для каждого языка, средства разбиения по словам которого зарегистрированы с помощью SQL Server. Каждая строка отображает код и имя языка.  
  
 [sys.fulltext_stoplists](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
 Содержит строку на каждый полнотекстовый список стоп-слов в базе данных.  
  
 [sys.fulltext_stopwords](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
 Содержит одну строку для каждого стоп-слова из всех списков стоп-слов в базе данных.  
  
 [sys.fulltext_system_stopwords](../../relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql.md)  
 Предоставляет доступ к системному списку стоп-слов.  
  
 [sys.registered_search_properties (Transact-SQL)](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)  
 Содержит строку для каждого свойства поиска, которое содержится в списке свойств поиска в текущей базе данных.  
  
 [sys.registered_search_property_lists (Transact-SQL)](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
 Содержит строку для каждого списка свойств поиска в текущей базе данных.  
  
## <a name="semantic-search-catalog-views"></a>Представления каталога семантического поиска (Transact-SQL)  
 [sys.fulltext_semantic_language_statistics_database (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)  
 Возвращает строку о базе данных статистики семантики языка, установленной на текущем экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [sys.fulltext_semantic_languages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)  
 Возвращает по одной строке для каждого языка, модель статистики которого зарегистрирована на экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Если языковая модель зарегистрирована, язык включается для семантического индексирования.  
  
## <a name="see-also"></a>См. также  
 [Системные представления &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Компонент Full-Text Search и семантический поиск динамические административные представления и функции &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
