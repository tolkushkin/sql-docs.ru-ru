---
title: Параметры запроса профиля потенциальных ключей (задача "Профилирование данных") | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 8632dbc4-4394-4dc7-b19c-f9adeb21ba52
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e8ed8f3cdd8232cdf8fd66be1dce021f84d2e492
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727944"
---
# <a name="candidate-key-profile-request-options-data-profiling-task"></a>Параметры запроса профиля потенциальных ключей (задача «Профилирование данных»)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Для установки параметров варианта **Запрос профиля потенциальных ключей** , выделенного на панели запросов, используется панель **Свойства запроса** страницы **Запросы профиля** . Профиль потенциальных ключей сообщает о том, является ли данный столбец или набор столбцов ключом либо приблизительным ключом для выделенной таблицы. Этот профиль также поможет выявить проблемы в данных, например повторяющиеся значения в потенциальном ключевом столбце.  
  
> [!NOTE]  
>  В этом разделе описываются параметры, расположенные на странице **Запросы профиля** в **редакторе задачи «Профилирование данных»**. Дополнительные сведения об этой странице редактора см. в разделе [Редактор задачи "Профилирование данных" (страница "Запросы профиля")](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Дополнительные сведения об использовании задачи "Профилирование данных" см. в разделе [Установка задачи "Профилирование данных"](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Дополнительные сведения об использовании средства просмотра профиля данных для анализа результатов задачи "Профилирование данных" см. в разделе [Средство просмотра профиля данных](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-keycolumns-property"></a>Основные сведения о выборе столбцов для свойства KeyColumns  
 Каждый **Запрос профиля потенциальных ключей** вычисляет стойкость одного потенциального ключа, состоящего из одного столбца или из нескольких столбцов.  
  
-   При выборе только одного столбца в **KeyColumns**задача вычисляет стойкость ключа одного этого столбца.  
  
-   При выборе нескольких столбцов в **KeyColumns**задача вычисляет стойкость составного ключа, который состоит из всех выделенных столбцов.  
  
-   При выборе символа-шаблона **(\*)** в **KeyColumns** задача вычисляет стойкость ключа каждого столбца в таблице или представлении.  
  
 Рассмотрим, к примеру, образец таблицы, содержащей столбцы A, B и С. Пользователь выбирает следующие элементы в свойстве **KeyColumns**.  
  
-   Пользователь выбирает шаблон (\*) и столбец C в **KeyColumns**. Задача вычисляет стойкость ключа столбца C, а затем составных потенциальных ключей (A, C) и (B, C).  
  
-   Пользователь выбирает (\*) и (\*) в **KeyColumns**. Задача вычисляет силу ключей отдельных столбцов A, B и C, а затем составных потенциальных ключей (A, B), (A, C) и (B, C).  
  
> [!NOTE]  
>  Если выбрать символ (*), может потребоваться выполнение большого числа вычислений, что снизит производительность задачи. Однако если задача выявит подмножество, удовлетворяющее пороговому значению ключа, то эта задача не будет анализировать дополнительные сочетания. Например, если в описанном выше образце таблицы задача определяет, что столбец C является ключом, она не производит анализ составных потенциальных ключей.  
  
## <a name="request-properties-options"></a>Параметры области «Свойства запроса»  
 Для варианта **Запрос профиля потенциальных ключей**в панели **Свойства запроса** отображаются следующие группы параметров:  
  
-   **Данные**, куда входят параметры **TableOrView** и **KeyColumns**  
  
-   **Общие сведения**  
  
-   **Параметры**  
  
### <a name="data-options"></a>Параметры данных  
 **ConnectionManager**  
 Выберите существующий диспетчер подключений [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , использующий поставщик данных .NET для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) для подключения к базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которая содержит таблицу или представление для профилирования.  
  
 **TableOrView**  
 Выберите существующую таблицу или представление для профилирования.  
  
 Дополнительные сведения см. в подразделе «Параметры TableorView» данного раздела.  
  
 **KeyColumns**  
 Выберите существующий столбец или столбцы для профилирования. Выберите **(\*)**, чтобы выполнить профилирование всех столбцов.  
  
 Дополнительные сведения см. в подразделах «Основные сведения о выборе столбцов для свойства KeyColumns» и «Параметры KeyColumns» в этом разделе.  
  
#### <a name="tableorview-options"></a>Параметры TableOrView  
 **Схема**  
 Указывает схему, которой принадлежит выбранная таблица. Этот параметр доступен только для чтения.  
  
 **Таблица**  
 Отображает имя выбранной таблицы. Этот параметр доступен только для чтения.  
  
#### <a name="keycolumns-options"></a>Параметры KeyColumns  
 Следующие параметры представлены для каждого столбца, выбранного для профилирования в **KeyColumns**, или для параметра **(\*)**.  
  
 Дополнительные сведения см. в подразделе «Основные сведения о выборе столбцов для свойства KeyColumns» выше в этом разделе.  
  
 **IsWildcard**  
 Указывает, выбран ли подстановочный знак **(\*)**. Этот параметр принимает значение **True**, если выбран подстановочный знак **(\*)**, означающий профилирование всех столбцов. Значение **False** показывает, что для профилирования выбран отдельный столбец. Этот параметр доступен только для чтения.  
  
 **ColumnName**  
 Отображает имя выбранного столбца. Этот параметр пуст, если выбран подстановочный знак **(\*)**, означающий профилирование всех столбцов. Этот параметр доступен только для чтения.  
  
 **StringCompareOptions**  
 Выберите параметры для сравнения строковых значений. Это свойство имеет параметры, указанные в следующей таблице. По умолчанию значение этого параметра равно **Default**.  
  
> [!NOTE]  
>  Если для свойства **ColumnName** используется шаблон **(\*)**, свойство **CompareOptions** доступно только для чтения и получает значение **Default**.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Default**|Сортирует и сравнивает данные на основе параметров сортировки столбца в исходной таблице.|  
|**BinarySort**|Сортирует и сравнивает данные на основе битовых шаблонов, определенных для каждого символа. Двоичный порядок сортировки учитывает регистр и диакритические знаки. Двоичный порядок сортировки является самым быстрым.|  
|**DictionarySort**|Сортирует и сравнивает данные в соответствии с правилами сортировки и сравнения, определенными в словарях для соответствующего языка или алфавита.|  
  
 Если выбран вариант **DictionarySort**, можно дополнительно указать любое сочетание параметров, перечисленных в следующей таблице. По умолчанию эти дополнительные параметры не выбираются.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**IgnoreCase**|Указывает, следует ли при сравнении различать символы в верхнем и нижнем регистре. Если параметр задан, то строковое сравнение игнорирует регистр. Например, «ABC» при сравнении не отличается от «abc».|  
|**IgnoreNonSpace**|Указывает, следует ли при сравнении различать обычные символы и символы с диакритическими знаками. Если параметр задан, то строковое сравнение не учитывает диакритические знаки. Например, "Ã¥" будет считаться обычным символом "a".|  
|**IgnoreKanaType**|Указывает, следует ли различать при сравнении два типа символов японской азбуки: хирагана и катакана. Если параметр задан, то строковое сравнение игнорирует тип японской азбуки.|  
|**IgnoreWidth**|Указывает, следует ли при сравнении различать однобайтовые символы или аналогичные двухбайтовые символы. Если параметр задан, то строковое сравнение рассматривает однобайтовое и двухбайтовое представления символа как один и тот же символ.|  
  
### <a name="general-options"></a>Общие параметры  
 **RequestID**  
 Введите описательное имя для этого запроса профиля. Обычно не нужно менять автоматически сформированное значение.  
  
### <a name="options"></a>Параметры  
 **ThresholdSetting**  
 Это свойство имеет параметры, указанные в следующей таблице. Значение этого свойства по умолчанию равно **Specified**.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**None**|Пороговое значение не задано. Стойкость ключа указывается независимо от значения.|  
|**Specified**|Пороговое значение указывается свойством **KeyStrengthThreshold**. Стойкость ключа указывается лишь в том случае, если она превышает пороговое значение.|  
|**Exact**|Пороговое значение не задано. Стойкость ключа указывается лишь в том случае, если выделенные столбцы представляют собой точный ключ.|  
  
 **KeyStrengthThreshold**  
 Укажите пороговое значение (между 0 и 1), при превышении которого необходимо сообщать о стойкости ключа. Значение по умолчанию этого свойства равно 0,95. Этот параметр будет включен только в случае выбора для свойства **KeyStrengthThresholdSetting** значения **Определено**.  
  
 **MaxNumberOfViolations**  
 Укажите максимальное число нарушений потенциальных ключей для сообщения в выводе. Значение по умолчанию этого свойства равно 100. Этот параметр будет выключен только в случае выбора для свойства **KeyStrengthThresholdSetting** значения **Точно**.  
  
## <a name="see-also"></a>См. также:  
 [Редактор задачи "Профилирование данных" (страница "Общие")](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Форма быстрого профиля одной таблицы (задача "Профилирование данных")](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
