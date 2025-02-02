---
title: StrToSet (многомерные Выражения) | Документация Майкрософт
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ee1e0cbeaa4e33be223e1b777ff243b5c3ef2d01
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150187"
---
# <a name="strtoset-mdx"></a>StrToSet (многомерные выражения)


  Возвращает набор, заданный строкой в формате Многомерных выражений.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Аргументы  
 *Set_Specification*  
 Допустимое строковое выражение, обозначающее (напрямую или косвенно) набор.  
  
## <a name="remarks"></a>Примечания  
 **StrToSet** функция возвращает набор, заданный строковым выражением. **StrToSet** функция обычно используется в определяемых пользователем функций для передачи спецификации набора из внешней функции обратно в инструкцию многомерных Выражений или параметризован запрос многомерных Выражений.  
  
-   При использовании флага CONSTRAINED спецификация набора должна содержать полные или неполные имена элементов или набор кортежей, содержащий имена членов полное или неполное, заключенных в фигурные скобки {}. Этот флаг используется для уменьшения риска атак, использующих вставку инструкций SQL в указанную строку. Если указана строка, которая не имеет названия элементов напрямую разрешаться в полное или неполное, возникает следующая ошибка: «Ограничения, установленные CONSTRAINED нарушены флаг в функции STRTOSET.»  
  
-   Если флаг CONSTRAINED не используется, заданную спецификацию набора можно разрешить в допустимое многомерное выражение, возвращающее набор.  
  
-   Дополнительные сведения о различиях между наборами и элементами см. в разделах «Использование выражений наборов» и «Использование выражений элементов».  
  
## <a name="examples"></a>Примеры  
 В следующем примере возвращается набор элементов иерархии атрибута State-Province, с использованием **StrToSet** функции. Указанная спецификация набора является допустимым многомерным выражением набора.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 В следующем примере возвращается сообщение об ошибке, поскольку используется флаг CONSTRAINED. Несмотря на то что заданная спецификация набора является допустимым многомерным выражением набора, она должна содержать полные или неполные имена элементов, поскольку указан флаг CONSTRAINED.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 В следующем примере возвращается мера Reseller Sales Amount для стран Germany и Canada. Указанная спецификация набора содержит полные имена элементов, как этого требует флаг CONSTRAINED.  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по функциям многомерных выражений (многомерные выражения)](../mdx/mdx-function-reference-mdx.md)  
  
  
