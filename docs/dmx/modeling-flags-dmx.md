---
title: Флаги (расширения интеллектуального анализа данных) | Документация Майкрософт
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17280abc62cd75122fde1f54b321ca9b51a1b1d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62502970"
---
# <a name="modeling-flags-dmx"></a>Флаги моделирования (расширения интеллектуального анализа данных)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Флаги моделирования можно использовать в службах [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], чтобы включить в алгоритм интеллектуального анализа данных дополнительные сведения о данных, определенных в таблице вариантов. Алгоритм может использовать эти сведения для создания более точной модели интеллектуального анализа данных. Флаги моделирования можно задавать для столбцов структуры и модели интеллектуального анализа данных.  
  
 Службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] поддерживают следующие флаги моделирования:  
  
 **NOT NULL**  
 Значения столбца атрибутов никогда не должны включать значение NULL. Если службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] найдут значение NULL в данном столбце атрибутов в процессе обучения модели, будет выдана ошибка. Данный флаг задается для столбца структуры интеллектуального анализа данных.  
  
 **REGRESSOR**  
 Указывает, что алгоритм может использовать заданный столбец в формуле регрессии алгоритмов регрессии. Этот флаг поддерживается алгоритмами линейной регрессии [!INCLUDE[msCoName](../includes/msconame-md.md)] и дерева принятия решений [!INCLUDE[msCoName](../includes/msconame-md.md)], и задается для столбца модели интеллектуального анализа данных.  
  
 **MODEL_EXISTENCE_ONLY**  
 Значения столбца атрибутов являются менее важными, чем присутствие атрибута. Данный флаг задается для столбца модели интеллектуального анализа данных.  
  
 Алгоритмы сторонних разработчиков могут поддерживать дополнительные флаги моделирования. Чтобы определить флаги моделирования алгоритма поддерживает, используйте **SUPPORTED_MODELING_FLAGS** набора строк схемы. Можно также создавать запросы к службам интеллектуального анализа данных на сервере для определения того, какие флаги моделирования поддерживаются для того или иного алгоритма. К примеру, следующий запрос возвращает флаги моделирования, поддерживаемые алгоритмом линейной регрессии (Майкрософт) на текущем сервере:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Ожидаемый результат:  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Указание флагов моделирования в модели интеллектуального анализа данных  
 Примеры синтаксиса, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] поддерживает для указания флага для столбца структуры интеллектуального анализа данных, см. в разделе [CREATE MINING STRUCTURE &#40;расширений интеллектуального анализа данных&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Пример синтаксиса для указания флага моделирования для столбца модели интеллектуального анализа данных, см. в разделе [ALTER MINING STRUCTURE &#40;расширений интеллектуального анализа данных&#41;](../dmx/alter-mining-structure-dmx.md).  
  
 Дополнительные сведения о работе со столбцами модели интеллектуального анализа данных см. в разделе [столбцы модели интеллектуального анализа данных](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="see-also"></a>См. также  
 [Алгоритмы интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Справочник по расширениям интеллектуального анализа данных (расширения интеллектуального анализа данных)](../dmx/data-mining-extensions-dmx-reference.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; элементы синтаксиса](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; справочнике по функциям](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; Справочник по операторам](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; Справка по инструкции](../dmx/data-mining-extensions-dmx-statements.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; синтаксические обозначения](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Общие функции прогнозирования &#40;расширений интеллектуального анализа данных&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Структура и методы использования прогнозирующих запросов расширений интеллектуального анализа данных](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Общие сведения об инструкции SELECT в расширении интеллектуального анализа данных](../dmx/understanding-the-dmx-select-statement.md)  
  
  
