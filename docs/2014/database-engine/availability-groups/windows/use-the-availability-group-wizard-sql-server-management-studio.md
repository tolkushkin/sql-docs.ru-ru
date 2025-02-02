---
title: Использование мастера групп доступности (среда SQL Server Management Studio) | Документы Майкрософт
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.newagwizard.f1
- sql12.swb.newavgroupwiz.f1
helpviewer_keywords:
- New Availability Group Wizard, availability replicas
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], creating
ms.assetid: e1f1dccc-9e65-471d-8fd1-b45085c9484a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0772ab148c413d685f046a5a238761edf647641b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788688"
---
# <a name="use-the-availability-group-wizard-sql-server-management-studio"></a>Использование мастера групп доступности (SQL Server Management Studio)
  В этом разделе описывается использование мастера создания групп доступности (в среде [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]) для создания и настройки группы доступности AlwaysOn в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. *Группа доступности* определяет набор пользовательских баз данных, которые будут действовать при сбое как единое целое, и набор партнеров по обеспечению отработки отказа, называемых *репликами доступности*и поддерживающих отработку отказа.  
  
> [!NOTE]  
>  Базовые сведения о группах доступности см. в разделе [Обзор групп доступности AlwaysOn (SQL Server)](overview-of-always-on-availability-groups-sql-server.md).  
  
-   **Перед началом:**  
  
     [Предварительные условия, ограничения и рекомендации](#PrerequisitesRestrictions)  
  
     [безопасность](#Security)  
  
-   **Создание и настройка группы доступности с использованием:**  [Мастер создания группы доступности (SQL Server Management Studio)](#RunAGwiz)  
  
> [!NOTE]  
>  Вместо мастера создания групп доступности можно использовать [!INCLUDE[tsql](../../../includes/tsql-md.md)] или командлеты [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Дополнительные сведения см. в разделе [Создание группы доступности (Transact-SQL)](create-an-availability-group-transact-sql.md) или командлеты [Создание группы доступности (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md).  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
 Настоятельно рекомендуется прочитать этот раздел, прежде чем пытаться настроить свою первую группу доступности.  
  
###  <a name="PrerequisitesRestrictions"></a> Предварительные условия, ограничения и рекомендации  
 В большинстве случаев можно использовать мастер создания групп доступности для выполнения всех задач по созданию и настройке группы доступности. Однако некоторые задачи может потребоваться выполнить вручную.  
  
-   Перед созданием группы доступности необходимо, чтобы экземпляры [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , на которых находятся реплики доступности, были расположены на различных узлах одной отказоустойчивой кластеризации Windows Server (WSFC). Кроме того, убедитесь, что каждый из экземпляров сервера соответствует всем другим обязательным условиям [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Для получения дополнительных сведений настоятельно рекомендуется изучить раздел [Предварительные требования, ограничения и рекомендации для групп доступности AlwaysOn (SQL Server)](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Если экземпляр сервера, который выбран для размещения реплики доступности, запускается из-под учетной записи службы домена и не содержит конечной точки зеркального отображения базы данных, то мастер может создать конечную точку и предоставить учетной записи службы экземпляра сервера разрешение CONNECT. Но если служба [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] запущена от имени встроенной учетной записи, такой как «Локальная система», «Локальная служба» или «Сетевая служба», или от имени учетной записи, не входящей в домен, то для проверки подлинности конечных точек необходимо пользоваться сертификатами, а мастер не сможет создать точку зеркального отображения базы данных на этом экземпляре сервера. В этом случае рекомендуется создать конечные точки зеркального отображения базы данных вручную до запуска мастера создания групп доступности.  
  
     `To use certificates for a database mirroring endpoint:`  
  
     [CREATE ENDPOINT (Transact-SQL)](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
     [Использование сертификатов для конечной точки зеркального отображения базы данных (Transact-SQL)](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   Экземпляры отказоустойчивого кластера SQL Server не поддерживают автоматический переход на другой ресурс с учетом групп доступности, поэтому любая реплика доступности, размещенная в них, должна быть настроена для перехода на другой ресурс вручную.  
  
-   Если база данных зашифрована или содержит ключ шифрования базы данных, то нельзя использовать [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] или [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] для добавления базы данных в группу доступности. Если зашифрованная база данных была расшифрована, то в резервных копиях ее журналов могут содержаться зашифрованные данные. В этом случае выполнение полной начальной синхронизации данных в базе данных может завершиться ошибкой. Причина этого заключается в том, что операции восстановления журнала может потребоваться сертификат, который был использован ключами шифрования базы данных, который в данный момент недоступен.  
  
     Чтобы сделать расшифрованную базу данных доступной для добавления в группу доступности с помощью мастера, выполните следующие шаги.  
  
    1.  Создайте резервную копию журнала базы данных-источника.  
  
    2.  Создайте полную резервную копию базы данных-источника.  
  
    3.  Восстановите резервную копию базы данных на экземпляре сервера, на котором размещается вторичная реплика.  
  
    4.  Создайте новую резервную копию журнала базы данных-источника.  
  
    5.  Восстановите эту резервную копию журнала в базе данных-получателе.  
  
-   **Предварительные условия для выполнения мастером полной первоначальной синхронизации данных**  
  
    -   Все пути к файлам базы данных должны быть одинаковыми на всех экземплярах сервера, на которых размещены реплики группы доступности.  
  
    -   На экземпляре сервера, содержащем вторичную реплику, не может существовать имя базы данных-источника. Это означает, что еще не может существовать ни одна из новых баз данных-получателей.  
  
    -   Чтобы при помощи мастера можно было создавать резервные копии и обращаться к ним, необходимо будет указать общую сетевую папку. Для каждой первичной реплики учетная запись, используемая для запуска [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , должна иметь разрешения в файловой системе на чтение и запись в общей сетевой папке. Для вторичных реплик учетная запись должна иметь разрешение на чтение в сетевой папке.  
  
        > [!IMPORTANT]  
        >  Резервные копии журналов будут входить в цепочку резервных копий журналов. Храните файлы резервных копий журналов надлежащим образом.  
  
     Если нет возможности воспользоваться мастером для выполнения полной первоначальной синхронизации данных, то базы данных-получатели нужно подготовить вручную. Это можно сделать до или после запуска мастера. Дополнительные сведения см. в разделе [Подготовка базы данных-получателя для присоединения к группе доступности вручную (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Требуется членство в предопределенной роли сервера **sysadmin** и разрешение сервера CREATE AVAILABILITY GROUP, ALTER ANY AVAILABILITY GROUP или CONTROL SERVER.  
  
 Кроме того, требуется разрешение CONTROL ON ENDPOINT, если мастер группы доступности должен иметь возможность управлять конечной точкой зеркального отображения базы данных.  
  
##  <a name="RunAGwiz"></a> Использование мастера создания группы доступности  
  
1.  В обозревателе объектов подключитесь к экземпляру сервера, на котором размещена первичная реплика доступности.  
  
2.  Разверните узел **Высокий уровень доступности AlwaysOn** и узел **Группы доступности** .  
  
3.  Для запуска мастера создания группы доступности выберите команду **Создать группу доступности** .  
  
4.  При первом запуске этого мастера отображается страница **Введение** . Чтобы в будущем эта страница не отображалась, можно щелкнуть **Больше не показывать эту страницу**. Прочитав эту страницу, нажмите кнопку **Далее**.  
  
5.  На странице **Укажите имя группы доступности** введите имя новой группы доступности в поле **Имя группы доступности** . Это имя должно быть действительным идентификатором [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , который является уникальным для отказоустойчивого кластера WSFC и для домена в целом. Максимальная длина имени группы доступности составляет 128 символов.  
  
6.  На странице **Выбор баз данных** в сетке приведен список пользовательских баз данных на подключеном экземпляре сервера, которые могут стать *базами данных доступности*. Выберите одну или несколько из указанных баз данных для участия в новой группе доступности. Эти базы данных станут первоначальными *базами данных-источниками*.  
  
     Для каждой из перечисленных баз данных столбец **Размер** отображает размер базы данных, если он известен. Столбец **Состояние** показывает, соответствует ли эта база данных [предварительным условиям](prereqs-restrictions-recommendations-always-on-availability.md), необходимым для баз данных доступности. Если необходимые условия не выполняются, краткое описание состояния указывает на причину того, почему эта база данных не может использоваться. Например, если для нее не используется модель полного восстановления. Для получения дополнительны сведений щелкните описание состояния.  
  
     После изменения базы данных для обеспечения соответствия требованиям щелкните **Обновить** , чтобы обновить сетку баз данных.  
  
7.  На странице **Выбор реплик** укажите и настройте одну или несколько реплик для новой группы доступности. Страница содержит четыре вкладки. Эти вкладки представлены в следующей таблице. Дополнительные сведения см. в статье [Страница "Указание реплик" (мастер создания группы доступности: мастер добавления реплики)](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md).  
  
    |Вкладка|Краткое описание|  
    |---------|-----------------------|  
    |**Реплики**|На этой вкладке можно задать каждый экземпляр [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , где будет размещена вторичная реплика. Обратите внимание, что первичная реплика должна быть размещена на экземпляре сервера, с которым в данный момент установлено соединение.|  
    |**Конечные точки**|Эту вкладку можно использовать для проверки существующих конечных точек зеркального отображения баз данных, а также для их автоматического создания в случае, если они отсутствуют на экземпляре сервера, служба которого использует проверку подлинности Windows. **Примечание.**  Если любой экземпляр сервера работает под учетной записью пользователя домена, необходимо сделать вручную перейти на свой экземпляр сервера, прежде чем перейти в мастере. Дополнительные сведения см. в подразделе [Предварительные условия](#PrerequisitesRestrictions)ранее в этом разделе.|  
    |**Параметры резервного копирования**|Эту вкладку можно использовать для задания настроек резервного копирования для группы доступности в целом, а также для задания приоритетов резервного копирования для отдельных реплик доступности.|  
    |**Средство прослушивания**|Эта вкладка используется для создания прослушивателя группы доступности. По умолчанию мастер не создает прослушиватель.|  
  
8.  На странице **Выбор начальной синхронизации данных** выберите, как именно необходимо создать новые базы данных-получатели и присоединить их к группе доступности. Выберите один из следующих параметров.  
  
    -   **Полный**  
  
         Выберите этот режим, если ваша среда удовлетворяет требованиям для автоматического запуска начальной синхронизации данных (дополнительные сведения см. в подразделе [Предварительные условия, ограничения и рекомендации](#PrerequisitesRestrictions)ранее в этом разделе).  
  
         При выборе режима **Полная**после создания группы доступности мастер выполнит резервное копирование всех баз данных-источников из журналов транзакций в сетевую папку и восстановит резервные копии на всех экземплярах серверов, на которых размещены вторичные реплики. После этого мастер выполнит присоединение всех баз данных-получателей к группе доступности.  
  
         В поле **Выберите сетевую папку, доступную для всех реплик:** укажите общую папку резервной копии, к которой имеют доступ на чтение и запись все экземпляры серверов, на которых размещаются реплики. Дополнительные сведения см. в подразделе [Предварительные условия](#PrerequisitesRestrictions)ранее в этом разделе.  
  
    -   **Только присоединение**  
  
         Если вы вручную подготовили базы данных-получатели на экземплярах серверов, на которых будут размещены вторичные реплики, то можно указать этот режим. Мастер выполнит присоединение существующих баз данных-получателей к группе доступности.  
  
    -   **Пропустить начальную синхронизацию данных**  
  
         Выберите этот параметр, если вы хотите использовать собственные резервные копии баз данных-источников и их журналов. Дополнительные сведения см. в разделе [Запуск перемещения данных в базе данных-получателе AlwaysOn (SQL Server)](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
9. На странице **Проверка** выполняется проверка соответствия значений, заданных в этом мастере, требованиям мастера создания группы доступности. Чтобы внести изменения, нажмите кнопку **Назад** , вернитесь к предыдущей странице мастера и измените одно или несколько значений. Нажмите кнопку **Далее** , чтобы вернуться на страницу **Проверка** , а затем кнопку **Повторить проверку**.  
  
10. На странице **Сводка** проверьте параметры, выбранные для новой группы доступности. Чтобы внести изменения, щелкните **Назад** , чтобы вернуться на нужную страницу. После внесения изменений нажмите кнопку **Далее** , чтобы вернуться на страницу **Сводка** .  
  
    > [!IMPORTANT]  
    >  Если учетная запись службы [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] для экземпляра сервера, на котором будет размещаться новая реплика доступности, еще не существует в качестве имени входа, то мастер создания группы доступности должен создать имя входа. На странице **Сводка** мастер показывает сведения об имени входа, которое будет создано. Если нажать кнопку **Готово**, мастер создаст это имя входа для учетной записи SQL Server и предоставит ему разрешение CONNECT.  
  
     Если параметры выбраны правильно, можно нажать кнопку **Скрипт** , чтобы создать скрипт шагов, которые будут выполняться мастером. Теперь нажмите кнопку **Готово**, чтобы создать и настроить новую группу доступности.  
  
11. На странице **Выполнение установки** отображается ход выполнения этапов создания группы доступности (настройка конечных точек, создание группы доступности и присоединение к группе вторичной реплики).  
  
12. После завершения выполнения этих шагов на странице **Результаты** отображаются результаты выполнения каждого шага. Если эти шаги завершатся успешно, новая группа доступности будет полностью настроена. Если один из шагов завершится ошибкой, то может потребоваться завершение настройки вручную или использование мастера для ошибочного шага. Сведения о причинах данной ошибки можно отобразить, перейдя по соответствующей ссылке «Ошибка» в столбце **Результат** .  
  
     По завершении работы мастера нажмите кнопку **Закрыть** , чтобы выйти из него.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Завершение настройки группы доступности**  
  
-   [Присоединение вторичной реплики к группе доступности (SQL Server)](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Подготовка базы данных-получателя для присоединения к группе доступности вручную (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Присоединение базы данных-получателя к группе доступности (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Создание или настройка прослушивателя группы доступности (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Другие способы создания группы доступности**  
  
-   [Использование диалогового окна "Создание группы доступности" (среда SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Создание группы доступности (Transact-SQL)](create-an-availability-group-transact-sql.md)  
  
-   [Создание группы доступности (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)  
  
 **Чтобы включить группы доступности AlwaysOn**  
  
-   [Включение и отключение групп доступности AlwaysOn (SQL Server)](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Настройка конечной точки зеркального отображения базы данных**  
  
-   [Создание базы данных конечной точки зеркального отображения для групп доступности AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Создание конечной точки зеркального отображения базы данных с проверкой подлинности Windows (Transact-SQL)](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Использование сертификатов для конечной точки зеркального отображения базы данных (Transact-SQL)](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [Укажите URL-адрес конечной точки при добавлении или изменении реплики доступности (SQL Server)](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Устранение неполадок с конфигурацией групп доступности AlwaysOn**  
  
-   [Устранение неполадок с конфигурацией групп доступности AlwaysOn &#40;SQL Server&#41;удален](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Устранение неполадок с операцией добавления файла, завершившейся сбоем &#40;группы доступности AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> См. также  
  
-   **Блоги**  
  
     [AlwaysON — HADRON обучающая серия. Использование рабочего пула для баз данных с HADRON](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Блоги группы AlwaysOn SQL Server: Официальный блог по SQL Server AlwaysOn Team](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Блоги инженеров CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Видеоролики**  
  
     [Серия Microsoft SQL Server с кодовым названием «Denali» AlwaysOn, часть 1: вводные сведения о решении следующего поколения по обеспечению высокого уровня доступности](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Серия Microsoft SQL Server с кодовым названием «Denali» AlwaysOn, часть 2: Создание решения критически важных высокого уровня доступности с помощью AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Технические документы**  
  
     [Microsoft SQL Server AlwaysOn Solutions Guide for высокий уровень доступности и аварийного восстановления](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Технические документы Майкрософт Microsoft по SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Технические документы группы консультантов по SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>См. также:  
 [Конечная точка зеркального отображения базы данных (SQL Server)](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Обзор групп доступности AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Предварительные требования, ограничения и рекомендации для групп доступности AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
