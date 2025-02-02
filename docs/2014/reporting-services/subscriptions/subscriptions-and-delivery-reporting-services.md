---
title: Подписки и доставка (Reporting Services) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- reports [Reporting Services], distributing
- distributing reports [Reporting Services]
- published reports [Reporting Services], distributing
- sending reports
- sharing reports
- delivering reports [Reporting Services]
- distributing reports [Reporting Services], subscriptions
- subscriptions [Reporting Services], about subscriptions
- subscriptions [Reporting Services]
ms.assetid: be7ec052-28e2-4558-bc09-8479e5082926
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f598946ec6231d1ca5edacf1810431beb4638f88
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66100671"
---
# <a name="subscriptions-and-delivery-reporting-services"></a>Subscriptions and Delivery (Reporting Services)
  Подписка [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] представляет собой конфигурацию, создающую отчет в определенное время или в ответ на конкретное событие. Отчет выводится в указанном формате файла. Например, каждую среду отчет MonthlySales.rdl можно сохранять в виде документа Microsoft Word на общем файловом ресурсе. С помощью подписок можно планировать и автоматизировать создание отчетов, в которых будет использоваться заданный набор значений параметров.  
  
 Чтобы применить различные варианты подписки, для одного отчета можно создать несколько подписок. Например, можно указать различные значения параметров, чтобы сформировать три версии отчета, а именно: отчет о продажах в западном регионе, отчет о продажах в восточном регионе и отчет об общих продажах.  
  
 ![Пример потока подписки SSRS](../media/ssrs-subscription-example-flow.png "Пример потока подписки SSRS")  
  
 Подписки доступны не во всех выпусках [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Перечень функций, поддерживаемых в разных выпусках [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], см. в разделе [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!NOTE]
>  Начиная с версии [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], вы можете передавать владение подписки программным путем. Пользовательского интерфейса, который можно использовать для передачи владения подписками, не существует. Дополнительные сведения см. в разделе <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>и [использование PowerShell для изменения и список Reporting Services Subscription Owners and Run a Subscription](manage-subscription-owners-and-run-subscription-powershell.md).  
  
 **В этом разделе:**  
  
-   [Сценарии подписки и доставки](#bkmk_subscription_scenarios)  
  
-   [Стандартные и управляемые данными подписки](#bkmk_standard_and_datadriven)  
  
-   [Требования к подписке](#bkmk_subscription_requirements)  
  
-   [Модули доставки](#bkmk_delivery_extensions)  
  
-   [Части подписки](#bkmk_parts_of_subscription)  
  
-   [Обработка подписок](#bkmk_subscription_processing)  
  
-   [Обработка подписок](#bkmk_subscription_processing)  
  
 **Темы в этом разделе**  
  
-   [Доставка электронной почтой в службах Reporting Services](e-mail-delivery-in-reporting-services.md) . Описание принципов работы и настройки доставки отчетов по электронной почте сервером отчетов.  
  
-   [File Share Delivery in Reporting Services](file-share-delivery-in-reporting-services.md) Описание принципов работы и настройки доставки отчетов на общий файловый ресурс сервером отчетов.  
  
-   [SharePoint Library Delivery in Reporting Services](sharepoint-library-delivery-in-reporting-services.md) Описание принципов доставки подписки в библиотеку SharePoint.  
  
-   [Подписки, управляемые данными](data-driven-subscriptions.md) . Сведения об использовании подписок, управляемых данными, для настройки вывода отчета во время выполнения.  
  
-   [Создание и администрирование подписок для серверов отчетов в собственном режиме](../create-manage-subscriptions-native-mode-report-servers.md)  
  
-   [Создание подписок для серверов отчетов, работающих в режиме интеграции с SharePoint, и управление этими подписками](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
-   [Отслеживание подписок служб Reporting Services](monitor-reporting-services-subscriptions.md)  
  
-   [Использование PowerShell для смены и перечисления владельцев подписок служб Reporting Services и запуска подписки](manage-subscription-owners-and-run-subscription-powershell.md)  
  
##  <a name="bkmk_subscription_scenarios"></a> Сценарии подписки и доставки  
 Для каждой подписки настраиваются варианты доставки, которые зависят от выбранного модуля доставки. Модуль доставки — это модуль, поддерживающий определенный способ распространения. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] предлагает несколько модулей доставки. Кроме того, могут быть доступны модули доставки сторонних поставщиков.  
  
 Разработчик может создавать собственные модули доставки для поддержки дополнительных сценариев. Дополнительные сведения см. в статье [Implementing a Delivery Extension](../extensions/delivery-extension/implementing-a-delivery-extension.md).  
  
 В следующей таблице описаны распространенные сценарии подписки [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .  
  
|Сценарий|Описание|  
|--------------|-----------------|  
|Отчеты по электронной почте|Отправка отчетов по электронной почте отдельным пользователям и группам. Создайте подписку и укажите псевдоним группы или псевдоним электронной почты для получения отчета, который нужно распространить. Службы [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] могут определять данные о подписке во время выполнения. Чтобы отправить один отчет группе, список членов которой изменяется, можно составить запрос, получающий список подписки во время выполнения.|  
|Просмотр отчетов в автономном режиме|Отчеты, которые нужно поместить в архив, можно отправлять непосредственно в общую папку, для которой по ночам создаются резервные копии. Крупные отчеты, на загрузку которых в браузере уходит слишком много времени, можно отправить в общую папку в формате, позволяющем просмотр в приложении для настольных систем. Пользователи могут выбрать один из следующих форматов для вывода подписки:<br /><br /> XML-файл с данными отчета<br /><br /> CSV (с разделителями-запятыми)<br /><br /> PDF<br /><br /> MHTML (веб-архив)<br /><br /> Microsoft Excel<br /><br /> TIFF-файл<br /><br /> Microsoft Word|  
|Предварительная загрузка кэша|При наличии нескольких экземпляров параметризованного отчета или большого количества пользователей, просматривающих отчеты, можно предварительно загрузить отчет, что позволит сократить время обработки, необходимое для отображения отчета.|  
|Отчеты, управляемые данными|Управляемые данными подписки позволяют настраивать выходные данные отчета, параметры доставки и значения параметров отчета во время выполнения. Подписка с помощью запроса получает входные значения из источника данных во время выполнения. Управляемые данными подписки позволяют выполнять операцию слияния почты, которая отправляет отчет списку подписчиков, определяемому во время обработки подписки.|  
  
##  <a name="bkmk_standard_and_datadriven"></a> Стандартные и управляемые данными подписки  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] поддерживают два типа подписок: **стандартные** и **управляемые данными**. Стандартные подписки создаются и управляются отдельными пользователями. Стандартная подписка состоит из статических значений, которые не могут изменяться в течение обработки подписки. Для каждой стандартной подписки есть только один набор параметров представления отчета, параметров доставки и параметров отчета.  
  
 Управляемые данными подписки получают сведения о подписке динамически, направляя запросы внешнему источнику данных, который предоставляет значения, используемые для указания получателя, параметров отчета или формата приложения. Можно использовать управляемые данными подписки, если существует очень большой список получателей или если желательно менять вывод отчета для каждого получателя. Чтобы использовать управляемые данными подписки, необходимо иметь опыт в построении запросов и понимать, как применяются параметры. Создают эти подписки и управляют ими обычно администраторы сервера отчетов. Дополнительные сведения см. в следующих разделах:  
  
-   [Подписки, управляемые данными](data-driven-subscriptions.md)  
  
-   [Создание управляемой данными подписки (учебник по службам SSRS)](../create-a-data-driven-subscription-ssrs-tutorial.md)  
  
##  <a name="bkmk_subscription_requirements"></a> Требования к подписке  
 Прежде чем может быть создана подписка на отчет, должны быть соблюдены следующие требования.  
  
|Требование|Описание|  
|-----------------|-----------------|  
|Разрешения|Пользователь должен иметь доступ к отчету. Прежде чем можно будет подписаться на отчет, пользователь должен иметь разрешения на его просмотр.<br /><br /> Назначение ролей должно включать задачу «Управление индивидуальными подписками».|  
|Сохраненные учетные данные|Чтобы создать подписку, отчет должен использовать или не использовать сохраненные учетные записи для извлечения данных во время выполнения. Нельзя подписаться на отчет, настроенный для использования олицетворенных или делегированных учетных данных текущего пользователя для подключения к внешнему источнику данных. Хранимые учетные данные могут быть или учетной записью Windows, или учетной записью базы данных. Дополнительные сведения см. в разделе [Задание учетных данных и сведений о соединении для источников данных отчета](../report-data/specify-credential-and-connection-information-for-report-data-sources.md).<br /><br /> Для просмотра отчета и создания отдельных подписок необходимо иметь соответствующее разрешение. На сервере отчетов должны быть включены**Запланированные события и доставка отчетов** . Дополнительные сведения см. в разделе [Создание подписок для работающих в основном режиме серверов отчетов и управление этими подписками](../create-manage-subscriptions-native-mode-report-servers.md).|  
|Зависящие от пользователя значения в отчете|Только для стандартных подписок можно создавать подписки на отчеты, которые включают сведения пользовательской учетной записи в фильтре или как текст, появляющийся в отчете. В таком отчете имя учетной записи пользователя указывается через выражение `User!UserID`, которое возвращает текущего пользователя. При создании подписки текущим считается пользователь, создающий эту подписку.|  
|Отсутствие безопасности элементов модели|Нельзя подписаться на отчет построителя отчетов, который в качестве источника данных использует модель, содержащую настройки безопасности элементов модели. Только отчеты, использующие безопасность элементов модели отчета, входят в это ограничение.|  
|Значения параметра|Если отчет использует параметры, их значения должны быть заданы в самом отчете или в определяемой подписке. Если в отчете были определены значения по умолчанию, то в параметрах можно указать, чтобы использовались они.|  
  
##  <a name="bkmk_delivery_extensions"></a> Модули доставки  
 Подписки обрабатываются на сервере отчетов и распространяются с помощью модулей доставки, развернутых на этом сервере. По умолчанию допускается создание подписок, которые направляют отчеты в общую папку или на адрес электронной почты. После настройки сервера отчетов на работу в режиме интеграции с SharePoint можно также отправить отчет в библиотеку SharePoint.  
  
 При создании подписки можно задать способ доставки отчета, выбрав один из доступных модулей доставки. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] имеются следующие модули доставки отчета.  
  
|Модуль доставки|Описание|  
|------------------------|-----------------|  
|Общая папка Windows|Доставляет отчет в виде статического файла приложения в общую папку, доступную в сети.|  
|электронная почта|Доставляет уведомление или отчет в виде электронного вложения или URL-ссылки.|  
|Библиотека SharePoint|Доставляет отчет в виде статического файла приложения в библиотеку SharePoint, доступную с сайта SharePoint. Этот сайт должен быть интегрирован с сервером отчетов, который выполняется в режиме интеграции с SharePoint.|  
|NULL|Отсутствующий поставщик доставки — узко специализированный модуль доставки, используемый для предварительной загрузки в кэш готовых для просмотра параметризованных отчетов. Этот метод не доступен пользователям при отдельных подписках. Отсутствующий поставщик доставки используется администраторами в управляемых данными подписках, чтобы улучшить работу сервера отчетов путем предварительной загрузки кэша.|  
  
> [!NOTE]  
>  Доставка отчетов представляет собой расширяемую часть архитектуры служб [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Сторонние поставщики могут создавать пользовательские модули доставки для направления отчетов в разные места или на разные устройства. Дополнительные сведения о пользовательских модулях доставки см. в разделе [Implementing a Delivery Extension](../extensions/delivery-extension/implementing-a-delivery-extension.md).  
  
##  <a name="bkmk_parts_of_subscription"></a> Части подписки  
 Определение подписки состоит из следующих частей.  
  
-   Указатель на отчет, который может запускаться автоматически (то есть отчет, использующий сохраненные учетные данные или не использующий их).  
  
-   Метод доставки (например, электронная почта) и настройки для режима доставки (такие как почтовый адрес).  
  
-   Модуль подготовки отчетов, чтобы представить отчет в указанном формате.  
  
-   Условия для обработки подписки, которая представлена как событие.  
  
     Обычно условия для выполнения отчета основаны на времени. Например, можно создавать определенный отчет каждый вторник в 15:00. Однако, если отчет запускается как моментальный снимок, можно указать, что подписка запускается каждый раз, когда обновляется моментальный снимок.  
  
-   Параметры, используемые при работе отчета.  
  
     Параметры являются необязательными и указаны только для отчетов, которые принимают значения параметра. Поскольку подписка является обычно пользовательской, указанные значения параметра изменяются от подписки к подписке. Например менеджеры продаж из различных отделов будут использовать параметры, которые возвращают данные именно в их отдел. Все параметры должны иметь явно определенное значение или иметь допустимое значение по умолчанию.  
  
 Сведения о подписке сохраняются вместе с индивидуальными отчетами в базе данных сервера отчетов. Нельзя управлять подписками отдельно от отчета, к которому они привязаны. Учтите, что подписки не могут быть расширены для включения описаний, другого заказного текста или других элементов. Подписки могут содержать только элементы, перечисленные ранее.  
  
##  <a name="bkmk_subscription_processing"></a> Обработка подписок  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] реализован обработчик планирования и доставки, который обеспечивает планирование отчетов и их доставку пользователям. Сервер отчетов непрерывно реагирует на контролируемые им события. Когда происходит событие, соответствующее условиям, определенным для подписки, сервер отчетов считывает подписку, чтобы определить, как следует обработать и доставить отчет. Сервер отчетов запрашивает модуль доставки, указанный в подписке. После запуска модуля доставки сервер отчетов извлекает из подписки сведения о доставке и передает ее для обработки модулю доставки.  
  
 Модуль доставки готовит отчет к просмотру в формате, определенном в подписке, после чего доставляет отчет или уведомление указанному адресату. Если доставка отчета невозможна, в файл журнала сервера отчетов добавляется соответствующая запись. На сервере отчетов можно настроить повторение попыток доставки в случае, если первая попытка заканчивается неудачей.  
  
### <a name="processing-a-standard-subscription"></a>Обработка стандартной подписки  
 Стандартные подписки создают один экземпляр отчета. Отчет доставляется в одну общую папку или рассылается по адресам электронной почты, указанным в подписке. Макет отчета и данные не меняются. Если в отчете используются параметры, стандартная подписка обрабатывается с одним значением для каждого параметра в отчете.  
  
### <a name="processing-a-data-driven-subscription"></a>Обработка управляемой данными подписки  
 Управляемые данными подписки могут формировать несколько экземпляров отчетов, которые доставляются по разным адресатам. Макет отчета не меняется, но данные отчетов могут быть разными, если значения параметров передаются из результирующего набора подписчиков. Параметры доставки, влияющие на подготовку отчета к просмотру и на способ доставки (в виде вложения или ссылки в электронном сообщении), также могут быть разными для разных подписчиков, если они передаются из набора строк.  
  
 Управляемые данными подписки могут создавать большое количество доставок. Сервер отчетов создает доставку для каждой строки из набора строк, возвращенного запросом подписки.  
  
### <a name="report-delivery-characteristics"></a>Характеристики доставки отчетов  
 Отчеты, которые доставляются с использованием стандартных подписок, обычно готовятся к просмотру как статические отчеты. Эти отчеты либо основаны на снимке состояния выполнения отчета, либо создаются в виде статических отчетов специально для выполнения доставки. Если выбран параметр **Включить ссылку** в подписке на выполняемый по требованию отчет, то сервер отчетов будет запускать отчет при щелчке гиперссылки.  
  
> [!NOTE]  
>  Отчеты, доставляемые с помощью URL-адреса, остаются подключенными к серверу отчетов, и их можно обновлять или удалять между просмотрами. Параметры доставки для подписки определяют, доставляется ли отчет в виде URL-адреса, внедренного в тело электронного сообщения, или присылается в виде вложения.  
  
 Отчеты, доставляемые с помощью управляемой данными подписки, могут быть сформированы повторно во время обработки подписки. Сервер отчетов не блокирует определенный экземпляр отчета или его набор данных для обработки управляемой данными подписки. Если в подписке разные значения параметров используются для разных подписчиков, то сервер отчетов повторно формирует отчет для достижения необходимых результатов. Если лежащие в основе отчета данные обновляются после создания и доставки первой копии отчета, то пользователи, которые получат более поздние копии, могут увидеть данные, основанные на другом результирующем наборе. Чтобы один и тот же экземпляр отчета был доставлен всем подписчикам, можно использовать отчет, запускающийся как моментальный снимок. Однако если во время обработки подписки происходит запланированное обновление моментального снимка, то пользователи все же могут получить в отчетах разные данные.  
  
### <a name="triggering-subscription-processing"></a>Запуск обработки подписки  
 Для запуска на сервере отчетов обработки подписки используются два типа событий: события, управляемые временем, которые запланированы в расписании, и события обновления моментального снимка.  
  
 Управляемый временем триггер использует расписание отчета или общее расписание, чтобы запустить подписку. Для кэшированных отчетов и отчетов по требованию расписания являются единственным вариантом триггера.  
  
 Событие обновления моментального снимка запускает подписку при запланированном обновлении моментального снимка отчета. Можно определить подписку, которая будет запускаться при каждом обновлении отчета новыми данными в зависимости от свойств выполнения отчета.  
  
## <a name="see-also"></a>См. также  
 [Создание управляемой данными подписки (учебник по службам SSRS)](../create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Расписания](schedules.md)   
 [Сервер отчетов служб Reporting Services (основной режим)](../report-server/reporting-services-report-server-native-mode.md)   
 [Создание подписок для работающих в основном режиме серверов отчетов и управление этими подписками](../create-manage-subscriptions-native-mode-report-servers.md)   
 [Отслеживание подписок служб Reporting Services](monitor-reporting-services-subscriptions.md)  
  
  
