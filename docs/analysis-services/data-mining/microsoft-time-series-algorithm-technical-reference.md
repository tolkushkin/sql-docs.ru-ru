---
title: Microsoft Time Series Algorithm Technical Reference | Документация Майкрософт
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd520413e425ad7ef43eb44511365c43c51022f9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62753585"
---
# <a name="microsoft-time-series-algorithm-technical-reference"></a>Microsoft Time Series Algorithm Technical Reference
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  алгоритм временных рядов [!INCLUDE[msCoName](../../includes/msconame-md.md)] включает два отдельных алгоритма для анализа временных рядов:  
  
-   алгоритм ARTXP, который появился в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], оптимизирован для прогнозирования следующего вероятного значения в ряду;  
  
-   алгоритм ARIMA, добавленный в [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] для повышения точности долгосрочного прогнозирования.  
  
 По умолчанию службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] используют каждый алгоритм отдельно для обучения модели, а затем объединяют результаты, чтобы получить самый лучший прогноз для переменного числа прогнозов. Также можно выбрать для использования только один алгоритм, в зависимости от имеющихся данных и требований к прогнозам. В выпуске [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]также можно настроить точку раздела, которая управляет совместным применением алгоритмов в ходе создания прогнозов.  
  
 В этом разделе приводятся дополнительные сведения о реализации каждого алгоритма и о возможностях его настройки путем задания параметров для точной фильтрации результатов анализа и прогнозов.  
  
## <a name="implementation-of-the-microsoft-time-series-algorithm"></a>Реализация алгоритма временных рядов (Майкрософт)  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] разработала оригинальный алгоритм ARTXP, который применялся в SQL Server 2005. Он основан на реализации алгоритма дерева принятия решений [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Таким образом, алгоритм ARTXP можно описать, как модель дерева с авторегрессией для представления данных в периодических временных рядах. Этот алгоритм устанавливает соотношение между переменным количеством предыдущих элементов и каждым текущим элементом, для которого выполняется прогноз. Название ARTXP отражает тот факт, что алгоритм ART (или метод дерева с авторегрессией) применяется ко многим неизвестным первоначальным состояниям. Подробное описание алгоритма ARTXP см. в статье [Модели деревьев с авторегрессией для анализа временных рядов](http://go.microsoft.com/fwlink/?LinkId=45966).  
  
 Алгоритм ARIMA был добавлен к алгоритму временных рядов (Майкрософт) в SQL Server 2008 для повышения точности долгосрочного прогнозирования. Это реализация процесса вычисления интегрированных скользящих средних с авторегрессией, описанного Боксом и Дженкинсом. Методология ARIMA (интегрированное скользящее среднее с авторегрессией) позволяет определять зависимости в результатах наблюдений в форме последовательных временных рядов, при этом модель включает описание случайных скачков. Метод ARIMA также поддерживает мультипликативную сезонность. Читателям, интересующимся работой алгоритма ARIMA, рекомендуется прочесть основополагающую работу Бокса и Дженкинса; в этом разделе приводятся конкретные подробности реализации методологии ARIMA в алгоритме временных рядов (Майкрософт).  
  
 По умолчанию алгоритм временных рядов (Майкрософт) использует оба метода (ARIMA и ARTXP) и объединяет результаты для повышения точности прогнозирования. Если необходимо использовать один определенный метод, можно настроить параметры алгоритма на использование только метода ARTXP или ARIMA либо выбрать определенное сочетание результатов работы методов. Обратите внимание, что алгоритм ARTXP поддерживает перекрестное прогнозирование, а алгоритм ARIMA — нет. Поэтому перекрестное прогнозирование доступно, только если используется сочетание алгоритмов или если в модели задано использование только алгоритма ARTXP.  
  
## <a name="understanding-arima-difference-order"></a>Основные сведения о разностном порядке ARIMA  
 В этом разделе вводятся термины, необходимые для описания модели ARIMA, и обсуждается конкретная реализация *вычисления разностей* в алгоритме временных рядов (Майкрософт). С полным описанием этих терминов и понятий рекомендуется ознакомиться в публикации Бокса и Дженкинса.  
  
-   Член — это компонент математического уравнения. Например, член полиномного уравнения может состоять из сочетания переменных и констант.  
  
-   Формула ARIMA, включенная в алгоритм временных рядов (Майкрософт), использует как *авторегрессивные* члены, так и члены *скользящего среднего* .  
  
-   Модели временных рядов могут быть *стационарными* или *нестационарными*. *Стационарные модели* возвращаются к среднему значению, хотя им может быть свойственна цикличность, а у *нестационарных* моделей отсутствует точка равновесия, они подвержены большей дисперсии — изменениям, вызываемым влиянием *возмущений*или внешних переменных.  
  
-   Цель *вычисления разностей* заключается в стабилизации временного ряда, который должен стать стационарным.  
  
-   *Разностный порядок* представляет количество операций вычисления разности между значениями для временного ряда.  
  
 Алгоритм временных рядов (Майкрософт) извлекает значения из ряда данных и пытается согласовать их с шаблоном. Если ряд данных еще не является стационарным, алгоритм применяет разностный порядок. Каждое повышение разностного порядка, как правило, делает временной ряд более стационарным.  
  
 Например, если имеется временной ряд (z1, z2, …, zn) и выполнять вычисления с использованием единичного разностного порядка, будет получен новый ряд (y1, y2,..., yn-1), где `yi = zi+1-zi`. Если разностный порядок равен 2, алгоритм формирует новый ряд \`(x1, x2, …, xn-2) ", основываясь на ряде, полученном из уравнения первого порядка. Правильное количество операций вычисления разности зависит от данных. В моделях, отображающих постоянные тренды, чаще всего используется единичный разностный порядок; второй разностный порядок может указывать на изменяющийся со временем тренд.  
  
 По умолчанию разностный порядок, используемый в алгоритме временных рядов (Майкрософт), равен -1, то есть алгоритм автоматически выбирает оптимальное значение разностного порядка. Как правило, оптимальное значение равно 1 (если требуется вычисление разности), но в некоторых определенных ситуациях алгоритм увеличивает это значение до максимального, равного 2.  
  
 Алгоритм временных рядов (Майкрософт) определяет оптимальный разностный порядок ARIMA, используя значения авторегрессии. Алгоритм исследует значения AR и устанавливает скрытый параметр ARIMA_AR_ORDER, который представляет порядок членов AR. Этот скрытый параметр ARIMA_AR_ORDER может принимать значения от -1 до 8. При значении по умолчанию, равном -1, алгоритм автоматически выбирает оптимальный разностный порядок.  
  
 Если значение параметра ARIMA_AR_ORDER больше 1, алгоритм умножает временной ряд на полиномный член. Если один из членов полиномной формулы разрешается с корнем 1 или близким к 1, алгоритм пытается сохранить стабильность модели, удаляя такой член и увеличивая разностный порядок на 1. Если разностный порядок уже максимален, член удаляется, а разностный порядок не изменяется.  
  
 Например, если значение AR = 2, получаемый полиномный член AR может иметь следующий вид: `1 - 1.4B + .45B^2 = (1- .9B) (1- 0.5B)`. Обратите внимание на член `(1- .9B)` , корень которого составляет около 0,9. Алгоритм удаляет этот член из полиномной формулы, но не может увеличить разностный порядок на единицу, так как он уже равен максимальному значению 2.  
  
 Важно отметить, что единственный способ **принудительного** изменения разностного порядка — это использование недокументированного и неподдерживаемого параметра ARIMA_DIFFERENCE_ORDER. Этот скрытый параметр определяет, сколько раз алгоритм выполняет вычисление разностей для временных рядов, и может устанавливаться посредством ввода пользовательского параметра алгоритма. Однако изменять это значение не рекомендуется, если вы не готовы к экспериментам и не знакомы с выполняемыми вычислениями. Кроме того, учтите, что на данный момент нет механизма (и скрытых параметров), позволяющего управлять пороговым значением, при котором срабатывает увеличение разностного порядка.  
  
 Наконец, учтите, что описанная выше формула относится к упрощенному случаю, без подсказок сезонности. При указании подсказок сезонности в левую часть уравнения добавляется по одному отдельному полиномному члену AR для каждой из подсказок сезонности, а для исключения членов, которые могут дестабилизировать разностные ряды, применяется та же стратегия.  
  
## <a name="customizing-the-microsoft-time-series-algorithm"></a>Настройка алгоритма временных рядов (Майкрософт)  
 Алгоритм временных рядов [!INCLUDE[msCoName](../../includes/msconame-md.md)] поддерживает следующие параметры, которые влияют на порядок работы, производительность и точность итоговой модели интеллектуального анализа данных.  
  
> [!NOTE]  
>  Алгоритм временных рядов (Майкрософт) доступен во всех выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], однако некоторые дополнительные функции, в том числе параметры для настройки анализа временных рядов, доступны только в специальных выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Сведения о функциях, поддерживаемых различными выпусками [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], см. в статье [Возможности, поддерживаемые выпусками SQL Server 2016](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).  
  
### <a name="detection-of-seasonality"></a>Обнаружение сезонности  
 Оба алгоритма ARIMA и ARTXP поддерживают обнаружение сезонности или периодичности. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] используют быстрое преобразование Фурье для определения сезонности до этапа обучения. Тем не менее можно повлиять на обнаружение сезонности и результаты анализа временных рядов, задав параметры алгоритма.  
  
-   Изменяя значение параметра *AUTODETECT_SEASONALITY*, можно изменить возможное количество создаваемых временных интервалов.  
  
-   Задавая значение (или несколько значений) для параметра *PERIODICITY_HINT*, можно предоставить алгоритму данные об ожидаемых циклах в данных и, вероятно, повысить точность обнаружения.  
  
> [!NOTE]  
>  Алгоритмы ARTXP и ARIMA очень чувствительны к подсказкам сезонности. Поэтому указание неправильной подсказки может отрицательно сказаться на результатах.  
  
### <a name="choosing-an-algorithm-and-specifying-the-blend-of-algorithms"></a>Выбор алгоритма и указание комбинации алгоритмов  
 По умолчанию, а также в случае выбора параметра MIXED службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] объединяют алгоритмы и назначает им равный вес. Однако в выпуске Enterprise Edition можно указать определенный алгоритм или настроить пропорциональное соотношение алгоритмов в результатах, задав параметр, который будет смещать баланс результатов в сторону краткосрочного или долгосрочного прогнозирования. По умолчанию параметр *FORECAST_METHOD* имеет значение MIXED, и службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] используют оба алгоритма, назначая для них весовые коэффициенты, которые максимально учитывают преимущества каждого алгоритма.  
  
-   Выбор алгоритмов управляется параметром *FORECAST_METHOD* .  
  
-   Если необходимо использовать перекрестное прогнозирование, необходимо указать параметр ARTXP или MIXED, поскольку алгоритм ARIMA не поддерживает перекрестное прогнозирование.  
  
-   Задайте для параметра *FORECAST_METHOD* значение ARTXP, если предпочтителен краткосрочный прогноз.  
  
-   Задайте для параметра *FORECAST_METHOD* значение ARIMA, если необходимо улучшить долгосрочное прогнозирование.  
  
 В выпуске Enterprise Edition также можно настроить метод, которым службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] сочетают использование алгоритмов ARIMA и ARTXP. Можно задать стартовую точку для объединения результатов, а также скорость изменения, установив параметр *PREDICTION_SMOOTHING* .  
  
-   Если параметр *PREDICTION_SMOOTHING* равен 0, то в модели будет использоваться только алгоритм ARTXP.  
  
-   Если параметр *PREDICTION_SMOOTHING* равен 1, то в модели будет использоваться только алгоритм ARIMA.  
  
-   Если значение параметра *PREDICTION_SMOOTHING* лежит между 0 и 1, то модель использует алгоритм ARTXP как источник весовых коэффициентов — экспоненциально убывающую функцию шагов прогнозирования. Алгоритм ARIMA получает весовые коэффициенты, которые в сумме с коэффициентами ARTXP составляют 1. Для сглаживания кривых в модели используется константа нормирования и стабилизации.  
  
 Если прогноз охватывает не более 5 временных срезов, то алгоритм ARTXP почти всегда будет лучшим выбором. Однако чем больше число прогнозируемых временных срезов, тем, как правило, лучшие результаты дает алгоритм ARIMA.  
  
 На следующей диаграмме показано, как модель объединяет результаты алгоритмов, если параметр *PREDICTION_SMOOTHING* имеет значение по умолчанию (0,5). Вначале алгоритмы ARIMA и ARTXP получают равные весовые коэффициенты, но по мере увеличения числа шагов прогнозирования вес алгоритма ARIMA растет.  
  
 ![Стандартная кривая для сочетания алгоритмов временных рядов](../../analysis-services/data-mining/media/time-series-mixing-default.gif "Стандартная кривая для сочетания алгоритмов временных рядов")  
  
 Для сравнения представлена следующая диаграмма, где показано объединение алгоритмов в случае, если параметр *PREDICTION_SMOOTHING* имеет значение 0,2. На шаге [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]модель присваивает ARIMA вес 0,2, а ARTXP — вес 0,8. Затем весовые коэффициенты для ARIMA экспоненциально возрастают, а для ARTXP — убывают.  
  
 ![Кривая затухания для сочетания моделей временных рядов](../../analysis-services/data-mining/media/time-series-blending-curve.gif "кривая затухания для сочетания моделей временных рядов")  
  
### <a name="setting-algorithm-parameters"></a>Задание параметров алгоритма  
 В следующей таблице описаны параметры, которые можно использовать с алгоритмом временных рядов [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
|Параметр|Описание|  
|---------------|-----------------|  
|*AUTO_DETECT_PERIODICITY*|Указывает числовое значение от [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] до 1, используемое для обнаружения периодичности. Значение по умолчанию равно 0,6.<br /><br /> Если значение ближе к [!INCLUDE[tabValue](../../includes/tabvalue-md.md)], то периодичность обнаруживается только для строго периодических данных.<br /><br /> Установка этого значения в значение, более близкое к 1, повышает вероятность обнаружения многих закономерностей, близких к периодическим, и автоматического создания подсказок периодичности.<br /><br /> Примечание. Освободили большого количества подсказок периодичности, скорее всего, приведет к значительно увеличит время обучения модели, но более точных моделей.|  
|*COMPLEXITY_PENALTY*|Управляет ростом дерева решений. Значение по умолчанию равно 0,1.<br /><br /> Уменьшение этого значения повышает вероятность разбиения. Увеличение этого значения снижает вероятность разбиения.<br /><br /> Примечание. Этот параметр доступен только в некоторых выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*FORECAST_METHOD*|Указывает, какой алгоритм используется для анализа и прогнозирования. Возможные значения — ARTXP, ARIMA и MIXED. Значением по умолчанию является MIXED.|  
|*HISTORIC_MODEL_COUNT*|Указывает число моделей с предысторией, которые будут построены. Значение по умолчанию равно 1.<br /><br /> Примечание. Этот параметр доступен только в некоторых выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*HISTORICAL_MODEL_GAP*|Указывает временной промежуток между двумя последовательными моделями с предысторией. Значение по умолчанию равно 10. Это значение выражено в единицах времени, которые определяются моделью.<br /><br /> Например, если установить это значение равным g, модели с предысторией будут строиться для данных, усеченных временными срезами с интервалами g, 2\*g, 3\*g и так далее.<br /><br /> Примечание. Этот параметр доступен только в некоторых выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*INSTABILITY_SENSITIVITY*|Управляет точкой, в которой дисперсия прогноза превышает определенное пороговое значение, после чего алгоритм ARTXP запрещает такие прогнозы. Значение по умолчанию — 1.<br /><br /> Примечание. Этот параметр не применяется к моделям, использующим только алгоритм ARIMA.<br /><br /> Значение по умолчанию (1) означает режим работы, аналогичный [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] наблюдают за нормализованным стандартным отклонением для каждого прогноза. Как только это значение превышает пороговое значение для какого-либо прогноза, алгоритм временных рядов возвращает значение NULL и прекращает процесс прогнозирования.<br /><br /> Значение [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] отключает проверку нестабильности. Это значит, что можно создавать неограниченное число прогнозов независимо от дисперсии.<br /><br /> Примечание. Этот параметр можно изменить только в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise. В выпуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] используют только значение по умолчанию (1).|  
|*MAXIMUM_SERIES_VALUE*|Указывает максимальное значение, используемое для прогнозов. Этот параметр используется наряду с параметром *MINIMUM_SERIES_VALUE*для ограничения прогнозов с учетом некоторого ожидаемого диапазона. Например, можно указать, что прогнозируемый объем продаж в течение любых суток никогда не должен превышать величину запасов товаров.<br /><br /> Примечание. Этот параметр доступен только в некоторых выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*MINIMUM_SERIES_VALUE*|Задает минимальное прогнозируемое значение. Этот параметр используется наряду с параметром *MAXIMUM_SERIES_VALUE*для ограничения прогнозов с учетом некоторого ожидаемого диапазона. Например, можно указать, что прогнозируемый объем продаж никогда не должен быть отрицательным числом.<br /><br /> Примечание. Этот параметр доступен только в некоторых выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*MINIMUM_SUPPORT*|Указывает минимальное количество временных срезов, необходимых для разбиения каждого дерева временных рядов. Значение по умолчанию равно 10.|  
|*MISSING_VALUE_SUBSTITUTION*|Указывает порядок заполнения пропусков в данных с предысторией. По умолчанию пропуски в данных не допускаются. В следующей таблице перечислены возможные значения для этого параметра.<br /><br /> **Предыдущий**: Повторяет значение из предыдущего временного среза.<br /><br /> **Среднее**. Использует значение скользящего среднего среди временных рядов, использованных в обучении.<br /><br /> Числовая константа: Использует конкретное число для замены всех отсутствующих значений.<br /><br /> **Нет**. По умолчанию. Замещает отсутствующие значения значениями, расположенными на кривой обученной модели.<br /><br /> <br /><br /> Обратите внимание: если в данных содержится несколько рядов, ряды не могут иметь неоднородные границы. Это значит, что для всех рядов начальные и конечные точки должны совпадать. <br />                    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] также используют значение этого параметра, чтобы заполнять пропуски в новых данных в ходе выполнения инструкции **PREDICTION JOIN** в модели временных рядов.|  
|*PERIODICITY_HINT*|Предоставляет подсказку для алгоритма, касающуюся периодичности данных. Например, если продажи варьируются в зависимости от года, а в ряду в качестве единицы измерения используются месяцы, то периодичность равна 12. Этот параметр имеет формат {n [, n]}, где n — любое положительное число.<br /><br /> Число n внутри квадратных скобок [] является необязательным и может повторяться сколь угодно часто. Например, чтобы задать несколько подсказок периодичности для данных, пополняемых ежемесячно, можно ввести {12, 3, 1}, чтобы обнаруживать закономерности, проявляющиеся ежегодно, ежемесячно и ежеквартально. Однако подсказки периодичности сильно влияют на качество работы модели. Если заданное указание отличается от реальной периодичности, это может отрицательно сказаться на результатах.<br /><br /> Значение по умолчанию — {1}.<br /><br /> Обратите внимание: фигурные скобки указывать обязательно. Кроме того, этот параметр имеет строковый тип данных. Поэтому, если нужно ввести этот параметр в составе инструкции расширений интеллектуального анализа данных, необходимо поместить в кавычки числовое значение в фигурных скобках.|  
|*PREDICTION_SMOOTHING*|Указывает, как модель должна использовать сочетание двух алгоритмов для оптимизации прогнозов. Можно ввести любое число от [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] до 1 или использовать одно из следующих значений.<br /><br /> [!INCLUDE[tabValue](../../includes/tabvalue-md.md)].<br />                          Указывает, что при прогнозировании используется только алгоритм ARTXP. Процесс прогнозирования оптимизируется для небольшого числа прогнозов.<br /><br /> 1: Указывает, что прогноза используется только алгоритм ARIMA. Процесс прогнозирования оптимизируется для большого числа прогнозов.<br /><br /> 0.5: По умолчанию. Указывает, что при прогнозировании используются оба алгоритма, а их результаты объединяются.<br /><br /> <br /><br /> При выполнении сглаживания прогноза используйте параметр *FORECAST_METHOD* для управления обучением.   Обратите внимание, что этот параметр доступен только в некоторых выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
### <a name="modeling-flags"></a>Флаги моделирования  
 Алгоритм временных рядов [!INCLUDE[msCoName](../../includes/msconame-md.md)] поддерживает следующие флаги модели. Чтобы задать порядок обработки в ходе анализа значений в каждом столбце, во время создания структуры или модели интеллектуального анализа данных определяются флаги модели. Дополнительные сведения см. в разделе [Флаги моделирования (интеллектуальный анализ данных)](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
|Флаг моделирования|Описание|  
|-------------------|-----------------|  
|NOT NULL|Указывает, что столбец не может принимать значение NULL. Если во время обучения модели службы Analysis Services обнаружат значение NULL, возникнет ошибка.<br /><br /> Применяется к столбцам структуры интеллектуального анализа данных.|  
|MODEL_EXISTENCE_ONLY|Означает, что столбец будет обрабатываться как имеющий два возможных состояния: Отсутствует и присутствует. NULL означает отсутствие значения.<br /><br /> Применяется к столбцам модели интеллектуального анализа данных.|  
  
## <a name="requirements"></a>Требования  
 Модель временных рядов должна иметь ключевой столбец времени, содержащий уникальные значения, а также входные столбцы и по крайней мере один прогнозируемый столбец.  
  
### <a name="input-and-predictable-columns"></a>Входные и прогнозируемые столбцы  
 В следующей таблице перечислены конкретные типы содержимого входных столбцов, типы содержимого прогнозируемых столбцов и флаги модели, поддерживаемые алгоритмом временных рядов [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
|Столбец|Типы содержимого|  
|------------|-------------------|  
|Входной атрибут|Непрерывные, ключевые, ключевые времени и табличные|  
|Прогнозируемый атрибут|Непрерывные, табличные|  
  
> [!NOTE]  
>  Типы содержимого Cyclical и Ordered поддерживаются, но алгоритм обрабатывает их как дискретные величины и не производит их особой обработки.  
  
## <a name="see-also"></a>См. также  
 [Алгоритм временных рядов (Майкрософт)](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Примеры запросов моделей временных рядов](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Содержимое моделей интеллектуального анализа данных для моделей временных рядов (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
