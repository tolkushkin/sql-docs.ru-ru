---
title: SET IDENTITY_INSERT (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET IDENTITY_INSERT
- SET_IDENTITY_INSERT_TSQL
- IDENTITY_INSERT_TSQL
- IDENTITY_INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY_INSERT option
- SET IDENTITY_INSERT statement
- identity values [SQL Server], explicit values
- identity columns [SQL Server], explicit values
ms.assetid: a5dd49f2-45c7-44a8-b182-e0a5e5c373ee
author: CarlRabeler
ms.author: carlrab
manager: craigg
monkerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||=azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 2ba70fdf917fba3a8dbd730db7e8d9b89cd1b094
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65949018"
---
# <a name="set-identityinsert-transact-sql"></a>SET IDENTITY_INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Позволяет вставлять явные значения в столбец идентификаторов таблицы.  

 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
SET IDENTITY_INSERT [ [ database_name . ] schema_name . ] table_name { ON | OFF }  
```  
  
## <a name="arguments"></a>Аргументы  
 *database_name*  
 Имя базы данных, в которой находится указанная таблица.  
  
 *schema_name*  
 Имя схемы, которой принадлежит таблица.  
  
 *table_name*  
 Имя таблицы со столбцом идентификаторов.  
  
## <a name="remarks"></a>Remarks  
 В каждый момент времени только для одной таблицы в сеансе свойство IDENTITY_INSERT может принимать значение ON. Если у какой-то таблицы это свойство уже имеет значение ON и инструкция SET IDENTITY_INSERT ON адресована другой таблице, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вернет сообщение об ошибке, в котором будет сказано, что свойство SET IDENTITY_INSERT уже приняло значение ON, и приведено имя соответствующей таблицы.  
  
 Если вставляемое значение больше текущего значения идентификатора в данной таблице, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] автоматически будет использовать вставленное значение в качестве текущего.  
  
 Задание параметра SET IDENTITY_INSERT происходит во время выполнения или запуска инструкций, а не их синтаксического анализа.  
  
## <a name="permissions"></a>Разрешения  
 Пользователь должен быть владельцем таблицы или иметь разрешение ALTER на таблицу.  
  
## <a name="examples"></a>Примеры  
 В следующем примере создается таблица со столбцом идентификаторов, и показывается, как можно использовать параметр `SET IDENTITY_INSERT` для заполнения промежутков между значениями идентификаторов, вызванных выполнением инструкции `DELETE`.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create tool table.  
CREATE TABLE dbo.Tool(  
   ID INT IDENTITY NOT NULL PRIMARY KEY,   
   Name VARCHAR(40) NOT NULL  
);  
GO  
-- Inserting values into products table.  
INSERT INTO dbo.Tool(Name)   
VALUES ('Screwdriver')  
        , ('Hammer')  
        , ('Saw')  
        , ('Shovel');  
GO  
  
-- Create a gap in the identity values.  
DELETE dbo.Tool  
WHERE Name = 'Saw';  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
  
-- Try to insert an explicit ID value of 3;  
-- should return an error:
-- An explicit value for the identity column in table 'AdventureWorks2012.dbo.Tool' can only be specified when a column list is used and IDENTITY_INSERT is ON.
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
-- SET IDENTITY_INSERT to ON.  
SET IDENTITY_INSERT dbo.Tool ON;  
GO  
  
-- Try to insert an explicit ID value of 3.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
-- Drop products table.  
DROP TABLE dbo.Tool;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [Свойство IDENTITY (Transact-SQL)](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SCOPE_IDENTITY (Transact-SQL)](../../t-sql/functions/scope-identity-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [Инструкции SET (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
