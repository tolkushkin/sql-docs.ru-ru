---
title: Создание мер и групп мер в многомерных моделях | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 357b7d9e6ec63de52c5a7128b60330ce53943251
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65357372"
---
# <a name="create-measures-and-measure-groups-in-multidimensional-models"></a>Создание мер и групп мер в многомерных моделях
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  *Мера* — это агрегат значений числовых данных, например сумма, количество, минимальное, максимальное, среднее или созданное вами многомерное выражение. *Группа мер* — это контейнер для одной или нескольких мер. Все меры находятся в группе мер даже в том случае, если имеется только одна мера. Куб должен иметь как минимум одну меру и группу мер.  
  
 Этот раздел включает следующие подразделы:  
  
-   [Подходы к созданию мер](#bkmk_create)  
  
-   [Компоненты меры](#bkmk_comps)  
  
-   [Моделирование мер и групп мер по фактам и таблицам фактов](#bkmk_modeling)  
  
-   [Гранулярность группы мер](#bkmk_grain)  
  
##  <a name="bkmk_create"></a> Подходы к созданию мер  
 Меры могут быть статическим элементом куба, созданного во время разработки, и всегда присутствуют при доступе к кубу. Кроме того, меру можно определить как *вычисляемый элемент* с помощью многомерных выражений, когда ее значение вычисляется на основе других мер в кубе. Вычисляемый элемент можно распространить на сеанс или пользователя.  
  
 Чтобы создать меру или группу мер, используйте один из следующих подходов:  
  
|||  
|-|-|  
|Мастер кубов|Запустите мастер кубов в [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] для создания куба.<br /><br /> В обозревателе решений щелкните правой кнопкой мыши узел **Кубы** и выберите команду **Создать куб**. Справку по этим действиям см. в разделе [Многомерное моделирование (учебник по Adventure Works)](../../analysis-services/multidimensional-tutorial/multidimensional-modeling-adventure-works-tutorial.md).<br /><br /> При создании куба на основе таблиц из существующего хранилища данных определения мер и групп мер материализуются в качестве части процесса создания куба. В мастере выберите, какие факты и таблицы фактов нужно использовать в качестве основы для объектов меры и группы мер в кубе.|  
|Диалоговое окно создания меры|Если куб уже существует в [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], дважды щелкните имя куба в обозревателе решений, чтобы открыть его в конструкторе кубов. В области "Меры" щелкните правой кнопкой мыши верхний узел, чтобы создать новую группу мер или новую меру с помощью указания исходной таблицы, столбца и типа агрегирования. Этот подход требует выбора метода агрегирования из фиксированного списка готовых функций. В разделе [Use Aggregate Functions](../../analysis-services/multidimensional-models/use-aggregate-functions.md) представлено описание наиболее часто используемых агрегатов.|  
|вычисляемый элемент|Вычисляемые элементы позволяют добиться гибкости и широких возможностей анализа кубов в [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , так как можно управлять временем и способом их создания. Иногда мера требуется только временно — в течение сеанса пользователя или в среде Management Studio в рамках исследования.<br /><br /> В [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте вкладку "Вычисления", чтобы создать новый вычисляемый элемент.<br /><br /> Выберите этот подход при создании меры на основе многомерного выражения. Дополнительные сведения см. [Построение мер в многомерных Выражениях](../../analysis-services/multidimensional-models/mdx/mdx-building-measures.md), [вычисления](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md), [вычисления в многомерных моделях](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md) и [основные принципы создания скриптов многомерных Выражений &#40;служб Analysis Services&#41; ](../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).|  
|Многомерные выражения или XMLA|В SQL Server Management Studio можно выполнять многомерные выражения или XMLA, чтобы изменить базу данных для включения новой вычисляемой меры. Этот подход полезен для нерегламентированной проверки данных после развертывания решения на сервере. См. раздел [Document and Script an Analysis Services Database](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md).|  
  
##  <a name="bkmk_comps"></a> Компоненты меры  
 Мера представляет собой объект со свойствами. Кроме имени мера должна иметь тип агрегата и исходный столбец или выражение, используемое для наполнения меры данными. Можно изменить определение меры, задавая ее свойства.  
  
|||  
|-|-|  
|**источник**|Большинство мер являются производными от числовых столбцов таблиц фактов во внешнем хранилище данных, например столбца Sales Amount в таблицах Sales и Reseller Sales из хранилища данных AdventureWorks, однако можно создать новые меры, основываясь целиком на определяемых вычислениях.<br /><br /> Столбцы атрибутов из таблиц измерения можно использовать для определения мер, но такие меры обычно являются полуаддитивными или неаддитивными в отношении статистической обработки. Дополнительные сведения о режиме полуаддитивном см. в разделе [Определение полуаддитивного режима](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md).|  
|**агрегат**|По умолчанию меры суммируются вдоль каждого измерения. Однако свойство **AggregateFunction** позволяет изменить это. См. список в разделе [Use Aggregate Functions](../../analysis-services/multidimensional-models/use-aggregate-functions.md) .|  
|**Свойства**|См. описания дополнительных свойств в разделе [Configure Measure Properties](../../analysis-services/multidimensional-models/configure-measure-properties.md) .|  
  
##  <a name="bkmk_modeling"></a> Моделирование мер и групп мер по фактам и таблицам фактов  
 Перед запуском мастера важно знать принципы моделирования определения меры.  
  
 Меры и группы мер — многомерные объекты, представляющие факты и таблицы фактов во внешнем хранилище данных. В большинстве случаев меры и группы мер будет основываться на объектах в представлении источника данных, которые в свою очередь создаются из базового хранилища данных.  
  
 На следующей диаграмме показана таблица фактов **FactSalesQuota** и две связанные с ней таблицы измерений — **DimTime** и **DimEmployee**. В образце куба Adventure Works эти таблицы используются в качестве основы для группы мер Sales Quotas и измерений Time и Employee.  
  
 ![Таблица FactSalesQuota с двумя таблицами измерений](../../analysis-services/multidimensional-models/media/factsalesquota.gif "таблица FactSalesQuota с двумя таблицами измерений")  
  
 Таблица фактов содержит столбцы двух основных типов: столбцы атрибутов и столбцы мер.  
  
-   Столбцы атрибутов используются для создания связей между внешними ключами и таблицами измерений, чтобы количественные данные в столбцах мер можно было организовать по данным, содержащимся в таблицах измерений. Столбцы атрибутов используются также для определения гранулярности таблицы фактов и ее группы мер.  
  
-   Столбцы мер определяют меры, которые содержатся в группе мер.  
  
 При запуске мастера кубов внешние ключи отфильтровываются. В списке оставшихся столбцов для выбора находятся столбцы мер, а также столбцы атрибутов, которые не определены как внешний ключ. В **FactSalesQuota** примере мастер предложит **CalendarYear** и **CalendarQuarter** в дополнение к **SalesAmountQuota**. Только столбец меры **SalesAmountQuota** приведет к созданию поддающейся обработке меры для многомерной модели. Для определения суммы каждой квоты существуют другие столбцы на основе даты. Следует исключить из списка мер в мастере кубов другие столбцы — **CalendarYear** и **CalendarQuarter**(или позднее удалить их из группы мер в конструкторе).  
  
 Вывод из данного обсуждения: не все столбцы, предлагаемые мастером, полезны в качестве меры. Полагайтесь на собственное понимание данных и того, как они будут использоваться, при выборе столбцов для использования в качестве меры. Помните, что можно щелкнуть правой кнопкой мыши таблицу в представлении источника данных для нахождения данных, которые помогут определить, какие столбцы использовать в качестве мер. Дополнительные сведения см. в разделе [Просмотр данных в представлении источника данных (службы Analysis Services)](../../analysis-services/multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md).  
  
> [!NOTE]  
>  Не все меры извлекаются непосредственно из значения, хранимого в столбце таблицы фактов. Например, мера **Sales Person Count** , определенная в группе мер **Sales Quota** примера куба Adventure Works, фактически основана на подсчете уникальных значений (или числа различных элементов) в столбце **EmployeeKey** таблицы фактов **FactSalesQuota** .  
  
##  <a name="bkmk_grain"></a> Гранулярность группы мер  
 Группы мер имеют гранулярность, которая описывает уровень детализации, поддерживаемой таблицей фактов. Гранулярность устанавливается через отношение внешнего ключа к измерению.  
  
 Например, таблица фактов **FactSalesQuota** имеет связь по внешнему ключу с таблицей **DimEmployee** , каждая запись в таблице **FactSalesQuota** относится к одному сотруднику, таким образом, гранулярность группы мер с точки зрения измерения Employee находится на уровне индивидуального сотрудника.  
  
 Гранулярность группы мер не может быть задана мельче самого нижнего уровня измерения, из которого просматривается эта группа мер, а крупнее ее можно сделать при помощи дополнительных атрибутов. Например, в таблице фактов **FactSalesQuota** столбцы **TimeKey**, **CalendarYear**и **CalendarQuarter**используются для установки гранулярности связи с таблицей **DimTime** . В результате этого гранулярность группы мер, как видно из измерения «Время», соответствует календарному кварталу, а не дню, который является нижним уровнем измерения «Время».  
  
 Можно задать гранулярность группы мер по определенному измерению с помощью вкладки **Использование измерений** конструктора кубов. Дополнительные сведения о связях между измерениями см. в разделе [Dimension Relationships](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
## <a name="see-also"></a>См. также  
 [Кубы в многомерных моделях](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [Меры и их группы](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)  
  
  
