---
title: Выполнение добавочной загрузки нескольких таблиц | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],multiple tables
ms.assetid: 39252dd5-09c3-46f9-a17b-15208cfd336d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fee01a2531ce405f212c2559d91ec0ea241b9784
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728619"
---
# <a name="perform-an-incremental-load-of-multiple-tables"></a>Выполнение добавочной загрузки нескольких таблиц

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  На диаграмме в разделе [Улучшение добавочных загрузок с помощью системы отслеживания измененных данных](../../integration-services/change-data-capture/change-data-capture-ssis.md)показан базовый пакет, выполняющий добавочную загрузку только для одной таблицы. Однако чаще требуется добавочная загрузка не одной, а нескольких таблиц  
  
 Если выполняется добавочная загрузка нескольких таблиц, некоторые шаги достаточно выполнить один раз для всех таблиц, а другие приходится повторять для каждой исходной таблицы. Существуют следующие режимы выполнения этих шагов в службах [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Использование родительского пакета и дочерних пакетов.  
  
-   Использование нескольких задач потока данных в одном пакете.  
  
## <a name="loading-multiple-tables-by-using-a-parent-package-and-multiple-child-packages"></a>Загрузка нескольких таблиц с помощью родительского пакета и нескольких дочерних пакетов  
 Для шагов, которые достаточно выполнить один раз, можно использовать родительский пакет. Дочерние пакеты выполнят шаги, которые необходимо повторить для каждой исходной таблицы.  
  
#### <a name="to-create-a-parent-package-that-performs-those-steps-that-only-have-to-be-done-once"></a>Создание родительского пакета для шагов, которые достаточно выполнить один раз.  
  
1.  Создайте родительский пакет.  
  
2.  В потоке управления используйте задачу «Выполнение SQL» или выражения служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , чтобы вычислить конечные точки.  
  
     Пример вычисления конечных точек см. в разделе [Задание интервала для информации об изменениях данных](../../integration-services/change-data-capture/specify-an-interval-of-change-data.md).  
  
3.  Если требуется, используйте контейнер «цикл по элементам», чтобы задержать выполнение, пока не будут готовы измененные данные для выбранного периода.  
  
     Пример подобного контейнера "цикл по элементам" см. в разделе [Определение готовности информации об изменениях данных](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md).  
  
4.  Используйте несколько задач «Выполнение пакета», чтобы выполнить дочерние пакеты для каждой загружаемой таблицы. Передайте конечные точки, вычисленные в родительском пакете, в каждый дочерний пакет с помощью конфигураций переменной родительского пакета.  
  
     Дополнительные сведения см. в разделах [Задача "Выполнение пакета"](../../integration-services/control-flow/execute-package-task.md) и [Использование значений переменных и параметров в дочернем пакете](../../integration-services/packages/legacy-package-deployment-ssis.md#child).  
  
#### <a name="to-create-child-packages-to-perform-those-steps-that-have-to-be-done-for-each-source-table"></a>Создание дочерних пакетов для шагов, которые нужно выполнить для каждой исходной таблицы  
  
1.  Создайте дочерний пакет для каждой исходной таблицы.  
  
2.  В потоке управления используйте задачу «Скрипт» или «Выполнение SQL», чтобы составить инструкцию SQL, которая будет использоваться для запроса изменений.  
  
     Пример по сборке запроса см. в разделе [Подготовка к запросу информации об изменениях](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md).  
  
3.  Используйте одну задачу потока данных в каждом дочернем пакете, чтобы загрузить измененные данные и применить их к назначению. Настройте поток данных, как описано ниже.  
  
    1.  В потоке данных используйте исходный компонент, чтобы запросить изменения из таблиц изменений, входящие в диапазон выбранных конечных точек.  
  
         Пример запроса таблиц изменений см. в разделе [Получение и интерпретация измененных данных](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md).  
  
    2.  Преобразование «Условное разбиение» предназначено для направления операций вставки, обновления и удаления на различные выходы для необходимой обработки.  
  
         Пример, демонстрирующий настройку этого преобразования на непосредственный вывод, см. в разделе [Обработка операций вставки, обновления и удаления](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md).  
  
    3.  Используйте компонент назначения, чтобы применить операции вставки в целевой базе данных. Преобразования «Команда OLE DB» с параметризованными инструкциями UPDATE и DELETE предназначены для применения операций обновления и удаления в целевой базе данных.  
  
         Пример, демонстрирующий использование этого преобразования для применения операций обновления и удаления, см. в разделе [Применение изменений в назначении](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md).  
  
## <a name="loading-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>Загрузка нескольких таблиц с помощью нескольких задач потока данных в одном пакете  
 Можно также использовать один пакет, содержащий отдельную задачу потока данных для каждой загружаемой исходной таблицы.  
  
#### <a name="to-load-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>Загрузка нескольких таблиц с помощью нескольких задач потока данных в одном пакете  
  
1.  Создайте один пакет.  
  
2.  В потоке управления используйте задачу «Выполнение SQL» или выражения служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , чтобы вычислить конечные точки.  
  
     Пример вычисления конечных точек см. в разделе [Задание интервала для информации об изменениях данных](../../integration-services/change-data-capture/specify-an-interval-of-change-data.md).  
  
3.  Если требуется, используйте контейнер «цикл по элементам», чтобы задержать выполнение, пока не будут готовы измененные данные для выбранного интервала.  
  
     Пример подобного контейнера "цикл по элементам" см. в разделе [Определение готовности информации об изменениях данных](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md).  
  
4.  Используйте задачу «Скрипт» или задачу «Выполнение SQL», чтобы собрать инструкцию SQL, которая будет использоваться для запроса изменений.  
  
     Пример по сборке запроса см. в разделе [Подготовка к запросу информации об изменениях](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md).  
  
5.  Используйте несколько задач потока данных, чтобы загрузить измененные данные из каждой исходной таблицы и применить их к назначению. Настройте каждую задачу потока данных, как описано ниже.  
  
    1.  В каждом потоке данных используйте исходный компонент для запроса изменений, находящихся в диапазоне выбранных конечных точек, из таблиц изменений.  
  
         Пример запроса таблиц изменений см. в разделе [Получение и интерпретация измененных данных](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md).  
  
    2.  Преобразование «Условное разбиение» предназначено для направления операций вставки, обновления и удаления на различные выходы для необходимой обработки.  
  
         Пример, демонстрирующий настройку этого преобразования на непосредственный вывод, см. в разделе [Обработка операций вставки, обновления и удаления](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md).  
  
    3.  Используйте компонент назначения, чтобы применить операции вставки в целевой базе данных. Преобразования «Команда OLE DB» с параметризованными инструкциями UPDATE и DELETE предназначены для применения операций обновления и удаления в целевой базе данных.  
  
         Пример, демонстрирующий использование этого преобразования для применения операций обновления и удаления, см. в разделе [Применение изменений в назначении](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md).  
  
  
