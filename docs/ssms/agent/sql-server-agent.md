---
title: Агент SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, about SQL Server Agent
- automatic administration steps
ms.assetid: 8d1dc600-aabb-416f-b3af-fbc9fccfd0ec
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6788b27f4260905c18487866d22fe9434f34b5ff
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65097552"
---
# <a name="sql-server-agent"></a>Агент SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] — это служба Microsoft Windows, выполняющая запланированные административные задачи, которые называются *заданиями* в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
**В этом разделе**  
  
-   [Преимущества агента SQL Server](#Benefits)  
  
-   [Компоненты агента SQL Server](#Components)  
  
-   [Безопасность при администрировании агента SQL Server](#Security)  
  
## <a name="Benefits"></a>Преимущества агента SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] использует [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для хранения сведений о заданиях. Задание состоит из одного или нескольких шагов. Каждый шаг содержит собственную задачу, например создание резервной копии базы данных.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может выполнять задания по расписанию в ответ на определенное событие или по требованию. Например, можно автоматизировать задачу создания резервной копии всех серверов компании, чтобы она выполнялась ежедневно по окончании рабочего дня. Запланируйте запуск резервного копирования после 22:00 с понедельника по пятницу; если во время создания резервной копии возникает проблема, агент SQL Server регистрирует соответствующее событие и выдает уведомление.  
  
> [!NOTE]  
> Служба агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] по умолчанию отключена, если во время установки [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] явно не выбран автоматический запуск службы.  
  
## <a name="Components"></a>Компоненты агента SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] использует следующие компоненты, чтобы определить задачи для выполнения, время для выполнения задач и порядок уведомления об успешном или неудачном завершении задач.  
  
### <a name="jobs"></a>Задания  
*Задание* — это указанная последовательность действий, выполняемых агентом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Используйте задания, чтобы определить задачу управления, которую можно выполнить однажды или неоднократно и контролировать на предмет успешного или неудачного выполнения. Задание может выполняться на одном локальном сервере или на нескольких удаленных серверах.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которые выполнялись во время отработки отказа на экземпляре отказоустойчивого кластера [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , не возобновляются после отработки отказа и переключения на другой узел отказоустойчивого кластера. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Задания агента, которые выполнялись во время приостановки работы узла Hyper-V, не возобновляются, если приостановка вызывает отработку отказа с переходом на другой узел. Задания, выполнение которых было начато, но не завершилось в связи с событием отработки отказа, регистрируются в журнале как начатые, но дополнительных записей журнала о завершении или сбое нет. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выглядят как незавершенные.  
  
Выполнять задания можно несколькими способами:  
  
-   по одному или нескольким расписаниям;  
  
-   в ответ на одно или несколько предупреждений;  
  
-   Посредством выполнения хранимой процедуры sp_start_job.  
  
Каждое действие в задании является *шагом задания*. Например шаг задания может состоять из выполнения инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] , выполнения пакета служб [!INCLUDE[ssIS](../../includes/ssis_md.md)] или выдачи команды серверу служб Analysis Services. Шагами задания управляют как частью задания.  
  
Каждый шаг задания выполняется в указанном контексте безопасности. Для шагов заданий, использующих [!INCLUDE[tsql](../../includes/tsql-md.md)], применяйте инструкцию EXECUTE AS, чтобы указать контекст безопасности для шага задания. Для других типов шагов заданий используйте учетную запись-посредник, чтобы указать контекст безопасности для шага задания.  
  
### <a name="schedules"></a>Расписания  
*Расписание* определяет время выполнения задания. Сразу несколько заданий могут выполняться по одному и тому же расписанию, а несколько расписаний могут применяться к одному и тому же заданию. Расписание может определить следующие условия для времени выполнения задания:  
  
-   При каждом запуске агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   каждый раз, когда использование ЦП компьютера будет достигать уровня, который определен как уровень простоя;  
  
-   однажды, в указанные дату и время;  
  
-   Согласно повторяющемуся расписанию.  
  
Дополнительные сведения см. в разделе [Создание и присоединение расписаний к заданиям](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
### <a name="alerts"></a>видны узлы  
*Предупреждение* — это автоматический ответ на наступление указанного события. Например, событие может быть заданием, которое начинает выполняться, или системным ресурсом, достигшим указанного порогового значения. Пользователь определяет условия, при которых выдается предупреждение.  
  
Предупреждение может быть реакцией на одно из следующих условий:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] события  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] условия производительности;  
  
-   события инструментария управления Microsoft Windows (WMI) на компьютере, где работает агент SQL Server;  
  
Предупреждение может выполнять следующие действия:  
  
-   Уведомить один или несколько операторов  
  
-   Осуществить запуск задания  
  
Дополнительные сведения см. в статье [Предупреждения](../../ssms/agent/alerts.md).  
  
### <a name="operators"></a>Операторы  
*Оператор* определяет контактные сведения о лице, ответственном за обслуживание одного или нескольких экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. В некоторых организациях обязанности оператора возлагаются на одно лицо. В организациях, использующих несколько серверов, обязанности оператора могут быть разделены между несколькими лицами. Оператор не обладает данными безопасности и не определяет субъекта безопасности.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может уведомлять операторов о предупреждениях одним или несколькими способами из нижеследующих:  
  
-   электронная почта;  
  
-   пейджер (через электронную почту);  
  
-   **команда net send.**  
  
> [!NOTE]  
> Чтобы сделать возможной отправку уведомлений с помощью **net send**, служба Windows Messenger должна быть запущена на компьютере, где работает агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
> Режимы отправки уведомлений с помощью пейджера и команды **net send** будут удалены из агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в следующей версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Старайтесь не использовать эти функции в новых разработках и предусмотрите соответствующие изменения в приложениях, которые используют их в настоящее время.  
  
Для отправки операторам уведомлений по электронной почте или на пейджер необходимо настроить агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для использования компонента Database Mail. Дополнительные сведения см. в разделе [Database Mail](../../relational-databases/database-mail/database-mail.md).  
  
Можно определить оператора как псевдоним для группы лиц. Таким способом все члены этого псевдонима будут уведомлены одновременно. Дополнительные сведения см. в статье [Операторы](../../ssms/agent/operators.md).  
  
## <a name="Security"></a>Безопасность при администрировании агента SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] использует предопределенные роли базы данных **SQLAgentUserRole**, **SQLAgentReaderRole**и **SQLAgentOperatorRole** в базе данных **msdb** для управления доступом к агенту [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для пользователей, не входящих в предопределенную роль сервера **sysadmin** . Помимо этих предопределенных ролей базы данных, подсистемы и учетные записи-посредники позволяют администраторам базы данных гарантировать, что каждый шаг задания выполняется с минимальными разрешениями, необходимыми для выполнения задачи.  
  
### <a name="roles"></a>Роли  
Доступ к агенту **имеют члены предопределенных ролей базы данных**SQLAgentUserRole **,** SQLAgentReaderRole **и** SQLAgentOperatorRole **в базе данных**msdb **, а также члены предопределенной роли сервера** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Пользователь, не принадлежащий ни к одной из этих ролей, не может использовать агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения о ролях, используемых агентом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , см. в разделе [Обеспечение безопасности агента SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
### <a name="subsystems"></a>Подсистемы  
Подсистема — это предопределенный объект, который содержит функции, доступные шагу задания. Каждая учетная запись-посредник имеет доступ к одной или нескольким подсистемам. Подсистемы обеспечивают безопасность, поскольку разграничивают доступ учетных записей-посредников к функциям. Каждый шаг задания выполняется в контексте учетной записи-посредника, за исключением этапов задания [!INCLUDE[tsql](../../includes/tsql-md.md)] . На этапах задания [!INCLUDE[tsql](../../includes/tsql-md.md)] применяйте команду EXECUTE AS, чтобы задать контекст безопасности для владельца задания.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] определяет подсистемы, перечисленные в следующей таблице:  
  
|Имя подсистемы|Описание|  
|--------------|-----------|  
|Скрипт Microsoft ActiveX|Выполните шаг задания со скриптом ActiveX.<br /><br />**Предупреждение** Подсистема сценариев ActiveX будет удалена из агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в последующей версии [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется.|  
|Операционная система (**CmdExec**)|Запустите исполняемую программу.|  
|PowerShell|Выполните шаг задания со скриптом PowerShell.|  
|Распространитель репликации|Выполните шаг задания, на котором активируется агент распространителя репликации.|  
|Репликация слиянием|Выполните шаг задания, на котором активируется агент репликации слиянием.|  
|Агент чтения очереди репликации|Выполните шаг задания, на котором активируется агент чтения очереди репликации.|  
|Моментальный снимок репликации|Выполните шаг задания, на котором активируется агент моментальных снимков.|  
|Агент чтения журнала транзакций репликации|Выполните шаг задания, на котором активируется агент чтения журнала.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Command|Выполните команду служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] .|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Запрос|Выполните запрос служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] .|  
|[!INCLUDE[ssIS](../../includes/ssis_md.md)] выполнение пакетов служб|Выполните пакет служб [!INCLUDE[ssIS](../../includes/ssis_md.md)] .|  
  
> [!NOTE]  
> Поскольку в шагах задания [!INCLUDE[tsql](../../includes/tsql-md.md)] учетные записи-посредники не используются, какие-либо подсистемы агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для шагов задания [!INCLUDE[tsql](../../includes/tsql-md.md)] отсутствуют.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] применяет ограничения подсистемы принудительно, даже если обычно субъект безопасности для учетной записи-посредника имеет разрешение на выполнение задачи на шаге задания. Например, пользователь, являющийся членом предопределенной роли сервера sysadmin, не сможет выполнить шаг задания служб [!INCLUDE[ssIS](../../includes/ssis_md.md)] , если его учетная запись-посредник не имеет доступа к подсистеме служб [!INCLUDE[ssIS](../../includes/ssis_md.md)] , несмотря на то, что пользователь может выполнять пакеты служб [!INCLUDE[ssIS](../../includes/ssis_md.md)] .  
  
### <a name="proxies"></a>Учетные записи-посредники  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для управления контекстами безопасности использует учетные записи-посредники. Учетная запись-посредник может быть использована на нескольких шагах задания. Создавать учетные записи-посредники могут члены предопределенной роли сервера **sysadmin** .  
  
Каждой учетной записи-посреднику соответствует учетная запись системы безопасности. и может быть связана с множеством подсистем и множеством имен входа. Учетная запись-посредник может применяться только для шагов задания, которые используют связанную с этой учетной записью-посредником подсистему. Чтобы создать шаг задания, использующий определенную учетную запись-посредник, владелец задания должен либо использовать связанное с ней имя входа, либо быть членом роли, имеющей неограниченный доступ к учетным записям-посредникам. Члены предопределенной роли сервера **sysadmin** имеют неограниченный доступ к учетным записям-посредникам. Члены ролей **SQLAgentUserRole**, **SQLAgentReaderRole**и **SQLAgentOperatorRole** могут использовать только учетные записи-посредники, на которые им был предоставлен особый доступ. Каждому пользователю, входящему в одну из предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , необходимо предоставить доступ к конкретным учетным записям-посредникам, чтобы пользователь мог создавать шаги задания, которые будут использовать эти учетные записи-посредники.  
  
## <a name="related-tasks"></a>Связанные задачи  
Используйте следующие шаги для настройки агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для автоматического администрирования [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
1.  Определите, какие административные задачи или события сервера происходят регулярно, а также можно ли эти задачи или события администрировать программным путем. Подходящей для автоматизации является такая задача, которая включает предсказуемую последовательность шагов и выполняется в определенное время или в ответ на определенное событие.  
  
2.  Определите набор заданий, расписаний, предупреждений и операторов, используя среду [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], скрипты [!INCLUDE[tsql](../../includes/tsql-md.md)] или управляющие объекты (SMO) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в разделе [Создание заданий](../../ssms/agent/create-jobs.md).  
  
3.  Запустите назначенные задания агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
> В экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]по умолчанию служба [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имеет имя SQLSERVERAGENT. В именованных экземплярах служба агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имеет имя SQLAgent$*имя_экземпляра*.  
  
Если запущено несколько экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], то чтобы автоматизировать общие для всех экземпляров задания, можно использовать администрирование нескольких серверов. Дополнительные сведения см. в статье [Автоматизация администрирования в масштабах предприятия](../../ssms/agent/automated-administration-across-an-enterprise.md).  
  
Используйте следующие задачи, чтобы начать работу с агентом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Описание|Раздел|  
|-----------|-----|  
|Содержит инструкции по настройке агента SQL Server.|[Настройка агента SQL Server](../../ssms/agent/configure-sql-server-agent.md)|  
|Описывает запуск, остановку и приостановку службы агента SQL Server.|[Запуск, остановка или приостановка службы агента SQL Server](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)|  
|Описывает вопросы задания учетных записей для службы агента SQL Server.|[Выбор учетной записи для службы агента SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)|  
|Описывает использование журнала ошибок агента SQL Server.|[Журнал ошибок агента SQL Server](../../ssms/agent/sql-server-agent-error-log.md)|  
|Содержит инструкции по использованию объектов производительности.|[Использование объектов производительности](../../ssms/agent/use-performance-objects.md)|  
|Описывает мастер планов обслуживания программу, которая используется для создания заданий, оповещений и операторов для автоматизации администрирования экземпляра SQL Server.|[Использование мастера планов обслуживания](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|  
|Описывает автоматизацию задач администрирования с помощью агента SQL Server.|[Задачи автоматизированного администрирования (агент SQL Server)](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)|  
  
## <a name="see-also"></a>См. также:  
[Настройка контактной зоны](../../relational-databases/security/surface-area-configuration.md)  
  
