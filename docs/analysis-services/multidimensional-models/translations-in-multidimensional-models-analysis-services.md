---
title: Переводы в многомерных моделях (службы Analysis Services) | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f25023f6a0191cb645134d327f40ea84ba64932f
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65357315"
---
# <a name="translations-in-multidimensional-models-analysis-services"></a>Переводы в многомерных моделях (службы Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Можно определить переводы в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , воспользовавшись соответствующим конструктором для объекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , который нужно перевести. При определении перевода создается объект **Translation** , связанный с соответствующим объектом служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и обладающий указанными явными символьными значениями (на выбранном языке) для свойств связанного объекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="elements-of-a-multi-lingual-data-model"></a>Элементы многоязычной модели данных.  
 Модели данных, используемой в многоязычном решении, нужны не только переведенные метки (имена полей и описания). Также модели необходимо предоставить значения данных, которые выводятся в различных скриптах. Для создания многоязычного решения необходимы отдельные атрибуты, привязанные к столбцам во внешней базе данных, возвращающие данные.  
  
 Образцы баз данных Adventure Works (многомерное и реляционное хранилище данных) демонстрируют возможности перевода у служб Analysis Services. Образец модели содержит переведенные заголовки и описания. Образец реляционного хранилища данных содержит столбцы переведенных значений, предоставляющих локализованные элементы атрибутов в модели.  
  
 Для просмотра переведенных значений данных, доступных для модели выполните следующее.  
  
1.  Откройте многомерную модель Adventure Works в конструкторе.  
  
2.  В обозревателе решений откройте представления источников данных и дважды щелкните файл Adventure Works DW\<версия > .dsv.  
  
3.  Найдите dimDate, dimProduct, dimProductCategory или dimProductSubcateogry. Все эти измерения содержат атрибуты для преобразованных элементов месяца, дня недели, названия продукта, имени категории и т. д.  
  
4.  Щелкните правой кнопкой мыши любое поле и выберите **Просмотр данных**. Вы увидите английский, испанский и французский переводы для каждого элемента.  
  
 Форматы даты, времени и валюты не реализуются с помощью переводов. Для динамического предоставления определенных форматов на основе языкового стандарта клиента используйте мастер преобразования валюты и свойство **FormatString** . Дополнительные сведения см. в разделах [Конвертация валюты (службы Analysis Services)](../../analysis-services/currency-conversions-analysis-services.md) и [Элемент FormatString (ASSL)](https://docs.microsoft.com/bi-reference/assl/properties/formatstring-element-assl).  
  
## <a name="defining-translations"></a>Определение переводов  
  
### <a name="add-translations-to-a-cube"></a>Добавление переводов в куб  
 Можно добавлять переводы для куба, мер, групп мер, измерения куба, перспектив, КПИ, действий, именованных наборов и вычисляемых элементов.  
  
1.  В обозревателе решений дважды щелкните имя куба, чтобы открыть конструктор кубов.  
  
2.  Перейдите на вкладку **Переводы** . На этой странице перечислены все объекты, которые поддерживают переводы.  
  
3.  Для каждого объекта укажите целевой язык (автоматически преобразуется в код языка), переведенный заголовок и переведенное описание. Список языков в службах Analysis Services согласован как для языка сервера в Management Studio, так и при добавлении переопределения перевода для одного атрибута.  
  
     Помните, что невозможно изменить параметры сортировки. Куб фактически использует один набор параметров сортировки, даже если вы поддерживаете несколько языков с помощью перевода заголовков (для атрибутов измерений есть исключение, описанное ниже). Если окажется, что в языках при общих параметрах сортировки сортировка работает неправильно, потребуется сделать копии куба, чтобы разместить требования к параметрам сортировки.  
  
4.  Постройте и разверните проект.  
  
5.  Подключитесь к базе данных с помощью клиентского приложения, например Excel, добавив в строку подключения код языка. Дополнительные сведения см. в разделе [Советы и рекомендации по глобализации (службы Analysis Services)](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>Добавление переводов в измерение и атрибуты  
 Переводы можно добавить в измерения базы данных, атрибуты, иерархии и уровни в иерархии.  
  
 Переведенные заголовки добавляются к модели вручную с помощью клавиатуры или копирования и вставки, но для элементов атрибута измерения переведенные значения можно получить из внешней базы данных. В частности, свойство **CaptionColumn** атрибута может быть привязано к столбцу в представлении источника данных.  
  
 На уровне атрибута можно переопределить параметры сортировки, например может потребоваться учитывать ширину или использовать двоичную сортировку для конкретного атрибута. В [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]параметры сортировки предоставляется там, где определены привязки данных. Поскольку вы привязываете перевод атрибута измерения к другому исходному столбцу в другом исходном столбце в DSV, доступны параметры сортировки, с помощью которых можно настроить сортировку, используемую исходным столбцом. Подробные сведения о параметрах сортировки столбца в реляционной базе данных см. в разделе [Set or Change the Column Collation](../../relational-databases/collations/set-or-change-the-column-collation.md) .  
  
1.  В обозревателе решений дважды щелкните имя измерения, чтобы открыть конструктор измерений.  
  
2.  Перейдите на вкладку **Переводы** . На этой странице перечислены все объекты измерений, которые поддерживают переводы.  
  
     Для каждого объекта укажите целевой язык (автоматически преобразуется в код языка), переведенный заголовок и переведенное описание. Список языков в службах Analysis Services согласован как для языка сервера в Management Studio, так и при добавлении переопределения перевода для одного атрибута.  
  
3.  Привязка атрибута к столбцу, который предоставляет переведенные значения  
  
    1.  В конструкторе измерений в области **Переводы**добавьте новый перевод. Выберите язык. На странице появится новый столбец, чтобы принять переведенные значения.  
  
    2.  Поместите курсор в пустую ячейку рядом с одним из атрибутов. Атрибут не может быть ключом, но все остальные атрибуты допустимы. Вы увидите маленькую кнопку с точкой. Нажмите ее, чтобы открыть диалоговое окно **Перевод данных атрибута**.  
  
    3.  Введите перевод заголовка. Он используется как метка данных на целевом языке, например как имя поля в списке полей сводной таблицы.  
  
    4.  Выберите исходный столбец, который предоставляет переведенные значения элементов атрибута. Доступны только существующие столбцы в таблице или запросе, связанные с измерением. Если столбец не существует, необходимо изменить представление источника данных, измерение и куб, чтобы выбрать столбец.  
  
    5.  Выберите параметры и порядок сортировки, если применимо.  
  
4.  Постройте и разверните проект.  
  
5.  Подключитесь к базе данных с помощью клиентского приложения, например Excel, добавив в строку подключения код языка. Дополнительные сведения см. в разделе [Советы и рекомендации по глобализации (службы Analysis Services)](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md).  
  
### <a name="add-a-translation-of-the-database-name"></a>Добавление перевода имени базы данных  
 На уровне базы данных можно добавлять переводы имени и описания. Переведенное имя базы данных может быть видимо для клиентских подключений, которые указывают код языка, но это зависит от используемого средства. Например, при просмотре базы данных в среде Management Studio не покажется переведенное имя сортировки, даже если указать код языка для соединения. API, который используется Management Studio для подключения к службам Analysis Services, не читает свойство **Language** .  
  
1.  В обозревателе решений щелкните правой кнопкой мыши имя проекта и выберите **Изменить базу данных** , чтобы открыть конструктор баз данных.  
  
2.  В области "Перевод" укажите целевой язык (автоматически преобразуется в код языка), переведенный заголовок и переведенное описание. Список языков в службах Analysis Services согласован как для языка сервера в Management Studio, так и при добавлении переопределения перевода для одного атрибута.  
  
3.  На странице свойств базы данных задайте в свойстве **Language** код языка, указанный для перевода. При необходимости задайте значение свойства **Collation** , если значение по умолчанию больше не имеет смысла.  
  
4.  Постройте и разверните базу данных.  
  
## <a name="deleting-translation-objects"></a>Удаление объектов перевода  
 Можно щелкнуть правой кнопкой мыши объект перевода в измерении или в конструкторе кубов, чтобы окончательно удалить его. Нельзя восстановить или повторно использовать удаленный объект, поэтому следует проверить список удаляемых объектов перед продолжением.  
  
## <a name="resolving-translations"></a>Разрешение переводов  
 Если клиентское приложение запрашивает сведения по заданному идентификатору языка, экземпляр служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] пытается разрешить данные и метаданные для объектов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] в ближайший возможный идентификатор языка. Если клиентское приложение не задает язык по умолчанию или задает нейтральный код локали (0) или идентификатор языка процесса по умолчанию (1024), то службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] используют язык по умолчанию для экземпляра, чтобы вернуть данные и метаданные для объектов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Если клиентское приложение задает идентификатор языка, отличный от идентификатора языка по умолчанию, экземпляр последовательно рассматривает все возможные переводы для всех возможных объектов. Если указанный идентификатор языка соответствует идентификатору языка перевода, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] возвращают этот перевод. Если соответствие не найдено, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] пытаются использовать один из следующих методов, чтобы вернуть переводы с идентификатором языка, ближайшим к указанному.  
  
-   Для следующих идентификаторов языка службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] пытаются использовать альтернативный идентификатор, если перевод для указанного идентификатора языка не определен.  
  
    |Заданный идентификатор языка|Альтернативный идентификатор языка|  
    |-----------------------------------|-----------------------------------|  
    |3076 — китайский (Гонконг, КНР)|1028 — китайский (Тайвань)|  
    |5124 — китайский (Макао)|1028 — китайский (Тайвань)|  
    |1028 — китайский (Тайвань)|Язык по умолчанию|  
    |4100 — китайский (Сингапур)|2052 — китайский (КНР)|  
    |2074 — хорватский|Язык по умолчанию|  
    |3098 — хорватский (кириллица)|Язык по умолчанию|  
  
-   Для всех остальных заданных идентификаторов языков службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] получают первичный язык по указанному идентификатору и возвращают идентификатор того языка, который Windows предлагает в качестве наилучшего совпадения с первичным. Язык по умолчанию используется, если для перевода не удается найти наиболее подходящий язык, а также, если указанный идентификатор языка наилучшим образом соответствует первичному языку.  
  
## <a name="see-also"></a>См. также  
 [Сценарии глобализации для служб Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Языки и параметры сортировки (службы Analysis Services)](../../analysis-services/languages-and-collations-analysis-services.md)  
  
  
