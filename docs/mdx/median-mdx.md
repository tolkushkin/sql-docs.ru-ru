---
title: Median (многомерные Выражения) | Документация Майкрософт
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e962507d6e437974708aa042919ea6fb7bd632d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048528"
---
# <a name="median-mdx"></a>Median (многомерные выражения)


  Возвращает медиант числового выражения, вычисляемого на наборе.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Median(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Аргументы  
 *Set_Expression*  
 Допустимое многомерное выражение, возвращающее набор.  
  
 *Numeric_Expression*  
 Допустимое числовое выражение (обычно многомерное выражение координат ячейки), возвращающее число.  
  
## <a name="remarks"></a>Примечания  
 Если числовое выражение указано, оно вычисляется для всех элементов набора и затем возвращается медиана вычислений. Если числовое выражение не указано, указанный набор вычисляется в текущем контексте элементов набора и возвращается медиана вычислений.  
  
 Медиана — это значение из середины набора упорядоченных чисел. (Не путайте медиана со средним значением, которое представляет собой сумму набора чисел, разделенную на их количество). Для определения медианы находится такое наименьшее значение, которое не превышает минимум половину всех значений набора. Если набор содержит нечетное количество чисел, медиана равняется одному значению. Если количество чисел четное, медиана равняется усредненному значению двух чисел посередине.  
  
> [!NOTE]  
>  Службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] не обрабатывают неопределенные значения при вычислении значения медианы для набора упорядоченных чисел.  
  
## <a name="example"></a>Пример  
 В следующем примере возвращается медиана сумм от продаж за месяц для каждого квартала и страны в кубе Adventure Works.  
  
```  
WITH MEMBER Measures.x AS Median   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по функциям многомерных выражений (многомерные выражения)](../mdx/mdx-function-reference-mdx.md)  
  
  
