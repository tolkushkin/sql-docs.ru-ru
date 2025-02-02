---
title: Размещение меток на диаграмме (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5db74e0b-8be8-4b47-b386-faab56dffa9b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc04d47058c1ef1bc3929d941a6680eb013fcc53
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105440"
---
# <a name="position-labels-in-a-chart-report-builder-and-ssrs"></a>Размещение меток на диаграмме (построитель отчетов и службы SSRS)
  Поскольку формы всех типов диаграмм различны, метки точек данных помещаются в оптимальные положения, не ухудшающие удобочитаемость диаграммы. Позиции меток по умолчанию зависят от типа диаграммы:  
  
-   на диаграммах с накоплением метки могут располагаться только внутри рядов;  
  
-   на воронкообразных и пирамидальных диаграммах метки помещаются за пределами столбца;  
  
-   на круговых диаграммах метки помещаются внутри отдельных срезов;  
  
-   на линейчатых диаграммах метки помещаются за пределами столбцов, представляющих точки данных;  
  
-   на полярных диаграммах метки помещаются за пределами круговой области, представляющей точки данных.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-position-of-point-labels-in-a-pie-chart"></a>Изменение положения меток точек на круговой диаграмме  
  
1.  Создайте круговую диаграмму.  
  
2.  В области конструктора щелкните правой кнопкой мыши диаграмму и выберите команду **Отобразить метки данных**.  
  
3.  Откройте панель «Свойства». На вкладке **Вид** щелкните **Свойства**.  
  
4.  Щелкните диаграмму в области конструктора. В панели «Свойства» отображаются свойства диаграммы.  
  
5.  В разделе **Общие** разверните узел **CustomAttributes** . Отобразится список атрибутов круговой диаграммы.  
  
6.  Выберите значение для свойства PieLabelStyle.  
  
### <a name="to-change-the-position-of-point-labels-in-a-funnel-or-pyramid-chart"></a>Изменение положения меток точек на воронкообразной или пирамидальной диаграмме  
  
1.  Создайте воронкообразную или пирамидальную диаграмму.  
  
2.  В области конструктора щелкните правой кнопкой мыши диаграмму и выберите команду **Отобразить метки данных**.  
  
3.  Откройте панель «Свойства». На вкладке **Вид** щелкните **Свойства**.  
  
4.  Щелкните диаграмму в области конструктора. В панели «Свойства» отображаются свойства диаграммы.  
  
5.  В разделе **Общие** разверните узел **CustomAttributes** . Отобразится список атрибутов воронкообразной диаграммы.  
  
6.  Для воронкообразной диаграммы выберите значение для свойства FunnelLabelStyle. Для воронкообразной диаграммы выберите значение для свойства PyramidLabelStyle.  
  
    > [!NOTE]  
    >  Если это свойство имеет значение `OutsideInColumn`, метки отображаются в вертикальном столбце. Положение столбца изменить невозможно.  
  
### <a name="to-change-the-position-of-point-labels-in-a-bar-chart"></a>Изменение положения меток точек на линейчатой диаграмме  
  
1.  Создайте линейчатую диаграмму.  
  
2.  В области конструктора щелкните правой кнопкой мыши диаграмму и выберите команду **Отобразить метки данных**.  
  
3.  Откройте панель «Свойства». На вкладке **Вид** щелкните **Свойства**.  
  
4.  Щелкните диаграмму в области конструктора. В панели «Свойства» отображаются свойства диаграммы.  
  
5.  В разделе **Общие** разверните узел **CustomAttributes** . Отобразится список атрибутов линейчатой диаграммы.  
  
6.  Выберите значение для свойства BarLabelStyle.  
  
 Если стиль линейчатой диаграммы имеет значение `Outside`, метки будут располагаться за пределами линейки, пока она помещается в области диаграммы. Если метку не удается поместить за пределами линейки, но ее можно расположить в области диаграммы, метка помещается внутри линейки в позиции, ближайшей к концу линейки.  
  
### <a name="to-change-the-position-of-point-labels-in-an-area-column-line-or-scatter-chart"></a>Изменение положения меток точек в диаграмме с областями, гистограмме, графике и точечной диаграмме  
  
1.  Создайте диаграмму с областями, гистограмму, график или точечную диаграмму.  
  
2.  В области конструктора щелкните правой кнопкой мыши диаграмму и выберите команду **Отобразить метки данных**.  
  
3.  Откройте панель «Свойства». На вкладке **Вид** щелкните **Свойства**.  
  
4.  Щелкните ряд в области конструктора. На панели «Свойства» отображаются свойства ряда.  
  
5.  В разделе **Данные** разверните узел **Точка данных** , а затем узел **Метка**.  
  
6.  Выберите значение для свойства Position.  
  
## <a name="see-also"></a>См. также  
 [Круговые диаграммы (построитель отчетов и службы SSRS)](charts-report-builder-and-ssrs.md)   
 [Линейчатые диаграммы (построитель отчетов и службы SSRS)](bar-charts-report-builder-and-ssrs.md)   
 [Форматирование меток оси на диаграмме (построитель отчетов и службы SSRS)](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Форматирование меток оси в виде значений даты или валюты &#40;построитель отчетов и службы SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Отображение меток точек данных за пределами круговой диаграммы (построитель отчетов и службы SSRS)](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Форматирование точек данных на диаграмме (построитель отчетов и службы SSRS)](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
