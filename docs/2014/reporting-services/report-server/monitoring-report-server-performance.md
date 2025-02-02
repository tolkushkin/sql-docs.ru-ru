---
title: Наблюдение за производительностью сервера отчетов | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- report servers [Reporting Services], performance
- counters [Reporting Services]
- monitoring performance [Reporting Services]
- SQL Server Reporting Services, performance
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: c1bc13d4-8297-4daf-bb19-4c1e5ba292a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f020dd812b53e531a3f4634ccba0d2cba980b89e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103797"
---
# <a name="monitoring-report-server-performance"></a>Наблюдение за производительностью сервера отчетов
  Для наблюдения за производительностью сервера отчетов используются средства наблюдения за производительностью, позволяющие оценить активность сервера, наблюдать тренды, диагностировать узкие места системы и собирать данные, помогающие определить адекватность текущей конфигурации системы. Для настройки производительности сервера можно задать частоту очистки домена приложений сервера отчетов. Дополнительные сведения см. в разделе [Настройка доступной памяти для приложений сервера отчетов](../report-server/configure-available-memory-for-report-server-applications.md).  
  
## <a name="sources-of-performance-data"></a>Источники данных производительности  
 Для получения всеобъемлющих сведений о работе системы используется комбинация определенных технологий и средств. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server предоставляют сведения о производительности с помощью следующих средств:  
  
-   Диспетчер задач  
  
-   Средство просмотра событий  
  
-   Консоль производительности  
  
 Диспетчер задач предоставляет сведения о программах и процессах, выполняющихся на компьютере. Диспетчер задач можно использовать для контроля ключевых показателей производительности сервера отчетов. Можно также получить доступ к параметрам активности выполняющихся процессов и просматривать данные и графики использования ЦП и памяти. Дополнительные сведения об использовании диспетчера задач см. в документации по продукту [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Консоль производительности и средство просмотра событий можно использовать для создания журналов и предупреждений об обработке отчетов и потреблении ресурсов. Сведения о событиях Windows, формируемых службами [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], см. в разделе [Журнал приложений Windows](windows-application-log.md). Дополнительные сведения о консоли производительности см. в подразделе «Счетчики производительности Windows», далее в этом разделе.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляют также сведения о базе данных сервера отчетов и временных базах данных, используемых для кэширования и управления сеансами.  
  
## <a name="windows-performance-counters"></a>Счетчики производительности Windows  
 Контроль конкретных счетчиков производительности позволяет:  
  
-   оценить системные требования, необходимые для поддержки предполагаемой рабочей нагрузки;  
  
-   определить базовый уровень производительности для оценки влияния изменений конфигурации или обновлений приложений;  
  
-   контролировать производительность приложений при определенных нагрузках, естественных или искусственных;  
  
-   убедиться в том, что обновление оборудования оказывает необходимое влияние на производительность;  
  
-   убедиться в том, что изменения конфигурации системы оказывают необходимое влияние на производительность.  
  
## <a name="reporting-services-performance-objects"></a>Объекты производительности служб Reporting Services  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] содержат следующие объекты производительности.  
  
-   **Веб-службы MSRS 2011** и `MSRS 2011 SharePoint Mode Web Service` для наблюдения за производительностью сервера отчетов. Эти объекты производительности включают коллекцию счетчиков, используемых для отслеживания работы сервера отчетов, обычно инициируемой интерактивными операциями просмотра отчетов. Эти счетчики сбрасываются, когда платформа [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] останавливает веб-службу сервера отчетов.  
  
-   `MSRS 2011 Windows Service` и `MSRS 2011 Windows Service SharePoint Mode` — для наблюдения за проводимыми по расписанию операциями и доставкой отчетов. Эти объекты производительности включают коллекцию счетчиков, используемых для отслеживания обработки отчетов, обычно инициируемой операциями по расписанию. Назначенные операции включают подписку и доставку, создание снимков состояния выполнения отчетов, а также ведение журнала отчетов.  
  
-   `ReportServer:Service` и `ReportServerSharePoint:Service` — для наблюдения за связанными с HTTP событиями и управления памятью. Эти счетчики являются уникальными для служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]— они отслеживают связанные с HTTP события для сервера отчетов, такие как запросы, соединения и попытки входа. Этот объект производительности также включает счетчики для отслеживания событий управления памятью.  
  
 Если на одном компьютере имеется несколько экземпляров сервера отчетов, их можно контролировать вместе или по отдельности. При добавлении счетчика необходимо выбрать включаемые в него экземпляры. Дополнительные сведения об использовании консоли производительности и добавлении счетчиков см. в документации по продукту [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="other-performance-counters"></a>Другие счетчики производительности  
 Пользовательские счетчики производительности служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] доступны только для объектов `MSRS 2008 Web Service`, `MSRS 2008 Windows Service` и `ReportServer:Service`. Следующие счетчики производительности предоставляют дополнительные возможности наблюдения за производительностью для сервера отчетов.  
  
|Объект производительности|Примечания|  
|------------------------|-----------|  
|`.NET CLR Data` и `.NET CLR Memory`|Диспетчер отчетов использует счетчики производительности [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Дополнительные сведения см. в статье по улучшению производительности и стабильности приложений .NET (Improving .NET Application Performance and Scalability) в MSDN.|  
|`Process`|Для отслеживания времени обработки по идентификатору обработки нужно добавить счетчики производительности `Elapsed Time` и `ID Process` в экземпляр ReportingServicesService.|  
  
## <a name="sharepoint-events"></a>События SharePoint  
 Кроме объектов производительности служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , можно также настроить события SharePoint, если сервер отчетов запущен в режиме интеграции с SharePoint, а среда создания отчетов настроена для использования продукта SharePoint. В данном разделе используйте события для сервера отчетов в режиме интеграции с SharePoint для просмотра диагностических событий компонента, которые могут предоставить полезные сведения, в случае если среда подготовки отчетов интегрирована с SharePoint.  
  
## <a name="in-this-section"></a>в этом разделе  
 [Счетчики производительности для MSRS 2014 Web Service и объекты производительности компонента MSRS 2014 Windows Service &#40;собственный режим&#41;](performance-counters-msrs-2011-web-service-performance-objects.md)  
 Содержит описание счетчиков производительности, используемых веб-службой сервера отчетов.  
  
 [Счетчики производительности для MSRS 2014 Web Service SharePoint Mode и MSRS 2014 Windows Service SharePoint режим, объекты производительности &#40;режиме интеграции с SharePoint&#41;](performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
 Содержит описание счетчиков производительности, используемых службой Windows сервера отчетов.  
  
 [Счетчики производительности для объектов производительности ReportServer:Service и ReportServerSharePoint:Service](performance-counters-reportserver-service-performance-objects.md)  
 Содержит описание счетчиков производительности в службах [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], связанных с HTTP и с памятью.  
  
 События для сервера отчетов в режиме интеграции с SharePoint  
 Содержит описание полезных диагностических событий, возникающих при запуске среды создания отчетов с продуктом SharePoint.  
  
## <a name="see-also"></a>См. также  
 [Настройка доступной памяти для приложений сервера отчетов](../report-server/configure-available-memory-for-report-server-applications.md)   
 [Сервер отчетов служб Reporting Services (основной режим)](reporting-services-report-server-native-mode.md)   
 [Инструментальные средства служб Reporting Services](../tools/reporting-services-tools.md)  
  
  
