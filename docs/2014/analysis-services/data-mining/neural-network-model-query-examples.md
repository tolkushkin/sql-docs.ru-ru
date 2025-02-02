---
title: Примеры запросов к модели нейронной сети | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- neural network algorithms [Analysis Services]
- content queries [DMX]
- neural network model [Analysis Services]
ms.assetid: 81b06183-620f-4e0c-bc10-532e6a1f0829
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a249a83aba62c7881be024caa3931cb5ad07204
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083284"
---
# <a name="neural-network-model-query-examples"></a>Примеры запросов к модели нейронной сети
  К модели интеллектуального анализа данных можно создать два вида запросов: запросы содержимого, возвращающие подробные сведения о закономерностях, обнаруженных при анализе, и прогнозирующие запросы, в которых используются закономерности, содержащиеся в модели, для прогнозирования новых данных. Например, запрос содержимого для модели нейронной сети может вернуть метаданные модели — в частности, число скрытых слоев. Или же прогнозирующий запрос может дать сведения для классификации на основе входа и, по желанию, предоставить значения вероятности для каждой классификации.  
  
 Этот раздел посвящен созданию запросов для моделей, основанных на алгоритме нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Запросы содержимого**  
  
 [Получение метаданных модели с помощью расширений интеллектуального анализа данных](#bkmk_Query1)  
  
 [Получение метаданных модели из набора строк схемы](#bkmk_Query2)  
  
 [Получение входных атрибутов модели](#bkmk_Query3)  
  
 [Получение весов из скрытого слоя](#bkmk_Query4)  
  
 **Прогнозирующие запросы**  
  
 [Создание одноэлементных прогнозов](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>Поиск сведений о модели нейронной сети  
 Все модели интеллектуального анализа данных возвращают содержимое, полученное алгоритмом, в соответствии со стандартизованной схемой — набором строк схемы модели интеллектуального анализа данных. Эта информация содержит детальные сведения о модели, в том числе базовые метаданные, структуры, обнаруженные при анализе, и параметры, использованные при обработке. Запросы к содержимому модели интеллектуального анализа данных можно создавать при помощи инструкций DMX.  
  
###  <a name="bkmk_Query1"></a> Образец запроса 1. Получение метаданных модели с помощью расширений интеллектуального анализа данных  
 Следующий запрос возвращает некоторые базовые метаданные модели, построенной с помощью алгоритма нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Родительский узел модели нейронной сети содержит только имя модели, имя базы данных, где она хранится, и количество дочерних узлов модели. Однако узел граничной статистики (NODE_TYPE = 24) предоставляет и эти базовые метаданные, и некоторые полученные путем вывода статистические данные о входных столбцах, использованных в модели.  
  
 Следующий образец запроса основан на модели интеллектуального анализа данных с именем [, созданной в](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)учебнике по интеллектуальному анализу данных среднего уровня `Call Center Default NN`. Модель получает данные из центра обработки звонков и исследует возможные взаимосвязи между кадрами и количеством звонков, заказов и проблем. Инструкция DMX получает данные с граничного узла статистики модели нейронной сети. В запрос входит ключевое слово FLATTENED, поскольку интересующая нас статистика, описывающая входные атрибуты, хранится во вложенной таблице, NODE_DISTRIBUTION. Однако если используемый поставщик запросов поддерживает иерархические наборы строк, ключевое слово FLATTENED можно не использовать.  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  Имена столбцов `[SUPPORT]` и `[PROBABILITY]` вложенной таблицы следует заключить в квадратные скобки, чтобы отличить их от одноименных зарезервированных ключевых слов языка многомерных выражений.  
  
 Пример результатов:  
  
|MODEL_CATALOG|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Средние затраты времени на решение проблемы|Missing|0|0|1|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Средние затраты времени на решение проблемы|< 64.7094100096|11|0.407407407|5|  
  
 Узнать, что означают эти столбцы в наборе строк схемы в контексте модели нейронной сети, можно в разделе [Содержимое моделей интеллектуального анализа данных для моделей нейронных сетей (службы Analysis Services — интеллектуальный анализ данных)](mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query2"></a> Образец запроса 2. Получение метаданных модели из набора строк схемы  
 Получить те же сведения, которые возвращаются DMX-запросом содержимого, можно с помощью запроса набора строк схемы интеллектуального анализа данных. Однако в наборе строк схемы содержатся и дополнительные столбцы. В следующем образце запроса возвращается дата создания, изменения и последней обработки модели. Этот запрос также возвращает прогнозируемые столбцы, которые не так просто получить из содержимого модели, а также параметры, которые использовались при построении модели. Эта информация может оказаться полезной для документирования модели.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 Пример результатов:  
  
|||  
|-|-|  
|MODEL_NAME|Call Center Default NN|  
|DATE_CREATED|1/10/2008 17:07:38|  
|LAST_PROCESSED|1/10/2008 17:24:02|  
|PREDICTION_ENTITY|Средние затраты времени на решение проблемы<br /><br /> Уровень обслуживания<br /><br /> Количество заказов|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a> Образец запроса 3. Получение входных атрибутов модели  
 Можно получить пары атрибут-значение, которые использовались при создании модели. Для этого надо создать запрос к дочерним узлам (NODE_TYPE = 20) входного слоя (NODE_TYPE = 18). Следующий запрос возвращает список входных атрибутов из описаний узлов.  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 Пример результатов:  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|Средние затраты времени на решение проблемы=64.7094100096 - 77.4002099712|  
|ДеньНедели=Пятница|  
|Операторы Уровня 1|  
  
 Далее показаны лишь несколько наиболее представительных строк результата. Однако можно видеть, что параметр NODE_DESCRIPTION предоставляет несколько другую информацию в зависимости от типа данных входного атрибута.  
  
-   Если атрибут представляет собой дискретное или дискретизированное значение, возвращается атрибут и его значение (либо его дискретизированный диапазон).  
  
-   Если атрибут представляет собой непрерывный числовой тип данных, параметр NODE_DESCRIPTION содержит только имя атрибута. Можно, однако, извлечь данные из вложенной таблицы NODE_DISTRIBUTION для получения среднего или возвратить столбец NODE_RULE для получения минимального и максимального значений числового диапазона.  
  
 Этот запрос показывает, каким образом можно составить запрос к вложенной таблице NODE_DISTRIBUTION, чтобы вернуть атрибуты в виде столбца, а их значения — в виде другого столбца. Для непрерывных атрибутов значение атрибута представляется именно таким способом.  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 Пример результатов:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|Средние затраты времени на решение проблемы|64.7094100096 - 77.4002099712|  
|День недели|Пт|  
|Операторы Уровня 1|3.2962962962963|  
  
 Минимальное и максимальное значения диапазона хранятся в столбце NODE_RULE и представляются в виде фрагмента на языке XML, как показано в следующем примере:  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a> Образец запроса 4. Получение весов из скрытого слоя  
 Содержимое модели нейронной сети структурируется так, чтобы легче было получать детальные сведения о любом узле сети. Более того, числовые идентификаторы узлов предоставляют информацию, которая помогает выявлять связи между типами узлов.  
  
 Следующий запрос демонстрирует получение коэффициентов, хранимых в определенном узле скрытого слоя. Скрытый слой состоит из узла-организатора (NODE_TYPE = 19), содержащего только метаданные, и нескольких дочерних узлов (NODE_TYPE = 22), содержащих коэффициенты для различных сочетаний атрибутов и значений. Этот запрос возвращает только узлы с коэффициентами.  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 Пример результатов:  
  
|NODE_UNIQUE_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0.178616518|7|  
|70000000200000000|6000000000000000b|-0.267561918|7|  
|70000000200000000|6000000000000000c|0.11069497|7|  
|70000000200000000|6000000000000000d|0.123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0.188805045|7|  
  
 Приведенные здесь частичные результаты показывают, как модель нейронной сети соотносит скрытый узел с входными узлами.  
  
-   Уникальные имена узлов на скрытом уровне всегда начинаются с 70000000.  
  
-   Уникальные имена узлов на входном уровне всегда начинаются с 60000000.  
  
 Таким образом, эти результаты говорят о том, что узлу с идентификатором 70000000200000000 передается шесть разных коэффициентов (VALUETYPE = 7). Значения коэффициентов находятся в столбце ATTRIBUTE_VALUE. Используя идентификатор узла в столбце ATTRIBUTE_NAME, можно в точности определить, для какого атрибута служит этот коэффициент. Например, узел с идентификатором 6000000000000000a относится к атрибуту и значению `Day of Week = 'Tue.'` . Можно использовать идентификатор узла для создания запроса или переместиться в этот узел с помощью [средства просмотра деревьев содержимого общего вида (Майкрософт)](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
 Подобным же образом с помощью запроса к таблице NODE_DISTRIBUTION узлов внешнего слоя (NODE_TYPE = 23) можно увидеть коэффициенты для каждого выходного значения. Однако указатели в выходном слое указывают назад, на узлы скрытого слоя. Дополнительные сведения см. в разделе [Mining Model Content for Neural Network Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>Использование модели нейронной сети для создания прогнозов  
 Алгоритм нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] поддерживает и классификацию, и регрессию. С этими моделями можно использовать прогнозирующие функции, чтобы получать новые данные и создавать одноэлементные и пакетные запросы.  
  
###  <a name="bkmk_Query5"></a> Образец запроса 5. Создание одноэлементных прогнозов  
 Построить прогнозирующий запрос в модели нейронной сети проще всего с помощью построителя прогнозирующих запросов, доступного на вкладке **Прогноз интеллектуального анализа данных** конструктора интеллектуального анализа данных в средах [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] и [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Модель можно просматривать с помощью средства просмотра нейронных сетей [!INCLUDE[msCoName](../../includes/msconame-md.md)] для выделения атрибутов, представляющих интерес, и просмотра трендов. Затем можно переключиться на вкладку **Прогноз интеллектуального анализа данных** для создания запроса и прогнозирования новых величин для этих трендов.  
  
 Например, можно просмотреть модель центра обработки звонков, чтобы найти взаимосвязи между объемами заказов и другими атрибутами. Для этого откройте модель в средстве просмотра, а также для **ввода**выберите  **\<все >**.  Далее в области **Выход**выберите **Количество заказов**. В качестве значения **Значение 1**выберите диапазон, представляющий наибольшее количество заказов, а для **Значение 2**— диапазон, представляющий наименьшее количество заказов. Это позволяет наглядно увидеть все атрибуты, у которых модель обнаруживает корреляцию с объемом заказа.  
  
 Просматривая результаты с помощью средства просмотра, можно видеть, что для некоторых дней недели характерны пониженные объемы заказов и что увеличение количества сотрудников, по-видимому, коррелирует с повышением продаж. Затем можно использовать прогнозирующий запрос на модели для проверки гипотетических сценариев и задаться вопросом, приведет ли увеличение количества сотрудников уровня 2 в день с низкими объемами заказов к увеличению заказов. Это можно сделать с помощью следующего запроса.  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 Пример результатов:  
  
|Спрогнозированное количество заказов|Вероятность|  
|----------------------|-----------------|  
|364|0.9532...|  
  
 Спрогнозированный объем продаж выше текущего диапазона продаж для вторника, и вероятность этого прогноза очень высока. Однако иногда нужно создавать множественные прогнозы с помощью пакетного процесса для проверки на модели нескольких гипотез.  
  
> [!NOTE]  
>  Надстройки интеллектуального анализа данных для Excel 2007 предоставляют мастера логистической регрессии, которые помогают получить ответы на сложные вопросы, например определение числа операторов второго уровня, которое необходимо для повышения показателя обслуживания до заданного уровня для определенной смены. Надстройки интеллектуального анализа данных загружаются бесплатно и содержат мастера, которые основаны на алгоритмах нейронной сети и логистической регрессии. Дополнительные сведения см. в статье [Надстройки интеллектуального анализа данных для Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790) .  
  
## <a name="list-of-prediction-functions"></a>Список прогнозирующих функций  
 Все алгоритмы [!INCLUDE[msCoName](../../includes/msconame-md.md)] поддерживают общий набор функций. У алгоритма нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] нет присущих только ему прогнозирующих функций, однако он поддерживает функции, перечисленные в следующей таблице.  
  
|||  
|-|-|  
|прогнозирующую функцию|Использование|  
|[IsDescendant (расширения интеллектуального анализа данных)](/sql/dmx/isdescendant-dmx)|Определяет, является ли один узел дочерним для другого узла в диаграмме нейронной сети.|  
|[PredictAdjustedProbability (расширения интеллектуального анализа данных)](/sql/dmx/predictadjustedprobability-dmx)|Возвращает взвешенную вероятность.|  
|[PredictHistogram (расширения интеллектуального анализа данных)](/sql/dmx/predicthistogram-dmx)|Возвращает таблицу значений, связанную с текущим прогнозируемым значением.|  
|[PredictVariance (расширения интеллектуального анализа данных)](/sql/dmx/predictvariance-dmx)|Возвращает дисперсию для прогнозируемого значения.|  
|[PredictProbability (расширения интеллектуального анализа данных)](/sql/dmx/predictprobability-dmx)|Возвращает вероятность для прогнозируемого значения.|  
|[PredictStdev (расширения интеллектуального анализа данных)](/sql/dmx/predictstdev-dmx)|Возвращает стандартное отклонение для прогнозируемого значения.|  
|[PredictSupport (расширения интеллектуального анализа данных)](/sql/dmx/predictsupport-dmx)|Для моделей нейронной сети и логистической регрессии возвращает единственное значение, представляющее собой размер обучающего набора для всей модели.|  
  
 Синтаксис отдельных функций см. в статье [Справочник по функциям расширений интеллектуального анализа данных (расширения интеллектуального анализа данных)](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>См. также  
 [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)   
 [Технический справочник по алгоритму нейронной сети (Майкрософт)](microsoft-neural-network-algorithm-technical-reference.md)   
 [Содержимое моделей интеллектуального анализа данных для моделей нейронных сетей (службы Analysis Services — интеллектуальный анализ данных)](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Занятие 5. Построение моделей логистической регрессии нейронной сети и &#40;средний уровень учебник по интеллектуальному анализу данных&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
  
