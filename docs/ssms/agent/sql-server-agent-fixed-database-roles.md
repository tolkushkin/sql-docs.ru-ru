---
title: Предопределенные роли базы данных агента SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c7f65ad3957280953faa58792ea39e48ce16f20e
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089709"
---
# <a name="sql-server-agent-fixed-database-roles"></a>Предопределенные роли базы данных агента SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имеет следующие предопределенные роли базы данных **msdb** , предоставляющие администраторам возможности более точного управления доступом к агенту [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Далее приводятся роли, в порядке от имеющих наименьшие права к имеющим большие права доступа.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Если пользователи, не являющиеся членами одной из этих ролей, подключены к серверу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], узел **Агент SQL Server** в обозревателе объектов не виден. Для использования агента **пользователь должен быть членом одной из этих предопределенных ролей базы данных или членом предопределенной роли сервера** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>Разрешения предопределенных ролей базы данных агента SQL Server  
Разрешения роли базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имеют вложенную структуру: роли с более широкими правами наследуют разрешения ролей с менее широкими правами на объекты агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (включающие в себя предупреждения, операторы, задания, расписания и учетные записи-посредники). Например, если членам роли с наименее широкими правами **SQLAgentUserRole** предоставлен доступ к учетной записи-посреднику proxy_A, члены ролей **SQLAgentReaderRole** и **SQLAgentOperatorRole** автоматически имеют доступ к этой учетной записи, даже если доступ не был им явно предоставлен. Это может вызывать некоторые проблемы с безопасностью, которые обсуждаются в следующих разделах, где рассматривается каждая из указанных ролей.  
  
### <a name="sqlagentuserrole-permissions"></a>Разрешения роли SQLAgentUserRole  
Роль**SQLAgentUserRole** имеет наименьшие права из всех предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Она имеет разрешения только на операторы, локальные задания и расписания заданий. Члены роли **SQLAgentUserRole** имеют разрешения только на локальные задания и расписания заданий, которыми они владеют. Они не могут использовать многосерверные задания (задания с главным и целевым серверами) и изменять владение заданиями для получения доступа к заданиям, которыми не владеют в настоящее время. Члены роли**SQLAgentUserRole** могут просматривать список доступных учетных записей-посредников только в диалоговом окне **Свойства шага задания** среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. В обозревателе объектов среды **членам роли** SQLAgentUserRole [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] виден только узел **Задания**.  
  
> [!IMPORTANT]  
> При предоставлении доступа к прокси-объектам участникам **ролей** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agentdatabaserole**, оцените, как это повлияет на безопасность. Члены ролей **SQLAgentReaderRole** и **SQLAgentOperatorRole** автоматически являются членами роли **SQLAgentUserRole**. Это означает, что члены ролей **SQLAgentReaderRole** и **SQLAgentOperatorRole** имеют доступ ко всем учетным записям-посредникам агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которые были предоставлены роли **SQLAgentUserRole** , и могут использовать эти учетные записи.  
  
В следующей таблице приводится сводка разрешений роли **SQLAgentUserRole** на объекты агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Действие|Операторы|Локальные задания<br /><br />(только собственные задания)|Расписания заданий<br /><br />(только расписания собственных заданий)|Учетные записи-посредники|  
|----------|-------------|-----------------------------------|-------------------------------------------|-----------|  
|Создать/изменить/удалить|нет|Да<br /><br />Нельзя изменить владельца задания.|Да|нет|  
|Просмотреть список (перечислить)|Да<br /><br />Можно получить список доступных операторов для использования в процедуре **sp_notify_operator** и в диалоговом окне **Свойства задания** среды Management Studio.|Да|Да|Да<br /><br />Список учетных записей-посредников доступен только в диалоговом окне **Свойства шага задания** среды Management Studio.|  
|Включить/выключить|нет|Да|Да|Неприменимо|  
|Просмотреть свойства|нет|Да|Да|нет|  
|Выполнить/остановить/начать|Неприменимо|Да|Неприменимо|Неприменимо|  
|Просмотреть журнал заданий|Неприменимо|Да|Неприменимо|Неприменимо|  
|Удалить журнал заданий|Неприменимо|нет<br /><br />Для удаления журнала принадлежащих им заданий членам роли **SQLAgentUserRole** должно быть явно предоставлено разрешение EXECUTE на процедуру **sp_purge_jobhistory** . Они не могут удалить журналы никаких других заданий.|Неприменимо|Неприменимо|  
|Присоединить/отсоединить|Неприменимо|Неприменимо|Да|Неприменимо|  
  
### <a name="sqlagentreaderrole-permissions"></a>Разрешения SQLAgentReaderRole  
Роль**SQLAgentReaderRole** имеет все разрешения роли **SQLAgentUserRole** , а также разрешения на просмотр списка имеющихся многосерверных заданий, их свойств и их журнала. Члены этой роли могут также просматривать не только информацию о заданиях и расписаниях заданий, которыми они владеют, но и список всех имеющихся заданий, расписаний заданий и их свойств. Члены роли**SQLAgentReaderRole** не могут изменять владельцев заданий для получения доступа к не принадлежащим им заданиям. В обозревателе объектов среды **членам роли** SQLAgentReaderRole [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] виден только узел **Задания**.  
  
> [!IMPORTANT]  
> При предоставлении доступа к прокси-объектам участникам **ролей** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agentdatabaserole**, оцените, как это повлияет на безопасность. Члены роли **SQLAgentReaderRole** автоматически являются членами роли **SQLAgentUserRole**. Это означает, что члены роли **SQLAgentReaderRole** имеют доступ ко всем учетным записям-посредникам агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которые были предоставлены роли **SQLAgentUserRole** , и могут использовать эти учетные записи.  
  
В следующей таблице приводится сводка разрешений роли **SQLAgentReaderRole** на объекты агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Действие|Операторы|Локальные задания|Многосерверные задания|Расписания заданий|Учетные записи-посредники|  
|----------|-------------|--------------|--------------------|-----------------|-----------|  
|Создать/изменить/удалить|нет|Да (только собственные задания)<br /><br />Нельзя изменить владельца задания.|нет|Да (только расписания собственных заданий)|нет|  
|Просмотреть список (перечислить)|Да<br /><br />Можно получить список доступных операторов для использования в процедуре **sp_notify_operator** и в диалоговом окне **Свойства задания** среды Management Studio.|Да|Да|Да|Да<br /><br />Список учетных записей-посредников доступен только в диалоговом окне **Свойства шага задания** среды Management Studio.|  
|Включить/выключить|нет|Да (только собственные задания)|нет|Да (только расписания собственных заданий)|Неприменимо|  
|Просмотреть свойства|нет|Да|Да|Да|нет|  
|Редактировать свойства|нет|Да (только собственные задания)|нет|Да (только расписания собственных заданий)|нет|  
|Выполнить/остановить/начать|Неприменимо|Да (только собственные задания)|нет|Неприменимо|Неприменимо|  
|Просмотреть журнал заданий|Неприменимо|Да|Да|Неприменимо|Неприменимо|  
|Удалить журнал заданий|Неприменимо|нет<br /><br />Для удаления журнала принадлежащих им заданий членам роли **SQLAgentReaderRole** должно быть явно предоставлено разрешение EXECUTE на процедуру **sp_purge_jobhistory** . Они не могут удалить журналы никаких других заданий.|нет|Неприменимо|Неприменимо|  
|Присоединить/отсоединить|Неприменимо|Неприменимо|Неприменимо|Да (только расписания собственных заданий)|Неприменимо|  
  
### <a name="sqlagentoperatorrole-permissions"></a>Разрешения роли SQLAgentOperatorRole  
Роль**SQLAgentOperatorRole** имеет наибольшие права из всех предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Она имеет также все права ролей **SQLAgentUserRole** и **SQLAgentReaderRole**. Члены этой роли могут также просматривать свойства операторов и учетных записей-посредников, просматривать список доступных учетных записей-посредников и предупреждений на сервере.  
  
Члены роли**SQLAgentOperatorRole** имеют дополнительные разрешения на локальные задания и расписания. Они могут выполнять, останавливать или запускать все локальные задания, они могут удалять журнал заданий для любого локального задания на сервере. Они также могут включать и выключать все локальные задания и расписания на сервере. Для включения и выключения локальных заданий или расписаний члены этой роли должны использовать хранимые процедуры **sp_update_job** и **sp_update_schedule**. Члены роли **@enabled** могут указывать только параметры, задающие имя задания или расписания, либо идентификатор и параметр **SQLAgentOperatorRole**. Если они задают какие-либо другие параметры, выполнение хранимой процедуры завершается с ошибкой. Члены роли**SQLAgentOperatorRole** не могут изменять владельцев заданий для получения доступа к не принадлежащим им заданиям.  
  
В обозревателе объектов среды **членам роли**SQLAgentOperatorRole **видны узлы**Задания **,** Предупреждения **,** Операторы [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] и **Учетные записи-посредники**. Членам этой роли не доступен только узел **Журналы ошибок** .  
  
> [!IMPORTANT]  
> При предоставлении доступа к прокси-объектам участникам **ролей** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agentdatabaserole**, оцените, как это повлияет на безопасность. Члены роли **SQLAgentOperatorRole** автоматически являются членами ролей **SQLAgentUserRole** и **SQLAgentReaderRole**. Это означает, что члены роли **SQLAgentOperatorRole** имеют доступ ко всем учетным записям-посредникам агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которые были предоставлены роли **SQLAgentUserRole** или **SQLAgentReaderRole** , и могут использовать эти учетные записи.  
  
В следующей таблице приводится сводка разрешений роли **SQLAgentOperatorRole** на объекты агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Действие|видны узлы|Операторы|Локальные задания|Многосерверные задания|Расписания заданий|Учетные записи-посредники|  
|----------|----------|-------------|--------------|--------------------|-----------------|-----------|  
|Создать/изменить/удалить|нет|нет|Да (только собственные задания)<br /><br />Нельзя изменить владельца задания.|нет|Да (только расписания собственных заданий)|нет|  
|Просмотреть список (перечислить)|Да|Да<br /><br />Можно получить список доступных операторов для использования в процедуре **sp_notify_operator** и в диалоговом окне **Свойства задания** среды Management Studio.|Да|Да|Да|Да|  
|Включить/выключить|нет|нет|Да<br /><br />**SQLAgentOperatorRole** могут включать и выключать не принадлежащие им локальные задания с помощью хранимой процедуры **sp_update_job** и заданием значений для параметров **@enabled** и **@job_id** (или **@job_name**). Если член этой роли определяет другие параметры для этой хранимой процедуры, выполнение завершится неудачно.|нет|Да<br /><br />**SQLAgentOperatorRole** могут включать и выключать не принадлежащие им расписания с помощью хранимой процедуры **sp_update_schedule** и заданием значений для параметров **@enabled** и **@schedule_id** (или **@name**). Если член этой роли определяет другие параметры для этой хранимой процедуры, выполнение завершится неудачно.|Неприменимо|  
|Просмотреть свойства|Да|Да|Да|Да|Да|Да|  
|Редактировать свойства|нет|нет|Да (только собственные задания)|нет|Да (только расписания собственных заданий)|нет|  
|Выполнить/остановить/начать|Неприменимо|Неприменимо|Да|нет|Неприменимо|Неприменимо|  
|Просмотреть журнал заданий|Неприменимо|Неприменимо|Да|Да|Неприменимо|Неприменимо|  
|Удалить журнал заданий|Неприменимо|Неприменимо|Да|нет|Неприменимо|Неприменимо|  
|Присоединить/отсоединить|Неприменимо|Неприменимо|Неприменимо|Неприменимо|Да (только расписания собственных заданий)|Неприменимо|  
  
## <a name="assigning-users-multiple-roles"></a>Назначение пользователям нескольких ролей  
Члены предопределенной роли сервера **sysadmin** имеют доступ ко всем функциям агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Если пользователь не является членом роли **sysadmin** , но является членом нескольких предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , важно помнить о вложенной модели разрешений этих ролей. Так как роли с более широкими разрешениями всегда содержат все разрешения, предоставленные ролям с менее широкими разрешениями, пользователь, являющийся членом нескольких ролей, автоматически имеет разрешения, связанные с ролью с наиболее широкими разрешениями из всех ролей, членом которых является пользователь.  
  
## <a name="see-also"></a>См. также:  
[Обеспечение безопасности агента SQL Server](../../ssms/agent/implement-sql-server-agent-security.md)  
[sp_update_job (Transact-SQL)](https://msdn.microsoft.com/cbdfea38-9e42-47f3-8fc8-5978b82e2623)  
[sp_update_schedule (Transact-SQL)](https://msdn.microsoft.com/97b3119b-e43e-447a-bbfb-0b5499e2fefe)  
[sp_notify_operator (Transact-SQL)](https://msdn.microsoft.com/c440f5c9-9884-4196-b07c-55d87afb17c3)  
[sp_purge_jobhistory (Transact-SQL)](https://msdn.microsoft.com/237f9bad-636d-4262-9bfb-66c034a43e88)  
  
