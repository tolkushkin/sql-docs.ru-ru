---
title: Свойства задания — создание задания (страница "Расписания") | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.schedules.f1
ms.assetid: 0b03585b-a510-484d-8a63-9b32459def9c
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b0444310b6c0d226fefe093c281cf9e96c2ca0c4
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095818"
---
# <a name="job-properties---new-job-schedules-page"></a>Свойства задания — новое задание (страница "Расписания")
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Эта страница позволяет просматривать и организовывать расписания для задания агента [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Параметры  
**Список расписаний**  
Список расписаний для данного задания.  
  
**Создать**  
Создает новое расписание. После создания нового расписания оно добавляется к заданию.  
  
**Выбрать**  
Выбор расписания из существующих расписаний. Поскольку у задания и расписания должен быть один и тот же владелец, здесь можно выбирать только из расписаний, которыми владеете.  
  
**Изменить**  
Изменяет выбранное расписание задания.  
  
**Удалить**  
Удалить выбранное расписание из задания. Если больше ни одно задание не использует это расписание, оно удаляется из базы данных.  
  
## <a name="see-also"></a>См. также:  
[Реализация заданий](../../ssms/agent/implement-jobs.md)  
  
