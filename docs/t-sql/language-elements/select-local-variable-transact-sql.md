---
title: SELECT @local_variable (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- variable_TSQL
- '@loca_variable'
- '@local'
- variable
- '@loca_variable_TSQL'
- '@local_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- variables [SQL Server], assigning
- SELECT statement [SQL Server], @local_variable
- '@local_variable'
- local variables [SQL Server]
ms.assetid: 8e1a9387-2c5d-4e51-a1fd-a2a95f026d6f
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current ||>= sql-server-2016 ||= azure-sqldw-latest||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 3ea8dffc7256d08788b2a3b12812cd1f6e8f9cbd
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2019
ms.locfileid: "65981862"
---
# <a name="select-localvariable-transact-sql"></a>SELECT @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Присваивает локальную переменную значению выражения.  
  
 Для присваивания переменных рекомендуется использовать инструкцию [SET @local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md) вместо SELECT @*local_variable*.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
SELECT { @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression } 
    [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Аргументы  
@*local_variable*  
 Это объявленная переменная, которой должно быть присвоено значение.  
  
{= | += | -= | \*= | /= | %= | &= | ^= | |= }   
Присвоить значение справа переменной слева.  
  
Составной оператор присваивания:  
  |оператор |действие |   
  |-----|-----|  
  | = | Присваивает следующее за ним выражение переменной. |  
  | += | Сложение и присваивание |   
  | -= | Вычитание и присваивание |  
  | \*= | Умножение и присваивание |  
  | /= | Деление и присваивание |  
  | %= | Остаток от деления и присваивание |  
  | &= | Выполнение побитовой операции AND и присваивание |  
  | ^= | Выполнение побитовой операции XOR и присваивание |  
  | \|= | Выполнение побитовой операции OR и присваивание |  
  
 *expression*  
 Любое допустимое выражение [expression](../../t-sql/language-elements/expressions-transact-sql.md). В их число также входит скалярный вложенный запрос.  
  
## <a name="remarks"></a>Remarks  
 SELECT @*local_variable* обычно используется для возвращения одиночного значения в переменную. Однако, если аргумент *expression* является именем столбца, может вернуться несколько значений. Если инструкция SELECT возвращает более одного значения, переменной присваивается последнее возвращенное значение.  
  
 Если инструкция SELECT не возвращает ни одной строки, переменная сохраняет свое текущее значение. Если аргумент *expression* является скалярным вложенным запросом, который не возвращает значений, переменная принимает значение NULL.  
  
 Одна инструкция SELECT может инициализировать несколько локальных переменных.  
  
> [!NOTE]  
>  Инструкция SELECT, содержащая назначение переменной, не может быть использована для выполнения операций по получению типичного результирующего набора.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-use-select-localvariable-to-return-a-single-value"></a>A. Используйте инструкцию SELECT @local_variable для возвращения одиночного значения  
 В следующем примере переменной `@var1` присвоено значение `Generic Name`. Запрос к таблице `Store` не возвращает строк, потому что в ней отсутствует значение, указанное для `CustomerID`. Переменная сохраняет значение `Generic Name`.  
  
```sql  
-- Uses AdventureWorks    
  
DECLARE @var1 varchar(30);         
SELECT @var1 = 'Generic Name';         
SELECT @var1 = Name         
FROM Sales.Store         
WHERE CustomerID = 1000 ;        
SELECT @var1 AS 'Company Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Company Name  
 ------------------------------  
 Generic Name  
 ```  
  
### <a name="b-use-select-localvariable-to-return-null"></a>Б. Используйте инструкцию SELECT @local_variable для возвращения значения NULL  
 В следующем примере вложенный запрос используется для присвоения значения `@var1`. Так как значение, заданное для `CustomerID`, не существует, вложенный запрос не возвращает значение и переменная принимает значение `NULL`.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @var1 varchar(30)   
SELECT @var1 = 'Generic Name'   
SELECT @var1 = (SELECT Name   
FROM Sales.Store   
WHERE CustomerID = 1000)   
SELECT @var1 AS 'Company Name' ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Company Name  
----------------------------  
NULL  
```  
  
## <a name="see-also"></a>См. также:  
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Выражения (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Составные операторы (Transact-SQL)](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
  
  
