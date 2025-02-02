---
title: Обзор монитора зеркального отображения баз данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbmmonitor.main.f1
helpviewer_keywords:
- Database Mirroring Monitor [SQL Server], interface
ms.assetid: 8ebbdcd6-565a-498f-b674-289c84b985eb
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 6e92c372d4e71401e101b4f915bf4c6807cf0064
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795555"
---
# <a name="database-mirroring-monitor-overview"></a>Обзор монитора зеркального отображения баз данных
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  При наличии разрешения возможно использование монитора зеркального отображения баз данных для эффективного контроля любого набора зеркальных баз данных на экземпляре сервера. Процедура контроля позволяет проверить выполнение и правильность передачи данных во время сеанса зеркального отображения базы данных. Монитор зеркального отображения баз данных также полезен для диагностики причины уменьшения потока данных.  
  
 Можно поставить любую из зеркальных баз данных на индивидуальный контроль на каждом партнере по обеспечению отработки отказа. При регистрации базы данных монитор зеркального отображения баз данных кэширует следующие данные о базе данных:  
  
-   Имя базы данных  
  
-   имена двух экземпляров серверов-участников;  
  
-   последние известные роли каждого участника (основного или зеркального).  
  
## <a name="permissions"></a>Разрешения  
 Для мониторинга зеркального отображения базы данных необходимо быть членом предопределенной роли сервера **sysadmin** или предопределенной роли базы данных **dbm_monitor** в базе данных **msdb** на экземпляре сервера. Если пользователь является членом **sysadmin** или **dbm_monitor** только на одном экземпляре сервера-участника, то монитор сможет подключиться только к этому участнику; монитор не сможет получить данные от другого участника.  
  
 Если пользователь является членом только **dbm_monitor** на экземпляре сервера, то он обладает ограниченными разрешениями на этот экземпляр сервера. Возможен только просмотр последней строки состояния. При подключении экземпляра сервера с использованием разрешений **dbm_monitor** монитор зеркального отображения баз данных сообщает пользователю о наличии ограниченных разрешений.  
  
> [!IMPORTANT]  
>  Предопределенная роль базы данных **dbm_monitor** создается в базе данных **msdb** , когда первая база данных регистрируется в мониторе зеркального отображения баз данных. Новая роль **dbm_monitor** не имеет членов до тех пор, пока системный администратор не назначит ее пользователям.  
  
## <a name="navigation-tree"></a>Дерево навигации  
 Если какие-либо базы данных зарегистрированы для контроля монитором зеркального отображения баз данных, то перечень зарегистрированных баз данных будет отображаться в дереве навигации. Дерево автоматически обновляется каждые 30 секунд. Для просмотра состояния зарегистрированной базы данных выберите эту базу данных. Дополнительные сведения см. в разделе «Панель "Подробности"» ниже.  
  
 Следующие данные отображаются для каждой зарегистрированной базы данных.  
  
 _<имя_базы_данных>_ **(** _\<состояние>_ **,** _<ОСНОВНОЙ_СЕРВЕР>_ **->** _<ЗЕРКАЛЬНЫЙ_СЕРВЕР>_ **)**  
  
 *<имя_базы_данных>*  
 Имя зеркальной базы данных, зарегистрированной с помощью монитора зеркального отображения баз данных.  
  
 *\<Состояние >*  
 Возможны следующие состояния и значки их отображения.  
  
|Значок|Состояние|Описание|  
|----------|------------|-----------------|  
|Значок предупреждения|**Unknown**|Монитор не подключен ни к одному участнику. Единственными доступными данными являются данные, кэшированные монитором.|  
|Значок предупреждения|**Синхронизация**|Содержимое зеркальной базы данных отстает от содержимого основной базы данных. Экземпляр основного сервера отправляет записи журнала на экземпляр зеркального сервера, который применяет эти изменения к зеркальной базе данных для выполнения наката.<br /><br /> В начале сеанса зеркального отображения базы данных основная и зеркальная базы данных находятся в данном состоянии.|  
|Цилиндр стандартной базы данных|**синхронизировано;**|Когда зеркальный сервер достаточно догнал основной сервер, база данных переходит в состояние **Синхронизировано**. База данных сохраняет данное состояние, пока основной сервер продолжает отправлять изменения на зеркальный сервер, который в свою очередь продолжает применять изменения к зеркальной базе данных.<br /><br /> В режиме высокого уровня безопасности как отработка отказа автоматически, так и вручную возможны без потери данных.<br /><br /> Но и в режиме высокого уровня безопасности всегда остается актуальной потеря некоторых данных, даже в состоянии **Синхронизировано** .|  
|Значок предупреждения|**Приостановлена**|Основная база данных доступна, но не отправляет никаких записей журнала на зеркальный сервер.|  
|Значок ошибки|**Отключена**|Экземпляр сервера не может подключиться к участнику.|  
  
 *<ОСНОВНОЙ_СЕРВЕР>*  
 Имя участника, который в данный момент является экземпляром основного сервера. Имя имеет следующий формат:  
  
 *<СИСТЕМНОЕ_ИМЯ>* [ **\\** _<имя_экземпляра>_ ]  
  
 где *<SYSTEM_NAME>* — это имя системы, на которой расположен экземпляр сервера. Для не заданного по умолчанию экземпляра сервера имя экземпляра также отображается: _<СИСТЕМНОЕ_ИМЯ>_ **\\** _<имя_экземпляра>_ .  
  
 *<ЗЕРКАЛЬНЫЙ_СЕРВЕР>*  
 Имя участника, который в данный момент является экземпляром зеркального сервера. Формат аналогичен формату основного сервера.  
  
## <a name="detail-pane"></a>Панель «Подробности»  
 Отображение монитора зависит от того, выбрана база данных или нет. При открытии монитора панель подробностей отображает ссылку **Зарегистрировать зеркальную базу данных** . Щелкните данную ссылку, чтобы зарегистрировать базу данных. Зарегистрированные базы данных перечислены после узла **Монитор зеркального отображения баз данных** в дереве навигации. Монитор зеркального отображения баз данных всегда пытается подключиться к каждому экземпляру сервера, для которого он имеет сохраненные учетные данные.  
  
 При выборе базы данных ее состояние отображается на вложенной странице **Состояние** на панели подробностей. Содержимое данной страницы состоит из экземпляров основного и зеркального серверов. Эта страница заполняется асинхронно по мере сбора состояния в результате отдельных cоединений с экземплярами основного и зеркального сервера. Состояние автоматически обновляется каждые 30 секунд.  
  
> [!NOTE]  
>  Невозможно изменить частоту обновления монитора, но можно обновить таблицу состояния из диалогового окна **Журнал зеркального отображения базы данных** .  
  
 Системный администратор может просматривать предупреждения о текущей конфигурации базы данных посредством выбора вложенной страницы **Предупреждения** . Отсюда администратор может запустить диалоговое окно **Установка порогов предупреждений** для включения и настройки одного или более порогов предупреждений.  
  
 В баннере над вкладками в области сведений отображается информация о состоянии согласно последнему обновлению монитора в следующем виде: **Последнее обновление:** _\<дата>\<время>_ . Обычно монитор зеркального отображения баз данных получает сведения о состоянии от экземпляров основного и зеркального серверов в различное время. В зависимости от времени обновления отображается обновление, пришедшее раньше.  
  
## <a name="action-menu"></a>Меню «Действие»  
 Меню **Действие** всегда содержит следующие команды.  
  
|Command|Описание|  
|-------------|-----------------|  
|**Зарегистрировать зеркальную базу данных…**|Открытие диалогового окна **Зарегистрировать зеркальную базу данных** . Используйте это диалоговое окно для регистрации одной или нескольких баз данных на данном экземпляре сервера посредством добавления базы или баз данных к монитору зеркального отображения баз данных. Когда база данных добавлена, монитор зеркального отображения баз данных локально кэширует сведения о базе данных, ее участниках и о возможностях соединения с участниками.|  
|**Управление соединениями экземпляра сервера...**|При выборе данной команды открывается диалоговое окно **Управление соединениями сервера** . Здесь можно выбрать экземпляр сервера, которому необходимо указать учетные данные для монитора при подключении к данному участнику.<br /><br /> Для изменения учетных данных участника найдите его запись в сетке **Экземпляры сервера** и выберите **Изменить** в данной строке. Диалоговое окно **Соединение с сервером** появится с фиксированным именем экземпляра сервера и элементами управления учетными данными, установленными в текущее кэшированное значение. Измените при необходимости сведения о проверке подлинности, затем нажмите кнопку **Соединить**. Если учетные данные имеют достаточные права доступа, столбец **Соединиться при помощи** обновляется новыми учетными данными.|  
  
 Если выбрана база данных, меню **Действие** также должно содержать следующие команды.  
  
|Command|Описание|  
|-------------|-----------------|  
|**Отменить регистрацию этой базы данных**|Удалить выбранную базу данных из монитора зеркального отображения баз данных.|  
|**Установка порогов предупреждений...**|Открывается диалоговое окно **Установка значений порогов предупреждений** . Здесь системный администратор может включить или отключить предупреждения для базы данных на каждом участнике и изменить порог каждого предупреждения. Рекомендуется устанавливать порог для данного предупреждения на обоих участниках для гарантии, что предупреждение появляется при сбое базы данных. Соответствующий порог для каждого участника зависит от возможностей производительности системы участника.<br /><br /> Событие записывается в журнал событий по производительности только в случае, если его значение находится на границе порога или над порогом и если таблица состояния обновляется. Если пиковое значение немедленно достигает порога между обновлениями состояния, то данный пик опускается.|  
  
 **Мониторинг зеркального отображения баз данных в среде SQL Server Management Studio**  
  
-   [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>См. также:  
 [Мониторинг зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Запуск мастера настройки безопасности зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
