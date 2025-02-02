---
title: Cousin (многомерные Выражения) | Документация Майкрософт
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad604900ac31cbcfb7e9a68fba4241c5f539b491
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63284984"
---
# <a name="cousin-mdx"></a>Cousin (многомерные выражения)


  Возвращает дочерний элемент, позиция которого относительно родительского элемента совпадает с позицией заданного дочернего элемента.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>Аргументы  
 *Member_Expression*  
 Допустимое многомерное выражение, возвращающее элемент.  
  
 *Ancestor_Member_Expression*  
 Допустимое многомерное выражение элемента, возвращающее элемент-предок.  
  
## <a name="remarks"></a>Примечания  
 Функция обрабатывает порядок и положение элементов на уровнях. Если существуют две иерархии, первая из которых имеет четыре уровня, а вторая — пять, «кузен» третьего уровня первой иерархии находится на третьем уровне второй иерархии.  
  
## <a name="examples"></a>Примеры  
 В следующем примере возвращается родственный объект четвертого квартала 2002 финансового года, основанный на его предке на уровне года в 2003 финансовом году. Полученный родственный объект является четвертым кварталом 2003 финансового года.  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 В следующем примере возвращается родственный объект июля 2002 финансового года, основанный на его предке на уровне квартала в 2004 финансовом году (второй квартал). Полученный родственный объект является октябрем 2003 года.  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по функциям многомерных выражений (многомерные выражения)](../mdx/mdx-function-reference-mdx.md)  
  
  
