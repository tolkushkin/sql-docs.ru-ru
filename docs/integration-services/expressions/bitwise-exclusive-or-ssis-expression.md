---
title: ^ (битовое исключающее ИЛИ) (выражение служб SSIS) | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- bitwise exclusive OR (^)
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5aa564e8db4c3ba9d16fca1ad22c7f0b8ddfc74c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725624"
---
# <a name="-bitwise-exclusive-or-ssis-expression"></a>^ (битовое исключающее ИЛИ) (выражение служб SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Выполняет побитовую исключающую операцию ИЛИ для двух целочисленных значений. Она сравнивает каждый бит первого операнда с соответствующим битом второго операнда. Если один из битов равен 0, а второй равен 1, соответствующий бит результата устанавливается в 1. Если оба бита равны 0 или оба бита равны 1, соответствующий бит результата равен 0.  
  
 Оба условия должны относиться либо к целым числам со знаком, либо к беззнаковым целым числам.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## <a name="arguments"></a>Аргументы  
 *integer_expression1, integer_expression2*  
 Любое допустимое выражение: либо целое число со знаком, либо беззнаковое целое число. Дополнительные сведения см. в разделе [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Типы результата  
 Определяются типами данных обоих аргументов. Дополнительные сведения см. в разделе [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Remarks  
 Если значение любого из условий — NULL, то результат выражения тоже будет NULL.  
  
## <a name="expression-examples"></a>Примеры выражений  
 Этот пример выполняет битовую монопольную операцию ИЛИ над переменными **NumberA** и **NumberB**. **NumberA** содержит 3 (00000011), а **NumberB** — 7 (00000111).  
  
```  
@NumberA ^ @NumberB  
```  
  
 Результатом вычисления выражения будет 4 (00000100).  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000100  
  
 Этот пример производит побитовую исключающую операцию ИЛИ между столбцами **ReorderPoint** и **SafetyStockLevel** .  
  
```  
ReorderPoint ^ SafetyStockLevel  
```  
  
 Если **ReorderPoint** имеет значение 10, а **SafetyStockLevel** — значение 8, результат вычисления выражения равен 2 (00000010).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00000010  
  
 Этот пример выполняет побитовую исключающую операцию ИЛИ между двумя целыми числами.  
  
```  
3 ^ 5   
```  
  
 Результатом выполнения выражения будет 6 (00000110).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000110  
  
## <a name="see-also"></a>См. также:  
 [&#124;&#124; (логическое ИЛИ) (выражение служб SSIS)](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [&#124; (битовое включающее ИЛИ) (выражение служб SSIS)](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [Очередность и ассоциативность операторов](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Операторы (выражение служб SSIS)](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
