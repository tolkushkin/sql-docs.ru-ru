---
title: Просмотр или изменение заданий | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 71dd6352aacd7f2183c3d44cd89acba9950b571a
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65103194"
---
# <a name="view-or-modify-jobs"></a>Просмотр или изменение заданий
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Можно просматривать любые созданные задания. После запуска задания можно также просматривать его журнал. Просмотр журнала задания позволяет видеть, где было запущено задание, состояние задания в целом и состояние каждого шага задания. Можно определить, выполнялось ли ранее это задание с ошибками, когда было последнее успешное завершение задания, какой вывод создавался после каждого запуска задания. Члены предопределенной роли сервера **sysadmin** могут просматривать и изменять любые задания, независимо от того, кто их владелец.  
  
> [!NOTE]  
> Для создания журнала заданий, задание должно быть выполнено хотя бы раз. Можно ограничить общий размер журнала заданий, а также размеры журналов отдельных заданий.  
  
Наконец, можно изменить задание, чтобы оно отвечало новым требованиям. Можно менять:  
  
-   параметры ответа;  
  
-   Расписания  
  
-   шаги задания;  
  
-   владельца;  
  
-   категорию задания;  
  
-   целевые серверы (только для многосерверных заданий).  
  
Чтобы убедиться в том, что изменения многосерверных заданий вступили в силу, отправьте изменения в список загрузки, чтобы целевые серверы могли загрузить обновленное задание. Чтобы убедиться, что на целевых серверах находятся самые последние определения заданий, отправьте инструкцию INSERT после обновления многосерверного задания:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Дополнительные сведения см. в разделе [sp_purge_jobhistory (Transact-SQL)](https://msdn.microsoft.com/237f9bad-636d-4262-9bfb-66c034a43e88).  
  
Члены предопределенной роли сервера **sysadmin** могут просматривать определение и журнал любого задания, а также изменять любое задание.  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|||  
|-|-|  
|**Описание**|**Раздел**|  
|Описывает, как просмотреть задания агента [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[View a Job](../../ssms/agent/view-a-job.md)|  
|Описывает, как просматривать журнал заданий агента [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[View the Job History](../../ssms/agent/view-the-job-history.md)|  
|Описывает, как удалить содержимое журнала заданий агента [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Clear the Job History Log](../../ssms/agent/clear-the-job-history-log.md)|  
|Описывает установление ограничений на размер журналов заданий агента [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Resize the Job History Log](../../ssms/agent/resize-the-job-history-log.md)|  
|Описывает, как изменить свойства заданий агента [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Modify a Job](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>См. также:  
[sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
