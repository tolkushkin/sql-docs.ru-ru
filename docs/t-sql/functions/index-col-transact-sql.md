---
title: INDEX_COL (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INDEX_COL_TSQL
- INDEX_COL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying column names
- INDEX_COL function
- viewing column names
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 4db1fb3b-e46f-43fb-b269-a5b6e8b39ed0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5dbf3bbd011838bc9c000f271317c86623251896
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65946342"
---
# <a name="indexcol-transact-sql"></a>INDEX_COL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Возвращает имя индексированного столбца. Возвращает NULL для XML-индексов.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
INDEX_COL ( '[ database_name . [ schema_name ] .| schema_name ]  
    table_or_view_name', index_id , key_id )   
```  
  
## <a name="arguments"></a>Аргументы  
 *database_name*  
 Имя базы данных.  
  
 *schema_name*  
 Имя схемы, которой принадлежит индекс.  
  
 *table_or_view_name*  
 Имя таблицы или индексированного представления. Аргумент *table_or_view_name* должен быть отделен одинарными кавычками и может полностью определяться именем базы данных и именем схемы.  
  
 *index_id*  
 Идентификатор индекса. Аргумент *index_ID* имеет тип **int**.  
  
 *key_id*  
 Позиция ключевого столбца индекса. Аргумент *key_ID* имеет тип **int**.  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 **nvarchar (128** **)**  
  
## <a name="exceptions"></a>Исключения  
 Возвращает значение NULL в случае ошибки или если участник не имеет разрешений для просмотра объекта.  
  
 Пользователь может просматривать только метаданные защищаемых объектов, которыми он владеет или на которые пользователю были предоставлены разрешения. Это означает, что встроенные функции по формированию метаданных, например INDEX_COL, могут вернуть значение NULL, если пользователь не имеет каких-либо разрешений на объект. Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-using-indexcol-to-return-an-index-column-name"></a>A. Использование INDEX_COL для возвращения имени столбца индекса  
 В приведенном ниже примере возвращаются имена двух ключевых столбцов в индексе `PK_SalesOrderDetail_SalesOrderID_LineNumber`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   
    INDEX_COL (N'AdventureWorks2012.Sales.SalesOrderDetail', 1,1) AS  
        [Index Column 1],   
    INDEX_COL (N'AdventureWorks2012.Sales.SalesOrderDetail', 1,2) AS  
        [Index Column 2]  
;  
GO  
```  
  
 Результирующий набор:  
  
```  
Index Column 1      Index Column 2  
-----------------------------------------------  
SalesOrderID        SalesOrderDetailID  
```  
  
## <a name="see-also"></a>См. также:  
 [Выражения (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Функции метаданных (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
