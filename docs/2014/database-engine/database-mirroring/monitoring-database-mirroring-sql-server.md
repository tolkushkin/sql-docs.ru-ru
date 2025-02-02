---
title: Наблюдение за зеркальным отображением базы данных (SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring [SQL Server], database mirroring
- database mirroring [SQL Server], monitoring
ms.assetid: a7b1b9b0-7c19-4acc-9de3-3a7c5e70694d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 23c8c3c76b881f342f56490e5722a0ae641464ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62755368"
---
# <a name="monitoring-database-mirroring-sql-server"></a>Наблюдение за зеркальным отображением базы данных (SQL Server)
  В данном разделе приводятся общие сведения о мониторе зеркального отображения баз данных и системных хранимых процедурах **sp_dbmmonitor** , описывается, как работает наблюдение за зеркальным отображением базы данных (включая **задание наблюдения за зеркальным отображением баз данных**), а также приводятся сведения о сеансах зеркального отображения базы данных, которые можно получить при наблюдении. Кроме того, в данном разделе описывается определение пороговых значений предупреждений для набора стандартных событий зеркального отражения базы данных и установка предупреждений на любое событие зеркального отображения базы данных.  
  
 В сеансе зеркального отображения может производиться наблюдение за зеркальной базой данных, что позволяет следить за тем, идет ли передача данных и насколько хорошо. Для контроля за одной или несколькими зеркальными базами данных на экземпляре сервера можно воспользоваться монитором зеркального отображения баз данных или системными хранимыми процедурами **sp_dbmmonitor** .  
  
 **Задание монитора зеркального отображения баз данных**работает независимо от монитора зеркального отображения баз данных. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вызывает **Задание монитора зеркального отображения баз данных** через регулярные интервалы времени (по умолчанию раз в минуту), а оно вызывает хранимую процедуру, обновляющую состояние зеркального отображения. Если запуск сеанса зеркального отображения производился в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , то **Задание монитора зеркального отображения баз данных** создается автоматически. Но если для запуска зеркального отображения использовалась только инструкция ALTER DATABASE *<имя_базы_данных>* SET PARTNER, то необходимо создать задание с помощью хранимой процедуры.  
  
 **В этом разделе.**  
  
-   [Наблюдение за состоянием зеркального отображения](#MonitoringStatus)  
  
-   [Дополнительные источники сведений о зеркальной базе данных](#AdditionalSources)  
  
-   [Связанные задачи](#RelatedTasks)  
  
##  <a name="MonitoringStatus"></a> Наблюдение за состоянием зеркального отображения  
 Для наблюдения за настройкой и управлением одной или несколькими зеркальными базами данных на экземпляре сервера можно использовать монитор зеркального отображения баз данных или системные хранимые процедуры **dbmmonitor** . В сеансе зеркального отображения может производиться наблюдение за зеркальной базой данных, что позволяет следить за тем, идет ли передача данных и насколько хорошо.  
  
 В частности, с помощью мониторинга зеркально отображаемой базы данных можно выполнить следующее.  
  
-   Проверить работу зеркального отображения.  
  
     Основное состояние включает сведения о том, работают ли два экземпляра сервера, соединены ли серверы, перемещается ли журнал с основного сервера на зеркальный.  
  
-   Определить, согласована ли зеркальная база данных с основной базой данных.  
  
     В высокопроизводительном режиме основной сервер может создавать очередь неотправленных записей журнала, которые требуется отправить с основного сервера на зеркальный. Более того, в любом режиме работы зеркальный сервер может создавать очередь записей журнала, которые были записаны в файл журнала, но все еще нуждаются в восстановлении в зеркальной базе данных.  
  
-   Определить, сколько данных было потеряно, пока экземпляр основного сервера оставался недоступным в высокопроизводительном режиме.  
  
     Можно определить потерю данных, посмотрев объем неотправленного журнала транзакций (при наличии) и интервала времени, в течение которого потерянные транзакции были зафиксированы на основном сервере.  
  
-   Сравнить текущую производительность с прежней производительностью.  
  
     В случае возникновения ошибок администратор базы данных может просмотреть историю производительности зеркального отображения, чтобы понять текущее состояние. Просмотр истории может позволить пользователю определить тенденции роста или снижения производительности, определить модели ошибок производительности (такие как время дня, когда у сети низкая пропускная способность или количество команд, входящих в журнал, слишком большое).  
  
-   Устранить причину снижения потока данных между участниками зеркального отображения.  
  
-   Установить пороги предупреждений для ключевых метрик производительности.  
  
     Если новая строка состояния содержит значение, превышающее порог, в журнал событий Windows записывается информационное событие. Системный администратор может вручную настроить предупреждения по этим событиям. Дополнительные сведения см. в статье [Использование пороговых значений предупреждений и оповещений в метриках производительности зеркального отображения (SQL Server)](use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
###  <a name="tools_for_monitoring_dbm_status"></a> Средства для контроля над состоянием зеркального отображения базы данных  
 Состояние зеркального отображения можно контролировать с помощью монитора зеркального отображения баз данных или системной хранимой процедуры **sp_dbmmonitorresults** . Эти средства для наблюдения за зеркальным отображением любой базы данных на экземпляре локального сервера могут использовать как системные администраторы (то есть члены предопределенной роли сервера **sysadmin** ), так и пользователи, добавленные в предопределенную роль **dbm_monitor** базы данных **msdb** системным администратором. При использовании любого из этих средств системный администратор может также вручную обновлять состояние зеркального отображения.  
  
> [!NOTE]  
>  Системные администраторы могут также настраивать и просматривать пороги предупреждений для ключевых метрик производительности. Дополнительные сведения см. в статье [Использование пороговых значений предупреждений и оповещений в метриках производительности зеркального отображения (SQL Server)](use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
-   Монитор зеркального отображения баз данных.  
  
     Монитор зеркального отображения баз данных представляет собой графический пользовательский интерфейс, позволяющий системным администраторам просматривать и обновлять состояние и настраивать пороги предупреждений на нескольких ключевых метриках производительности. Члены предопределенной роли базы данных **dbm_monitor** также могут использовать монитор зеркального отображения баз данных для просмотра самых последних строк таблицы состояния зеркального отображения, однако обновлять таблицу состояния они не могут.  
  
     На мониторе отображается состояние, включая показатели производительности выбранной базы данных на вкладке **Состояние** . Содержимое данной страницы состоит из экземпляров основного и зеркального серверов. Эта страница заполняется асинхронно по мере сбора состояния в результате отдельных cоединений с экземплярами основного и зеркального сервера. Монитор пытается обновлять таблицу состояния с интервалом в 30 секунд. Обновление завершается успешно только в случае, если таблица не обновлялась в течение 15 секунд, а пользователь является членом предопределенной роли сервера **sysadmin** . Дополнительные сведения о данных, отображаемых на странице **Состояние** см. в подразделе « [Состояние, отображаемое монитором зеркального отображения баз данных](#perf_metrics_of_dbm_monitor)» далее в этом разделе.  
  
     Основные сведения об интерфейсе монитора зеркального отображения баз данных см. в разделе [Database Mirroring Monitor Overview](database-mirroring-monitor-overview.md). Сведения о запуске монитора зеркального отображения базы данных см. в статье [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md).  
  
-   Системные хранимые процедуры.  
  
     Получить или обновить текущее состояние можно с помощью системной хранимой процедуры **sp_dbmmonitorresults** . Другие хранимые процедуры из группы dbmmonitor позволяют настраивать мониторинг, изменять его параметры, просматривать текущий период обновления и отменять мониторинг на экземпляре сервера.  
  
     В следующей таблице приведены хранимые процедуры для использования мониторинга зеркального отображения и управления им независимо от монитора зеркального отображения баз данных.  
  
    |Процедура|Описание|  
    |---------------|-----------------|  
    |[sp_dbmmonitoraddmonitoring](/sql/relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql)|Создает задание, периодически обновляющее сведения о состоянии по каждой зеркально отображаемой базе данных на экземпляре сервера.|  
    |[sp_dbmmonitorchangemonitoring](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql)|Изменяет значение параметра мониторинга зеркального отображения базы данных.|  
    |[sp_dbmmonitorhelpmonitoring](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql)|Возвращает текущий интервал обновления.|  
    |[sp_dbmmonitorresults](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql)|Возвращает строки состояния для контролируемой базы данных и позволяет выбрать, будет ли эта процедура получать последнее состояние заблаговременно.|  
    |[sp_dbmmonitordropmonitoring](/sql/relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql)|Останавливает и удаляет задания слежения за зеркальным отображением для всех баз данных на экземпляре сервера.|  
  
     Системные хранимые процедуры из группы **dbmmonitor** можно использовать в качестве дополнения к монитору зеркального отображения баз данных. Например, даже если мониторинг был настроен при помощи процедуры **sp_dbmmonitoraddmonitoring**, для просмотра состояния может использоваться монитор зеркального отображения баз данных.  
  
### <a name="how-monitoring-works"></a>Как работает мониторинг  
 Этот раздел знакомит с таблицей состояния зеркального отображения баз данных, заданием монитора зеркального отображения баз данных и самим монитором, с тем, как пользователи могут контролировать состояние зеркального отображения баз данных и удалять задания зеркального отображения.  
  
#### <a name="database-mirroring-status-table"></a>Таблица состояния зеркального отображения базы данных  
 Состояние зеркального отображения базы данных хранится во внутренней, недокументированной таблице состояния зеркального отображения базы данных в базе данных **msdb** . Эта таблица создается автоматически при первом обновлении состояния зеркального отображения на экземпляре сервера.  
  
 Таблица состояния может обновляться автоматически или вручную системным администратором с минимальным интервалом обновления 15 секунд. Минимальный интервал 15 секунд предотвращает перегрузку экземпляров сервера запросами о состоянии.  
  
 Таблица состояния обновляется автоматически как монитором зеркального отображения баз данных, так и заданием монитора зеркального отображения баз данных (если она запущена). **Задание монитора зеркального отображения баз данных** по умолчанию обновляет эту таблицу раз в минуту (системный администратор может изменять интервал от 1 до 120 минут). Для сравнения: монитор зеркального отображения баз данных обновляет эту таблицу автоматически каждые 30 секунд. Для выполнения этих обновлений как **Задание монитора зеркального отображения баз данных** , так и монитор зеркального отображения баз данных вызывают процедуру **sp_dbmmonitorupdate**.  
  
 При первом запуске процедуры **sp_dbmmonitorupdate** создается **таблица состояний зеркального отображения баз данных** и предопределенная роль базы данных **dbm_monitor** в базе данных **msdb** . Хранимая процедура**sp_dbmmonitorupdate** обычно обновляет состояние зеркального отображения, вставляя новую строку в таблицу состояний для каждой отображаемой базы данных на экземпляре сервера. Дополнительные сведения см. в статье "Таблица состояния зеркального отображения базы данных" далее в этом разделе. Эта процедура также оценивает метрики производительности в новых строках и отсекает строки, превышающие текущий срок хранения (по умолчанию — 7 дней). Дополнительные сведения см. в статье [sp_dbmmonitorupdate (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql).  
  
> [!NOTE]  
>  Если монитор зеркального отображения базы данных не используется в данный момент членом предопределенной роли сервера **sysadmin** , таблица состояния автоматически обновляется только в том случае, если существует **Задание монитора зеркального отображения баз данных** и запущен агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
#### <a name="database-mirroring-monitor-job"></a>Задание монитора зеркального отображения баз данных  
 Задание, контролирующее зеркальное отображение базы данных, **Задание монитора зеркального отображения баз данных**, работает независимо от монитора зеркального отображения баз данных. **Задание монитора зеркального отображения баз данных** создается автоматически только в том случае, если для запуска сеанса зеркального отображения используется среда [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Если для запуска зеркального отображения всегда используются инструкции ALTER DATABASE *имя_базы_данных* SET PARTNER, это задание существует, только если администратор выполнит хранимую процедуру **sp_dbmmonitoraddmonitoring** .  
  
 После создания **Задания монитора зеркального отображения баз данных** при условии, что агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запущен, это задание вызывается по умолчанию раз в минуту. Затем оно вызывает системную хранимую процедуру **sp_dbmmonitorupdate** .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] По умолчанию агент раз в минуту вызывает **Задание монитора зеркального отображения баз данных** , после чего это задание вызывает процедуру **sp_dbmmonitorupdate** для обновления таблицы состояния. Системные администраторы могут изменить периодичность с помощью системной хранимой процедуры **sp_dbmmonitorchangemonitoring** и просмотреть текущий период обновления с помощью системной хранимой процедуры **sp_dbmmonitorchangemonitoring** . Дополнительные сведения см. в статье [sp_dbmmonitoraddmonitoring (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql) и [sp_dbmmonitorchangemonitoring (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql).  
  
#### <a name="monitoring-database-mirroring-status-by-system-administrators"></a>Контроль над состоянием зеркального отображения базы данных (системными администраторами)  
 Члены предопределенной роли сервера **sysadmin** могут просматривать и обновлять таблицу состояния.  
  
-   Использование монитора зеркального отображения баз данных.  
  
     С помощью монитора зеркального отображения баз данных системный администратор может вручную обновлять страницу **Состояние** , дерево навигации или страницу **Журнал** . При этом также обновляется таблица состояния, если она еще не была обновлена в течение предыдущего 15-секундного периода.  
  
     Чтобы просмотреть журнал состояния зеркального отображения на данном экземпляре сервера, системный администратор может также нажать кнопку **Журнал** для экземпляра сервера (на странице **Состояние** ). Журнал отобразится в диалоговом окне **Журнал зеркального отображения базы данных** . В этом окне системный администратор может просматривать несколько или все строки таблицы состояния экземпляра сервера.  
  
     Дополнительные сведения о метриках страницы **Состояние** см. в подразделе «Метрики производительности, отображаемые монитором зеркального отображения баз данных» далее в этом разделе.  
  
-   Использование процедуры **sp_dbmmonitorresults**.  
  
     Системные администраторы могут использовать системную хранимую процедуру **sp_dbmmonitorresults** для просмотра и, при необходимости, для обновления таблицы состояния, если она не была обновлена в предыдущие 15 секунд. Эта процедура в свою очередь вызывает процедуру **sp_dbmmonitorupdate** и возвращает одну или более строк журнала, в зависимости от количества, запрашиваемого при вызове процедуры. Дополнительные сведения о состоянии в результирующем наборе см. в статье [sp_dbmmonitorresults (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql).  
  
#### <a name="monitoring-database-mirroring-status-by-dbmmonitor-members"></a>Контроль над состоянием зеркального отображения базы данных (членами роли dbm_monitor)  
 Как уже упоминалось, при первом выполнении процедуры **sp_dbmmonitorupdate** в базе данных **msdb** создается предопределенная роль **dbm_monitor** . Члены предопределенной роли базы данных **dbm_monitor** могут просматривать текущее состояние зеркального отображения при помощи монитора зеркального отображения баз данных или хранимой процедуры **sp_dbmmonitorresults** . Но эти пользователи не могут обновлять таблицу состояния. Чтобы узнать возраст отображаемого состояния, пользователь может посмотреть время в метках **Журнал основной базы данных (***\<время>***)** и **Журнал зеркальной базы данных (***\<время>***)** на странице **Состояние**.  
  
 Члены предопределенной роли базы данных **dbm_monitor** для обновления таблицы состояния через определенные промежутки времени полагаются на **Задание монитора зеркального отображения баз данных** . Если это задание не существует или агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] остановлен, состояние постепенно устаревает и может более не отражать реальную конфигурацию сеанса зеркального отображения. Например, после отработки отказа может оказаться, что партнеры используют одинаковую роль основного или зеркального сервера или текущий основной сервер может отображаться как зеркальный, в то время как текущий зеркальный сервер отображается как основной.  
  
#### <a name="dropping-the-database-mirroring-monitor-job"></a>Удаление задания монитора зеркального отображения баз данных  
 Задание, контролирующее зеркальное отображение баз данных ( **Задание монитора зеркального отображения баз данных**) работает до своего удаления. Контролирующее задание должно управляться системным администратором. Чтобы удалить **Задание монитора зеркального отображения баз данных**, используйте процедуру **sp_dbmmonitordropmonitoring**. Дополнительные сведения см. в статье [sp_dbmmonitordropmonitoring (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql).  
  
###  <a name="perf_metrics_of_dbm_monitor"></a> Состояние, отображаемое монитором зеркального отображения баз данных  
 На странице **Состояние** монитора зеркального отображения баз данных описываются участники, а также состояние сеанса зеркального отображения. Состояние включает метрики производительности, такие как состояние журнала транзакций, и другие сведения, позволяющие оценить время, необходимое для завершения отработки отказа, а также возможные потери данных, если сеанс не синхронизован. Кроме того, на странице **Состояние** отображается состояние и сведения о сеансе зеркального отображения в общем.  
  
> [!NOTE]  
>  Основные сведения о мониторе зеркального отображения баз данных и странице **Состояние** см. в подразделе " [Средства для контроля над состоянием зеркального отображения базы данных](#tools_for_monitoring_dbm_status)" выше в этом разделе.  
  
 Краткая информация о каждом из них приведена в следующих разделах.  
  
#### <a name="partners"></a>Участники  
 На странице **Состояние** отображаются следующие сведения о каждом из участников.  
  
-   Экземпляр сервера  
  
     Имя экземпляра сервера, состояние которого отображается в строке **Состояние** .  
  
-   Текущая роль.  
  
     Текущая роль этого экземпляра сервера. Возможные состояния:  
  
    -   Основной  
  
    -   Зеркальное отображение  
  
-   Состояние зеркального отображения.  
  
     Возможные состояния:  
  
    -   Неизвестно  
  
    -   Синхронизация  
  
    -   синхронизировано;  
  
    -   Приостановлена  
  
    -   Отключено  
  
-   Соединение следящего сервера.  
  
     Состояние соединение следящего сервера. Возможные состояния:  
  
    -   Неизвестно  
  
    -   Подключен  
  
    -   отключен.  
  
#### <a name="log-on-the-principal-server"></a>Журнал основного сервера  
 На странице **Состояние** отображаются следующие сведения о состоянии журнала на основном сервере на указанный момент времени.  
  
-   Неотправленный журнал  
  
     Объем данных журнала в очереди на отправку в килобайтах (КБ).  
  
-   Самая старая неотправленная транзакция  
  
     Возраст самой старой неотправленной транзакции в очереди на отправку. Этот срок указывает, сколько минут транзакции не отправлялись на экземпляр зеркального сервера. Это значение позволяет оценить потенциальные потери данных по времени.  
  
-   Время на отправку журнала (предполагаемое).  
  
     Предполагаемое количество минут, необходимых экземпляру основного сервера для отправки журнала, находящегося в очереди на отправку на экземпляр зеркального сервера, на основании текущей скорости отправки. Фактическое время отправки журнала будет зависеть от скорости входящих транзакций, которая может сильно различаться. Однако значение **Время на отправку журнала (предполагаемое)** может быть полезно для приблизительной оценки времени, необходимого для отработки отказа вручную.  
  
-   Текущая скорость отправки  
  
     Скорость, с которой транзакции отправляются на экземпляр зеркального сервера, в КБ в секунду.  
  
-   Текущая скорость новых транзакций.  
  
     Скорость, с которой входящие транзакции попадают в журнал основного сервера, в КБ в секунду. Чтобы определить отставание зеркального отображения, задержку или запаздывание, сравните это значение со значением **Предполагаемое время на отправку журнала** .  
  
#### <a name="log-on-the-mirror-server"></a>Журнал зеркального сервера  
 На странице **Состояние** отображаются следующие сведения о состоянии журнала на зеркальном сервере на указанный момент времени.  
  
-   Невосстановленный журнал  
  
     Объем данных журнала в очереди повторов в килобайтах (КБ).  
  
-   Время на восстановление журнала (предполагаемое).  
  
     Приблизительное количество минут, необходимых для применения журнала, находящегося в очереди повторов, к зеркальной базе данных.  
  
-   Текущая скорость восстановления  
  
     Скорость, с которой транзакции восстанавливаются в зеркальной базе данных (в КБ в секунду).  
  
#### <a name="mirroring-session"></a>Сеанс зеркального отображения  
 Кроме того, на странице **Состояние** отображаются следующие сведения о сеансе зеркального отображения.  
  
-   Затраты на фиксацию изменений на зеркальном сервере.  
  
     Среднее значение задержки на транзакцию в миллисекундах (имеет смысл только в режиме высокой безопасности). Задержка — это объем дополнительной нагрузки во время ожидания экземпляром основного сервера экземпляра зеркального сервера для добавления записи журнала транзакции в очередь повтора.  
  
-   Время, необходимое для отправки и восстановления всего текущего журнала (предполагаемое).  
  
     Предполагаемое время, необходимое для отправки всего неотправленного журнала, который был зафиксирован на основном сервере и для восстановления всего журнала, находящегося в очереди повторов. Это предполагаемое значение может быть меньше суммы значений полей **Время на отправку журнала (предполагаемое)** и **Время на восстановление журнала (предполагаемое)** , так как отправка и восстановление могут выполняться параллельно.  
  
-   Адрес следящего сервера.  
  
     Сетевой адрес экземпляра следящего сервера. Сведения о формате этого адреса см. в разделе [Указание сетевого адреса сервера (зеркальное отображение базы данных)](specify-a-server-network-address-database-mirroring.md).  
  
-   Режим работы  
  
     Режим работы сеанса зеркального отображения базы данных.  
  
    -   Высокая производительность (асинхронный)  
  
    -   Высокий уровень безопасности без автоматического перехода на другой ресурс (синхронного)  
  
    -   Высокий уровень безопасности с автоматическим переходом на другой ресурс (синхронным)  
  
##  <a name="AdditionalSources"></a> Дополнительные источники сведений о зеркальной базе данных  
 Помимо использования монитора зеркального отображения баз данных и хранимых процедур dbmmonitor для наблюдения за зеркальной базой данных и установки предупреждений в переменных мониторинга производительности, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] предоставляет представления каталога, счетчики производительности и уведомления о событиях для зеркального отображения базы данных.  
  
 **В этом разделе.**  
  
-   [Метаданные зеркального отображения базы данных](#DbmMetadata)  
  
-   [Счетчики производительности зеркального отображения базы данных](#DbmPerfCounters)  
  
-   [Уведомления о событиях зеркального отображения базы данных](#DbmEventNotif)  
  
###  <a name="DbmMetadata"></a> Метаданные зеркального отображения базы данных  
 Каждый сеанс зеркального отображения базы данных описывается в метаданных, доступных через следующие динамические административные представления или представления каталога.  
  
-   **sys.database_mirroring**  
  
     Это представление отображает метаданные зеркального отображения базы данных для каждой зеркально отображаемой базы данных на экземпляре сервера. Дополнительные сведения см. в разделе [sys.database_mirroring (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql).  
  
-   **sys.database_mirroring_endpoints**  
  
     Представление каталога **sys.database_mirroring_endpoints** отображает сведения о конечной точке зеркального отображения базы данных на экземпляре сервера. Дополнительные сведения см. в статье [sys.database_mirroring_endpoints (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql).  
  
-   **sys.database_mirroring_witnesses**  
  
     Это представление каталога отображает метаданные зеркального отображения базы данных для каждого сеанса, в котором экземпляр сервера является следящим сервером. Дополнительные сведения см. в статье [sys.database_mirroring_witnesses (Transact-SQL)](/sql/relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses).  
  
-   **sys.dm_db_mirroring_connections**  
  
     Это динамическое административное представление возвращает по одной строке для каждого сетевого подключения зеркального отображения базы данных.  
  
     Дополнительные сведения см. в статье [sys.dm_db_mirroring_connections (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections).  
  
###  <a name="DbmPerfCounters"></a> Счетчики производительности зеркального отображения базы данных  
 Счетчики производительности позволяют отслеживать производительность при зеркальном отображении баз данных. Например, можно просмотреть счетчик **Задержка транзакции** , чтобы узнать, влияет ли зеркальное отображение базы данных на производительность основного сервера, или просмотреть счетчики **Очередь на повтор** и **Очередь отправки журнала** , чтобы узнать, насколько быстро зеркальная база данных воспроизводит изменения основной базы данных. Можно просмотреть счетчик **Отправлено байтов журнала/с** , чтобы отследить объем данных журнала, пересылаемый за секунду.  
  
 В системном мониторе любого из участников зеркального отображения базы данных счетчики производительности находятся в объекте производительности зеркального отображения базы данных (**SQLServer:Database Mirroring**). Дополнительные сведения см. в статье [SQL Server, Database Mirroring Object](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md).  
  
 **Запуск системного монитора**  
  
-   [Запуск системного монитора (Windows)](../../relational-databases/performance/start-system-monitor-windows.md)  
  
###  <a name="DbmEventNotif"></a> Уведомления о событиях зеркального отображения базы данных  
 Уведомление о событии является особым типом объекта базы данных. Уведомления о событиях выполняются в ответ на множество инструкций языка DDL Transact-SQL и на события трассировки SQL. Уведомления отправляют сведения о событиях сервера и базы данных службе [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
 При зеркальном отображении базы данных доступны следующие события.  
  
-   Класс событий**Database Mirroring State Change**   
  
     Указывает, что состояние зеркального отображения зеркальной базы данных изменилось. Дополнительные сведения см. в статье [Database Mirroring State Change Event Class](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md).  
  
-   Класс событий**Audit Database Mirroring Login**   
  
     Содержит сведения о сообщениях аудита, связанных с безопасностью транспорта зеркального отображения базы данных. Дополнительные сведения см. в статье [Audit Database Mirroring Login Event Class](../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md).  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Использование пороговых значений предупреждений и оповещений в метриках производительности зеркального отображения (SQL Server)](use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
-   [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [Просмотр состояния зеркального отображения базы данных (среда SQL Server Management Studio)](view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
 **Хранимые процедуры**  
  
-   [sp_dbmmonitoraddmonitoring (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql)  
  
-   [sp_dbmmonitorchangealert (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql)  
  
-   [sp_dbmmonitorchangemonitoring (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql)  
  
-   [sp_dbmmonitordropalert (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql)  
  
-   [sp_dbmmonitordropmonitoring (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql)  
  
-   [sp_dbmmonitorhelpalert (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql)  
  
-   [sp_dbmmonitorhelpmonitoring (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql)  
  
-   [sp_dbmmonitorresults (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql)  
  
-   [sp_dbmmonitorupdate (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql)  
  
## <a name="see-also"></a>См. также:  
 [Зеркальное отображение базы данных (SQL Server)](database-mirroring-sql-server.md)   
 [Основные понятия о поставщике WMI для событий сервера](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
