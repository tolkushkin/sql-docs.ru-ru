---
title: Побитовые операторы (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 06/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8fd4a6fe9ba55aa3e30f0df94721c7aeeef225fa
ms.sourcegitcommit: 561cee96844b82ade6cf543a228028ad5c310768
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2019
ms.locfileid: "66506419"
---
# <a name="bitwise-operators-transact-sql"></a>побитовые операторы (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Побитовые операторы выполняют побитовые действия над двумя выражениями с любым типом данных, относящимся к категории типа данных integer.  
  Побитовые операторы преобразуют два целочисленных значения в двоичные разряды, выполняют операцию И, ИЛИ или НЕ с каждым разрядом и предоставляют результат. Затем результат преобразуется в целое число.  
  
  Например, целое число 170 преобразуется в двоичное число 1010 1010.
Целое число 75 преобразуется в двоичное число 0100 1011.

|оператор|побитовая операция|
|---- |---- |
|AND <br> Если оба бита в определенной позиции равны 1, результат равен 1. |1010 1010 = 170 <br>0100 1011 = 75 <br>-----------------  <br> 0000 1010 = 10 |
|OR <br> Если хотя бы один бит в определенной позиции равен 1, результат равен 1. |1010 1010 = 170 <br>0100 1011 = 75 <br>-----------------  <br> 1110 1011 = 235|
|NOT  <br> Меняет значение бита в каждой позиции на противоположное. |1010 1010 = 170 <br>----------------- <br>  0101 0101 =   85 |
  
См. следующие статьи:   
* [& (побитовое И)](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [&= (присваивание побитового И)](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124; (побитовое ИЛИ)](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124;= (присваивание побитового ИЛИ)](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ (побитовое исключающее ИЛИ)](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^= (присваивание побитового исключающего ИЛИ)](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ (побитовое НЕ)](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
 Операнды побитовых операторов могут принадлежать к любому из целочисленных типов данных или к категории типов данных "двоичная строка" (кроме типа данных **image**), однако оба операнда не могут относиться к типам данных из категории "двоичная строка". Следующая таблица показывает поддерживаемые типы данных операндов.  
  
|Левый операнд|Правый операнд|  
|------------------|-------------------|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint** или **tinyint**|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|**int**, **smallint**, **tinyint** или **bit**|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** или **varbinary**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** или **varbinary**|  
|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** или **varbinary**|  
|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** или **varbinary**|  
|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint** или **tinyint**|  
  
## <a name="see-also"></a>См. также:  
 [Операторы (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)   
 [Типы данных (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [Составные операторы (Transact-SQL)](../../t-sql/language-elements/compound-operators-transact-sql.md)
