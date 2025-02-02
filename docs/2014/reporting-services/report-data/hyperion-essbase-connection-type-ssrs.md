---
title: Тип подключения к Hyperion Essbase (службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 108a00b6-799f-4066-b796-da59e95c09fd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8a0c38487f58a6db6e80d48c2b39b09e3ed93106
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107271"
---
# <a name="hyperion-essbase-connection-type-ssrs"></a>Тип соединения Hyperion Essbase (службы SSRS)
  Чтобы включить данные из внешнего источника данных [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] в отчет, пользователь должен иметь набор данных, основанный на источнике данных отчета типа [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]. Этот встроенный тип источника данных основан на модуле обработки данных для [!INCLUDE[extEssbase](../../includes/extessbase-md.md)], позволяющего извлекать многомерные данные из внешнего источника данных [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] .  
  
 Используйте сведения в этом разделе для создания источника данных. Пошаговые инструкции см. в разделе [Добавление и проверка подключения к данным или источнику данных &#40;построитель отчетов и службы SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Строка подключения  
 Приведенный ниже пример строки соединения указывает источник данных [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] на сервере, использующем порт 13080 и XML для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (XMLA) при подключении к каталогу образцов через Интернет с использованием протокола SOAP:  
  
```  
Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample  
```  
  
 Дополнительные сведения о примерах строки подключения см. в разделе [Подключения к данным, источники данных и строки подключения в построителе отчетов](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
  
##  <a name="Credentials"></a> Учетные данные  
 Учетные данные необходимы для запуска запросов, локального предварительного просмотра отчетов, а также для предварительного просмотра отчетов на сервере отчетов.  
  
 После публикации отчета может понадобиться изменить учетные данные источника данных, чтобы разрешения, необходимые для получения данных при запуске отчета на сервере отчетов, были допустимыми.  
  
 Дополнительные сведения см. в разделе [подключения к данным, источники данных и строки подключения в службах Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) или [указание учетных данных в построителе отчетов](../specify-credentials-in-report-builder.md).  
  
  
##  <a name="Query"></a> Запросы  
 Запрос можно задавать следующими способами.  
  
-   Интерактивное построение отчета. Для просмотра метаданных во внешнем источнике данных и создания запроса с применением синтаксиса многомерных выражений (MDX) можно использовать графический конструктор запросов в режиме конструктора или в режиме запроса.  
  
    -   **Представление конструктора.** Перетащите измерения, элементы, свойства элементов, меры и ключевые показатели эффективности из браузера метаданных на панель **Данные** для создания запроса многомерных выражений. Перетащите вычисляемые элементы с панели "Вычисляемые элементы" на панель "Данные", чтобы определить дополнительные поля наборов данных.  
  
    -   **Представление запроса.** Перетащите измерения, элементы, свойства элементов, меры и ключевые показатели эффективности из браузера метаданных на панель «Запрос» для создания запроса многомерных выражений. Текст многомерного выражения можно изменять непосредственно на панели запроса. Перетащите вычисляемые элементы из панели "Вычисляемые элементы" в панель "Запрос" для определения дополнительных полей наборов данных.  
  
     Дополнительные сведения см. в статье [Пользовательский интерфейс конструктора запросов Hyperion Essbase (построитель отчетов)](../hyperion-essbase-query-designer-user-interface-report-builder.md).  
  
-   Импорт существующего запроса многомерных выражений из отчета. Воспользуйтесь кнопкой **Импорт** , чтобы указать RDL-файл и импортировать запрос. Можно импортировать запрос из отчета, содержащего внедренный набор данных, основанный на источнике данных служб [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] . Импорт запроса многомерных выражений непосредственно из MDX-файла не поддерживается.  
  
 Во время разработки выполните запрос, чтобы просмотреть результирующий набор. После создания запроса просмотрите коллекцию полей набора данных, созданную из метаданных в области данных отчета. При запуске отчета фактические данные возвращаются из внешнего источника данных.  
  
 Модуль обработки данных служб [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] поддерживает расширенные свойства полей набора данных. Эти значения доступны из внешнего источника данных, но они не отображаются в области данных отчета. Дополнительные сведения см. в подразделе [Расширенные свойства поля](#Extended) далее в этом разделе.  
  
  
##  <a name="Parameters"></a> Параметры  
 Чтобы включить параметры запроса, необходимо создать фильтр в области фильтра конструктора запросов и пометить фильтр как параметр. Для каждого фильтра будет автоматически создан набор данных, предоставляющий доступные значения. По умолчанию эти наборы данных не отображаются в области данных отчета. Дополнительные сведения см. в разделе [Отображение скрытых наборов данных для значений параметра в многомерных данных (построитель отчетов и службы SSRS)](show-hidden-datasets-for-parameter-values-multidimensional-data.md).  
  
 По умолчанию каждый параметр отчета имеет тип данных **Текст**. После создания параметров отчета можно изменить значения по умолчанию. Дополнительные сведения см. в разделах [Параметры отчета (построитель отчетов и конструктор отчетов)](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Extended"></a> Расширенные свойства поля  
 Модуль обработки данных [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] поддерживает расширенные свойства полей. Расширенные свойства полей дополняют свойства `Value` и `IsMissing`, заданные для полей набора данных с помощью модуля обработки данных. Расширенные свойства включают стандартные свойства и пользовательские. Стандартные свойства — это свойства, общие для многих источников данных. Пользовательские свойства уникальны для каждого источника данных.  
  
 Расширенные свойства полей не отображаются в области данных отчета как элементы, которые можно перетащить в макет отчета. Вместо этого вы перетаскиваете в отчет родительское поле свойства, а затем меняете свойство по умолчанию с `Value` на свойство, которое требуется.  
  
 Имя расширенного свойства поля появляется в подсказке, если задержать указатель мыши над любым полем на панели метаданных конструктора запросов. Дополнительные сведения об использовании конструктора запросов для исследования базовых данных см. в разделе [Hyperion Essbase Query Designer User Interface](hyperion-essbase-query-designer-user-interface.md).  
  
> [!NOTE]  
>  Значения расширенных свойств полей доступны только в том случае, когда они включены в многомерное выражение, а источник данных предоставляет эти значения в момент выполнения отчета и получения им данных. Затем можно ссылаться на эти значения свойства `Field` из любого выражения с помощью синтаксиса, описанного в следующем разделе. Но поскольку эти поля относятся только к этому поставщику данных и не являются частью языка определения отчетов, изменения в этих значениях не сохраняются вместе с определением отчета.  
  
  
### <a name="predefined-field-properties"></a>Стандартные свойства полей  
 Стандартные свойства поля поддерживаются большинством поставщиков данных и указываются в запросах многомерных выражений к набору данных для отчета. Например, свойство измерения MEMBER_UNIQUE_NAME многомерного выражения сопоставлено со стандартным свойством `UniqueName` поля набора данных для отчета. Для включения в текстовое поле уникального имени используется следующее выражение: `=Fields!`*\<имя_поля>*`.UniqueName`.  
  
 В следующей таблице представлен список стандартных свойств поля, которые можно использовать для источника данных [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] .  
  
|**Свойство**|**Тип**|**Описание или ожидаемое значение**|  
|------------------|--------------|---------------------------------------|  
|`Value`|`Object`|Указывает значение данных поля.<br /><br /> Для свойства измерения оно сопоставлено с параметром MEMBER_CAPTION. Для меры оно сопоставлено со значением данных.|  
|`IsMissing`|`Boolean`|Указывает, найдено ли поле в результирующем наборе данных.|  
|`FormattedValue`|`String`|Возвращает форматированное значение для ключевой цифры.<br /><br /> В многомерном выражении сопоставляется с FORMATTED_VALUE.|  
|`BackgroundColor`|`String`|Возвращает цвет фона, заданный в базе данных для этого поля.<br /><br /> В многомерном выражении сопоставляется с BACK_COLOR.|  
|`Color`|`String`|Возвращает цвет переднего плана, заданный в базе данных для этого элемента.<br /><br /> В многомерном выражении сопоставляется с FORE_COLOR.|  
|`UniqueName`|`String`|Возвращает полное имя уровня.<br /><br /> В многомерном выражении сопоставляется с MEMBER_UNIQUE_NAME.|  
  
 Дополнительные сведения об использовании полей и свойств полей в выражении см. в разделе [Встроенные коллекции в выражениях (построитель отчетов и службы SSRS)](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
  
### <a name="custom-properties"></a>Пользовательские свойства  
 Пользовательские свойства полей поддерживаются поставщиками данных и могут быть указаны в базовом запросе многомерных выражений для набора данных отчета, однако не отражаются на панели наборов данных отчета в виде полей. Например, **Long Names** — это свойство элемента, определенное для уровня измерения. Для включения в текстовое поле этого значения используйте выражение `=Fields!`*\<имя_поля>*`("Long Names")`. Имена полей в выражении учитывают регистр символов.  
  
 Для обращения к пользовательским расширенным свойствам в выражении применяется следующий синтаксис:  
  
-   *Fields!ИмяПоля("ИмяСвойства")*  
  
 В следующей таблице приведен список пользовательских свойств поля, которые могут быть использованы для источника данных [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] .  
  
|**Свойство**|**Тип**|**Описание или ожидаемое значение**|  
|------------------|--------------|---------------------------------------|  
|`FORMAT_STRING`|`String`|Определяется для меры, это `FormattedValue`, доступное в виде типа String.|  
  
  
##  <a name="Remarks"></a> Замечания  
 Этот поставщик данных поддерживает не все режимы доставки отчетов. Доставка отчетов с помощью управляемых данными подписок для этого модуля обработки данных не предусмотрена. Дополнительные сведения см. в разделе [Использование внешнего источника данных для данных подписчика (управляемая данными подписка)](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md) документации по службам [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в [электронной документации](https://go.microsoft.com/fwlink/?linkid=121312) по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Дополнительные сведения см. в разделе [Использование служб SQL Server 2005 Reporting Services совместно с Hyperion Essbase Intelligence](https://go.microsoft.com/fwlink/?LinkId=81970).  
  
  
##  <a name="HowTo"></a> Инструкции  
 В этом разделе содержатся пошаговые инструкции по работе с подключениями к данным, источниками данных и наборами данных.  
  
 [Добавление и проверка подключения к данным или источнику данных &#40;построитель отчетов и службы SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Создание общего или внедренного набора данных (построитель отчетов и службы SSRS)](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Добавление фильтра к набору данных (построитель отчетов и службы SSRS)](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> См. также  
 В этих разделах документации содержатся подробные сведения о данных отчетов, а также методические сведения об определении, настройке и использовании элементов отчетов, связанных с данными.  
  
 [Добавление данных в отчет &#40;построитель отчетов и службы SSRS&#41;](report-datasets-ssrs.md)  
 Предоставляет общие сведения о доступе к данным отчета.  
  
 [Подключения к данным, источники данных и строки подключения в построителе отчетов](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Предоставляет сведения о подключениях к данным и источникам данных.  
  
 [Внедренные и общие наборы данных отчета (построитель отчетов и службы SSRS)](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Предоставляет сведения об общих и внедренных наборах данных.  
  
 [Коллекция полей набора данных (построитель отчетов и службы SSRS)](dataset-fields-collection-report-builder-and-ssrs.md)  
 Предоставляет сведения о коллекции полей, создаваемой запросом набора данных.  
  
 [Источники данных, поддерживаемые службами Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md), см. в документации [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в [электронной документации](https://go.microsoft.com/fwlink/?linkid=121312) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Предоставляет подробные сведения о поддержке платформ и версий для каждого модуля обработки данных.  
  
 [Использование служб SQL Server 2005 Reporting Services совместно с Hyperion Essbase Intelligence](https://go.microsoft.com/fwlink/?LinkId=81970)  
 Предоставляет подробные сведения о работе с этим модулем обработки данных.  
  
  
## <a name="see-also"></a>См. также  
 [Параметры отчета (построитель отчетов и конструктор отчетов)](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Фильтрация, группирование и сортировка данных (построитель отчетов и службы SSRS)](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Выражения (построитель отчетов и службы SSRS)](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
