---
title: Исключить столбец из модели интеллектуального анализа данных | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70049092909b625a1f304f16f153bf4287d5bcdf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66084560"
---
# <a name="exclude-a-column-from-a-mining-model"></a>исключить столбец из модели интеллектуального анализа данных
  При создании новой модели интеллектуального анализа данных может отсутствовать необходимость использовать все столбцы, существующие в структуре интеллектуального анализа данных, на которой основывается модель. Например возможно, добавили столбец имен заказчиков для детализации, но не хотите использовать при моделировании. Или же может потребоваться создать несколько копий столбца с различной дискретизацией так, чтобы только одна из таких копий использовалась в каждой модели, а остальные пропускались. Также можно избирательно добавлять входные столбцы в некоторые модели для того, чтобы увидеть, как добавленные переменные повлияют на выходной столбец.  
  
 Не требуется создавать новую структуру интеллектуального анализа данных для каждой комбинации столбцов. Вместо этого можно просто отметить столбцы, которые не будут использоваться в конкретной модели.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>Исключение столбца из модели интеллектуального анализа данных  
  
1.  На вкладке **Модели интеллектуального анализа данных** конструктора интеллектуального анализа данных в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]выберите ячейку, которая соответствует столбцу, который необходимо исключить, под соответствующей моделью интеллектуального анализа данных.  
  
2.  Выберите пункт **Пропустить** из раскрывающегося списка.  
  
## <a name="see-also"></a>См. также  
 [Задачи и инструкции по модели интеллектуального анализа данных](mining-model-tasks-and-how-tos.md)  
  
  
