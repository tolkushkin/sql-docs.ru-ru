---
title: Изменение измерения Product | Документация Майкрософт
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 668d68fcdb3231a476d2da8296baa1120a79f3c6
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403656"
---
# <a name="lesson-3-3---modifying-the-product-dimension"></a>Занятие 3 – 3-изменение измерения Product
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

При выполнении задач этого раздела будут использованы именованные вычисления, чтобы предоставить понятные имена для линий товаров, определена иерархия в измерении «Продукт» и указано имя элемента «(Все)» для иерархии. Также атрибуты будут сгруппированы в папки отображения.  
  
## <a name="adding-a-named-calculation"></a>Добавление именованного вычисления  
К таблице в представлении источника данных может быть добавлено именованное вычисление. В следующей задаче будет создано именованное вычисление, которое отображает полное наименование линейки продуктов.  
  
#### <a name="to-add-a-named-calculation"></a>Добавление именованного вычисления  
  
1.  Чтобы открыть представление источника данных **Adventure Works DW 2012** , дважды щелкните **Adventure Works DW 2012** в папке **Представления источников данных** в обозревателе решений.  
  
2.  В нижней части панели диаграмм щелкните правой кнопкой мыши заголовок таблицы **Продукт** и выберите команду **Создать именованное вычисление**.  
  
3.  В диалоговом окне **Создание именованного вычисления** в поле **Имя столбца** введите **ProductLineName** .  
  
4.  В поле **Выражение** введите или скопируйте и вставьте следующую инструкцию **CASE** :  
  
    ```  
    CASE ProductLine  
       WHEN 'M' THEN 'Mountain'  
       WHEN 'R' THEN 'Road'  
       WHEN 'S' THEN 'Accessory'  
       WHEN 'T' THEN 'Touring'  
       ELSE 'Components'  
    END  
    ```  
  
    Эта инструкция **CASE** для каждой строки товара в кубе создает понятные имена.  
  
5.  Нажмите кнопку **ОК** , чтобы создать именованное вычисление **ProductLineName** . Возможно, потребуется подождать.  
  
6.  В меню **Файл** выберите команду **Сохранить все**.  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>Изменение свойства NameColumn атрибута  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>Изменение значения свойства NameColumn атрибута  
  
1.  В конструкторе измерений откройте измерение Product. Для этого дважды щелкните измерение **Продукт** в узле **Измерения** обозревателя решений.  
  
2.  На панели **Атрибуты** вкладки **Структура измерения** выберите **Product Line**.  
  
3.  В окне свойств в правой части экрана щелкните **NameColumn** свойство поле в нижней части окна, а затем нажмите кнопку обзора (**...** ) кнопку, чтобы открыть **столбец имени** диалоговое окно. Возможно, потребуется перейти на вкладку **Свойства** в правой части окна, чтобы открыть окно "Свойства".  
  
4.  Выберите пункт **ProductLineName** внизу списка **Исходный столбец** и нажмите кнопку **OK**.  
  
    Теперь поле NameColumn содержит текст **Product.ProductLineName (WChar)**. После этого элементы иерархии атрибута **Product Line** будут содержать не сокращенное, а полное наименование линейки продуктов.  
  
5.  На панели **Атрибуты** вкладки **Структура измерения** выберите **Product Key**.  
  
6.  В окне «Свойства» щелкните **NameColumn** свойство поле, а затем нажмите кнопку обзора (**...** ) кнопку, чтобы открыть **столбец имени** диалоговое окно.  
  
7.  Выберите в списке **Исходный столбец** значение **EnglishProductName** и нажмите кнопку **ОК**.  
  
    Теперь поле NameColumn содержит текст **Product.EnglishProductName (WChar)**.  
  
8.  Прокрутите окно свойств вверх, щелкните поле свойства **Имя** и введите **Product Name**.  
  
## <a name="creating-a-hierarchy"></a>Создание иерархии  
  
#### <a name="to-create-a-hierarchy"></a>Создание иерархии  
  
1.  Перетащите атрибут **Product Line** с панели **Атрибуты** на панель **Иерархии** .  
  
2.  Перетащите атрибут **Model Name** с панели **Атрибуты** в ячейку **<new level>** на панели **Иерархии** под уровнем **Product Line** .  
  
3.  Перетащите атрибут **Product Name** с панели **Атрибуты** в ячейку **<new level>** на панели **Иерархии** под уровнем **Model Name** . («Ключ продукта» был переименован в «Имя продукта» в предыдущем разделе.)  
  
4.  На панели **Иерархии** вкладки **Структура измерения** щелкните правой кнопкой мыши строку заголовка окна **Иерархия** , выберите команду **Переименовать**и введите **Product Model Lines**.  
  
    Теперь иерархия называется **Product Model Lines**.  
  
5.  В меню **Файл** выберите команду **Сохранить все**.  
  
## <a name="specifying-folder-names-and-all-member-names"></a>Определение имен папок и имени элемента «Все»  
  
#### <a name="to-specify-the-folder-and-member-names"></a>Указание имен папок и элементов  
  
1.  На панели **Атрибуты** выберите следующие атрибуты (щелкните каждый из них, удерживая нажатой клавишу CTRL):  
  
    -   **Class**  
  
    -   **Color**  
  
    -   **Days To Manufacture**  
  
    -   **Reorder Point**  
  
    -   **Safety Stock Level**  
  
    -   **Размер**  
  
    -   **Size Range**  
  
    -   **Стиль**  
  
    -   **Weight**  
  
2.  В окне свойств в поле свойства **AttributeHierarchyDisplayFolder** введите **Stocking**.  
  
    Атрибуты сгруппированы в единую папку отображения.  
  
3.  На панели **Атрибуты** выберите следующие атрибуты:  
  
    -   **Dealer Price**  
  
    -   **List Price**  
  
    -   **Standard Cost**  
  
4.  В ячейке свойства **AttributeHierarchyDisplayFolder** окна свойств введите значение **Financial**.  
  
    Атрибуты сгруппированы во вторую папку отображения.  
  
5.  На панели **Атрибуты** выберите следующие атрибуты:  
  
    -   **End Date**  
  
    -   **Дата начала**  
  
    -   **Состояние**  
  
6.  В ячейке свойства **AttributeHierarchyDisplayFolder** окна свойств введите **History**.  
  
    Атрибуты сгруппированы в третью папку отображения.  
  
7.  На панели **Иерархии** выберите иерархию **Product Model Lines** и для свойства **AllMemberName** в окне свойств задайте значение **All Products**.  
  
8.  Щелкните открытую область панели **Иерархии** и измените свойство **AttributeAllMemberName** в верхней части окна свойств на **Все продукты**.  
  
    Щелкнув рабочую область, можно изменять свойства самого измерения Product. Также можно щелкнуть значок измерения **Продукт** в начале списка атрибутов на панели **Атрибуты** .  
  
9. В меню **Файл** выберите команду **Сохранить все**.  
  
## <a name="defining-attribute-relationships"></a>Определение связей атрибутов  
Необходимо определять связи между атрибутами, если базовые данные это поддерживают. Определение связей между атрибутами ускоряет обработку измерений, секций и запросов. Дополнительные сведения см. в разделах [Определение связей атрибутов](../multidimensional-models/attribute-relationships-define.md) и [Связи атрибутов](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Определение связей атрибутов  
  
1.  В окне **Конструктор измерений** для измерения Product откройте вкладку **Связи атрибутов**.  
  
2.  На диаграмме щелкните правой кнопкой мыши атрибут **Имя модели** и выберите команду **Создать связь атрибутов**.  
  
3.  В диалоговом окне **Создание связи атрибутов** поле **Исходный атрибут** имеет значение **Имя модели**. Задайте для поля **Связанный атрибут** значение **Линейка продуктов**.  
  
    В списке **Тип связи** оставьте выбранным тип **Гибкая** , так как связи между элементами могут измениться с течением времени. Например, модель товара со временем могла быть перенесена в другую линию товаров.  
  
4.  Нажмите кнопку **ОК**.  
  
5.  В меню **Файл** выберите команду **Сохранить все**.  
  
## <a name="reviewing-product-dimension-changes"></a>Просмотр изменений в измерении Product  
  
#### <a name="to-review-the-product-dimension-changes"></a>Просмотр изменений в измерении Product  
  
1.  В меню **Построение** среды [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]выберите команду **Развернуть Analysis Services Tutorial**.  
  
2.  Получив сообщение **Развертывание выполнено успешно** , перейдите на вкладку **Браузер** окна **Конструктор измерений** для измерения **Продукт** и нажмите на панели инструментов кнопку повторного соединения.  
  
3.  Убедитесь в том, что в списке **Иерархия** выбрана вкладка **Product Model Lines** и разверните узел **All Products**.  
  
    Обратите внимание, что элемент **Все** отображается как **All Products**. Причина этого заключается в том, что свойство **AllMemberName** иерархии ранее на этом занятии было заменено на **All Products** . Кроме того, все элементы уровня **Product Line** теперь имеют понятные имена, а не однобуквенные сокращения.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
[Изменение измерения Date](lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>См. также  
[Определение именованных вычислений в представлении источника данных (службы Analysis Services)](../multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
[Создание пользовательских иерархий](../multidimensional-models/user-defined-hierarchies-create.md)  
[Настройка уровня (Все) для иерархий атрибутов](../multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
