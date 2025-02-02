---
title: (SQL Server Data Mining Add-ins) Диаграмма роста прибыли | Документация Майкрософт
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- profit chart
- mining models, charting
- mining models, testing
ms.assetid: 5c902543-4da9-4db3-99d5-4ce04c43d7ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32ee1539c734c549f89d5b3db8ec4add467a72b2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070589"
---
# <a name="profit-chart-sql-server-data-mining-add-ins"></a>Диаграмма роста прибыли (надстройки интеллектуального анализа данных SQL Server)
  ![Кнопка диаграммы роста прибыли на ленте «Интеллектуальный анализ данных»](media/dmc-profitchart.gif "Диаграмма роста прибыли кнопки на ленте «Интеллектуальный анализ данных»")  
  
 На диаграмме роста прибыли отображается оцененное увеличение прибыли, связанное с использованием модели интеллектуального анализа данных для определения, с какими заказчиками должна связаться компания в соответствии со сценарием. Ось Y на диаграмме представляет прибыль, в то время как ось X — процент совокупности, с которым связалась компания. На типичной диаграмме роста прибыли отображается увеличение прибыли до определенной точки, после которой прибыль уменьшается при связи с еще большей совокупностью.  
  
## <a name="configuring-the-profit-chart"></a>Настройка диаграммы роста прибыли  
 Диаграмма точности оценивает только вероятность точности или неточности прогнозов, а диаграмма роста прибыли содержит в своем прогнозе реальные знания о последствиях предпринимаемых действий. Это достигается с помощью принятия в расчет следующих факторов, указываемых при работе с мастером.  
  
-   **Заполнение**  
  
     Количество вариантов в наборе данных, используемое для создания диаграммы точности прогнозов. Например, количество потенциальных покупателей.  
  
-   **Фиксированные затраты**  
  
     Фиксированные издержки, связанные с бизнес-задачами. При оценке решения целевой рассылки эти издержки не будут зависеть от таких переменных, как количество телефонных звонков или количество рекламных писем.  
  
-   **Индивидуальные издержки**  
  
     Расходы, добавляющиеся к фиксированным издержкам, которые могут быть связаны с обращением к каждому заказчику. Например, рекламные письма или телефонные звонки.  
  
-   **Доход на единицу**  
  
     Сумма прибыли, связанная с каждой успешной продажей.  
  
## <a name="using-the-profit-chart-wizard"></a>Использование мастера диаграмм роста прибыли  
 При создании диаграммы роста прибыли необходимо ссылаться на существующую модель интеллектуального анализа данных. Можно просматривать модели, чтобы найти подходящую модель, данные, нажав кнопку **Управление моделями** или **Обзор** просмотреть сведения об алгоритме, который был использован и столбцы в модели интеллектуального анализа данных.  
  
 Дополнительные сведения см. в разделе [Просмотр моделей в Excel &#40;SQL Server Data Mining Add-ins&#41; ](browsing-models-in-excel-sql-server-data-mining-add-ins.md) и [Управление моделями &#40;SQL Server Data Mining Add-ins&#41;](manage-models-sql-server-data-mining-add-ins.md).  
  
#### <a name="to-create-a-profit-chart"></a>Создание диаграммы роста прибыли  
  
1.  Выберите существующую модель.  
  
2.  Укажите столбец для выполнения прогноза и целевое значение, если необходимо.  
  
3.  Выберите источник данных, данные из которого будут использоваться моделью для создания прогноза. Эти данные не должны совпадать с данными, которые использовались при создании модели.  
  
4.  Сопоставьте столбцы с новыми (исходными) данными со столбцами, используемыми в модели интеллектуального анализа данных. Если имена столбцов аналогичны, мастер сопоставит их автоматически.  
  
5.  Введите сведения о затратах, необходимые мастеру: фиксированные издержки, индивидуальные издержки, заполнение и ожидаемый доход.  
  
6.  При необходимости можно ввести прогрессивный ряд затрат (нажмите кнопку обзора **(...)**  кнопки). Например, отправку можно удешевить, увеличив количество отправляемых элементов, так что можно ввести различную стоимость в зависимости от количества элементов, а мастер автоматически установит затраты для каждого типового размера.  
  
7.  Мастер создает диаграмму, которая включает анализ затрат для модели.  
  
### <a name="requirements"></a>Требования  
 Если прогнозируется дискретное числовое значение, необходимо выбрать для прогноза точное целевое значение.  
  
## <a name="understanding-the-profit-chart"></a>Основные сведения о диаграмме роста прибыли  
 Диаграмма роста прибыли содержит серую вертикальную линию, которую можно перемещать, щелкая в разных местах диаграммы. **Обозначения интеллектуального анализа данных** отображает оценку, коррекция совокупности и вероятность прогноза, связанные с местоположением серой линии на диаграмме. Если при применении этой серой линии выбрать точку максимальной прибыли, то можно использовать значение вероятности прогнозирования, чтобы определить порог вероятности для связи с заказчиком.  
  
 Например, пик кривой прибыли лежит на 55 % совокупности, а соответствующая вероятность прогнозирования равна 20 %, это указывает на то, что для достижения максимальной прибыли необходимо связаться только с заказчиками, чья вероятность ответа равна 20 % или выше.  
  
## <a name="see-also"></a>См. также  
 [Проверка моделей и использование моделей для прогнозирования &#40;интеллектуального анализа данных надстройки для Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
