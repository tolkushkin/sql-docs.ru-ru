---
title: LAST_VALUE (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LAST_VALUE
- LAST_VALUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- analytic functions, LAST_VALUE
- LAST_VALUE function
ms.assetid: fd833e34-8092-42b7-80fc-95ca6b0eab6b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 04566cfdaf5fe3bda557d38ca47122ca5dae1814
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948769"
---
# <a name="lastvalue-transact-sql"></a>LAST_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  Возвращает последнее значение из упорядоченного набора значений в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
LAST_VALUE ( [ scalar_expression ] )   
    OVER ( [ partition_by_clause ] order_by_clause rows_range_clause )   
```  
  
## <a name="arguments"></a>Аргументы  
 *scalar_expression*  
 Возвращаемое значение. *scalar_expression* может быть столбцом, вложенным запросом или другим выражением, результатом вычисления которого является единичное значение. Другие аналитические функции использовать нельзя.  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause* [ *rows_range_clause* ] **)**  
 *partition_by_clause* делит результирующий набор, полученный с помощью предложения FROM, на секции, к которым применяется функция. Если этот параметр не указан, функция обрабатывает все строки результирующего набора запроса как отдельные группы.  
  
 *order_by_clause* определяет порядок данных перед применением функции. Аргумент *order_by_clause* является обязательным. *rows_range_clause* еще больше ограничивает строки в пределах секции, задавая начальную и конечную точки. Дополнительные сведения см. в статье [Предложение OVER (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 Тот же тип, что и *scalar_expression*.  
  
## <a name="general-remarks"></a>Общие замечания  
 Функция LAST_VALUE не детерминирована. Дополнительные сведения см. в разделе [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-using-lastvalue-over-partitions"></a>A. Использование LAST_VALUE для секций  
 В следующем примере показано возвращение даты найма последнего сотрудника каждого отдела для указанной заработной платы (Rate). Предложение PARTITION BY разделяет сотрудников по отделам, а функция LAST_VALUE применяется к каждой секции в отдельности. Предложение ORDER BY, указанное в предложении OVER, определяет логический порядок, в котором функция LAST_VALUE применяется к строкам каждой секции.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate, HireDate,   
    LAST_VALUE(HireDate) OVER (PARTITION BY Department ORDER BY Rate) AS LastValue  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
INNER JOIN HumanResources.EmployeePayHistory AS eph    
    ON eph.BusinessEntityID = edh.BusinessEntityID  
INNER JOIN HumanResources.Employee AS e  
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department                  LastName                Rate         HireDate     LastValue  
--------------------------- ----------------------- ------------ ----------   ----------  
Document Control            Chai                    10.25        2003-02-23   2003-03-13  
Document Control            Berge                   10.25        2003-03-13   2003-03-13  
Document Control            Norred                  16.8269      2003-04-07   2003-01-17  
Document Control            Kharatishvili           16.8269      2003-01-17   2003-01-17  
Document Control            Arifin                  17.7885      2003-02-05   2003-02-05  
Information Services        Berg                    27.4038      2003-03-20   2003-01-24  
Information Services        Meyyappan               27.4038      2003-03-07   2003-01-24  
Information Services        Bacon                   27.4038      2003-02-12   2003-01-24  
Information Services        Bueno                   27.4038      2003-01-24   2003-01-24  
Information Services        Sharma                  32.4519      2003-01-05   2003-03-27  
Information Services        Connelly                32.4519      2003-03-27   2003-03-27  
Information Services        Ajenstat                38.4615      2003-02-18   2003-02-23  
Information Services        Wilson                  38.4615      2003-02-23   2003-02-23  
Information Services        Conroy                  39.6635      2003-03-08   2003-03-08  
Information Services        Trenary                 50.4808      2003-01-12   2003-01-12  
  
```  
  
### <a name="b-using-firstvalue-and-lastvalue-in-a-computed-expression"></a>Б. Использование функций FIRST_VALUE и LAST_VALUE в вычисляемом выражении  
 В следующем примере с помощью функций FIRST_VALUE и LAST_VALUE, указанных в вычисляемых выражениях, показывается разница между значением квоты продаж для текущего квартала и для первого и последнего квартала года соответственно для данного числа сотрудников. Функция FIRST_VALUE возвращает значение квоты продаж за первый квартал года, затем вычитает его из значения квоты продаж за текущий квартал. Итог возвращается в производном столбце с именем DifferenceFromFirstQuarter. За первый квартал года значение столбца DifferenceFromFirstQuarter составляет 0. Функция LAST_VALUE возвращает значение квоты продаж за последний квартал года, затем вычитает его из значения квоты продаж за текущий квартал. Итог возвращается в производном столбце с именем DifferenceFromLastQuarter. За последний квартал года значение столбца DifferenceFromLastQuarter составляет 0.  
  
 Предложение RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING необходимо в этом примере для ненулевых значений, возвращаемых в столбце DifferenceFromLastQuarter, как показано ниже. Диапазоном по умолчанию является RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW. В этом примере результатом использования указанного диапазона по умолчанию (если не включать диапазон, будет использоваться диапазон по умолчанию) будет возврат нулей в столбце DifferenceFromLastQuarter. Дополнительные сведения см. в статье [Предложение OVER (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
SELECT BusinessEntityID, DATEPART(QUARTER,QuotaDate)AS Quarter, YEAR(QuotaDate) AS SalesYear,   
    SalesQuota AS QuotaThisQuarter,   
    SalesQuota - FIRST_VALUE(SalesQuota)   
        OVER (PARTITION BY BusinessEntityID, YEAR(QuotaDate)   
              ORDER BY DATEPART(QUARTER,QuotaDate) ) AS DifferenceFromFirstQuarter,   
    SalesQuota - LAST_VALUE(SalesQuota)   
        OVER (PARTITION BY BusinessEntityID, YEAR(QuotaDate)   
              ORDER BY DATEPART(QUARTER,QuotaDate)   
              RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING ) AS DifferenceFromLastQuarter   
FROM Sales.SalesPersonQuotaHistory   
WHERE YEAR(QuotaDate) > 2005   
AND BusinessEntityID BETWEEN 274 AND 275   
ORDER BY BusinessEntityID, SalesYear, Quarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Quarter     SalesYear   QuotaThisQuarter      DifferenceFromFirstQuarter DifferenceFromLastQuarter  
---------------- ----------- ----------- --------------------- --------------------------- -----------------------  
274              1           2006        91000.00              0.00                        -63000.00  
274              2           2006        140000.00             49000.00                    -14000.00  
274              3           2006        70000.00              -21000.00                   -84000.00  
274              4           2006        154000.00             63000.00                    0.00  
274              1           2007        107000.00             0.00                        -9000.00  
274              2           2007        58000.00              -49000.00                   -58000.00  
274              3           2007        263000.00             156000.00                   147000.00  
274              4           2007        116000.00             9000.00                     0.00  
274              1           2008        84000.00              0.00                        -103000.00  
274              2           2008        187000.00             103000.00                   0.00  
275              1           2006        502000.00             0.00                        -822000.00  
275              2           2006        550000.00             48000.00                    -774000.00  
275              3           2006        1429000.00            927000.00                   105000.00  
275              4           2006        1324000.00            822000.00                   0.00  
275              1           2007        729000.00             0.00                        -489000.00  
275              2           2007        1194000.00            465000.00                   -24000.00  
275              3           2007        1575000.00            846000.00                   357000.00  
275              4           2007        1218000.00            489000.00                   0.00  
275              1           2008        849000.00             0.00                        -20000.00  
275              2           2008        869000.00             20000.00                    0.00  
  
(20 row(s) affected)  
  
```  
  
  
