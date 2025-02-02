---
title: Определение связей атрибутов в пользовательской иерархии | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 456c2a47-d395-45f9-9efa-89f3fa2ac621
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 490d9f6e1cdaeab274290649d2bb7f5c691595ae
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063033"
---
# <a name="specifying-attribute-relationships-between-attributes-in-a-user-defined-hierarchy"></a>Определение связей атрибутов в определенной пользователем иерархии
  Как уже было рассмотрено в этом учебнике, иерархии атрибутов внутри пользовательских иерархий можно упорядочивать по уровням, чтобы предоставлять пользователям пути перемещения в кубе. Пользовательская иерархия может отражать естественную иерархию, такую как города, область и страна, или просто путь перемещения,например фамилию сотрудника, его должность и название отдела. Для пользователя, перемещающегося по иерархии, нет разницы между этими двумя типами пользовательских иерархий.  
  
 В естественной иерархии, если определены связи между атрибутами, составляющими уровни, службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] могут использовать статистические вычисления по одному атрибуту для получения результатов из связанного атрибута. Если связи атрибутов не определены, в службах [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] будут выполняться статистические вычисления по всем неключевым атрибутам из ключевого атрибута. Таким образом, если базовые данные позволяют, необходимо определить связи между атрибутами. Это повышает производительность обработки измерений, секций и выполнения запросов. Дополнительные сведения см. в разделах [Определение связей атрибутов](multidimensional-models/attribute-relationships-define.md) и [Связи атрибутов](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 При определении связи атрибутов можно указать ее тип: гибкая или жесткая. Если связь определена как жесткая, агрегаты в службах [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] сохраняются при обновлении измерения. Если изменяется связь, определенная как жесткая, а измерение обработано не полностью, в службах [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] формируется ошибка при обработке. Указание подходящих связей и свойств связей повышает производительность запросов и производительность обработки. Дополнительные сведения см. в разделах [Определение связей атрибутов](multidimensional-models/attribute-relationships-define.md) и [Свойства пользовательской иерархии](multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md).  
  
 В задачах этого раздела будут определены связи атрибутов, входящих в естественные пользовательские иерархии в проекте [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. В их число входит иерархия **География заказчика** измерения **Заказчик**, иерархия **Территория продаж** измерения **Территория продаж** , иерархия **Линии моделей товаров** измерения **Продукт** и иерархии **Финансовая дата** и **Календарная дата** измерения **Дата** . Все эти пользовательские иерархии являются естественными иерархиями.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>Определение связей атрибутов в иерархии Customer Geography  
  
1.  Откройте измерение "Заказчик" в конструкторе измерений и перейдите на вкладку **Структура измерения** .  
  
     На панели **Иерархии** обратите внимание на уровни определяемой пользователем иерархии **География заказчика** . Эта иерархия в настоящий момент представляет для пользователя только путь детализации, так как между уровнями и атрибутами никакие связи не определены.  
  
2.  Перейдите на вкладку **Связи атрибутов** .  
  
     Обратите внимание на четыре связи атрибутов, которые связывают неключевые атрибуты из таблицы **Geography** с ключевым атрибутом из таблицы **Geography** . Обратите внимание, что атрибут **География** связан с атрибутом **Полное имя** . Атрибут **Почтовый индекс** косвенно связан с атрибутом **Полное имя** через атрибут **География** , так как **Почтовый индекс** связан с атрибутом **География** , а атрибут **География** связан с атрибутом **Полное имя** . Затем необходимо изменить связи атрибутов таким образом, чтобы исключить использование атрибута **География** .  
  
3.  На диаграмме щелкните правой кнопкой мыши атрибут **Полное имя** и выберите команду **Создать связь атрибутов**.  
  
4.  В диалоговом окне **Создание связи атрибутов** свойство **Исходный атрибут** имеет значение **Полное имя**. Задайте для свойства **Связанный атрибут** значение **Почтовый индекс**. В списке **Тип связи** оставьте выбранным тип **Гибкая**, так как связи между элементами могут измениться с течением времени.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     На диаграмме появляется значок предупреждения, поскольку эта связь избыточна. Связь **Полное имя** -> **География**-> **Почтовый индекс** уже существует, и вы только что создали связь **Полное имя** -> **Почтовый индекс**. Теперь связь **География**-> **Почтовый индекс** является избыточной, поэтому удалим ее.  
  
6.  На панели **Связи атрибутов** щелкните правой кнопкой мыши связь **География**-> **Почтовый индекс** , а затем выберите команду **Удалить**.  
  
7.  В открывшемся диалоговом окне **Удаление объектов** нажмите кнопку **ОК**.  
  
8.  На диаграмме щелкните правой кнопкой мыши атрибут **Почтовый индекс** и выберите команду **Создать связь атрибутов**.  
  
9. В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Почтовый индекс**. Задайте для поля **Связанный атрибут** значение **Город**. В списке **Тип связи** оставьте выбранным тип **Гибкая**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Теперь связь **География**-> **Город** является избыточной, поэтому удалим ее.  
  
11. На панели "Связи атрибутов" щелкните правой кнопкой мыши связь **География**-> **Город** , а затем выберите команду **Удалить**.  
  
12. В открывшемся диалоговом окне **Удаление объектов** нажмите кнопку **ОК**.  
  
13. На диаграмме щелкните правой кнопкой мыши атрибут **Город** и выберите команду **Создать связь атрибутов**.  
  
14. В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** содержит значение **Город**. Для поля **Связанный атрибут** задайте значение **Республика — область или край**. В списке **Тип связи** задайте тип связи **Жесткая** , так как связь между городом и штатом со временем не изменится.  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. Щелкните правой кнопкой мыши стрелку между элементами **География** и **Республика — область или край** и выберите команду **Удалить**.  
  
17. В открывшемся диалоговом окне **Удаление объектов** нажмите кнопку **ОК**.  
  
18. На диаграмме щелкните правой кнопкой мыши атрибут **Республика — область или край** и выберите команду **Создать связь атрибутов**.  
  
19. В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Республика — область или край**. Задайте для поля **Связанный атрибут** значение **Страна — регион**. В списке **Тип связи** выберите тип связи **Жесткая** , так как связь между республикой (областью, краем) и страной (регионом) со временем не изменится.  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. На панели "Связи атрибутов" щелкните правой кнопкой мыши связь **География**-> **Страна — регион** , а затем выберите команду **Удалить**.  
  
22. В открывшемся диалоговом окне **Удаление объектов** нажмите кнопку **ОК**.  
  
23. Перейдите на вкладку **Структура измерения** .  
  
     Обратите внимание, что при удалении последней связи между атрибутом **География** и другими атрибутами удаляется сам атрибут **География** . Это происходит, поскольку атрибут больше не используется.  
  
24. В меню «Файл» выберите команду **Сохранить все**.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>Определение связей атрибутов в иерархии Sales Territory  
  
1.  Откройте измерение **Территория продаж** в конструкторе измерений и перейдите на вкладку **Связи атрибутов** .  
  
2.  На диаграмме щелкните правой кнопкой мыши атрибут **Страна территории продаж** и выберите команду **Создать связь атрибутов**.  
  
3.  В диалоговом окне **Создание связи атрибутов** свойство **Исходный атрибут** имеет значение **Страна территории продаж**. Задайте для свойства **Связанный атрибут** значение **Группа территории продаж**. В списке **Тип связи** оставьте выбранным тип **Гибкая**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Атрибут **Группа территории продаж** теперь связан с атрибутом **Страна территории продаж**, а он, в свою очередь, с атрибутом **Регион территории продаж**. Свойству **Тип связи** для каждой из этих связей должно быть присвоено значение **Гибкая**, так как со временем распределение регионов по стране и стран по группам может измениться.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>Определение связей атрибутов в иерархии Product Model Lines  
  
1.  Откройте измерение **Продукт** в конструкторе измерений и перейдите на вкладку **Связи атрибутов** .  
  
2.  На диаграмме щелкните правой кнопкой мыши атрибут **Имя модели** и выберите команду **Создать связь атрибутов**.  
  
3.  В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Имя модели**. Задайте для поля **Связанный атрибут** значение **Линейка продуктов**. В списке **Тип связи** оставьте выбранным тип **Гибкая**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>Определение связей атрибутов в иерархии Fiscal Date  
  
1.  Откройте в конструкторе измерений измерение **Дата** и перейдите на вкладку **Связи атрибутов** .  
  
2.  На диаграмме щелкните правой кнопкой мыши атрибут **Название месяца** и выберите команду **Создать связь атрибутов**.  
  
3.  В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Название месяца**. Установите поле **Связанный атрибут** в значение **Fiscal Quarter**. В списке **Тип связи** выберите тип **Жесткая**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  На диаграмме щелкните правой кнопкой мыши атрибут **Финансовый квартал** и выберите команду **Создать связь атрибутов**.  
  
6.  В диалоговом окне **Создание связи атрибутов** свойство **Исходный атрибут** имеет значение **Финансовый квартал**. Задайте для свойства **Связанный атрибут** значение **Финансовый семестр**. В списке **Тип связи** выберите тип **Жесткая**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  На диаграмме щелкните правой кнопкой мыши атрибут **Финансовый семестр** и выберите команду **Создать связь атрибутов**.  
  
9. В диалоговом окне **Создание связи атрибутов** свойство **Исходный атрибут** имеет значение **Финансовый семестр**. Задайте для свойства **Связанный атрибут** значение **Финансовый год**. В списке **Тип связи** выберите тип **Жесткая**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>Определение связей атрибутов в иерархии Calendar Date  
  
1.  На диаграмме щелкните правой кнопкой мыши атрибут **Название месяца** и выберите команду **Создать связь атрибутов**.  
  
2.  В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Название месяца**. Задайте для поля **Связанный атрибут** значение **Календарный квартал**. В списке **Тип связи** выберите тип **Жесткая**.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  На диаграмме щелкните правой кнопкой мыши атрибут **Календарный квартал** , а затем выберите команду **Создать связь атрибутов**.  
  
5.  В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Calendar Quarter**. Задайте для поля **Связанный атрибут** значение **Календарное полугодие**. В списке **Тип связи** выберите тип **Жесткая**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  На диаграмме щелкните правой кнопкой мыши атрибут **Календарное полугодие** и выберите команду **Создать связь атрибутов**.  
  
8.  В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Календарное полугодие**. Задайте для поля **Связанный атрибут** значение **Календарный год**. В списке **Тип связи** выберите тип **Жесткая**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>Определение связей атрибутов в иерархии Geography  
  
1.  Откройте измерение "География" в конструкторе измерений и перейдите на вкладку **Связи атрибутов** .  
  
2.  На диаграмме щелкните правой кнопкой мыши атрибут **Почтовый индекс** и выберите команду **Создать связь атрибутов**.  
  
3.  В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Почтовый индекс**. Задайте для поля **Связанный атрибут** значение **Город**. В списке **Тип связи** выберите тип **Гибкая**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  На диаграмме щелкните правой кнопкой мыши атрибут **Город** и выберите команду **Создать связь атрибутов**.  
  
6.  В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** содержит значение **Город**. Для поля **Связанный атрибут** задайте значение **Республика — область или край**. В списке **Тип связи** выберите тип **Жесткая**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  На диаграмме щелкните правой кнопкой мыши атрибут **Республика — область или край** и выберите команду **Создать связь атрибутов**.  
  
9. В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Республика — область или край**. Задайте для поля **Связанный атрибут** значение **Страна — регион**. В списке **Тип связи** выберите тип **Жесткая**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. На диаграмме щелкните правой кнопкой мыши атрибут **Ключ географии** и выберите пункт **Свойства**.  
  
12. Установите свойство **AttributeHierarchyOptimizedState** в значение **NotOptimized**, а свойства **AttributeHierarchyOrdered** и **AttributeHierarchyVisible** — в значение **False**.  
  
13. В меню **Файл** выберите команду **Сохранить все**.  
  
14. В меню **Построение** среды [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]выберите команду **Развернуть Analysis Services Tutorial**.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
 [Определение свойств Unknown Member и Null Processing](../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>См. также  
 [Определение связей атрибутов](multidimensional-models/attribute-relationships-define.md)   
 [Свойства пользовательской иерархии](multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
