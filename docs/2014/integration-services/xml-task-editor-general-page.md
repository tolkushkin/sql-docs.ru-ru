---
title: Редактор задачи XML (страница "Общие") | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML Task Editor
ms.assetid: b9622c48-3243-4408-a1de-9ba20e32ff70
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aa0f92cc3275810b73d1dbe661a1f8473c7234df
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054282"
---
# <a name="xml-task-editor-general-page"></a>Редактор задачи «XML» (страница «Общие»)
  Используйте **Узел «Общие»** диалогового окна **Редактор задачи «XML»** для задания типа и настройки операции.  
  
 Дополнительные сведения об этой задаче см. в разделе [XML Task](control-flow/xml-task.md). Дополнительные сведения о работе с XML-документами и данными см. в разделе «[Employing XML in the .NET Framework](https://go.microsoft.com/fwlink/?LinkId=56214)» в библиотеке MSDN.  
  
## <a name="static-options"></a>Статические параметры  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **Source** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку **\<Создать переменную>**, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
## <a name="operationtype-dynamic-options"></a>Динамические параметры OperationType  
  
### <a name="operationtype--validate"></a>OperationType = Проверка  
 Задайте параметры для операции проверки.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции проверки.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Выберите существующий диспетчер подключений файлов или нажмите кнопку \<**Создать подключение...**>, чтобы создать новый диспетчер подключений.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
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
 Если значение свойства равно True, данные об ошибках будут содержать подробные сведения. Дополнительные сведения см. в разделе [Validate XML with the XML Task](control-flow/validate-xml-with-the-xml-task.md).  
  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **XPathStringSourceType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
### <a name="operationtype--xslt"></a>OperationType = XSLT  
 Задайте параметры для операции XSLT.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции XSLT.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **XPathStringSourceType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
### <a name="operationtype--xpath"></a>OperationType = XPATH  
 Задайте параметры для операции XPath.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции XPath.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **XPathStringSourceType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
 **PutResultInOneNode**  
 Укажите, записывается ли результат в один узел.  
  
 **XPathOperation**  
 Выберите тип результата операции XPath. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Ознакомительная версия**|Возвращает результаты функции XPath.|  
|**Список узлов**|Возвращаются выбранные узлы в качестве фрагмента кода XML.|  
|**Значения**|Возвращает текстовые представления содержимого всех выбранных узлов, объединенные в одну строку.|  
  
### <a name="operationtype--merge"></a>OperationType = Объединение  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **XPathStringSourceType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных в службах Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md)  
  
 При использовании инструкции XPath для определения места в исходном документе, куда необходимо вставить данные, ожидается, что инструкция возвратит единственный узел. Если инструкция возвращает несколько узлов, то используется только первый узел. Содержимое второго документа добавляется в первый узел, который возвращается запросом XPath.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции объединения.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **SecondOperandType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных в службах Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--diff"></a>OperationType = инструмент сравнения  
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
|**IgnoreNamespaces**|Укажите, сравнивать ли универсальный идентификатор ресурсов (URI) пространства имен элементов и имена атрибутов этих элементов.<br /><br /> Примечание. Если этот параметр имеет значение `True`, два элемента, имеющие одинаковое локальное имя, но разные пространства имен, считаются идентичными.|  
|**IgnoreProcessingInstructions**|Укажите, сравнивать ли инструкции по обработке.|  
|**IgnoreOrderOf ChildElements**|Укажите, сравнивать ли порядок дочерних элементов.<br /><br /> Примечание. Если этот параметр имеет значение `True`, дочерние элементы, отличающиеся только положением в списке одноуровневых элементов, считаются идентичными.|  
|**IgnoreComments**|Укажите, сравнивать ли узлы комментариев.|  
|**IgnorePrefixes**|Укажите, сравнивать ли префиксы элементов и имена атрибутов.<br /><br /> Примечание. При выборе этого параметра `True`, два элемента, имеющие одинаковое локальное имя, но разные коды URI пространств имен и префиксы, считаются идентичными.|  
  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **SecondOperandType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных в службах Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--patch"></a>OperationType = Patch  
 Задайте параметры для операции обновления.  
  
 **SaveOperationResult**  
 Укажите, сохраняет ли задача «XML» вывод операции обновления.  
  
 **OverwriteDestination**  
 Укажите, перезаписывать ли файл или переменную назначения.  
  
 **Назначение**  
 Если параметр **DestinationType** имеет значение **Соединение с файлом**, выберите диспетчер подключений файлов или нажмите кнопку \<**Создать соединение...**>, чтобы создать его.  
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **DestinationType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных служб Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
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
  
 **См. также:** подробные сведения о [диспетчере файловых подключений](connection-manager/file-connection-manager.md) и о [редакторе диспетчера файловых подключений](../../2014/integration-services/file-connection-manager-editor.md).  
  
 Если параметр **SecondOperandType** имеет значение **Переменная**, выберите существующую переменную или нажмите кнопку \<**Создать переменную...**>, чтобы создать ее.  
  
 **См. также**: подробные сведения о [переменных в службах Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) и о [добавлении переменной](../../2014/integration-services/add-variable.md).  
  
## <a name="see-also"></a>См. также  
 [Справочник по сообщениям об ошибках служб Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Страница «Выражения»](expressions/expressions-page.md)  
  
  
