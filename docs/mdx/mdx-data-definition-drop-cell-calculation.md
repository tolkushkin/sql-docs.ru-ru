---
title: Инструкция DROP CELL CALCULATION (многомерные Выражения) | Документация Майкрософт
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 509717221a51ac790b92969ff052d0a8a5d0143d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248265"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>Определение данных многомерных выражений — DROP CELL CALCULATION


  Удаляет указанное вычисление ячейки.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>Аргументы  
 *Cube_Name*  
 Допустимое строковое выражение, представляющее имя выражения куба.  
  
 *CellCalc_Name*  
 Допустимое строковое выражение, возвращающее имя вычисления ячейки, которое необходимо удалить.  
  
## <a name="see-also"></a>См. также  
 [Инструкция CREATE CELL CALCULATION (многомерные выражения)](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Инструкции определения данных многомерных Выражений &#40;многомерных Выражений&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
