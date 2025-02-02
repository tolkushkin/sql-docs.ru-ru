---
title: DROP TYPE (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP TYPE
- DROP_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [SQL Server], deleting
- UDTs [SQL Server], deleting
- alias data types [SQL Server], removing
- DROP TYPE statement
ms.assetid: 11bf83f9-0718-4238-a835-83d2eb14ae7b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b6416febd415ef75f2455a55c14c2e220c4b5b0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62681523"
---
# <a name="drop-type-transact-sql"></a>DROP TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Удаляет псевдоним типа данных или пользовательский тип данных среды CLR из текущей базы данных.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>Аргументы  
 *IF EXISTS*  
 **Применимо к**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (с [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] до [текущей версии](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Условное удаление таблицы только в том случае, если она уже существует.  
  
 *schema_name*  
 Имя схемы, к которой относится тип псевдонима или определяемый пользователем тип.  
  
 *type_name*  
 Имя псевдонима типа данных или пользовательского типа, который необходимо удалить.  
  
## <a name="remarks"></a>Примечания  
 Инструкция DROP TYPE не будет выполняться, если справедливо что-либо из перечисленного ниже.  
  
-   В базе данных есть таблицы, содержащие столбцы с псевдонимом типа данных или определяемым пользователем типом данных. Сведения о столбцах с псевдонимом типа данных или пользовательским типом данных можно получить с помощью запроса к представлению каталога [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) или [sys.column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md).  
  
-   На псевдоним типа данных или пользовательский тип данных ссылаются определения вычисляемых столбцов, ограничений CHECK, привязанных к схеме представлений и функций. Сведения о данных ссылках можно получить с помощью запроса к представлению каталога [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md).  
  
-   В базе данных созданы функции, хранимые процедуры или триггеры, и эти процедуры используют переменные и параметры с псевдонимом типа данных или пользовательским типом данных. Сведения о параметрах псевдонима типа данных или определяемого пользователем типа данных можно получить с помощью запроса к представлению каталога [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) или [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md).  
  
## <a name="permissions"></a>Разрешения  
 Требует либо разрешения CONTROL на *type_name*, либо разрешения ALTER на *schema_name*.  
  
## <a name="examples"></a>Примеры  
 В следующем примере используется тип данных с названием `ssn`, уже созданный в текущей базе данных.  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a>См. также  
 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
