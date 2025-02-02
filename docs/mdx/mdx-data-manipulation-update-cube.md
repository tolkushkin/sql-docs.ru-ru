---
title: Инструкция UPDATE CUBE (многомерные Выражения) | Документация Майкрософт
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 878f103e236a198ff71181a64b39400c8f6ea0ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187619"
---
# <a name="mdx-data-manipulation---update-cube"></a>Операции с данными многомерных выражений — UPDATE CUBE


  Инструкция UPDATE CUBE используется для обратной записи данных в любую ячейку куба, которая суммируется с родительским элементом с помощью агрегатного выражения SUM. Дополнительные сведения и пример см. в разделе «Общие сведения о приложениях» в этой записи блога: [Создание приложения обратной записи с помощью служб Analysis Services (блог)](https://go.microsoft.com/fwlink/?LinkId=394977).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>Аргументы  
 *Cube_Name*  
 Допустимое строковое выражение, возвращающее имя куба.  
  
 *Tuple_Expression*  
 Допустимое многомерное выражение, возвращающее кортеж.  
  
 *Новое_значение*  
 Допустимое числовое выражение.  
  
 *Weight_Expression*  
 Допустимое числовое многомерное выражение, возвращающее десятичное значение от 0 до 1.  
  
## <a name="remarks"></a>Примечания  
 Можно обновить значение указанной конечной или неконечной ячейки куба, по желанию размещая значение для указанной неконечной ячейки в зависимых конечных ячейках. Ячейка, указанная кортежным выражением, может представлять любую ячейку многомерного пространства (другими словами, ячейка необязательно должна быть конечной). Тем не менее, ячейки должны быть собраны с [Sum](../mdx/sum-mdx.md) агрегатной функции и не должны содержать вычисляемый элемент в кортеже, который используется для определения ячейки.  
  
 Он может быть полезным подумать об **UPDATE CUBE** инструкции как подпрограмму, которая автоматически создаст серию отдельных операций обратной записи в конечные и неконечные ячейки, сводимые в указанную сумму.  
  
 Ниже приведено описание методов выделения.  
  
 **USE_EQUAL_ALLOCATION:** В каждой конечной ячейке, которая участвует в обновлении ячейки будут назначаться одинаковые значения в соответствии со следующим выражением.  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:** каждой конечной ячейке, которая участвует в обновлении ячейки, изменяется в соответствии с следующее выражение.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** В каждой конечной ячейке, которая участвует в обновлении ячейки будут назначаться одинаковые значения, основанный на следующее выражение.  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** В каждой конечной ячейке, которая участвует в обновлении ячейки изменятся в соответствии с следующее выражение.  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 Если выражение веса не указано, **UPDATE CUBE** инструкции неявно использует следующее выражение.  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 Выражение веса должно быть отображено как десятичное значение от нуля (0) до 1. Оно определяет ту часть размещаемого значения, которую требуется присвоить конечным ячейкам, участвующим в размещении. Задачей программиста клиентского приложения является создание выражений, статистических значений, свертки которых будут равны размещаемому значению выражения.  
  
> [!CAUTION]  
>  Клиентское приложение должно выполнять размещение во всех измерениях параллельно, чтобы избежать возможных непредвиденных результатов, в том числе неправильных значений свертки или несогласованности данных.  
  
 Каждый **UPDATE CUBE** неделимым транзакций целях можно рассматривать выделения. Это означает, что в случае сбоя при выполнении одной из операций размещения по какой-либо причине (например, вследствие ошибки в формуле или нарушения защиты), вся инструкция UPDATE CUBE завершается ошибкой. Перед обработкой вычислений отдельных операций размещения создается моментальный снимок данных, что обеспечивает правильность итоговых вычислений.  
  
> [!CAUTION]  
>  При использовании для меры, содержащей целые значения, метод USE_WEIGHTED_ALLOCATION может возвращать неточные результаты, что обусловлено округлениями при приращениях.  
  
> [!IMPORTANT]  
>  Если обновленные ячейки не пересекаются, свойство строки подключения **Update Isolation Level** может быть использовано для повышения производительности инструкции UPDATE CUBE.  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Инструкции для манипулирования данными многомерных Выражений &#40;многомерных Выражений&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
