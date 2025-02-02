---
title: Задача "XML" | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.xmltask.f1
- sql13.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f41f693c05c2f5977301ac4863fe978cc876ea4f
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727296"
---
# <a name="xml-task"></a>Задача «XML»

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Задача «XML» используется для работы с XML-данными. С помощью этой задачи пакет может получать XML-документы, выполнять операции над документами с помощью преобразований XSLT и выражений XPath, объединять несколько документов, проверять, сравнивать и сохранять обновленные документы в файлы и переменные.  
  
 Эта задача позволяет пакету служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] динамически изменять XML-документы во время выполнения. Можно использовать задачу «XML» для следующих целей.  
  
-   Изменение формата XML-документа. Например, задача может получить доступ к отчету, который хранится в XML-файле, и динамически настроить представление документа с помощью таблицы стилей XSLT.  
  
-   Выбор разделов XML-документа. Например, задача может получить доступ к отчету, который хранится в XML-файле, и динамически выбрать раздел документа с помощью выражения XPath. Эта операция также может получить значения обработки в документе.  
  
-   Объединение документов из нескольких источников. Например, задача может загрузить отчет из нескольких источников и динамически объединить их в единый общий XML-документ.  
  
-   Проверка XML-документов с возможностью получения подробных сведений об ошибках. Дополнительные сведения см. в разделе [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
 Можно включить XML-данные в поток данных, извлекая значения из XML-документа с помощью источника XML-данных. Дополнительные сведения см. в статье [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## <a name="xml-operations"></a>Операции XML  
 Вначале задача «XML» получает конкретный XML-документ. Это действие встроено в задачу «XML» и выполняется автоматически. Найденный XML-документ используется в качестве источника данных для операций, выполняемых задачей «XML».  
  
 Для XML-операций Diff, Merge и Patch требуются два операнда. Первый операнд указывает на исходный XML-документ. Второй операнд также указывает на XML-документ, содержимое которого зависит от требований операции. Например, операция Diff сравнивает два документа, следовательно, второй операнд указывает на другой, похожий XML-документ, с которым сравнивается исходный XML-документ.  
  
 Задача «XML» может использовать переменную или диспетчер соединения файлов в качестве их источника либо включить XML-данные в свойство задачи.  
  
 Если источником является переменная, то указанная переменная содержит путь к XML-документу.  
  
 Если в качестве источника задан диспетчер соединения файлов, то указанный диспетчер соединения файлов предоставляет исходные данные. Диспетчер соединения файлов настраивается отдельно от задачи «XML», в которой на него есть ссылка. Строка соединения диспетчера соединения файлов представляет собой путь к XML-файлу. Дополнительные сведения см. в статье [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 В задаче «XML» можно настроить сохранение результата в переменную или в файл. Если выполняется сохранение в файл, то задача «XML» использует для доступа к нему диспетчер соединения файлов. Кроме того, созданные операцией Diff результаты Diffgram можно сохранить в файлы или переменные.  
  
## <a name="predefined-xml-operations"></a>Стандартные операции XML  
 Задача «XML» поддерживает стандартный набор операций для работы с XML-документами. Данные операции описываются в следующей таблице.  
  
|Операция|Описание|  
|---------------|-----------------|  
|Поиск различий|Сравнивает два XML-документа. Операция Diff сравнивает исходный XML-документ в качестве основного со вторым XML-документом, находит различия между ними и записывает их в XML-документ Diffgram. Эта операция содержит свойства для настройки сравнения.|  
|Объединить|Выполняет слияние двух XML-документов. Операция Merge берет исходный XML-документ в качестве основного и добавляет к нему содержимое второго документа. Можно задать место в основном документе, куда будут вставлены данные.|  
|Обновление|Добавляет в указанный в XML-документ выходной документ операции Diff (документ Diffgram), чтобы получился новый документ, включающий в себя содержимое документа Diffgram.|  
|Проверить|Проверяется соответствие XML-документа определению типа документа (DTD) или схеме определения XML-схемы (XSD, XML Schema definition).|  
|XPath|Выполняет запросы и вычисления XPath.|  
|XSLT|Выполняет преобразование XSL в XML-документах.|  
  
### <a name="diff-operation"></a>Операция Diff  
 В операции Diff можно настроить использование различных алгоритмов сравнения в зависимости от того, каким должно быть сравнение: быстрым или точным. Кроме того, можно настроить автоматический выбор быстрого или точного сравнения в зависимости от размера сравниваемых документов.  
  
 Операция Diff имеет набор параметров для настройки сравнения XML-документов. В следующей таблице приводятся описания дополнительных параметров.  
  
|Параметр|Описание|  
|------------|-----------------|  
|**IgnoreComments**|Значение параметра указывает, нужно ли сравнивать комментарии.|  
|**IgnoreNamespaces**|Значение параметра указывает, нужно ли сравнивать URI пространства имен элемента и его имен атрибутов. Если этот параметр имеет значение **true**, то два элемента с одинаковым локальным именем, но различными пространствами имен будут считаться идентичными.|  
|**IgnorePrefixes**|Значение параметра показывает, нужно ли сравнивать префиксы элементов и имен атрибутов. Если этот параметр имеет значение **true,** , то два элемента с одинаковым локальным именем, но различными URI и префиксами пространства имен считаются идентичными.|  
|**IgnoreXMLDeclaration**|Значение параметра указывает, нужно ли сравнивать XML-декларации.|  
|**IgnoreOrderOfChildElements**|Значение параметра указывает, нужно ли сравнивать порядок дочерних элементов. Если этот параметр имеет значение **true**, то дочерние элементы, отличающиеся только по позиции одноуровневых элементов, считаются идентичными.|  
|**IgnoreWhiteSpaces**|Значение параметра указывает, нужно ли сравнивать пробелы.|  
|**IgnoreProcessingInstructions**|Значение параметра указывает, нужно ли сравнивать инструкции по обработке.|  
|**IgnoreDTD**|Значение параметра указывает, нужно ли пропускать DTD.|  
  
### <a name="merge-operation"></a>Операция Merge  
 При использовании инструкции XPath для определения места в исходном документе, куда необходимо вставить данные, ожидается, что инструкция возвратит единственный узел. Если инструкция возвращает несколько узлов, то используется только первый узел. Содержимое второго документа добавляется в первый узел, который возвращается запросом XPath.  
  
### <a name="xpath-operation"></a>Операция XPath  
 В операции XPath можно настроить использование различных типов функциональности XPath.  
  
-   Чтобы использовать такие функции XPath, как sum(), выберите параметр **Вычисление** .  
  
-   Выберите параметр **Список узлов** , чтобы вернуть выбранные узлы в виде XML-фрагмента.  
  
-   Чтобы вернуть внутренние текстовые значения всех выбранных узлов, объединенные в одну строку, выберите параметр **Значения** .  
  
### <a name="validation-operation"></a>Операция Validation  
 В операции Validation можно настроить использование определения типа документа (DTD) или определения схемы XML (XSD).  
  
 Чтобы получать подробные сведения об ошибках, активируйте свойство **ValidationDetails** . Дополнительные сведения см. в разделе [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
## <a name="xml-document-encoding"></a>Кодировка XML-документа  
 Задача «XML» поддерживает объединение только для документов в Юникоде. Это означает, что задача может применять операцию Merge только к документам в Юникоде. Использование других кодировок приведет к ошибке выполнения задачи «XML».  
  
> [!NOTE]  
>  В операциях Diff и Patch можно пропускать XML-декларацию в XML-данных второго операнда, что дает возможность использовать в этих операциях документы в других кодировках.  
  
 Чтобы проверить возможность использования XML-документа, просмотрите XML-декларацию. В декларации должно быть явно задано значение UTF-8, что означает 8-разрядную кодировку Юникод.  
  
 8-разрядную кодировку Юникод показывают следующие теги.  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>Пользовательские сообщения для ведения журнала, доступные в задаче «XML»  
 В приведенной ниже таблице перечислены пользовательские записи журнала для задачи «XML». Дополнительные сведения см. в разделе [Ведение журналов в службах Integration Services (SSIS)](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Запись журнала|Описание|  
|---------------|-----------------|  
|**XMLOperation**|Предоставляет сведения об операции, выполняемой задачей|  
  
## <a name="configuration-of-the-xml-task"></a>Настройка задачи «XML»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующих разделах:  
  
-   [Проверка XML с использованием задачи «XML»](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)  
  
-   [Страница «Выражения»](../../integration-services/expressions/expressions-page.md)  
  
 Дополнительные сведения об установке этих свойств в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в следующем разделе.  
  
-   [Задание свойств задач или контейнеров](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>Программная настройка задачи «XML»  
 Дополнительные сведения об установке этих свойств программными средствами см. в следующем разделе.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>Связанные задачи  
 [Задание свойств задач или контейнеров](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="xml-task-editor-general-page"></a>Редактор задачи «XML» (страница «Общие»)
  Используйте **Узел «Общие»** диалогового окна **Редактор задачи «XML»** для задания типа и настройки операции.  
  
 Сведения об этой задаче см. в разделе [Проверка XML с использованием задачи XML](../../integration-services/control-flow/validate-xml-with-the-xml-task.md). Дополнительные сведения о работе с XML-документами и данными см. в разделе «[Employing XML in the .NET Framework](https://go.microsoft.com/fwlink/?LinkId=56214)» в библиотеке MSDN.  
  
### <a name="static-options"></a>Статические параметры  
 **OperationType**  
 Выберите из списка тип операции. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Проверить**|Проверяется соответствие XML-документа определению типа документа (DTD) или схеме определения XML-схемы (XSD, XML Schema definition). При выборе этого параметра в разделе отображаются динамические параметры **Проверить**.|  
|**XSLT**|Выполняет преобразование XSL в XML-документах. При выборе этого параметра в разделе отображаются динамические параметры **XSLT**.|  
|**XPATH**|Выполняет запросы и вычисления XPath. При выборе этого параметра в разделе отображаются динамические параметры **XPATH**.|  
|**Объединить**|Выполняет слияние двух XML-документов. При выборе этого параметра отображаются динамические параметры в разделе **Слияние**.|  
|**Поиск различий**|Сравнивает два XML-документа. При выборе этого параметра отображаются динамические параметры в разделе **Поиск различий**.|  
|**Обновление**|Результат операции поиска различий применяется для создания нового документа. При выборе этого параметра в разделе отображаются динамические параметры **Обновление**.|  
  
 **Тип источника**  
 Выберите тип источника XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Прямой ввод**|Задайте источник для XML-документа.|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **Source**  
 Если параметр **Source** имеет значение **Прямой ввод**, укажите код XML или нажмите кнопку с многоточием **(...)**, а затем укажите код XML в диалоговом окне **Редактор исходного текста документа**.  
  
 Если параметр **Source** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **Source** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку **\<Создать переменную>**, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
### <a name="operationtype-dynamic-options"></a>Динамические параметры OperationType  
  
#### <a name="operationtype--validate"></a>OperationType = Проверка  
 Задайте параметры для операции проверки.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции проверки.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Выберите существующий диспетчер подключений файлов или нажмите кнопку \<**Создать подключение...**>, чтобы создать новый диспетчер подключений.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 **DestinationType**  
 Выберите тип назначения XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **ValidationType**  
 Выберите тип проверки. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**DTD**|Использование определения типа документа (DTD).|  
|**XSD**|Использование определения схемы XML (XSD). При выборе этого параметра в разделе отображаются динамические параметры **ValidationType**.|  
  
 **FailOnValidationFail**  
 Укажите, заканчивается ли операция с ошибкой, если не удается проверить документ.  
  
 **ValidationDetails**  
 Если значение свойства равно True, данные об ошибках будут содержать подробные сведения. Дополнительные сведения см. в разделе [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md).  
  
### <a name="validationtype-dynamic-options"></a>Динамические параметры ValidationType  
  
#### <a name="validationtype--xsd"></a>ValidationType = XSD  
 **SecondOperandType**  
 Выберите тип источника второго XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Прямой ввод**|Задайте источник для XML-документа.|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperand**  
 Если параметр **SecondOperandType** имеет значение **Прямой ввод**, укажите XML-код или нажмите кнопку с многоточием **(...)**, а затем введите XML-код в диалоговом окне **Редактор источника**.  
  
 Если параметр **SecondOperandType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **XPathStringSourceType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
#### <a name="operationtype--xslt"></a>OperationType = XSLT  
 Задайте параметры для операции XSLT.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции XSLT.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Выберите тип назначения XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperandType**  
 Выберите тип источника второго XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Прямой ввод**|Задайте источник для XML-документа.|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperand**  
 Если параметр **SecondOperandType** имеет значение **Прямой ввод**, укажите XML-код или нажмите кнопку с многоточием **(...)**, а затем введите XML-код в диалоговом окне **Редактор источника**.  
  
 Если параметр **SecondOperandType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **XPathStringSourceType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
#### <a name="operationtype--xpath"></a>OperationType = XPATH  
 Задайте параметры для операции XPath.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции XPath.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Выберите тип назначения XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperandType**  
 Выберите тип источника второго XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Прямой ввод**|Задайте источник для XML-документа.|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperand**  
 Если параметр **SecondOperandType** имеет значение **Прямой ввод**, укажите XML-код или нажмите кнопку с многоточием **(...)**, а затем введите XML-код в диалоговом окне **Редактор источника**.  
  
 Если параметр **SecondOperandType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **XPathStringSourceType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **PutResultInOneNode**  
 Укажите, записывается ли результат в один узел.  
  
 **XPathOperation**  
 Выберите тип результата операции XPath. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Ознакомительная версия**|Возвращает результаты функции XPath.|  
|**Список узлов**|Возвращаются выбранные узлы в качестве фрагмента кода XML.|  
|**Значения**|Возвращает текстовые представления содержимого всех выбранных узлов, объединенные в одну строку.|  
  
#### <a name="operationtype--merge"></a>OperationType = Объединение  
 Задайте параметры для операции объединения.  
  
 **XPathStringSourceType**  
 Выберите тип источника XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Прямой ввод**|Задайте источник для XML-документа.|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **XPathStringSource**  
 Если параметр **XPathStringSourceType** имеет значение **Прямой ввод**, укажите XML-код или нажмите кнопку с многоточием **(...)**, а затем введите XML-код в диалоговом окне **Редактор исходного текста документа**.  
  
 Если параметр **XPathStringSourceType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать подключение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **XPathStringSourceType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных в службах Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 При использовании инструкции XPath для определения места в исходном документе, куда необходимо вставить данные, ожидается, что инструкция возвратит единственный узел. Если инструкция возвращает несколько узлов, то используется только первый узел. Содержимое второго документа добавляется в первый узел, который возвращается запросом XPath.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции объединения.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Выберите тип назначения XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperandType**  
 Выберите тип получателя второго XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Прямой ввод**|Задайте источник для XML-документа.|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperand**  
 Если параметр **SecondOperandType** имеет значение **Прямой ввод**, укажите XML-код или нажмите кнопку с многоточием **(...)**, а затем укажите XML-код в диалоговом окне **Редактор исходного текста документа**.  
  
 Если параметр **SecondOperandType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **SecondOperandType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных в службах Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--diff"></a>OperationType = инструмент сравнения  
 Задайте параметры для операции поиска различий.  
  
 **DiffAlgorithm**  
 Выберите алгоритм поиска различий, который будет использоваться при сравнении документов. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Автоматически**|Предоставьте задаче «XML» определить, использовать ли быстрый или точный алгоритм.|  
|**Быстрый**|Применение быстрого, но менее точного алгоритма поиска различий.|  
|**Точный**|Применение точного алгоритма поиска различий.|  
  
 **Параметры операции поиска различий**  
 Задание параметров, применяемых в операции поиска различия. Эти параметры перечисляются в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|Укажите, сравнивать ли XML-декларации.|  
|**IgnoreDTD**|Укажите, пропускать ли обработку определения типа документа (DTD).|  
|**IgnoreWhite Spaces**|Укажите, пропускать ли различия в количестве пробелов при сравнении документов.|  
|**IgnoreNamespaces**|Укажите, сравнивать ли универсальный идентификатор ресурсов (URI) пространства имен элементов и имена атрибутов этих элементов.<br /><br /> Примечание. Если этот параметр имеет значение **True**, два элемента, имеющие одинаковое локальное имя, но разные пространства имен, считаются идентичными.|  
|**IgnoreProcessingInstructions**|Укажите, сравнивать ли инструкции по обработке.|  
|**IgnoreOrderOf ChildElements**|Укажите, сравнивать ли порядок дочерних элементов.<br /><br /> Примечание. Если этот параметр имеет значение **True**, дочерние элементы, отличающиеся только положением в списке одноуровневых элементов, считаются идентичными.|  
|**IgnoreComments**|Укажите, сравнивать ли узлы комментариев.|  
|**IgnorePrefixes**|Укажите, сравнивать ли префиксы элементов и имена атрибутов.<br /><br /> Примечание. Если этот параметр имеет значение **True**, два элемента, имеющие одинаковое локальное имя, но разные префиксы и коды URI пространств имен, считаются идентичными.|  
  
 **FailOnDifference**  
 Укажите, заканчивается ли задача с ошибкой, если не удается выполнить операцию поиска различий.  
  
 **SaveDiffGram**  
 Укажите, сохранять ли результаты сравнения в виде документа DiffGram.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции поиска различий.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Выберите тип назначения XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperandType**  
 Выберите тип назначения XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Прямой ввод**|Задайте источник для XML-документа.|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperand**  
 Если параметр **SecondOperandType** имеет значение **Прямой ввод**, укажите XML-код или нажмите кнопку с многоточием **(...)**, а затем укажите XML-код в диалоговом окне **Редактор исходного текста документа**.  
  
 Если параметр **SecondOperandType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **SecondOperandType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных в службах Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--patch"></a>OperationType = Patch  
 Задайте параметры для операции обновления.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции обновления.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **DestinationType**  
 Выберите тип назначения XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperandType**  
 Выберите тип назначения XML-документа. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Прямой ввод**|Задайте источник для XML-документа.|  
|**Соединение с файлом**|Выберите файл, содержащий XML-документ.|  
|**Переменная**|В качестве источника задайте переменную, содержащую XML-документ.|  
  
 **SecondOperand**  
 Если параметр **SecondOperandType** имеет значение **Прямой ввод**, укажите XML-код или нажмите кнопку с многоточием **(...)**, а затем укажите XML-код в диалоговом окне **Редактор исходного текста документа**.  
  
 Если параметр **SecondOperandType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](../../integration-services/connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Если параметр **SecondOperandType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных в службах Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) и о [добавлении переменной](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>См. также  

-   Образец CodePlex [Образец обработки пакета XML-данных](https://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples)на сайте www.codeplex.com  
  
  
