---
title: PERCENTILE_DISC (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6a514a1d1e3db96e3943b600b3de17d2184e9955
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65943513"
---
# <a name="percentiledisc-transact-sql"></a>PERCENTILE_DISC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Вычисляет определенный процентиль для отсортированных значений из всего набора строк или в пределах определенных секций набора строк в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Для данного значения процентиля *P* функция PERCENTILE_DISC сортирует значения выражения в предложении ORDER BY. Затем она возвращает значение с наименьшим заданным значением CUME_DIST, которое (по отношению к той же спецификации сортировки), больше или равно *P*. Например, функция PERCENTILE_DISC (0.5) вычислит 50-й процентиль (то есть медиану) выражения. Функция PERCENTILE_DISC вычисляет процентиль на основе дискретного распределения значений столбца. Результат вычисления равен определенному значению из столбца.  
  
 ![Значок ссылки на статью](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Аргументы  
 *literal*  
 Процентиль, который необходимо вычислить. Значение должно находиться в диапазоне от 0.0 до 1,0.  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC)**  
 Указывает список значений, который следует отсортировать и по которому будет вычисляться процентиль. Разрешен только один аргумент *order_by_expression*. По умолчанию задан порядок сортировки по возрастанию. Список значений может быть любого из типов данных, которые допустимы для операции сортировки.  
  
 OVER **(** \<partition_by_clause>)**  
 Разделяет результирующий набор предложения FROM на секции, к которым применяется функция вычисления процентиля. Дополнительные сведения см. в статье [Предложение OVER (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md). В функции PERCENTILE_DISC нельзя указывать \<предложение ORDER BY>, а также \<строки или предложение диапазона>.  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 Тип возвращаемого значения определяется типом *order_by_expression*.  
  
## <a name="compatibility-support"></a>Поддержка совместимости  
 При уровне совместимости 110 и выше WITHIN GROUP является зарезервированным ключевым словом. Дополнительные сведения см. в разделе [Уровень совместимости инструкции ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="general-remarks"></a>Общие замечания  
 Все значения NULL, имеющиеся в наборе данных, игнорируются.  
  
 Функция PERCENTILE_DISC не детерминирована. Дополнительные сведения см. в разделе [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Примеры  
  
### <a name="basic-syntax-example"></a>Пример простого синтаксиса  

 В следующем примере функции PERCENTILE_CONT и PERCENTILE_DISC используются для определения медианной заработной платы сотрудников в каждом отделе. Они могут возвращать только разные значения.
* Функция PERCENTILE_CONT возвращает соответствующее значение, даже если оно не существует в наборе данных.
* Функция PERCENTILE_DISC возвращает фактическое значение набора.  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 Здесь приводится частичный результирующий набор.  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Примеры: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="basic-syntax-example"></a>Пример простого синтаксиса  

 В следующем примере функции PERCENTILE_CONT и PERCENTILE_DISC используются для определения медианной заработной платы сотрудников в каждом отделе. Они могут возвращать только разные значения.
* Функция PERCENTILE_CONT возвращает соответствующее значение, даже если оно не существует в наборе данных. 
* Функция PERCENTILE_DISC возвращает фактическое значение набора.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
       ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianCont  
       ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 Здесь приводится частичный результирующий набор.  
  
 ```
DepartmentName        MedianCont    MedianDisc  
--------------------   ----------   ----------  
Document Control       16.826900    16.8269  
Engineering            34.375000    32.6923  
Human Resources        17.427850    16.5865  
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>См. также:  
 [PERCENTILE_CONT (Transact-SQL)](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  


