---
title: ABS (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ABS_TSQL
- ABS
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], positive
- values [SQL Server], absolute
- ABS function
- absolute positive value
ms.assetid: e2ea7a6d-3e2f-472c-afbc-437d3b835c03
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0bf5385adf8be483b569b7fc2f3213b73ba284b3
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948220"
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Математическая функция, возвращающая абсолютное (положительное) значение указанного числового выражения. (`ABS` изменяет отрицательные значения на положительные значения. `ABS` не влияет на ноль или положительные значения.)
  
![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Синтаксис  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>Аргументы  
*numeric_expression*  
Выражение категории точного числового или приблизительного числового типа данных.
  
## <a name="return-types"></a>Типы возвращаемых данных  
Возвращает тот же тип, что и аргумент *numeric_expression*.
  
## <a name="examples"></a>Примеры  
В этом примере показаны результаты применения функции `ABS` к трем различным числам.
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
Функция `ABS` может вызвать ошибку переполнения, если абсолютное значение числа превышает наибольшее число, которое может быть представлено указанным типом данных. Например, тип данных `int` поддерживает диапазон значений от `-2,147,483,648` до `2,147,483,647`. Расчет абсолютного значения для целого числа со знаком `-2,147,483,648` приводит к ошибке переполнения, так как его абсолютное значение превышает предел положительного диапазона для типа данных `int`.
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
Возвращает следующее сообщение об ошибке:
  
«Сообщение 8115, уровень 16, состояние 2, строка 3».
  
«Арифметическое переполнение при преобразовании выражения к типу данных int».

  
## <a name="see-also"></a>См. также раздел
[Функции CAST и CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Типы данных (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[Математические функции (Transact-SQL)](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Встроенные функции (Transact-SQL)](../../t-sql/functions/functions.md)
  
  

