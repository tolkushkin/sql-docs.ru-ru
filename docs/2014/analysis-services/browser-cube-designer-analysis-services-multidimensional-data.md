---
title: Браузер (конструктор кубов) (службы Analysis Services — многомерные данные) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.view.f1
ms.assetid: efb5ee1c-de50-4bfc-83ff-08a4f03c3ece
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4415fedb492eb32c2929c50999cad1542b41ca78
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064616"
---
# <a name="browser-cube-designer-analysis-services---multidimensional-data"></a>Браузер (конструктор кубов) (службы Analysis Services — многомерные данные)
  Используйте вкладку **браузера** в конструкторе кубов для просмотра измерений, мер и ключевых показателей эффективности в кубе. В [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]браузер кубов служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] интегрирован в конструктор запросов многомерных выражений и предоставляет графические интерфейсы пользователя, которые помогают создавать запросы многомерных выражений, фильтровать кубы и создавать их срезы, а также выполнять детализацию углублением иерархии.  
  
 **Браузера** вкладка имеет два режима: **Режим конструктора** и **режиме запросов**. В каждом из режимов объекты на панели **Метаданные** можно использовать для просмотра куба, также можно перетаскивать элементы с панели **Метаданные** в область запроса для создания запроса многомерных выражений, извлекающего нужные данные.  
  
 **Просмотр и запросы в режиме графического конструирования**  
  
 На следующем рисунке показан интерфейс **браузера** в графическом **режиме конструктора**.  
  
 ![Конструктор запросов многомерных выражений служб Analysis Services, режим конструктора](media/rsqd-dsawas-mdx-designmode.gif "Конструктор запросов многомерных выражений служб Analysis Services, режим конструктора")  
  
 При работе в режиме графического конструктора, если **Автовыполнение** (![автоматическое выполнение запроса](media/rsqdicon-autoexecute.gif "автоматическое выполнение запроса")) выбрана кнопка на панели инструментов, **Браузера** выполняет запрос каждый раз при помещении объекта метаданных на панель «данные». Вы можете также вручную выполнить запрос, нажав **выполнить запрос** (![выполните запрос](media/rsqdicon-run.gif "выполните запрос")) на панели инструментов.  
  
 Чтобы переключить графический конструктор запросов в режим **запроса** и работать с текстом инструкций многомерных выражений, нажмите кнопку **Режим конструирования** на панели инструментов.  
  
 **Просмотр и запросы многомерных Выражений текстовый режим**  
  
 В режиме текстового конструирования работа с многомерными выражениями идет напрямую. Панель **Метаданные** остается доступной и позволяет добавлять объекты в область конструирования запроса, также в нее можно перетаскивать функции и операторы многомерных выражений со списка на панели **Функции** .  
  
 На следующем рисунке показан интерфейс **браузера** в режиме запросов.  
  
 ![Конструктор запросов многомерных выражений для служб Analysis Services, режим запроса](media/rsqd-dsawas-mdx-querymode.gif "Конструктор запросов многомерных выражений для служб Analysis Services, режим запроса")  
  
 Можно начать работу в режиме графического конструирования, добавить нужные объекты, добавить фильтры для создания срезов куба, а затем переключиться в текстовый режим и расширить созданный по умолчанию запрос многомерных выражений, добавить дополнительные свойства элементов и ячеек.  
  
 Панель **Метаданные** содержит вкладки **Метаданные** и **Функции**. С вкладки **Метаданные** можно перетаскивать измерения, иерархии, ключевые показатели эффективности и меры в область конструирования запросов. Со вкладки **Функции** в область конструирования запросов можно перетаскивать функции. После выполнения запроса в области конструирования запроса отображаются результаты запроса многомерных выражений. Также можно нажать кнопку **Анализ в Excel** на **панели инструментов** , чтобы экспортировать данные в Microsoft Office Excel и просмотреть результаты с точки зрения пользователя в сводной таблице. В следующих разделах подробно описывается панель инструментов и все области для каждого режима вкладки **Браузер** .  
  
 Обратите внимание, что при работе в текстовом режиме, **Автовыполнение** (![автоматическое выполнение запроса](media/rsqdicon-autoexecute.gif "автоматическое выполнение запроса")) выключатель на панели инструментов недоступен. Тем не менее, можно вручную запускать запросы с использованием **выполнить запрос** (![выполните запрос](media/rsqdicon-run.gif "выполните запрос")) на панели инструментов.  
  
## <a name="sections"></a>Разделы  
 **Панель инструментов**  
 Панель инструментов содержит средство, которое может использоваться и в режиме конструктора, и в режиме запроса. Дополнительные сведения о панели инструментов и способах использования этих возможностей см. в разделе [Панель инструментов (вкладка "Браузер", конструктор кубов) (службы Analysis Services — многомерные данные)](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md).  
  
 **Анализ в Excel**  
 Используйте функцию **Анализ в Excel** для отправки выбранных в настоящий момент в кубе данных в Excel, чтобы просмотреть данные в сводной таблице. Текущий выбор данных основан на элементах, добавленных с панели **Метаданные** , и на всех фильтрах, которые определены с помощью функций фильтрации и создания запросов. Дополнительные сведения см. в разделе [Анализ в Excel (вкладка "Браузер", конструктор кубов) (службы Analysis Services — многомерные данные)](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md).  
  
 **Метаданные**  
 Используйте панель **Метаданные** для просмотра содержащихся в кубе объектов, для детализации углублением иерархий, а также для просмотра и использования мер. После выбора для просмотра связанных с ними данных на панели **Отчет** .? Дополнительные сведения об этой панели см. в разделе [Метаданные (вкладка "Браузер", конструктор кубов) (службы Analysis Services — многомерные данные)](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md).  
  
 **Фильтр и запрос**  
 Эта область конструктора используется для создания запросов многомерных выражений, для перетаскивания объектов с панели **Метаданные** и для определения условий фильтра в исходном кубе или измерении. Дополнительные сведения см. в разделе [Запрос и фильтр (вкладка "Браузер", конструктор кубов) (службы Analysis Services — многомерные данные)](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md).  
  
## <a name="see-also"></a>См. также  
 [Объекты куба &#40;службы Analysis Services — многомерные данные&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [Кубы в многомерных моделях](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Конструктор кубов &#40;службы Analysis Services — многомерные данные&#41;](cube-designer-analysis-services-multidimensional-data.md)  
  
  
