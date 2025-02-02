---
title: Отслеживание подписок служб Reporting Services | Документы Майкрософт
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], inactive
- subscriptions [Reporting Services], status
- monitoring [Reporting Services], subscriptions
- status information [Reporting Services]
- inactive subscriptions [Reporting Services]
ms.assetid: 054c4a87-60bf-4556-9a8c-8b2d77a534e6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cb4d7f64bf72aaf8844097277c78d6563b426cc1
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65578213"
---
# <a name="monitor-reporting-services-subscriptions"></a>Отслеживание подписок служб Reporting Services
  Вы можете отслеживать подписки [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в пользовательском интерфейсе, Windows PowerShell или в файлах журнала. Параметры, которые можно отслеживать, зависят от того, какой режим сервера отчетов используется.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Собственный режим &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Режим интеграции с SharePoint.|  
  
 **В этом разделе:**  
  
-   [Пользовательский интерфейс в собственном режиме](#bkmk_native_mode)  
  
-   [режим SharePoint](#bkmk_sharepoint_mode)  
  
-   [Использование PowerShell для отслеживания подписок](#bkmk_use_powershell)  
  
-   [Управление неактивными подписками](#bkmk_manage_inactive)  
  
##  <a name="bkmk_native_mode"></a> Пользовательский интерфейс в собственном режиме  
 Отдельные пользователи [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] могут наблюдать за состоянием подписки с помощью страницы **Мои подписки** или вкладки **Подписки** диспетчера отчетов. Страницы подписки содержат столбцы, в которых отображается состояние подписки и время ее последнего выполнения. Сообщения о состоянии обновляются, когда обработка подписки вносится в соответствующее расписание. Если триггер не срабатывает (например, если снимок состояния выполнения отчета не обновляется или расписание никогда не запускается), то сообщение о состоянии обновляться также не будет.  
  
 В следующей таблице показаны возможные значения для столбца **Состояние** .  
  
|Состояние|Описание|  
|------------|-----------------|  
|Новая подписка|Появляется при создании подписки.|  
|Неактивный|Появляется, если подписку невозможно обработать. Дополнительные сведения см. ниже в разделе «Управление неактивными подписками».|  
|Готово: всего обработано \<*число*> из \<*число*>; \<*число*> ошибок.|Состояние подписки, управляемой данными. Это сообщение обработчика планирования и доставки.|  
|\<*число*> обработано|Число уведомлений обработчика планирования и доставки об успешном завершении доставки или о прекращении дальнейших попыток доставки. При завершении управляемой данными доставки число обработанных уведомлений должно равняться общему количеству созданных уведомлений о доставке.|  
|\<*число*> всего|Общее количество уведомлений, созданных для последней доставки подписки.|  
|\<*число*> ошибка|Число уведомлений обработчика планирования и доставки о невозможности доставки или прекращении повторных попыток.|  
|Ошибка при отправке электронной почты: транспортной операции не удалось соединиться с сервером.|Показывает, что сервер отчетов не соединился с почтовым сервером. Это сообщение модуля доставки электронной почты.|  
|Файл \<*имя_файла* записан в папку \<путь>.|Показывает, что доставка в расположение общей папки завершилась успешно. Это сообщение модуля доставки в общую папку.|  
|Неизвестная ошибка при записи файла.|Показывает, что доставка в расположение общей папки завершилась неуспешно. Это сообщение модуля доставки в общую папку.|  
|Сбой при подключении к папке назначения \<путь>. Убедитесь в существовании папки назначения или общей папки.|Показывает, что невозможно найти указанную папку. Это сообщение модуля доставки в общую папку.|  
|Невозможно записать файл \<имя_файла> в \<путь>. Попытка повтора.|Показывает, что невозможно обновить файл новой версией. Это сообщение модуля доставки в общую папку.|  
|Ошибка записи файла \<имя_файла>: \<сообщение>|Показывает, что доставка в расположение общей папки завершилась неуспешно. Это сообщение модуля доставки в общую папку.|  
|\<пользовательские сообщения о состоянии>|Сообщения о состоянии (об успешном и неуспешном завершении доставки), формируемые модулями доставки. При использовании сторонних или пользовательских модулей доставки могут выводиться дополнительные сообщения о состоянии.|  
  
 Кроме того, администраторы сервера отчетов могут отслеживать обработку стандартных подписок, выполняемую в настоящий момент. Отслеживать обработку подписок, управляемых данными, невозможно. Дополнительные сведения см. в разделе [Управление запущенным процессом](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
 Если подписку доставить не удается (например, если почтовый сервер недоступен), то модуль доставки повторяет доставку. Число повторных попыток задается соответствующим параметром конфигурации. По умолчанию количество повторных попыток равно нулю. Иногда отчет обрабатывается без данных (например, если источник данных работает в режиме «вне сети»). В таком случае сведения об этом приводятся в теле сообщения.  
  
### <a name="native-mode-log-files"></a>Файлы журналов в собственном режиме  
 Если во время доставки возникает ошибка, то в журнале трассировки сервера отчетов делается соответствующая запись.  
  
 Чтобы определить состояние доставки подписки, администратор сервера отчетов может просмотреть файлы **reportserverservice_\*.log**. При доставке по электронной почте журналы сервера отчетов содержат записи обработки, а также сведения о доставке специальным учетным записям электронной почты. Ниже указано расположение файлов журналов по умолчанию.  
  
 `C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\LogFiles`  
  
 Ниже представлен пример имени файла журнала.  
  
 `ReportServerService__05_21_2014_00_05_07.log`  
  
 Ниже приведен пример сообщения об ошибке трассировки журнала файла, связанного с подписками.  
  
-   library!WindowsService_7!b60!05/20/2014-22:34:36:: i СВЕДЕНИЯ: Инициализация EnableExecutionLogging как True, как указано в Server system properties.emailextension!WindowsService_7!b60!05/20/2014-22:34:41:: e ОШИБКА: **Ошибка при отправке сообщения**. Исключение: System.Net.Mail.SmtpException: SMTP-серверу требуется безопасное соединение, или клиент не прошел проверку подлинности. Ответ сервера: 5.7.1. Клиент не прошел проверку подлинности в System.Net.Mail.MailCommand.CheckResponse(SmtpStatusCode statusCode, String response).  
  
 Файл журнала не содержит сведения об открытии отчета или об успешном фактическом выполнении доставки. Успешная доставка означает, что ошибки обработчика планирования и доставки отсутствуют и сервер отчетов подключился к почтовому серверу. Если при попытке доставки по электронной почте в почтовый ящик пользователя пришло сообщение о невозможности доставки отчета, то эти сведения не будут включены в файл журнала. Дополнительные сведения о файлах журналов см. в разделе [Файлы и источники журналов служб Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
##  <a name="bkmk_sharepoint_mode"></a> режим SharePoint  
 Отслеживание подписки в режиме SharePoint: состояние подписки можно отслеживать на странице **Управление подписками** .  
  
1.  Перейдите к библиотеке документов, которая содержит отчет.  
  
2.  Откройте контекстное меню отчета (**...**).  
  
3.  Выберите опцию развернутого меню (**...**).  
  
4.  Выберите **Управление подписками**.  
  
### <a name="sharepoint-uls-log-files"></a>Файлы журналов SharePoint ULS  
 Данные о подписке записываются в журнал ULS SharePoint. Дополнительные сведения о настройке событий [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] для журнала ULS см. в разделе [Включение событий служб Reporting Services для журнала трассировки SharePoint (ULS)](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md).  Ниже приведен пример записи журнала ULS, относящейся к подпискам [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||||||||  
|-|-|-|-|-|-|-|  
|Дата|Процесс|Область|Категория|Level|Correlation|Сообщение|  
|5/21/2014 14:34:06:15|Пул приложений: a0ba039332294f40bc4a81544afde01d|службы SQL Server Reporting Services|Расширение электронной почты сервера отчетов|Непредвиденное|(пусто)|**Ошибка при отправке сообщения электронной почты.** Исключение: System.Net.Mail.SmtpException: почтовый ящик недоступен. Ответ сервера: 5.7.1. У клиента нет разрешений для отправки, так как данный отправитель в System.Net.Mail.DataStopCommand.CheckResponse(SmtpStatusCode statusCode, String serverResponse) в System.Net.Mail.DataStopCommand.Send(SmtpConnection conn) в System.Net.Mail.SmtpClient.Send(MailMessage message) в Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider.Deliver(Notification notification).|  
  
##  <a name="bkmk_use_powershell"></a> Использование PowerShell для отслеживания подписок  
 Примеры скриптов PowerShell для проверки состояния подписок в собственном режиме или в режиме SharePoint см. в разделе [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
##  <a name="bkmk_manage_inactive"></a> Управление неактивными подписками  
 Если подписка становится неактивной, то ее следует удалить либо активировать повторно путем устранения основных причин, препятствующих ее обработке. Подписки становятся неактивными, если их обработке препятствуют какие-либо условия. К таким условиям относятся следующие.  
  
-   Удаление или отмена установки модуля доставки, указанного в подписке.  
  
-   Переключение параметров учетных данных с хранимых на интегрированные либо на значения, вводимые по запросу.  
  
-   Изменение имени аргумента или типа данных в определении отчета и последующая повторная публикация отчета. Если подписка содержит параметр, который стал недопустимым, то она становится неактивной.  
  
-   Изменение режима выполнения отчета (например, такое изменение отчета по требованию, при котором он выполняется как снимок состояния выполнения отчета). Дополнительные сведения см. в разделе [Установка свойств обработки отчетов](../../reporting-services/report-server/set-report-processing-properties.md).  
  
 Неактивная подписка обозначается соответствующим сообщением в самой подписке. Оно содержит сведения о причине неактивности подписки и действиях, необходимых для ее повторной активации.  
  
 Если какие-либо условия приводят к деактивации подписки, то она отразит этот факт, когда сервер отчетов пытается запустить ее. Если в расписании подписки задана доставка отчета каждую пятницу в 2:00 утра, а применяемый подпиской модуль доставки удален в понедельник в 9:00 утра, то подписка не отразит свое неактивное состояние до 2:00 утра пятницы.  
  
## <a name="see-also"></a>См. также:  
 [old_Создание подписок для работающих в основном режиме серверов отчетов и управление этими подписками](https://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)   
 [Подписки и доставка (службы Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  
