---
title: Инструкции CALL (многомерные Выражения) | Документация Майкрософт
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4052134e9fd7d3c6877894c61480897e40982b59
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187675"
---
# <a name="mdx-data-manipulation---call"></a>Операции с данными многомерных выражений — CALL


  Выполняет хранимую процедуру, которая возвращает значение void в текущей области или (по желанию) в указанном кубе.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>Аргументы  
 *SP_Name*  
 Допустимое строковое выражение, представляющее имя хранимой процедуры.  
  
 *SP_Argument*  
 Допустимое строковое выражение, представляющее аргумент хранимой процедуры.  
  
 *Cube_Expression*  
 Допустимое строковое выражение куба, представляющее имя куба.  
  
## <a name="remarks"></a>Примечания  
 **ВЫЗОВИТЕ** инструкция запускает указанный регистрируемой хранимой процедуры, при необходимости включая один или несколько аргументов для указанной хранимой процедуры. **ВЫЗОВИТЕ** инструкция может использоваться только с хранимые процедуры, возвращающие значение void. Ее нельзя сочетать с другими функциями и операторами в многомерном выражении. Зарегистрированные хранимые процедуры, возвращающие значения, можно явно вызывать в многомерных выражениях и использовать совместно с другими функциями и операторами многомерных выражений.  
  
 Если куб не указан, инструкция выполняет хранимую процедуру над текущим кубом.  
  
> [!NOTE]  
>  Если хранимая процедура не зарегистрирована на стороне клиента, **вызвать** оператор пытается вызвать хранимую процедуру из экземпляра [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>См. также  
 [Инструкции для манипулирования данными многомерных Выражений &#40;многомерных Выражений&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Использование хранимых процедур (MDX)](../mdx/using-stored-procedures-mdx.md)  
  
  
