---
title: Алгоритм нейронной сети (Майкрософт) | Документация Майкрософт
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54896093b887985fc658e823f7d277347a70f0ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724998"
---
# <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Алгоритм нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] представляет собой реализацию архитектуры распространенной и адаптируемой нейронной сети для машинного обучения.  Алгоритм работает путем тестирования каждого возможного состояния входного атрибута с каждым возможным состоянием прогнозируемого атрибута и использует обучающие данные для вычисления вероятностей каждого сочетания. Эти вероятности можно использовать для задач классификации или регрессии, а также для прогнозирования исхода на основе входных атрибутов. Нейронную сеть можно также использовать для анализа взаимосвязей.  
  
 При создании модели интеллектуального анализа данных с помощью алгоритма нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] можно включить несколько выходных данных, а алгоритм создаст несколько сетей. Количество сетей, содержащихся в одной модели интеллектуального анализа данных, зависит от числа состояний (или значений атрибута) во входных столбцах, а также от числа прогнозируемых столбцов, используемых в модели интеллектуального анализа данных, и числа состояний в этих столбцах.  
  
## <a name="example"></a>Пример  
 Алгоритм нейронной сети ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] ) полезен при анализе сложных входных данных, полученных, например в результате производственного или коммерческого процесса или бизнес-задач, для которых предоставляется значительный объем обучающих данных, но при этом затруднено образование производных правил при помощи других алгоритмов.  
  
 Предлагаются следующие сценарии использования алгоритма нейронной сети ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] ):  
  
-   Анализ маркетинга и рекламы, например измерение эффективности прямой почтовой рассылки или рекламной кампании, проводимой по радио.  
  
-   Прогнозирование изменений цен на акции, колебаний валютных курсов или других изменчивых финансовых данных из данных с предысторией.  
  
-   Анализ производственных и промышленных процессов.  
  
-   Интеллектуальный анализ текста  
  
-   Любая прогнозирующая модель, которая анализирует сложные связи между большим количеством входных атрибутов и сравнительно малым количеством выходных атрибутов.  
  
## <a name="how-the-algorithm-works"></a>Принцип работы алгоритма  
 Алгоритм нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] создает сеть, состоящую из двух или трех слоев узлов (иногда называемых *нейронами*). Такими слоями являются *входной слой*, *скрытый слой*и *выходной слой*.  
  
 **Входной слой.** Входные узлы определяют все значения входных атрибутов для модели интеллектуального анализа данных и их вероятности.  
  
 **Скрытый слой.** Скрытые узлы получают входные данные от входных узлов и передают выходные данные выходных узлов. В скрытом слое различным вероятностям входных атрибутов назначаются весовые коэффициенты. Весовой коэффициент описывает существенность или важность отдельного входного атрибута для скрытого узла. Чем больше весовой коэффициент, назначенный входному атрибуту, тем большую важность имеет его значение. Весовые коэффициенты могут быть отрицательными. Входной атрибут с отрицательным коэффициентом препятствует, а не способствует наступлению выбранного результата.  
  
 **Выходной слой.** Выходные узлы представляют значения прогнозируемых атрибутов для модели интеллектуального анализа данных.  
  
 Подробное объяснение процесса создания и оценки входного, скрытого и выходного слоев см. в разделе [Технический справочник по алгоритму нейронной сети (Майкрософт)](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).  
  
## <a name="data-required-for-neural-network-models"></a>Данные, необходимые для моделей нейронной сети  
 Модель нейронной сети должна содержать ключевой столбец, один или несколько входных и прогнозируемых столбцов.  
  
 Модели интеллектуального анализа данных, использующие алгоритм нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] сильно зависят от значений, указанных для параметров, доступных в алгоритме. Эти параметры определяют порядок выборки данных, способ распределения или ожидаемого распределения данных в каждом столбце, а также условия, при которых вызывается выбор компонентов для ограничения значений, используемых в конечной модели.  
  
 Дополнительные сведения о задании параметров для настройки поведения модели см. в разделе [Технический справочник по алгоритму нейронной сети (Майкрософт)](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).  
  
## <a name="viewing-a-neural-network-model"></a>Просмотр модели нейронной сети  
 Для работы с данными и демонстрации корреляции между входами и выходами модели можно использовать **средство просмотра нейронных сетей (Майкрософт)**. С помощью этого средства просмотра можно применить фильтр по входным атрибутам и их значениям, чтобы получить графическое представление об их влиянии на выходные атрибуты. Подсказки в средстве просмотра покажут вероятность и точность, связанные с каждой парой входных и выходных значений. Дополнительные сведения см. в разделе [Просмотр модели с помощью средства просмотра нейронных сетей (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 Просмотреть структуру модели проще всего с помощью **средства просмотра деревьев содержимого общего вида (Майкрософт)**. Можно просмотреть входные и выходные атрибуты, а также сети, созданные моделью. Щелкнув любой узел, его можно развернуть и просмотреть статистику, связанную с узлами входного, выходного или скрытого слоя. Дополнительные сведения см. в разделе [Просмотр модели в средстве просмотра деревьев содержимого общего вида (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
## <a name="creating-predictions"></a>Создание прогнозов  
 После обработки модели сеть и весовые коэффициенты, хранящиеся в каждом узле, можно использовать для составления прогнозов. Модель нейронной сети поддерживает регрессионный анализ, анализ взаимосвязей и классификационный анализ. Поэтому каждый прогноз может иметь различное значение. Также можно запросить непосредственно модель, чтобы проверить обнаруженные взаимосвязи и получить связанную статистику. Примеры создания запросов к модели нейронной сети см. в разделе [Примеры запросов к модели нейронной сети](../../analysis-services/data-mining/neural-network-model-query-examples.md).  
  
 Общие сведения о создании запроса к модели интеллектуального анализа данных см. в разделе [Запросы интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="remarks"></a>Примечания  
  
-   Не поддерживается детализация и измерения интеллектуального анализа данных. Это объясняется тем, что структура узлов в модели интеллектуального анализа данных не обязательно однозначно соответствует базовым данным.  
  
-   Не поддерживается создание моделей в формате языка разметки прогнозирующих моделей (PMML).  
  
-   Поддерживается использование моделей интеллектуального анализа OLAP.  
  
-   Не поддерживается создание измерений интеллектуального анализа данных.  
  
## <a name="see-also"></a>См. также  
 [Технический справочник по алгоритму нейронной сети (Майкрософт)](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Содержимое моделей интеллектуального анализа данных для моделей нейронных сетей (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Примеры запросов к модели нейронной сети](../../analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Алгоритм логистической регрессии (Майкрософт)](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)  
  
  
