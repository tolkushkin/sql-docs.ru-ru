---
title: Поиск, просмотр отчетов и управление ими (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.date: 05/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 5599300d-6bcd-4704-aba5-fa98e01c78a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7a93f71f886484d38996a867bebbc6ef32c33c86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175625"
---
# <a name="finding-viewing-and-managing-reports-report-builder-and-ssrs-"></a>Поиск, просмотр отчетов и управление ими (построитель отчетов и службы SSRS)
  В построителе отчетов можно просматривать папки на сервере отчетов или на сайте SharePoint для поиска отчетов, общих источников данных, моделей и других связанных элементов отчета, а также просматривать конкретный компьютер для поиска локальных отчетов. Чтобы было проще находить отчеты, построитель отчетов поддерживает список недавно использованных серверов и сайтов и предоставляет прямой доступ к папкам «Рабочий стол», «Мои документы» и «Мой компьютер» в файловой системе компьютера.  
  
 В конструкторе отчетов можно просматривать содержимое компьютера для поиска локальных докладов. Развернув отчеты на сервере отчетов или сайте SharePoint, вы можете искать отчеты на сервере отчетов (с помощью веб-портала) или сайте SharePoint. После развертывания отчеты и связанные элементы остаются доступными локально.  
  
> [!NOTE]  
> Можно использовать построитель отчетов в локальном режиме или подключиться к серверу отчетов. При отсутствии активного соединения с сервером отчетов действуют определенные ограничения.  
  
 Чтобы найти отчет на сервере отчетов или сайте SharePoint с помощью построителя отчетов, вам нужно указать URL-адрес этих ресурсов. При установке построителя отчетов впервые можно указать используемый URL-адрес. Это сервер или сайт, с которыми построитель отчетов подключается по умолчанию при сохранении или открытии отчетов.  
  
 Отчеты можно предварительно просматривать в построителе отчетов или конструкторе отчетов при их создании или обновлении. После публикации отчетов вы также можете просматривать и администрировать их на сервере отчетов (с помощью веб-портала) или на сайте SharePoint, интегрированном со службами Reporting Services, с помощью встроенных инструментов и функций SharePoint. Дополнительные сведения см. в разделах [Предварительный просмотр отчетов в построителе отчетов](../../reporting-services/report-builder/previewing-reports-in-report-builder.md) и [Предварительный просмотр отчетов](../../reporting-services/reports/previewing-reports.md).  
  
 При предварительном просмотре отчетов в построителе отчетов или конструкторе отчетов, а также при просмотре готовых отчетов на веб-портале или сайте SharePoint данные обновляются. При этом в отчетах отображается текущая информация из используемого источника данных. Если требуется просмотреть отчет без обновления его данных, то можно воспользоваться журналом отчета и кэшированными данными с опубликованными отчетами. Эти функции нельзя использовать при предварительном просмотре отчетов в построителе или конструкторе отчетов.  
  
> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="FindingAndViewingReportsRB30"></a> Поиск и просмотр отчетов в построителе отчетов  
 Чтобы найти отчет, который требуется для работы, или выбрать общий источник данных, изображение или вложенный отчет для использования в отчете, просмотрите конкретный компьютер, папки на сервере отчетов или сайт SharePoint, объединенный со службами Reporting Services.  
  
 Чтобы найти отчеты на сервере отчетов, необходимо задать URL-адрес для сервера отчетов и иметь соответствующие разрешения на папки, которые позволяют считывать и сохранять элементы отчета. Обратитесь к системному администратору сервера отчетов для получения нужного URL-адреса и необходимых разрешений.  
  
 После поиска и открытия отчета в построителе отчетов его можно просматривать и вносить в него изменения. При просмотре отчета можно видеть текущие данные. Дополнительные сведения см. в разделе [Previewing Reports in Report Builder](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
 Построитель отчетов может помочь в решении следующих задач.  
  
-   **Поиск отчетов** . При переходе к отчету можно использовать диалоговое окно **Открытие файла** , схожее по стилю с аналогичным окном в Microsoft Office и настроенное для построителя отчетов. Можно просматривать папки на сервере отчетов или в файловой системе, включая папки «Мои отчеты», «Сайты и серверы», «Рабочий стол», «Мои документы», «Мой компьютер». В папке «Сайты и серверы» хранится список недавно использованных серверов.  
  
-   **Поиск общих источников данных** . При поиске общего источника данных можно использовать список недавно использованных или перейти в другую папку на том же сервере отчетов, что и отчет.  
  
-   **Просмотр отчетов** . При создании или обновлении отчетов можно просматривать отчет в построителе отчетов. Если построитель отчетов подключен к серверу отчетов, то сервер отчетов загружает и обрабатывает отчет; в противном случае отчеты обрабатываются локально. Средство просмотра отчетов в построителе отчетов отображает отчет, готовый для просмотра.  
  
 
##  <a name="ViewingAndManagingReportServer"></a> Просмотр отчетов и управление отчетами на сервере отчетов  
 Веб-портал используется для просмотра и администрирования отчетов на сервере отчетов. С его помощью можно просматривать папки на сервере для поиска отчетов, запускать отчеты для отображения в браузере и выполнять административные задачи.  
  
 С помощью веб-портала можно выполнять следующие административные задачи:  
  
-   Просмотр и обновление свойств отчетов, общих источников данных и других элементов отчетов.  
  
-   Передача отчетов и создание новых общих источников данных для отчетов.  
  
-   Создание расписаний для запуска отчетов согласно указанным значениям времени и интервалам.  
  
-   Создание, изменение или удаление подписок на отчеты.  
  
-   Создание журнала отчетов и определение количества моментальных снимков отчета, предназначенных для хранения в журнале отчетов.  
  
-   Создание новых папок на сервере для организации хранения отчетов должным образом.  
  
 Часть этих задач, необходимых пользователю, может быть выполнена администратором сервера отчетов. Дополнительные сведения о задачах, выполняемых на сервере отчетов, см. в разделе [Сервер отчетов служб Reporting Services (собственный режим)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
Веб-портал, как правило, содержит папки, отчеты и источники данных, а также папку "Мои отчеты". Папка «Мои отчеты» — это личное рабочая область, которую можно использовать для хранения и использования собственных отчетов. Другие папки сервера отчетов являются общедоступными, и пользователи обычно должны иметь дополнительные разрешения, чтобы добавлять или изменять содержимое. В папке "Мои отчеты" можно создавать другие папки, чтобы упорядочить отчеты.  
  
 На веб-портале отчеты отображаются в средстве просмотра HTML-страниц служб Reporting Services. Средство просмотра HTML-страниц предоставляет инфраструктуру для просмотра отчетов в формате HTML и включает в себя панель инструментов для отчетов, раздел параметров, раздел учетных данных и схему документа. Панель инструментов отчета обеспечивает навигацию по страницам, масштабирование, обновление, поиск, экспорт, печать и работу с каналами данных. Панель инструментов отчета также появляется наверху окна браузера, если доступ к отчету осуществляется через URL-адрес. Возможности печати являются необязательными и должны быть включены администратором. Когда она доступна, на панели инструментов отчета появляется значок принтера. На следующем рисунке показана панель инструментов для отчетов на веб-портале.  
  
 ![Панель инструментов для отчетов на веб-портале](../../reporting-services/report-builder/media/finding-viewing-and-managing-reports-report-builder-and-ssrs/report-toolbar-in-the-web-portal.png)  
  
После запуска отчета его можно экспортировать в другой формат, например [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel или PDF. Можно также экспортировать отчет с помощью модуля обработки данных, например модуля подготовки отчетов к просмотру в формате CSV, а затем использовать файл данных CSV в качестве входного для другого приложения. См. подробнее об [экспорте отчетов (построитель отчетов и службы SSRS)](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).
  
 Самый простой способ выбрать и запустить отчет — открыть веб-портал отчетов и найти нужный отчет. См. подробнее об [открытии и закрытии отчетов](../../reporting-services/reports/open-and-close-a-report-report-manager.md).  
  
 После запуска отчета можно обновить его для просмотра новых данных.  
  
### <a name="refreshing-reports"></a>Обновление отчетов  
 Данные отчета часто изменяются, и может понадобиться обновить отчет для просмотра самых свежих данных. Отчет можно обновить тремя разными способами.  
  
|Параметр|Результат|  
|------------|------------|  
|Кнопка**Обновить** в окне браузера|Выводит отчет, который хранится в кэше сеанса. Кэш сеанса создается, когда пользователь открывает отчет. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] используют сеансы браузера для поддержания согласованных условий просмотра, пока отчет открыт.|  
|![Кнопка обновления в браузере на панели инструментов для отчетов](../../reporting-services/report-builder/media/finding-viewing-and-managing-reports-report-builder-and-ssrs/browser-refresh-button-on-report-toolbar.png)|При нажатии кнопки **Обновить** на панели инструментов отчета сервер отчетов повторно выполняет запрос и обновляет данные отчета, если он выполняется по запросу. Если отчет кэшируется или является моментальным снимком, при нажатии кнопки **Обновить** выводится отчет, хранящийся в базе данных сервера отчетов.|  
|Сочетание клавиш CTRL + F5|Обеспечивает тот же результат, что и нажатие кнопки **Обновить** на панели инструментов отчета.|  
  
  
##  <a name="ViewingAndManagingSharePointSite"></a> Просмотр и управление элементами сервера отчетов с сайта SharePoint  
 Если системный администратор настроит сервер отчетов для работы в режиме интеграции с SharePoint, то на сайте SharePoint можно будет просматривать отчеты и другие элементы сервера отчетов, а также управлять этими элементами.  
  
 На сайте SharePoint есть страницы для задания свойств источников данных, работы с журналом отчета, задания параметров обработки отчетов, назначения расписаний, оформления подписок, задания параметров отчетов и создания общих расписаний. Элементами сервера отчетов можно управлять на сайте SharePoint, используя те же методы, что и при работе с другими средствами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Чтобы получить доступ к страницам приложения, выберите относящиеся к элементу действия из раскрывающегося меню в отчете или в другом элементе сервера отчетов, ранее добавленном в библиотеку SharePoint. В зависимости от типа элемента и наличия необходимых разрешений может быть доступно создание отчетов в построителе отчетов, формирование моделей и задание параметров безопасности для элементов моделей.  
  
 Подробнее о службах Reporting Services и технологии SharePoint см. в руководстве по [настройке и администрированию сервера отчетов (службы Reporting Services в режиме интеграции с SharePoint)](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).
  
### <a name="finding-report-server-items-on-a-sharepoint-site"></a>Поиск элементов сервера отчетов на сайте SharePoint  
 Перед заданием свойств элемента необходимо определить его расположение. Элементы сервера отчетов всегда хранятся в библиотеках или в папке в пределах библиотеки.  
  
 При обращении к сайту SharePoint отобразится страница «Обзор» и вкладка «Средства библиотеки». На странице «Обзор» отображается список таблиц и содержимое выбранной библиотеки. Вы можете просмотреть отчет, папки и прочие элементы в библиотеке, а также использовать поиск элементов на сайте.  
  
 Чтобы отличить элементы сервера отчетов от других элементов на сайте SharePoint, можно использовать значки для визуального определения элементов или навести указатель мыши на тип элемента и прочитать расширение файла. На следующем изображении показаны папки и определение отчета в библиотеке **Отчеты**:  
  
 ![Библиотека Sharepoint с элементами сервера отчетов](../../reporting-services/report-builder/media/rs-sharepointlibrary.gif "Библиотека Sharepoint с элементами сервера отчетов")  
  
### <a name="viewing-reports"></a>Просмотр отчетов  
 Определения отчетов (RDL-файлы), которые передаются в библиотеку SharePoint, просматриваются с помощью веб-части «Обозреватель отчетов», которая устанавливается вместе с надстройкой Reporting Services. Во время установки надстройки автоматически определяется сопоставление для RDL-файлов. Отчет автоматически откроется в веб-компоненте средства просмотра отчетов. После открытия отчета можно использовать входящую в состав веб-части панель инструментов для перемещения по страницам отчета, поиска данных в отчете, изменения масштаба и печати отчета. На панели инструментов имеется параметр «Экспорт потока данных» для экспорта отчетов в виде потока данных Atom и меню **Действия** с параметрами, обеспечивающими возможность печати, подписки и экспорта отчета в другие форматы, такие как PDF, Word и Excel. В меню **Действия** также можно открыть отчет в построителе отчетов. На следующем рисунке показан отчет и параметры функции «Экспорт» в меню **Действия** .  
  
 ![rs_SharePointRunReport](../../reporting-services/report-builder/media/rs-sharepointrunreport.gif "rs_SharePointRunReport")  
  
### <a name="managing-items-through-actions"></a>Управление элементами с помощью действий  
 Задачи управления для каждого элемента поддерживаются с помощью действий, выбираемых из раскрывающегося меню. Для всех элементов, хранящихся в библиотеке SharePoint, существует общий набор стандартных действий, определяемый разрешениями пользователя. Примерами общих действий являются**Просмотреть свойства** и **Изменить свойства** . Нестандартные действия реализуют функции управления, индивидуальные для каждого типа элементов. На рисунке показаны действия для определения отчета. Примерами нестандартных действий для определения отчета служат **Управление подписками** и **Управление параметрами обработки**.  
  
 ![Команды меню для элементов сервера отчетов](../../reporting-services/report-builder/media/rs-ecbforrsitems.gif "Команды меню для элементов сервера отчетов")  
  
  
##  <a name="DeskTop"></a> Просмотр отчетов в приложении для настольных компьютеров  
 Можно отказаться от просмотра в веб-браузере, а в качестве средства просмотра отчетов использовать классическое приложение, например [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. Для этого определите подписку, определяющую формат приложения рабочего стола и общую папку назначения. Сервер отчетов формирует отчет в виде файла приложения, добавляет к нему расширение и сохраняет этот отчет в виде файла на жестком диске. Затем для просмотра отчетов вместо веб-браузера можно использовать [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel (или другое приложение).  
  
  
##  <a name="AboutUserSessions"></a> О пользовательских сеансах  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] используют сеансы браузера для поддержания согласованности при просмотре отчетов. Сеансы связываются с подключениями браузера, а не с прошедшими проверку подлинности пользователями. Новый сеанс создается каждый раз, когда пользователь открывает отчет в новом окне браузера. Когда сеанс браузера установлен, продолжается работа с версией отчета, которая была открыта в начале сеанса, даже если отчет на сервере отчетов был позднее изменен. Например, если открыть отчет в 11:00, после чего автор отчета повторно опубликует тот же отчет в 11:01, на все время существования открытого сеанса в нем будет доступна исходная версия отчета.  
  
 При обновлении отчета внутри того же сеанса с помощью кнопки браузера **Обновить** будет отображаться исходная версия отчета. При обновлении отчета по запросу с помощью кнопки **Обновить** на панели инструментов отчетов отчет будет перезапущен, и отобразятся новые данные, если они были добавлены или изменены.  
  
 Сведения о сеансах хранятся во временной базе данных сервера отчетов. Сервер отчетов не использует управление сеансами [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . При перезапуске сервера или выполнении операции восстановления базы данных состояние сеанса не восстанавливается. Дополнительные сведения об управлении сеансами см. в разделе [Определение состояния выполнения](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md).  
  
 
##  <a name="InThisSection"></a> в этом разделе  
 Следующие статьи содержат дополнительные сведения о просмотре и администрировании отчетов.  
  
 [Поиск, просмотр отчетов и управление ими](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)
  
 [Поиск и просмотр отчетов с помощью браузера (построитель отчетов и службы SSRS)](../../reporting-services/report-builder/finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs.md)  
 Описывает использование URL-адресов для поиска и просмотра отчета.  
  
 [Предварительный просмотр отчетов в построителе отчетов](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)  
 Описывает, как осуществлять предварительный просмотр отчетов при их создании или обновлении.  
  
## <a name="see-also"></a>См. также раздел  
 [Сохранение отчетов (построитель отчетов)](../../reporting-services/report-builder/saving-reports-report-builder.md)   
 [Построитель отчетов в SQL Server](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 