---
title: Свойства задания — создание задания (страница "Общие") | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.general.f1
ms.assetid: b6832840-1c18-4db8-94fc-080db880ae9f
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ff791be08180505689e5ccff235bac377a296cce
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095807"
---
# <a name="job-properties---new-job-general-page"></a>Свойства задания — создание задания (страница "Общие")
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Эта страница используется для просмотра и изменения общих свойств задания агента [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Параметры  
**Название**  
Изменение имени задания.  
  
**Владелец**  
Выбор владельца задания.  
  
**Категория**  
Выбор категории задания.  
  
**...**  
Просмотр заданий в выбранной категории.  
  
**Описание**  
Изменение описания задания.  
  
**Enabled**  
Включение задания. Если задание не включено, оно не будет выполняться по расписанию или предупреждению, но может быть запущено с помощью хранимой процедуры **sp_start_job** .  
  
**Source**  
Отображается главный сервер для задания. Доступно только на странице **Свойства задания — общие** .  
  
**Создан**  
Отображаются дата и время создания задания. Доступно только на странице **Свойства задания — общие** .  
  
**Изменено**  
Отображаются дата и время последнего изменения задания. Доступно только на странице **Свойства задания — общие** .  
  
**Последнее выполнение**  
Отображаются дата и время последнего запуска задания. Доступно только на странице **Свойства задания — общие** .  
  
**Просмотр журнала заданий**  
Просмотр журнала заданий. Доступно только на странице **Свойства задания — общие** .  
  
## <a name="see-also"></a>См. также:  
[Реализация заданий](../../ssms/agent/implement-jobs.md)  
[Категории заданий — управление категориями заданий](../../ssms/agent/job-categories-manage-job-categories.md)  
  
