---
title: Монитор активности заданий | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.jobactivitymonitor.alljobs.f1
- SQL13.SWB.ACTIVITYMON.F1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 63491a3ba15f9a52e7180597bce7f6295927961f
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65096403"
---
# <a name="job-activity-monitor"></a>Монитор активности заданий
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Эта страница позволяет просматривать текущую активность заданий агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Выберите пункт **Фильтр** для отбора выводимых заданий. Сетка **Активность заданий агента** доступна только для чтения. Щелкните заголовки столбцов для сортировки этой сетки. Для изменения задания дважды щелкните его, чтобы открыть диалоговое окно **Свойства задания** . Щелкните правой кнопкой мыши задание в сетке, чтобы запустить его на выполнение всех его шагов, запуска определенного шага задания, отключения или включения, обновления, удаления задания, просмотра его журнала и просмотра свойств задания. Нажмите кнопку **Обновить** для обновления сетки с текущими данными.  
  
## <a name="options"></a>Параметры  
**Название**  
Имя задания.  
  
**Enabled**  
Указывает, включено задание (**да**) или отключено (**нет**).  
  
**Состояние***  
Текущее состояние задания.  
  
**Результат последнего запуска**  
Состояние задания при последнем запуске.  
  
**Последний запуск**  
Дата и время последнего запуска задания с использованием локальной даты и времени сервера.  
  
**Следующий запуск***  
Дата и время запланированного следующего запуска задания с использованием локальной даты и времени сервера.  
  
**Категория**  
Категория, присвоенная заданию.  
  
**Готово к запуску**  
**Да** , если задание можно запустить; **Нет** , если задание запустить нельзя. Задание нельзя запустить, если оно не содержит шагов или если в нем не указан целевой сервер.  
  
**Назначено**  
**Да** , если заданию назначено расписание; **Нет** , если у задания нет расписания.  
  
* Только члены предопределенной роли сервера sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и группы администраторов сервера могут видеть значения этого столбца. Члены роли SQLAgentOperatorRole не могут видеть значения в этом столбце.  
  
#### <a name="to-open-the-job-activity-monitor"></a>Как открыть монитор активности заданий  
  
-   В **обозревателе объектов**разверните сервер, раскройте узел **Агент SQL Server**, щелкните правой кнопкой мыши **Монитор активности заданий**, затем выберите пункт **Просмотр активности заданий**.  
  
## <a name="see-also"></a>См. также:  
[Наблюдение за активностью заданий](../../ssms/agent/monitor-job-activity.md)  
  
