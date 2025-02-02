---
title: Управление источниками данных отчета | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- published reports [Reporting Services], data source connections
- shared data sources [Reporting Services]
- data sources [Reporting Services], managing
ms.assetid: 0475aded-c8fe-4337-a2b5-4df0ec4c46af
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 737e5eb03cabe655b4b1dc1da6735b9b4ef68c05
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107253"
---
# <a name="manage-report-data-sources"></a>Управление источниками данных отчета
  В службах [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]отчеты, модели отчетов и управляемые данными подписки получают данные из внешних источников данных. Чтобы подключиться к внешнему источнику данных, сервер отчетов использует сведения соединения с источником данных, которые определены в отчете, модели или подписке или на которые они ссылаются. Свойства соединения с источником данных всегда определяются при создании отчета или модели, но управление ими может выполняться отдельно после публикации отчета или модели на сервере отчетов.  
  
 Управление источниками данных отчета производится при помощи диспетчера отчетов для сервера отчетов, работающего в собственном режиме, либо страницы приложения на сайте SharePoint, если сервер отчетов развернут в режиме интеграции с SharePoint.  
  
 Управление соединениями с источниками данных связано с выполнением следующих задач, описываемых в этом разделе.  
  
-   Изменение строк соединений.  
  
-   Изменение учетных данных.  
  
-   Создание и использование общих источников данных на сервере отчетов, в том числе переключение внедренного источника данных для общего источника данных.  
  
-   Управление доступом к свойствам источников данных заданием разрешений для отчета, модели или используемых общих источников данных.  
  
 Обратите внимание, что изменение запросов в задачи управления соединениями с источниками данных не входит. Изменение запроса для отчета или модели необходимо производить при помощи средств разработки, а затем вносить изменения в определение отчета или модели.  
  
## <a name="managed-properties-data-source-type-connection-strings-and-credentials"></a>Управляемые свойства: Тип источника данных, строки подключения и учетные данные  
 Свойства источника данных, доступные для управления на сервере отчетов:  
  
|Свойство|Описание|Способ управления свойством|  
|--------------|-----------------|----------------------|  
|Тип источника данных|Определяет, какие модули обработки данных сервера отчетов должны использоваться для внешних данных. В качестве примеров процессоров данных могут быть указаны SQL Server, службы Analysis Services или база данных Oracle.|Тип источника данных является управляемым свойством, поскольку оно может быть настроено. Однако настраивать тип источника данных следует только при создании нового общего источника данных.<br /><br /> Изменять тип источника данных на страницах свойств опубликованного отчета или опубликованной модели не следует, так как это почти наверняка нарушит работоспособность соединения. Маловероятно, что на новой платформе данных структуры данных, необходимые отчету или модели, совпадут со старыми.|  
|Строка соединения|Устанавливает начальное соединение с внешним источником данных. Отчет может использовать статические или динамические строки соединения.<br /><br /> *Статическая строка соединения* представляет собой набор значений, которые отчет всегда использует для соединения с одним и тем же источником данных при каждом запуске отчета.<br /><br /> *Динамическая строка соединения* представляет собой выражение, встроенное в отчет, которое дает пользователю возможность выбрать источник данных, который следует использовать во время выполнения. Выражение и список выбора источников данных встраиваются в отчет во время его создания в конструкторе отчетов.|Изменение строки соединения может оказаться полезным при переносе источника данных на другой компьютер либо если отчет создается с использованием тестовых данных, но затем отчеты должны развертываться при помощи производственной базы данных.<br /><br /> Управление статическими строками соединения производится только путем их замены.<br /><br /> Возможности управления динамическими строками соединения в диспетчере отчетов или на сайте SharePoint ограничены заменой этой строки на статическую. Нельзя изменять ни само выражение, ни список выбора источников данных. Чтобы изменить выражение или список допустимых значений, необходимо изменить определение отчета и повторно опубликовать отчет на сервере отчетов. Дополнительные сведения см. в разделе [Подключения данных, источники данных и строки подключения в службе Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).|  
|Учетные данные|Предоставляют имя и пароль пользователя, имеющего разрешение на чтение данных из источника данных.<br /><br /> Если источник данных не поддерживает проверку подлинности (например, если источником данных является XML-файл или файловая система), то можно настроить учетную запись автоматического выполнения, чтобы сервер отчетов мог соединиться с источником внешних данных без передачи учетных данных.|Управление учетными данными позволяет обновить учетную запись или пароль пользователя при истечении срока его действия.<br /><br /> Можно также изменить способ получения учетных данных (например, предложив пользователю ввести учетные данные во время выполнения).<br /><br /> Если необходимо предоставить пользователям возможность подписки на отчет, то необходимо настроить отчет на использование сохраненных учетных данных.|  
  
## <a name="creating-and-using-shared-data-sources"></a>Создание и использование общих источников данных  
 Если публикация отчета производится с внедренными свойствами источника данных, необходимо рассмотреть вопрос перехода на свойства общего источника данных. Общими источниками данных легче управлять, поскольку они позволяют обновлять учетные данные и строки соединения на одной странице. Изменения мгновенно отразятся на всех отчетах, моделях и управляемых данных подписки, использующих этот источник данных. Работать с общим источником данных можно также в режиме «вне сети», эффективно приостановив отчет или подписку, чтобы предотвратить их выполнение во время устранения неполадок или исследования возникших проблем.  
  
## <a name="controlling-access-data-source-properties"></a>Управление доступом к свойствам источника данных  
 По умолчанию любой пользователь, имеющий разрешения на управление отчетами, может задавать для отчета любые свойства, в том числе определяющие тип источника данных, строку соединения, учетные данные, а также получение отчетом сведений о соединении из внедренного или общего источника данных. Дополнительные сведения о том, какие задачи и разрешения управляют доступом к свойствам источников данных на сервере отчетов, работающем в собственном режиме, см. в разделах [Защита элементов общего набора данных](../security/secure-shared-data-source-items.md) и [Защищенные отчеты и ресурсы](../security/secure-reports-and-resources.md).  
  
 Разрешения на просмотр и изменение свойств элементов в библиотеке SharePoint определяются администратором сайта. Дополнительные сведения о том, какие разрешения управляют доступом к свойствам подключения к источнику данных, см. в разделе [Справочная таблица по разрешениям на сайты SharePoint и списки для элементов сервера отчетов](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
## <a name="how-to-work-with-data-source-properties-on-a-report-server"></a>Работа со свойствами источника данных на сервере отчетов  
 Создание и изменение свойств источника данных может быть выполнено различными средствами. В следующей таблице приведено краткое описание подходов и средств со ссылками на дополнительные инструкции.  
  
|Задача|Инструмент|Ссылка|  
|----------|----------|----------|  
|Просмотр примеров строк соединения.||[Подключения данных, Источники данных и Строки подключения в службе Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Выбор подхода для получения учетных данных для соединения с источником данных.||[Задание учетных данных и сведениях о соединении для источников данных отчета](specify-credential-and-connection-information-for-report-data-sources.md)|  
|Добавление свойств соединения с источником данных в файл определения отчета (RDL).|конструктор отчетов|[Создание внедренного или общего источника данных (службы SSRS)](../create-an-embedded-or-shared-data-source-ssrs.md)|  
|Добавление и создание ссылки на файл общего источника данных (RDS) в проекте отчета.|конструктор отчетов|[Создание, изменение и удаление общих источников данных (службы SSRS)](create-modify-and-delete-shared-data-sources-ssrs.md)|  
|Создание стандартного списка, из которого пользователь выбирает источник данных во время выполнения. Когда пользователь запрашивает отчет, то список источников данных берется из отчета. Пользователь должен выбрать источник данных, который следует использовать при выполнении отчета. Для добавления в отчет списка выбора источников данных используется выражение.<br /><br /> Это называется динамическим соединением с источником данных.|конструктор отчетов|[Подключения данных, Источники данных и Строки подключения в службе Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Создание на сервере отчетов совместно используемого элемента источника данных.|Диспетчер отчетов|[Создание, удаление или изменение общего источника данных (диспетчер отчетов)](../create-delete-or-modify-a-shared-data-source-report-manager.md)|  
|Сохранение учетных данных, необходимых для создания подписок или моментальных снимков отчетов.|Диспетчер отчетов|[Сохраненные учетные данные в источнике данных Reporting Services](store-credentials-in-a-reporting-services-data-source.md)|  
|Изменение свойств соединения с источником данных для опубликованного отчета.|Диспетчер отчетов|[Настройка свойств источника данных для отчета (диспетчер отчетов)](configure-data-source-properties-for-a-report-report-manager.md)|  
|Создание на сервере отчетов совместно используемого элемента источника данных.|Сайт SharePoint|[Создание общих источников данных и управление ими (службы Reporting Services в режиме интеграции с SharePoint)](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)|  
|Использование с отчетом существующего ODC-файла, содержащего сведения о соединении.|Сайт SharePoint|[Использование ODC-файла подключения к данным Office в отчетах (службы Reporting Services в режиме интеграции с SharePoint)](use-an-office-data-connection-odc-with-reports.md)|  
  
> [!NOTE]  
>  Управление соединениями источников данных с источниками данных отчета отличается от управления соединением сервера отчетов с базой данных сервера отчетов. Дополнительные сведения о подключении сервера отчетов к внутреннему хранилищу данных см. в разделе [Настройка подключения к базе данных сервера отчетов (диспетчер конфигурации служб SSRS)](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>См. также  
 [Привязка отчета или модели к общему источнику данных (службы SSRS)](bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Создание, удаление или изменение общего источника данных (диспетчер отчетов)](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Сохранение учетных данных в источнике данных служб Reporting Services](store-credentials-in-a-reporting-services-data-source.md)   
 [Подключения к данным, источники данных и строки подключения в службах Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Источники данных, поддерживаемые службами Reporting Services (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Управление содержимым сервера отчетов (службы Reporting Services в собственном режиме)](../report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
