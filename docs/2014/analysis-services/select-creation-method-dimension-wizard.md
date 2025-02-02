---
title: Выбор метода создания (мастер измерений) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensiondefinition.f1
ms.assetid: 291b0b2d-a03a-4df6-82f7-90ad92d4d1cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d44afc5bb4c352a2cb5dfd39030a52db990e3a0b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069595"
---
# <a name="select-creation-method-dimension-wizard"></a>Выбор метода создания (мастер измерений)
  Страница **Выбор метода создания** используется, чтобы выбрать метод создания измерения.  
  
 **Чтобы открыть мастер измерений**  
  
-   В **обозревателе решений** [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] щелкните правой кнопкой мыши папку **Измерения** для проекта [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , а затем выберите команду **Новое измерение**.  
  
## <a name="options"></a>Параметры  
 **Использовать существующую таблицу**  
 Создайте измерение из одной или нескольких таблиц источника данных. Какие атрибуты будут доступны для измерения, будет зависеть от структуры данных в таблице.  
  
 Дополнительные сведения см. в разделе [Создание измерения с помощью существующей таблицы](multidimensional-models/create-a-dimension-by-using-an-existing-table.md).  
  
 **Создать в источнике данных таблицу времени**  
 Создайте таблицу времени в базовом источнике данных, а затем используйте эту таблицу, чтобы создать измерение времени. Используйте этот параметр, если такой таблицы не существует и нежелательно использовать скрипт для ее создания. В новой таблице времени будут содержаться данные для указанных в мастере диапазона данных, атрибутов и календарей.  
  
> [!NOTE]  
>  Чтобы использовать этот параметр, необходимо иметь разрешение на создание объектов в базовом источнике данных. Если отсутствует разрешение на создание объектов в источнике данных, попытайтесь использовать параметр **Создать на сервере таблицу времени** .  
  
 Дополнительные сведения см. в разделе [Создание измерения времени посредством формирования таблицы времени](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md).  
  
 **Создать на сервере таблицу времени**  
 Создайте таблицу времени непосредственно на сервере, а затем используйте эту таблицу, чтобы создать измерение времени. Используйте этот параметр, если отсутствует разрешение на создание объектов в базовом источнике данных. В новом измерении времени будут содержаться данные для указанных в мастере диапазона данных, атрибутов и календарей.  
  
 Дополнительные сведения см. в разделе [Создание измерения времени посредством формирования таблицы времени](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md).  
  
 **Создать в источнике данных таблицу, не содержащую время**  
 Спроектируйте измерение без базового реляционного источника данных, а затем создайте необходимую схему для источника данных. Этот подход известен как нисходящее моделирование.  
  
> [!NOTE]  
>  Чтобы использовать этот параметр, необходимо иметь разрешение на создание объектов в базовом источнике данных.  
  
 Можно построить измерение с шаблоном или без него. Чтобы построить измерение с шаблоном, выберите шаблон из списка **Шаблон** .  
  
 Дополнительные сведения см. в разделе [Создание измерения путем формирования в источнике данных таблицы, отличной от таблицы времени](multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md).  
  
 **Шаблон**  
 Выберите шаблон, используемый для создания измерения. Шаблоны предоставляют полный набор определений атрибутов и иерархий, ориентированных на конкретную бизнес-задачу.  
  
> [!NOTE]  
>  Этот параметр доступен только при выбранном параметре **Создать в источнике данных таблицу, не содержащую время** .  
  
## <a name="see-also"></a>См. также  
 [Справка F1 мастера измерений](dimension-wizard-f1-help.md)   
 [Измерения &#40;службы Analysis Services — многомерные данные&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Измерения в многомерных моделях](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
