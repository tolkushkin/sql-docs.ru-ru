---
title: Свойства задания — создание задания (страница "Уведомления") | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5d1cc28e21235dfde9c1b7de00d9c97522bab2cc
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095848"
---
# <a name="job-properties---new-job-notifications-page"></a>Свойства задания — создание задания (страница "Уведомления")
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Используйте эту страницу для установки действий агента [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], выполняемых после завершения задания.  
  
## <a name="options"></a>Параметры  
**Электронная почта**  
Установите этот параметр для отправки электронной почты после завершения задания. Выбрав этот параметр, выберите оператора, которому будет направлено извещение и состояние, вызывающее уведомление: **При успешном завершении задания**, **При ошибке задания** или **При завершении задания**.  
  
**Страница**  
Установите этот параметр для отправки электронной почты на пейджер оператора после завершения задания. Выбрав этот параметр, выберите оператора, которому будет направлено уведомление, и состояние, вызывающее уведомление: **При успешном завершении задания**, **При ошибке задания** или **При завершении задания**.  
  
**Команда Net send**  
Выберите этот параметр для использования команды NET SEND для оповещения оператора о завершении задания. Выбрав этот параметр, выберите оператора, которому будет направлено уведомление, и состояние, вызывающее уведомление: **При успешном завершении задания**, **При ошибке задания** или **При завершении задания**.  
  
**Использовать журнал событий приложений Windows**  
Выберите этот параметр для создания записи в журнале событий приложений при завершении выполнения задания. Выбрав этот параметр, выберите состояние, вызывающее запись в журнал: **При успешном завершении задания**, **При ошибке задания** или **При завершении задания**.  
  
**Автоматически удалить задание**  
Выберите этот параметр для автоматического удаления задания после его завершения. Выбрав этот параметр, выберите состояние, которое вызовет удаление задания: **При успешном завершении задания**, **При ошибке задания** или **При завершении задания**.  
  
## <a name="see-also"></a>См. также:  
[Реализация заданий](../../ssms/agent/implement-jobs.md)  
[Как настроить почту агента SQL Server на использование компонента Database Mail (среда SQL Server Management Studio)](https://msdn.microsoft.com/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
