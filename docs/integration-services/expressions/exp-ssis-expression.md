---
title: EXP (выражение служб SSIS) | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8ffe52a392dfec79afa301df7650cf73f2ad35ac
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725439"
---
# <a name="exp-ssis-expression"></a>EXP (выражение служб SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Возвращает значение экспоненты основания е числового выражения. Функция EXP дополняет действие функции LN и иногда называется обратным логарифмом.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>Аргументы  
 *numeric_expression*  
 Допустимое числовое выражение.  
  
## <a name="result-types"></a>Типы результата  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 Перед вычислением степени числовое выражение приводится к типу данных DT_R8. Дополнительные сведения см. в разделе [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Возвращаемый результат всегда является положительным числом.  
  
## <a name="expression-examples"></a>Примеры выражений  
 В этих примерах функция EXP применяется к положительным значениям, отрицательным значениям и к нулю.  
  
```  
EXP(74)  
```  
  
 Возвращает 1.373382979540176E+32.  
  
```  
EXP(-27)  
```  
  
 Возвращает 1.879528816539083E-12.  
  
```  
EXP(0)  
```  
  
 Возвращает значение 1.  
  
## <a name="see-also"></a>См. также:  
 [LOG (выражение служб SSIS)](../../integration-services/expressions/log-ssis-expression.md)   
 [Функции (выражение служб SSIS)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
