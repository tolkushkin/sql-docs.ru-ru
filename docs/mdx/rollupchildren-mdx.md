---
title: RollupChildren (многомерные Выражения) | Документация Майкрософт
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5df035ab7ae2949164869536c498c341327916c3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149308"
---
# <a name="rollupchildren-mdx"></a>RollupChildren (многомерные выражения)


  Возвращает значение, сформированное сверткой значений дочерних элементов указанного элемента с помощью указанного унарного оператора.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>Аргументы  
 *Member_Expression*  
 Допустимое многомерное выражение, возвращающее элемент.  
  
 *Unary_Operator*  
 Допустимое строковое выражение, возвращающее унарный оператор.  
  
## <a name="remarks"></a>Примечания  
 **RollupChildren** функция сворачивает значения дочерних элементов указанного элемента при помощи указанного унарного оператора.  
  
 В следующей таблице перечислены допустимые унарные операторы для этой функции.  
  
|Оператор|Результат|  
|--------------|------------|  
|**+**|сумма = сумма + текущий дочерний элемент|  
|**-**|сумма = сумма - текущий дочерний элемент|  
|**\***|сумма = сумма * текущий дочерний элемент|  
|**/**|сумма = сумма / текущий дочерний элемент|  
|**%**|сумма = (сумма / текущий дочерний элемент) * 100|  
|**~**|Дочерний элемент не участвует в свертке. Его значение не обрабатывается.|  
  
 Если в свойстве элемента указан оператор, которого нет в этом списке, возникает ошибка. Порядок вычисления определяется порядком элементов с общим родителем, а не старшинством операторов.  
  
## <a name="example"></a>Пример  
 В следующем примере для свертывания дочерних элементов иерархии Net Profit измерения Account применяется свойство элемента Alternate Rollup Operator, содержащее альтернативные значения для унарных операторов. Это свойство элемента отсутствует в кубе Adventure Works, но его можно создать. Такое использование **RollupChildren** функция может использоваться приложения составления бюджета для гипотетического анализа.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по функциям многомерных выражений (многомерные выражения)](../mdx/mdx-function-reference-mdx.md)  
  
  
