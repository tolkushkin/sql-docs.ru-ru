---
title: Понимание требований для временного ряда моделирование (учебник по интеллектуальному анализу интеллектуальному анализу данных) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1ce2b3e3-108a-4f7e-985f-a20b816d0da7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5b3438e832f28329cb0fec764d3a4846bae18ede
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043120"
---
# <a name="understanding-the-requirements-for-a-time-series-model-intermediate-data-mining-tutorial"></a>Основные сведения о требованиях для модели временных рядов (учебник по интеллектуальному анализу данных — средний уровень)
  Данные для модели прогнозирования при подготовке должны содержать один столбец, который может быть использован для идентификации этапов временных рядов. Этот столбец будет обозначаться `Key Time`. Этот столбец является ключом и должен содержать уникальные числовые значения.  
  
 Правильный выбор единицы для столбца `Key Time` является важной частью анализа. Например, пусть данные о продажах обновляются каждую минуту. В качестве единицы временного ряда не обязательно использовать минуты. Более разумно будет сводить данные о продажах по дням, неделям или месяцам. Если непонятно, какую единицу времени следует использовать, можно создать новое представление источника данных для каждого статистического выражения и построить связанные модели, чтобы посмотреть, не появляются ли разные тренды на каждом уровне статистической обработки.  
  
 В этом учебнике данные о продажах собираются ежедневно и заносятся в транзакционную базу данных продаж, но для интеллектуального анализа данные заранее объединены по месяцам с использованием представления.  
  
 Кроме того, для анализа желательно, чтобы в данных было как можно меньше промежутков. Если планируется анализ нескольких рядов данных, то желательно, чтобы все ряды начинались с одной даты и заканчивались одной датой. Если в данных имеются промежутки (кроме как в начале и в конце ряда), то для заполнения ряда можно использовать параметр MISSING_VALUE_SUBSTITUTION. Службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] также предоставляют несколько возможностей замены отсутствующих данных средними значениями или константами.  
  
> [!WARNING]  
>  Сводная диаграмма и сводная таблица, входившие в предыдущие версии конструктора представлений источников данных, больше не предоставляются. Рекомендуется заранее выявить промежутки в данных временных рядов, используя профилировщик данных, входящий в состав служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], и другие средства.  
  
### <a name="to-identify-the-time-key-for-the-forecasting-model"></a>Идентификация ключа времени для модели прогнозирования  
  
1.  В области **SalesByRegion.dsv [Design]**, щелкните правой кнопкой мыши таблицу vTimeSeries и выберите **Просмотр данных**.  
  
     Откроется новая вкладка, под названием **Просмотр таблицы vTimeSeries**.  
  
2.  На **таблицы** вкладке, просмотрите данные, используемые в столбцах TimeIndex и Reporting Date.  
  
     Оба столбца представляют собой последовательности уникальных значений. Любой из них может служить ключом временного ряда, однако типы данных в этих столбцах различаются. Алгоритм временных рядов (Майкрософт) не требует наличия типа данных `datetime`, необходимо только, чтобы значения были отличающимися и упорядоченными. Поэтому в качестве ключа времени для модели прогнозирования может быть использован любой столбец.  
  
3.  В области конструктора представления источника данных выберите столбец Reporting Date и **свойства**. Далее щелкните столбец TimeIndex и выберите **свойства**.  
  
     Поле TimeIndex имеет тип данных System.Int32, в то время как поле Reporting Date имеет тип данных System.DateTime. Во многих хранилищах данных значения даты и времени преобразуются в целые числа, и целочисленный столбец служит ключом, что повышает производительность индексирования. Однако если использовать такой столбец, то алгоритм временных рядов (Майкрософт) будет составлять прогнозы, используя значения из будущего: 201014, 201014 и т. д. Так как необходимо представить с использованием календарных дат прогноз данных продаж, будет использовать столбец Reporting Date в качестве уникального идентификатора последовательности.  
  
### <a name="to-set-the-key-in-the-data-source-view"></a>Задание ключа в представлении источников данных  
  
1.  В области **SalesByRegion.dsv**, выделите таблицу vTimeSeries.  
  
2.  Щелкните правой кнопкой мыши столбец Reporting Date и выберите **задать логический первичный ключ**.  
  
## <a name="handling-missing-data-optional"></a>Обработка отсутствующих данных (необязательно)  
 Если в каком-либо ряду имеются отсутствующие данные, то при попытке обработать модель может быть выдана ошибка. Устранить эту проблему можно несколькими способами.  
  
-   Службы Analysis Services могут заполнить отсутствующее значение вычисленным средним или предыдущим значением. Для этого необходимо задать параметр MISSING_VALUE_SUBSTITUTION при создании модели интеллектуального анализа данных. Дополнительные сведения об этом параметре см. в разделе [Microsoft Time Series Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md). Сведения о способах изменения параметров существующей модели интеллектуального анализа данных, см. в разделе [Просмотр или изменение параметров алгоритма](../../2014/analysis-services/data-mining/view-or-change-algorithm-parameters.md).  
  
-   Можно изменить источник данных или отфильтровать базовое представление, чтобы устранить неоднородность ряда или заменить значения. Это можно сделать в реляционном источнике данных. Также можно изменить представление источников данных, создавая пользовательские именованные запросы или именованные вычисления. Дополнительные сведения см. в разделе [Представления источников данных в многомерных моделях](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md). Последняя задача этого занятия представляет пример того, как построить именованный запрос и пользовательское вычисление.  
  
 Для этого сценария некоторые данные отсутствуют в начале одного ряда: то есть нет данных для строки продукта T1000 июля 2007 г. Все ряды заканчиваются в одну дату, и других отсутствующих значений нет.  
  
 Требованием алгоритма временных рядов Майкрософт является то, что все ряды, включенные в одну модель должна же **конца** точки. Поскольку модель велосипеда T1000 появилась в 2007 г., данные для этого ряда начинаются позже, чем для других моделей велосипедов, но ряд заканчивается на ту же дату, поэтому данные являются приемлемыми.  
  
#### <a name="to-close-the-data-source-view-designer"></a>Закрытие конструктора представлений источников данных  
  
-   Щелкните правой кнопкой мыши по вкладке **Просмотр таблицы vTimeSeries**и выберите **закрыть**.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
 [Создание структуры и модели прогнозирования &#40;средний уровень учебник по интеллектуальному анализу данных&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>См. также  
 [Алгоритм временных рядов (Майкрософт)](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
