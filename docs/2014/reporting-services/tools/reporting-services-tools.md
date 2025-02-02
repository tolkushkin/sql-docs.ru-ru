---
title: Средства служб Reporting Services | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SSRS, tools
- Reporting Services, tools
- components [Reporting Services]
- components [Reporting Services], about components
- Reporting Services, components
- SSRS, components
- reports [Reporting Services], tools
- SQL Server Reporting Services, components
- SQL Server Reporting Services, tools
- architecture [Reporting Services]
ms.assetid: 23d616e3-eb90-43fb-9b7a-869bd7e22e7b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 21c56f28a6f65b22d8fe334a1046f44f868c4453
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099913"
---
# <a name="reporting-services-tools"></a>Инструментальные средства служб Reporting Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] содержат набор графических средств и средств для работы со скриптами, поддерживающих разработку и использование отчетов с широкими возможностями в управляемой среде. В набор средств входят средства разработки, настройки и администрирования, а также средства просмотра отчетов. В этом разделе содержится краткий обзор средств в службах [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] и способов доступа к ним.  
  
 Это средство быстро найти нужное, см. в разделе [руководства: Инструкции по поиску и запуску Reporting средств служб Services &#40;SSRS&#41;](tutorial-how-to-locate-and-start-reporting-services-tools-ssrs.md).  
  
## <a name="tools-for-report-authoring"></a>Средства разработки отчетов  
 В следующей таблице перечислены доступные средства для создания отчетов в службах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Инструмент|Описание|Способ доступа|  
|----------|-----------------|-------------------|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]|интерактивное средство для просмотра и визуализации данных, предназначенное для создания отчетов на основе табличных моделей служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и взаимодействия с ними.<br /><br /> Примечание. Требуется [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в режиме интеграции с SharePoint.|Браузер с приложением Silverlight.|  
|конструктор отчетов|Это средство используется для конструирования отчетов и развертывания их на сервере отчетов в собственном режиме или в режиме интеграции с SharePoint.<br /><br /> Располагается в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<br /><br /> Область данных отчета для упорядочивания данных в отчете<br /><br /> Представления с вкладками для проектирования и предварительного просмотра для интерактивного конструирования отчета<br /><br /> Конструкторы запросов позволяют указывать, какие данные извлекать из источников данных и какие данные связаны с типами источников данных в [RSReportDesigner Configuration File](../report-server/rsreportdesigner-configuration-file.md)<br /><br /> Редактор выражений с поддержкой технологии IntelliSense для создания выражений [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , позволяющих настраивать содержимое и внешний вид отчетов<br /><br /> Поддерживает пользовательские элементы отчетов и пользовательские конструкторы запросов<br /><br /> <br /><br /> Дополнительные сведения см. в разделе [Службы Reporting Services в SQL Server Data Tools (службы SSDT)](reporting-services-in-sql-server-data-tools-ssdt.md).|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|  
|построитель отчетов|Это средство используется для конструирования отчетов и развертывания их на сервере отчетов в собственном режиме или в режиме интеграции с SharePoint.<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office средой<br /><br /> Возможность сохранять элементы отчетов как части отчета<br /><br /> Мастер создания карт<br /><br /> Агрегаты агрегатов<br /><br /> Улучшенная поддержка выражений<br /><br /> Конструкторы запросов позволяют указывать, какие данные извлекать из выбранных встроенных типов источников данных<br /><br /> <br /><br /> Дополнительные сведения см. в разделе [построитель отчетов &#40;SSRS&#41;](report-builder-authoring-environment-ssrs.md).|Загрузите MSI-файл или откройте из диспетчера отчетов или SharePoint|  
  
## <a name="tools-for-report-server-administration"></a>Средства для администрирования сервера отчетов  
 В службах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]доступен набор графических средств и средств работы со скриптами для администрирования сервера отчетов. Используемые средства зависят от режима развертывания сервера отчетов.  
  
### <a name="native-mode"></a>Собственный режим  
 В следующей таблице приведены доступные средства администрирования сервера отчетов, развернутого в собственном режиме.  
  
|Инструмент|Описание|Способ доступа|  
|----------|-----------------|-------------------|  
|Диспетчер конфигурации служб Reporting Services|Это средство используется для настройки установки служб Reporting Services. Обратите внимание на то, что диспетчер конфигурации служб Reporting Services не помогут управлять содержимым сервера отчетов, включения дополнительных компонентов или предоставления доступа к серверу. Доступны следующие задачи.<br /><br /> Настройка локальных и удаленных экземпляров сервера отчетов<br /><br /> Настройка учетной записи службы сервера отчетов.<br /><br /> Создание и настройка одного или нескольких URL-адресов веб-службы.<br /><br /> Настройка URL-адреса диспетчера отчетов<br /><br /> Создание и настройка базы данных сервера отчетов.<br /><br /> Настройка масштабного развертывания.<br /><br /> Резервное копирование, восстановление или замена симметричного ключа, используемого для шифрования хранимых строк подключения и учетных данных.<br /><br /> Настройка учетной записи автоматического выполнения.<br /><br /> Настройка SMTP-сервера для доставки электронной почты.<br /><br /> <br /><br /> Дополнительные сведения см. в разделе [Использование диспетчера конфигурации служб Reporting Services (собственный режим)](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).|Меню «Пуск»|  
|SQL Server Management Studio|Это средство используется для управления одним или несколькими экземплярами сервера отчетов в единой среде, включая следующие действия.<br /><br /> Управление локальными и удаленными экземплярами сервера отчетов<br /><br /> Установка свойств сервера отчетов<br /><br /> Изменение определений ролей<br /><br /> Отключение неиспользуемых функций сервера отчетов.<br /><br /> Управление заданиями<br /><br /> Управление общими расписаниями|Меню «Пуск»|  
|Диспетчер конфигурации SQL Server|Это средство используется для следующих целей.<br /><br /> Запуск и остановка служб Windows Reporting Services<br /><br /> Настройка передачи отзывов пользователей, расположения каталога дампа и отчетов об ошибках<br /><br /> <br /><br /> **\*\* Предупреждение \* \***  следует использовать это средство для настройки учетной записи службы. Используйте вместо него средство настройки служб Reporting Services.<br /><br /> Дополнительные сведения см. в разделе [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).|Меню «Пуск»|  
|Программа rsconfig|Это средство используется для настройки соединения сервера отчетов с базой данных сервера отчетов и управления им. Кроме того, с ее помощью можно указать учетную запись пользователя, которую следует использовать для автоматической обработки отчетов.<br /><br /> Дополнительные сведения см. в разделе [Программы командной строки сервера отчетов (службы SSRS)](report-server-command-prompt-utilities-ssrs.md).|С помощью командной строки|  
|Программа rskeymgmt|Это средство используется для следующих целей.<br /><br /> Извлечение, восстановление, создание и удаление симметричного ключа, используемого для шифрования данных сервера отчетов<br /><br /> Соединение экземпляров сервера отчетов при масштабном развертывании<br /><br /> <br /><br /> Дополнительные сведения см. в разделе [Программы командной строки сервера отчетов (службы SSRS)](report-server-command-prompt-utilities-ssrs.md).|С помощью командной строки|  
|Классы инструментария управления Windows (WMI)|Эти классы используются для автоматизации задач настройки в диспетчере конфигурации служб Reporting Services без использования графического пользовательского интерфейса.<br /><br /> Дополнительные сведения см. в разделе [Accessing the WMI Provider Programmatically](../accessing-the-wmi-provider-programmatically.md).|Скрипт Visual Basic|  
  
### <a name="sharepoint-integrated-mode"></a>Режим интеграции с SharePoint  
 В режиме SharePoint службы Reporting Services являются приложением-службой в архитектуре SharePoint и администрируются непосредственно через SharePoint  
  
|Инструмент|Описание|Способ доступа|  
|----------|-----------------|-------------------|  
|Центр администрирования SharePoint|Центр администрирования SharePoint используется для создания, запросов и управления общими приложениями-службами [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Дополнительные сведения см. в разделе [Настройка и администрирование сервера отчетов (режим интеграции с SharePoint служб Reporting Services)](../configure-administer-report-server-reporting-services-sharepoint-mode.md).|Открытие центра администрирования в браузере по URL-адресу сайта SharePoint|  
|Командлеты PowerShell|Командлеты PowerShell используются для создания, запросов и управления общими приложениями-службами [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Дополнительные сведения см. в разделе [Командлеты PowerShell для служб Reporting Services в режиме интеграции с SharePoint](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md).|Консоль управления SharePoint 2010|  
  
## <a name="tools-for-report-content-management"></a>Средства управления содержимым отчетов  
 В службах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]доступен набор графических средств и средств работы со скриптами для управления содержимым. Используемые средства зависят от режима развертывания сервера отчетов.  
  
|Инструмент|Описание|Способ доступа|  
|----------|-----------------|-------------------|  
|URL-адрес веб-службы сервера отчетов|Это средство используется для просмотра содержимого каталога отчетов на общей странице навигации по элементам.<br /><br /> Дополнительные сведения см. в разделе [Report Server Web Service](../report-server-web-service/report-server-web-service.md).|Браузер|  
|Диспетчер отчетов|**(Только в собственном режиме)** Это средство предназначено для администрирования одного экземпляра удаленного сервера отчетов через HTTP-соединение. Можно сделать следующее.<br /><br /> Просмотр, поиск, печать отчетов и подписка на отчеты.<br /><br /> Создания, защиты и поддержания иерархии папок для организации элементов на сервере.<br /><br /> Настройки безопасности на основе ролей, определяющей доступ к элементам и операциям.<br /><br /> Настройки свойств выполнения отчета, истории отчета и параметров отчета.<br /><br /> Создание моделей отчета, которые подключаются и получают данные из источника данных служб Microsoft SQL Server Analysis Services из реляционного источника данных SQL Server.<br /><br /> Задайте параметры безопасности элементов модели, чтобы обеспечить доступ к конкретным сущностям в модели, или сопоставьте сущности со стандартными отчетами с дополнительной информацией, созданными заранее.<br /><br /> Создания общего расписания и общих источников данных, чтобы упростить управление расписанием и соединениями с источниками данных.<br /><br /> Создания подписок, управляемых данными, которые распространяют отчеты среди большого количества получателей.<br /><br /> Создания связанных отчетов для повторного использования существующих отчетов различными способами.<br /><br /> Запустите построитель отчетов для создания отчетов, которые можно сохранить и запустить на сервере отчетов.<br /><br /> <br /><br /> Дополнительные сведения см. в разделе [Диспетчер отчетов (службы SSRS в собственном режиме)](../report-manager-ssrs-native-mode.md).||  
|Программа rs|Это средство является сервером скриптов, используемым для выполнения операций в форме скриптов. Используйте эту программу для выполнения скриптов [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , предназначенных для копирования данных из одной базы данных сервера отчетов в другую, публикации отчетов, создания объектов в базе данных сервера отчетов и т. д.<br /><br /> Дополнительные сведения см. в разделе [Программы командной строки сервера отчетов (службы SSRS)](report-server-command-prompt-utilities-ssrs.md).|С помощью командной строки|  
  
## <a name="see-also"></a>См. также:  
 [Сервер отчетов служб Reporting Services](../reporting-services-report-server.md)   
 [Основные понятия служб Reporting Services (SSRS)](../reporting-services-concepts-ssrs.md)   
 [Службы Reporting Services (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
