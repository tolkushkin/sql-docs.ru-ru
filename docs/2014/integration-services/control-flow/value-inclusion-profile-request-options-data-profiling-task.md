---
title: Параметры запроса профиля включения значений (задача "Профилирование данных") | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: ca94da82-a4c9-4e87-9cba-c2d85bd31f01
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0a2037297db3f8a303ffd08fb31241e51505aeff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829476"
---
# <a name="value-inclusion-profile-request-options-data-profiling-task"></a>Параметры запроса профиля включения значений (задача «Профилирование данных»)
  На панели **Свойства запроса** страницы **Запросы профиля** можно задать параметры для варианта **Запрос профиля включения значений** , выбранного на панели запросов. Профиль «Включение значений» находит перекрывающиеся значения в двух столбцах или наборах столбцов. Таким образом, он также определяет, подойдет ли столбец или набор столбцов в качестве внешнего ключа для выбранных таблиц. Этот профиль также поможет выявить проблемы в данных, например наличие недопустимых значений. Так, профиль «Включение значений» можно использовать для создания профиля столбца ProductID таблицы Sales. Профиль определяет, что в столбце содержатся значения, отсутствующие в столбце ProductID таблицы Products.  
  
> [!NOTE]  
>  В этом разделе описываются параметры, расположенные на странице **Запросы профиля** в **редакторе задачи «Профилирование данных»**. Дополнительные сведения об этой странице редактора см. в разделе [Редактор задачи "Профилирование данных" (страница "Запросы профиля")](data-profiling-task-editor-profile-requests-page.md).  
  
 Дополнительные сведения об использовании задачи "Профилирование данных" см. в разделе [Установка задачи "Профилирование данных"](data-profiling-task.md). Дополнительные сведения об использовании средства просмотра профиля данных для анализа результатов задачи "Профилирование данных" см. в разделе [Средство просмотра профиля данных](data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-inclusioncolumns-property"></a>Основные сведения о выборе столбцов для свойства InclusionColumns  
 **Запрос профиля включения значений** проверяет, все ли значения, имеющиеся в подмножестве, представлены также и в надмножестве. Такое надмножество часто представляет из себя уточняющий запрос или ссылочную таблицу. Например, столбец «Штат» в таблице адресов — таблица подмножества. Каждый двухсимвольный код штата в этом столбце должен также содержаться в таблице кодов штатов Почтовой службы США, которая представляет собой таблицу надмножества.  
  
 При указании символа шаблона (*) в таблице надмножества или подмножества задача «Профилирование данных» сравнивает каждый столбец на одной стороне с каждым столбцом, указанным на другой стороне.  
  
> [!NOTE]  
>  Если выбрать символ (*), может потребоваться выполнение большого числа вычислений, что снизит производительность задачи.  
  
## <a name="understanding-the-threshold-settings"></a>Основные сведения о настройке пороговых значений  
 Чтобы улучшить выход запроса профиля включения значений, можно использовать два различных пороговых значения.  
  
 При указании значения, отличного от **None** , для свойства **InclusionThresholdSetting**, профиль сообщает о повышении интенсивности включения подмножества в надмножество только при выполнении одного из следующих условий:  
  
-   Если интенсивность включения превышает порог, определенный свойством **InclusionStrengthThreshold**.  
  
-   Если интенсивность включения имеет значение 1,0, а свойству **InclusionStrengthThreshold** присвоено значение **Exact**.  
  
 Можно улучшить выход, отфильтровывая сочетания, в которых столбец надмножества не подходит на роль ключа таблицы надмножества, поскольку содержит неуникальные значения. При указании значения, отличного от **None** , для свойства **SupersetColumnsKeyThresholdSetting**, профиль сообщает о повышении интенсивности включения подмножества в надмножество только при выполнении одного из следующих условий:  
  
-   Если пригодность столбцов надмножества на роль ключа таблицы надмножества превосходит порог, определенный свойством **SupersetColumnsKeyThreshold**  
  
-   Если интенсивность включения имеет значение 1,0, а свойству **SupersetColumnsKeyThreshold** задано значение **Exact**.  
  
## <a name="request-properties-options"></a>Параметры области «Свойства запроса»  
 Для **Запроса профиля включения значений**панель **Свойства запроса** предлагает следующий набор параметров:  
  
-   **Данные**, включающий параметры **SubsetTableOrView**, **SupersetTableOrView**и **InclusionColumns**  
  
-   **Общие сведения**  
  
-   **Параметры**  
  
### <a name="data-options"></a>Параметры данных  
 **ConnectionManager**  
 Выберите существующий диспетчер подключений [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , использующий поставщик данных .NET для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) для подключения к базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которая содержит таблицу или представление для профилирования.  
  
 **SubsetTableOrView**  
 Выберите существующую таблицу или представление для профилирования.  
  
 Дополнительные сведения см. в подразделе «Параметры SubsetTableOrView и SupersetTableOrView» далее в этом разделе.  
  
 **SupersetTableOrView**  
 Выберите существующую таблицу или представление для профилирования.  
  
 Дополнительные сведения см. в подразделе «Параметры SubsetTableOrView и SupersetTableOrView» далее в этом разделе.  
  
 **InclusionColumns**  
 Выберите столбцы или наборы столбцов из таблиц подмножества и надмножества.  
  
 Дополнительные сведения см. в подразделах «Выбор столбцов для свойства InclusionColumns» и «Параметры InclusionColumns» выше в этом разделе.  
  
#### <a name="subsettableorview-and-supersettableorview-options"></a>Параметры SubsetTableOrView и SupersetTableOrView  
 **Схема**  
 Указывает схему, которой принадлежит выбранная таблица. Этот параметр доступен только для чтения.  
  
 **TableOrView**  
 Отображает имя выбранной таблицы. Этот параметр доступен только для чтения.  
  
#### <a name="inclusioncolumns-options"></a>Параметры InclusionColumns  
 Следующие параметры предлагаются каждому набору столбцов, выбранных для профилирования в **InclusionColumns**.  
  
 Дополнительные сведения см. в подразделе «Выбор столбцов для свойства InclusionColumns» выше в этом разделе.  
  
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
|**IgnoreNonSpace**|Указывает, следует ли при сравнении различать обычные символы и символы с диакритическими знаками. Если параметр задан, то строковое сравнение не учитывает диакритические знаки. Например, буква «a» с любыми диакритическими знаками будет считаться обычной буквой «a».|  
|**IgnoreKanaType**|Указывает, следует ли различать при сравнении два типа символов японской азбуки: хирагана и катакана. Если параметр задан, то строковое сравнение игнорирует тип японской азбуки.|  
|**IgnoreWidth**|Указывает, следует ли при сравнении различать однобайтовые символы или аналогичные двухбайтовые символы. Если параметр задан, то строковое сравнение рассматривает однобайтовое и двухбайтовое представления символа как один и тот же символ.|  
  
### <a name="general-options"></a>Общие параметры  
 **RequestID**  
 Введите описательное имя для этого запроса профиля. Обычно не нужно менять автоматически сформированное значение.  
  
### <a name="options"></a>Параметры  
 **InclusionThresholdSetting**  
 Выберите пороговое значение для улучшения выхода профиля. Значение этого свойства по умолчанию равно **Specified**. Дополнительные сведения см. в подразделе «Основные сведения о пороговых значениях» ранее в этом разделе.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**None**|Не задает пороговое значение. Стойкость ключа указывается независимо от значения.|  
|**Specified**|Используется пороговое значение, указанное в **InclusionStrengthThreshold**. Интенсивность включения отмечается только при превышении порогового значения.|  
|**Exact**|Не задает пороговое значение. Интенсивность включения отмечается, только если значения подмножества полностью входят в надмножество.|  
  
 **InclusionStrengthThreshold**  
 Укажите пороговое значение (от 0 до 1). Если интенсивность включения превысит этот порог, будет создаваться уведомление. Значение по умолчанию этого свойства равно 0,95. Этот параметр разрешен, только когда свойство **InclusionThresholdSetting** установлено в значение **Specified**.  
  
 Дополнительные сведения см. в подразделе «Основные сведения о пороговых значениях» ранее в этом разделе.  
  
 **SupersetColumnsKeyThresholdSetting**  
 Укажите пороговое значение для надмножества. Значение этого свойства по умолчанию равно **Specified**. Дополнительные сведения см. в подразделе «Основные сведения о пороговых значениях» ранее в этом разделе.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**None**|Не задает пороговое значение. Интенсивность включения отмечается независимо от стойкости ключа столбца надмножества.|  
|**Specified**|Используется пороговое значение, указанное в **SupersetColumnsKeyThreshold**. Интенсивность включения отмечается, только если стойкость ключа столбца надмножества превышает пороговое значение.|  
|**Exact**|Не задает пороговое значение. Интенсивность включения отмечается, только если столбцы надмножества являются точными ключами в таблице надмножества.|  
  
 **SupersetColumnsKeyThreshold**  
 Укажите пороговое значение (от 0 до 1). Если интенсивность включения превысит этот порог, будет создаваться уведомление. Значение по умолчанию этого свойства равно 0,95. Этот параметр разрешен, только когда свойство **SupersetColumnsKeyThresholdSetting** установлено в значение **Specified**.  
  
 Дополнительные сведения см. в подразделе «Основные сведения о пороговых значениях» ранее в этом разделе.  
  
 **MaxNumberOfViolations**  
 Укажите максимальное число нарушений включений для сообщения о них на выходе. Значение по умолчанию этого свойства равно 100. Этот параметр будет выключен только в случае выбора для свойства **InclusionThresholdSetting** значения **Точно**.  
  
## <a name="see-also"></a>См. также  
 [Редактор задачи "Профилирование данных" (страница "Общие")](../general-page-of-integration-services-designers-options.md)   
 [Форма быстрого профиля одной таблицы (задача "Профилирование данных")](single-table-quick-profile-form-data-profiling-task.md)  
  
  
