---
title: Просмотр модели с помощью средства просмотра нейронных сетей Майкрософт | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
- classification mining model [Analysis Services]
- Microsoft Neural Network Viewer
- regression algorithms [Analysis Services]
- Neural Network Viewer [Analysis Services]
- neural network model [Analysis Services]
ms.assetid: 2343d746-c4f4-499b-9d3c-17d63310a9a3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1628eff6e5c440071126ce3508b977f9f7508ba5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086058"
---
# <a name="browse-a-model-using-the-microsoft-neural-network-viewer"></a>Просмотр модели с помощью средства просмотра нейронных сетей (Майкрософт)
  Средство просмотра нейронных сетей ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] ) в службах [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] отображает модели интеллектуального анализа данных, построенные с помощью алгоритма нейронной сети ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] ). Алгоритм нейронной сети [!INCLUDE[msCoName](../../includes/msconame-md.md)] создает классификационные и регрессивные модели интеллектуального анализа данных, с помощью которых можно выполнять анализ из нескольких входящих и исходящих источников. Это делает его полезным при выполнении различных видов открытого анализа и изучения. Дополнительные сведения об этом алгоритме см. в разделе [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md).  
  
 При исследовании модели при помощи средства просмотра нейронных сетей [!INCLUDE[msCoName](../../includes/msconame-md.md)] , обычно выбирается некий целевой атрибут и состояние, после чего средство просмотра используется для того, чтобы узнать, как входящие атрибуты отражаются на результате  
  
 Например, о некотором классе потенциальных клиентов известны следующие факты:  
  
-   Средних лет (от 40 до 50 лет).  
  
-   Владеет собственным домом.  
  
-   Имеет двоих детей, которые по-прежнему живут дома.  
  
 Как эти факты можно соотнести с вероятностью того, что клиент приобретет товар?  
  
 Построив модель нейронных сетей, в которой используются покупательские предпочтения как целевой результат, можно исследовать множество комбинаций различных характеристик заказчиков, таких как высокий доход, и узнать, какая комбинация атрибутов с наибольшей вероятностью влияет на приобретение. Например, можно обнаружить, что определяющим фактором является расстояние, которое они преодолевают, чтобы добраться на работу.  
  
 Если необходимо просмотреть более подробные сведения, например уравнения, которые описывают каждую найденную закономерность , можно переключить представления и использовать средство просмотра деревьев содержимого общего вида [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Дополнительные сведения см. в разделах [Просмотр модели в средстве просмотра деревьев содержимого общего вида (Майкрософт)](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) и [Средство просмотра деревьев содержимого общего вида (Майкрософт) (интеллектуальный анализ данных)](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="BKMK_ViewerTabs"></a> Вкладки средства просмотра  
 При просмотре модели интеллектуального анализа данных в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]модель отображается на вкладке **Средство просмотра моделей интеллектуального анализа данных** конструктора интеллектуального анализа данных с использованием соответствующего средства просмотра для данной модели. Средство просмотра нейронных сетей [!INCLUDE[msCoName](../../includes/msconame-md.md)] содержит следующие вкладки для исследования моделей интеллектуального анализа данных, построенных на нейронных сетях:  
  
-   [Входные данные](#BKMK_Inputs)  
  
-   [Выходные данные](#BKMK_Outputs)  
  
-   [Переменные](#BKMK_Characteristics)  
  
###  <a name="BKMK_Inputs"></a> Входные данные  
 Используйте вкладку **Входы** , чтобы выбрать атрибуты и значения атрибутов, используемые в качестве входной информации модели. По умолчанию средство просмотра открывается и отображает все атрибуты. В этом представлении по умолчанию модель выбирает, какие значения атрибутов наиболее важны, и отображает их.  
  
 Чтобы выбрать входной атрибут, щелкните столбец **Атрибут** сетки **Входные данные** и выберите нужный атрибут из раскрывающегося списка. (Список содержит только те атрибуты, которые включены в модель.)  
  
 В столбце **Значение** появится первое уникальное значение. Если щелкнуть значение по умолчанию, раскроется список всех возможных состояний соответствующего атрибута. Выберите состояние, которое необходимо проанализировать. Можно выбрать произвольное число атрибутов.  
  
 [В начало](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Outputs"></a> Выходные данные  
 Используйте вкладку **Выводы** , чтобы выбрать итоговый атрибут для исследования. Если при создании модели столбцы были определены в качестве прогнозируемых атрибутов, то можно выбрать любые два состояния для сравнения.  
  
 Доступные атрибуты содержатся в списке **Выходной атрибут** . В списках **Значение 1** и **Значение 2** можно указать два состояния, связанные с выбранным атрибутом. Эти два состояния выходного атрибута будут сравниваться в области **Переменные** .  
  
 [В начало](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> Переменные  
 Сетка в **переменных** вкладка содержит следующие столбцы: **Атрибут**, **значение**, **предпочтения [значение 1]**, и **предпочтения [значение 2]**. По умолчанию таблица отсортирована по столбцу **Предпочитает [значение 1]** по возрастанию. Чтобы изменить порядок сортировки, щелкните заголовок нужного столбца.  
  
 Полоса, находящаяся справа от атрибута, показывает, какое состояние выходного атрибута является предпочтительным для указанного состояния входного атрибута. Размер этой полосы показывает, насколько строго выходное состояние соответствует входному.  
  
 [В начало](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>См. также  
 [Microsoft Neural Network Algorithm](microsoft-neural-network-algorithm.md)   
 [Задачи и инструкции средства просмотра моделей интеллектуального анализа данных](mining-model-viewer-tasks-and-how-tos.md)   
 [Задачи и инструкции средства просмотра моделей интеллектуального анализа данных](mining-model-viewer-tasks-and-how-tos.md)   
 [Средства интеллектуального анализа данных](data-mining-tools.md)   
 [Средства просмотра моделей интеллектуального анализа данных](data-mining-model-viewers.md)  
  
  
