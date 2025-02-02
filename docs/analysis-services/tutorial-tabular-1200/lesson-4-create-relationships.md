---
title: 'Занятие 4: Создание связей | Документы Майкрософт'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8cad8c81021587a9dc3742983d7c7c2cd80fc174
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404856"
---
# <a name="lesson-4-create-relationships"></a>Занятие 4: Создание связей
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

На этом занятии будут проверены связи, автоматически созданные во время импорта данных, и добавлены новые связи между различными таблицами. Связь — это соединение между двумя таблицами, которое определяет, каким образом должны соотноситься данные этих таблиц. Например, таблица DimProduct и таблица DimProductSubcategory содержат связь на основе того факта, что каждый продукт принадлежит подкатегории. Дополнительные сведения см. в разделе [связи](../tabular-models/relationships-ssas-tabular.md).
  
Предполагаемое время для выполнения этого занятия: **10 минут**  
  
## <a name="prerequisites"></a>предварительные требования  
Этот раздел является частью учебника по табличному моделированию, который необходимо изучать по порядку. Перед выполнением задач на этом занятии, необходимо завершить предыдущее занятие: [Занятие 3. Пометить как таблицу дат](lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Обзор существующих связей и добавление новых  
При импорте данных с помощью мастера импорта таблиц, вы получили семь таблиц из базы данных AdventureWorksDW. Как правило при импорте данных из реляционного источника существующие связи автоматически импортируются вместе с данными. Однако необходимо проверить правильность создания связей между таблицами, прежде чем продолжить создание модели. В этом учебнике будут также созданы три новые связи.  
  
#### <a name="to-review-existing-relationships"></a>Просмотр существующих связей  
  
1.  Нажмите кнопку **модели** меню > **представление модели** > **представление схемы**.  

    Конструктор моделей появится в представлении диаграммы — графическом формате отображения всех импортированных таблиц, соединенных линиями. Линии между таблицами указывают на связи, которые были автоматически созданы во время импорта данных.
    
    ![как табличных lesson4-схема](media/as-tabular-lesson4-diagram.png)
  
    Используйте элементы управления мини-карты в правом нижнем углу конструктора моделей, чтобы настроить представление, включив в него как можно большее число таблиц. Можно также щелкните и перетащите таблицы в другое место, сблизив их или расположив в определенном порядке. Перемещение таблиц не влияет на связи между ними. Для просмотра всех столбцов в определенной таблице, щелкните и перетащите ее край, чтобы развернуть или уменьшить ее.  
  
2.  Щелкните сплошную линию между **DimCustomer** таблицы и **DimGeography** таблицы. Сплошная линия между этими двумя таблицами показывает, что связь активна, то есть она используется по умолчанию при расчете DAX-формул.  
  
    Обратите внимание, что **GeographyKey** столбца в **DimCustomer** таблицы и **GeographyKey** столбца в **DimGeography** таблицы теперь оба Каждый появились в блоке. Эта передача это столбцы, используемые в связи. Свойства связи также отображаются в **свойства** окна.  
  
    > [!TIP]  
    > Помимо использования конструктора моделей в представлении диаграммы, можно также использовать диалоговое окно «Управление связями» для отображения связей между всеми таблицами в табличном формате. Щелкните правой кнопкой мыши **связи** в обозревателе табличных моделей, а затем выберите **управление связями**. Диалоговое окно «Управление связями» отображения связей, которые были автоматически созданы во время импорта данных.  
  
3.  Используйте конструктор моделей в представлении схемы или диалоговое окно «Управление связями», чтобы убедиться, что следующие связи были созданы во всех таблицах были импортированы из базы данных AdventureWorksDW.  
  
    |Активен|Таблица|Связанная таблица подстановки|  
    |----------|---------|------------------------|  
    |Да|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Да|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Да|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Да|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Да|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Если какие-либо связи в приведенной выше таблице отсутствуют, убедитесь, что модель включает в себя следующие таблицы: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory и FactInternetSales. Если таблицы импортируются из одного подключения к источнику данных несколько раз, связи между этими таблицами не будут созданы и их нужно будет создавать вручную.  

### <a name="take-a-closer-look"></a>Рассмотрим это более подробно
В представлении схемы вы заметите стрелка, звездочка и число на линиях, обозначающих связи между таблицами.

![как табличные lesson4-строки](media/as-tabular-lesson4-line.png)

Стрелка указывает направление фильтрации, звездочка показывает, это таблица относится к множественной стороне в кратности связи, а число 1 показывает, что эта таблица относится к одиночной стороне связи. Если вам нужно изменить связь; Например измените направление фильтрации или кратность, дважды щелкните линию связи в представлении диаграммы, чтобы открыть диалоговое окно Изменение связи.

![как табличные lesson4-редактирования](media/as-tabular-lesson4-edit.png)

Скорее всего никогда не потребуется изменять связь. Эти функции предназначены для расширенного моделирования данных и выходят за рамки данного руководства. Дополнительные сведения см. в разделе [двунаправленного кросс-фильтры для табличных моделей в SQL Server 2016 Analysis Services](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

В некоторых случаях может потребоваться создание дополнительных связей между таблицами в модели, чтобы поддержать определенную бизнес-логику. В этом учебнике вам нужно создать три дополнительные связи между таблицей FactInternetSales и DimDate.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Добавление новых связей между таблицами  
  
1.  В конструкторе моделей в **FactInternetSales** таблицы, нажмите и удерживайте **OrderDate** столбец, затем перетащите курсор **даты** столбец в  **DimDate** таблицы, а затем отпустите.  

    Появится сплошная линия, указывающая на создание активной связи между **OrderDate** столбца в **Интернет-продажи** таблицы и **даты** столбца в **Даты** таблицы. 
  
      ![AS табличных lesson4-new](media/as-tabular-lesson4-new.png) 
  
    > [!NOTE]  
    > При создании связей кратность и направление фильтрации между основной таблицей и связанной таблицей поиска выбирается автоматически.  
  
2.  В **FactInternetSales** таблицы, нажмите и удерживайте **DueDate** столбец, затем перетащите курсор **даты** столбца в **DimDate** таблицы, а затем отпустите.  
  
    Появится пунктирная линия была создана неактивная связь между **DueDate** столбца в **FactInternetSales** таблицы и **даты** столбец в  **DimDate** таблицы. Между таблицами можно создавать несколько связей, но одновременно может быть активна только одна связь.  
  
3.  Наконец создайте еще одну связь; в **FactInternetSales** таблицы, нажмите и удерживайте **ShipDate** столбец, затем перетащите курсор **даты** столбца в **DimDate**таблицы, а затем отпустите.  
    
     ![как табличных lesson4-newinactive](media/as-tabular-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Дальнейшие действия
Перейдите к следующему занятию: [Занятие 5. Создание вычисляемых столбцов](lesson-5-create-calculated-columns.md).
  
  
  
