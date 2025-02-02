---
title: Примеры запросов к упрощенной модели Байеса | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- naive bayes model [Analysis Services]
- naive bayes algorithms [Analysis Services]
- content queries [DMX]
ms.assetid: e642bd7d-5afa-4dfb-8cca-4f84aadf61b0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b713d9918dabcbaabba2085710dfaa5ed5d3a33b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083281"
---
# <a name="naive-bayes-model-query-examples"></a>Примеры запросов к модели упрощенного алгоритма Байеса
  К модели интеллектуального анализа данных можно создать два вида запросов: запросы содержимого, возвращающие подробные сведения о закономерностях, обнаруженных при анализе, и прогнозирующие запросы, использующие закономерности, содержащиеся в модели, для прогнозирования новых данных. Получение метаданных модели интеллектуального анализа данных выполняется с помощью запроса к набору строк схемы интеллектуального анализа данных. В этом разделе описывается процесс создания запросов к моделям, основанным на упрощенном алгоритме Байеса (Майкрософт).  
  
 **Запросы содержимого**  
  
 [Получение метаданных модели с помощью расширений интеллектуального анализа данных](#bkmk_Query1)  
  
 [Получение сводки обучающих данных](#bkmk_Query2)  
  
 [Получение дополнительных сведений об атрибутах](#bkmk_Query3)  
  
 [Использование системных хранимых процедур](#bkmk_Query4)  
  
 **Прогнозирующие запросы**  
  
 [Прогноз результатов с помощью одноэлементного запроса](#bkmk_Query5)  
  
 [Получение прогнозов со значениями вероятности и несущего множества](#bkmk_Query6)  
  
 [Прогноз взаимосвязей](#bkmk_Query7)  
  
## <a name="finding-information-about-a-naive-bayes-model"></a>Поиск сведений о модели упрощенного алгоритма Байеса  
 Содержимое модели упрощенного алгоритма Байеса предоставляет статистические данные о распределении значений в обучающих данных. Можно также получать информацию о метаданных модели с помощью запросов к наборам строк схемы интеллектуального анализа данных.  
  
###  <a name="bkmk_Query1"></a> Образец запроса 1. Получение метаданных модели с помощью расширений интеллектуального анализа данных  
 Используя запросы к набору строк схемы интеллектуального анализа данных, можно получать метаданные модели. Они включают в себя, например, время создания модели, время ее последней обработки, имя структуры интеллектуального анализа данных, на которой основана данная модель, и имена столбцов, использованных в качестве прогнозируемого атрибута. Также можно возвратить параметры, которые были использованы при первичном создании модели.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, DATE_CREATED, LAST_PROCESSED,  
SERVICE_NAME, PREDICTION_ENTITY, FILTER  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_NaiveBayes_Filtered'  
```  
  
 Образец результатов.  
  
|||  
|-|-|  
|MODEL_CATALOG|AdventureWorks|  
|MODEL_NAME|TM_NaiveBayes_Filtered|  
|DATE_CREATED|3/1/2008 19:15|  
|LAST_PROCESSED|3/2/2008 20:00|  
|SERVICE_NAME|Microsoft_Naive_Bayes|  
|PREDICTION_ENTITY|Покупатель велосипеда, годовой доход|  
|FILTER|[Region] = 'Europe' OR [Region] = 'North America'|  
  
 Модель, использованная в этом примере, основана на модели упрощенного алгоритма Байеса, созданной в занятии [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md), с некоторыми изменениями: в нее был добавлен второй прогнозируемый атрибут, и к обучающим данным применяется фильтр.  
  
###  <a name="bkmk_Query2"></a> Образец запроса 2. Получение сводки обучающих данных  
 В модели упрощенного алгоритма Байеса узел граничной статистики хранит статистические данные о распределении значений в обучающих данных. Эти сводные данные очень удобны и экономят время, избавляя от необходимости создавать запросы SQL к обучающим данным для получения той же информации.  
  
 В этом запросе используется DMX-запрос содержимого для получения данных из узла (NODE_TYPE = 24). Поскольку статистические данные хранятся во вложенной таблице, используется ключевое слово FLATTENED, чтобы сделать результаты удобнее для чтения.  
  
```  
SELECT FLATTENED MODEL_NAME,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE FROM NODE_DISTRIBUTION) AS t  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
> [!NOTE]  
>  Имена столбцов, SUPPORT и PROBABILITY, следует заключить в квадратные скобки, чтобы отличить их от одноименных зарезервированных ключевых слов языка многомерных выражений.  
  
 Частичные результаты:  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|TM_NaiveBayes|Покупатель велосипеда|Missing|0|0|1|  
|TM_NaiveBayes|Покупатель велосипеда|0|8869|0.507263784|4|  
|TM_NaiveBayes|Покупатель велосипеда|1|8615|0.492736216|4|  
|TM_NaiveBayes|Gender|Missing|0|0|1|  
|TM_NaiveBayes|Gender|Ж|8656|0.495081217|4|  
|TM_NaiveBayes|Gender|M|8828|0.504918783|4|  
  
 Эти результаты, в частности, содержат число обучающих вариантов для каждой дискретной величины (VALUETYPE = 4), а также вычисленную вероятность, скорректированную с поправкой на отсутствующие величины (VALUETYPE = 1).  
  
 Определения значений, указанных в таблице NODE_DISTRIBUTIO модели упрощенного алгоритма Байеса, см. в разделе [Содержимое моделей интеллектуального анализа данных для моделей упрощенного алгоритма Байеса (службы Analysis Services — интеллектуальный анализ данных)](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md). Дополнительные сведения о влиянии отсутствующих значений на вычисления мощности и вероятности см. в разделе [Отсутствующие значения (службы Analysis Services — интеллектуальный анализ данных)](missing-values-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query3"></a> Образец запроса 3. Получение дополнительных сведений об атрибутах  
 Поскольку модель упрощенного алгоритма Байеса часто содержит информацию о связях между различными атрибутами, проще всего просматривать эти связи с помощью [средства просмотра упрощенного алгоритма Байеса (Майкрософт)](browse-a-model-using-the-microsoft-naive-bayes-viewer.md). Однако для получения данных можно использовать и DMX-запросы.  
  
 Следующий пример показывает, как получить из модели информацию о конкретном атрибуте, `Region`.  
  
```  
SELECT NODE_TYPE, NODE_CAPTION,   
NODE_PROBABILITY, NODE_SUPPORT, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE ATTRIBUTE_NAME = 'Region'  
```  
  
 Этот запрос возвращает два типа узлов: узел, представляющий входной атрибут (NODE_TYPE = 10), и узлы для каждого значения атрибута (NODE_TYPE = 11). Для идентификации узла используется его заголовок, а не имя, поскольку заголовок узла содержит как имя атрибута, так и значение атрибута.  
  
|NODE_TYPE|NODE_CAPTION|NODE_PROBABILITY|NODE_SUPPORT|MSOLAP_NODE_SCORE|NODE_TYPE|  
|----------------|-------------------|-----------------------|-------------------|-------------------------|----------------|  
|10|Bike Buyer -> Region|1|17484|84.51555875|10|  
|11|Bike Buyer -> Region = Missing|0|0|0|11|  
|11|Bike Buyer -> Region = North America|0.508236102|8886|0|11|  
|11|Bike Buyer -> Region = Pacific|0.193891558|3390|0|11|  
|11|Bike Buyer -> Region = Europe|0.29787234|5208|0|11|  
  
 Некоторые столбцы, хранящиеся в узлах, совпадают с теми, которые можно получить из узлов граничной статистики — например, оценка вероятности узла и значения мощности поддерживающего множества узла. Однако MSOLAP_NODE_SCORE — это специальное значение, предоставляемое только для узлов входных атрибутов и указывающее относительную важность этого атрибута для модели. На панели сети зависимостей средства просмотра можно увидеть примерно ту же информацию; однако средство просмотра не выводит оценок.  
  
 Следующий запрос возвращает оценки важности всех атрибутов модели:  
  
```  
SELECT NODE_CAPTION, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
ORDER BY MSOLAP_NODE_SCORE DESC  
```  
  
 Образец результатов.  
  
|NODE_CAPTION|MSOLAP_NODE_SCORE|  
|-------------------|-------------------------|  
|Bike Buyer -> Total Children|181.3654836|  
|Bike Buyer -> Commute Distance|179.8419482|  
|Bike Buyer -> English Education|156.9841928|  
|Bike Buyer -> Number Children At Home|111.8122599|  
|Bike Buyer -> Region|84.51555875|  
|Bike Buyer -> Marital Status|23.13297354|  
|Bike Buyer -> English Occupation|2.832069191|  
  
 Просмотрев содержимое модели с помощью [средства просмотра деревьев содержимого общего вида (Майкрософт)](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md), можно понять, какие статистические показатели наиболее интересны. Продемонстрированные примеры довольно просты; чаще возникает необходимость выполнить несколько запросов или сохранить результаты для обработки на клиенте.  
  
###  <a name="bkmk_Query4"></a> Образец запроса 4. Использование системных хранимых процедур  
 Кроме написания собственных запросов к содержимому, можно использовать системные хранимые процедуры служб Analysis Services для исследования результатов. Для использования системной хранимой процедуры перед ее именем нужно поставить ключевое слово CALL:  
  
```  
CALL GetPredictableAttributes ('TM_NaiveBayes')  
```  
  
 Частичные результаты:  
  
|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|  
|---------------------|------------------------|  
|Покупатель велосипеда|100000001|  
  
> [!NOTE]  
>  Эти системные хранимые процедуры служат для внутренней коммуникации между сервером служб Analysis Services и клиентом; их рекомендуется использовать только для удобства при разработке и тестировании моделей интеллектуального анализа данных. При создании запросов для рабочей системы нужно создавать собственные запросы с помощью расширений интеллектуального анализа данных.  
  
 Дополнительные сведения о системных хранимых процедурах служб Analysis Services см. в разделе [Хранимые процедуры интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining).  
  
## <a name="using-a-naive-bayes-model-to-make-predictions"></a>Использование модели упрощенного алгоритма Байеса для создания прогнозов  
 Модель упрощенного алгоритма Байеса (Майкрософт) используется для прогнозирования реже, чем для исследования связей между входными и прогнозируемыми атрибутами. Однако модель поддерживает использование прогнозирующих функций как для прогнозов, так и для взаимосвязей.  
  
###  <a name="bkmk_Query5"></a> Образец запроса 5. Прогноз результатов с помощью одноэлементного запроса  
 Следующий запрос использует одноэлементный запрос для получения новой величины и прогнозирования на основании данной модели вероятности приобретения велосипеда клиентом с этими характеристиками. Проще всего создавать одноэлементные запросы на модели регрессии с помощью диалогового окна **Ввод одноэлементного запроса** . Например, можно построить следующий DMX-запрос, выбрав модель `TM_NaiveBayes` , затем **Одноэлементный запрос**, а затем величины из раскрывающихся списков значений `[Commute Distance]` и `Gender`.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Пример результатов:  
  
|Выражение|  
|----------------|  
|0|  
  
 Прогнозирующая функция вернет наиболее вероятное значение (в данном случае 0; это означает, что клиент такого типа вряд ли приобретет велосипед).  
  
###  <a name="bkmk_Query6"></a> Образец запроса 6. Получение прогнозов со значениями вероятности и несущего  
 Кроме прогнозирования результата, часто нужно знать, насколько надежен этот прогноз. Данный запрос использует тот же одноэлементный запрос, что и предыдущий, но в нем добавляется также прогнозирующая функция [PredictHistogram (расширения интеллектуального анализа данных)](/sql/dmx/predicthistogram-dmx), которая возвращает вложенную таблицу со статистикой, поддерживающей прогноз.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer]),  
  PredictHistogram([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Пример результатов:  
  
|Покупатель велосипеда|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|0|10161.5714|0.581192599|0.010530981|0|0|  
|1|7321.428768|0.418750215|0.008945684|0|0|  
||0.999828444|5.72E-05|5.72E-05|0|0|  
  
 Последняя строка таблицы показывает внесенные в мощность и вероятность поправки на отсутствующее значение. Дисперсия и стандартное отклонение всегда равны 0, поскольку модели упрощенного алгоритма Байеса не поддерживают непрерывных величин.  
  
###  <a name="bkmk_Query7"></a> Образец запроса 7. Прогноз взаимосвязей  
 Упрощенный алгоритм Байеса (Майкрософт) можно использовать для анализа взаимосвязей, если структура интеллектуального анализа данных содержит вложенную таблицу с прогнозируемым атрибутом в качестве ключа. Например, можно построить модель упрощенного алгоритма Байеса с помощью структуры интеллектуального анализа данных, созданной в [занятия 3: Построение сценария потребительской корзины &#40;учебнике по интеллектуальному данных&#41; ](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md) руководства интеллектуального анализа данных. Модель, использованная в этом примере, была изменена: в ее таблицу вариантов добавлена информация о доходе и географическом положении клиента.  
  
 Следующий пример запроса показывает одноэлементный запрос, предсказывающий продукты, связанные с покупкой данного продукта, `'Road Tire Tube'`. Эту информацию можно использовать, чтобы рекомендовать продукты определенным типам покупателей.  
  
```  
SELECT   PredictAssociation([Association].[v Assoc Seq Line Items])  
FROM [Association_NB]  
NATURAL PREDICTION JOIN  
(SELECT 'High' AS [Income Group],  
  'Europe' AS [Region],  
  (SELECT 'Road Tire Tube' AS [Model])   
AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Частичные результаты:  
  
|Модель|  
|-----------|  
|Женские шорты Mountain|  
|Фляга для воды|  
|Touring-3000|  
|Touring-2000|  
|Touring-1000|  
  
## <a name="function-list"></a>Список функций  
 Все алгоритмы [!INCLUDE[msCoName](../../includes/msconame-md.md)] поддерживают общий набор функций. Однако упрощенный алгоритм Байеса [!INCLUDE[msCoName](../../includes/msconame-md.md)] поддерживает дополнительные функции, приведенные в следующей таблице.  
  
|||  
|-|-|  
|прогнозирующую функцию|Использование|  
|[IsDescendant (расширения интеллектуального анализа данных)](/sql/dmx/isdescendant-dmx)|Определяет, является ли узел дочерним для другого узла модели.|  
|[Predict (расширения интеллектуального анализа данных)](/sql/dmx/predict-dmx)|Возвращает прогнозируемое значение или набор значений для указанного столбца.|  
|[PredictAdjustedProbability (расширения интеллектуального анализа данных)](/sql/dmx/predictadjustedprobability-dmx)|Возвращает взвешенную вероятность.|  
|[PredictAssociation (расширения интеллектуального анализа данных)](/sql/dmx/predictassociation-dmx)|Прогнозирует вхождение в ассоциативном наборе данных.|  
|[PredictNodeId (расширения интеллектуального анализа данных)](/sql/dmx/predictnodeid-dmx)|Возвращает параметр Node_ID для каждого случая.|  
|[PredictProbability (расширения интеллектуального анализа данных)](/sql/dmx/predictprobability-dmx)|Возвращает вероятность для прогнозируемого значения.|  
|[PredictSupport (расширения интеллектуального анализа данных)](/sql/dmx/predictsupport-dmx)|Возвращает опорное значение для указанного состояния.|  
  
 Синтаксис специальных функций см. в разделе [Справочник по функциям расширений интеллектуального анализа данных](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>См. также  
 [Технический справочник по упрощенному алгоритму Байеса (Майкрософт)](microsoft-naive-bayes-algorithm-technical-reference.md)   
 [Упрощенный алгоритм Байеса (Майкрософт)](microsoft-naive-bayes-algorithm.md)   
 [Содержимое моделей интеллектуального анализа данных для моделей упрощенного алгоритма Байеса (службы Analysis Services — интеллектуальный анализ данных)](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
