---
title: Журнал ошибок агента SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 362f31bf1daaf842f911bba5781683ac32915373
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095476"
---
# <a name="sql-server-agent-error-log"></a>Журнал ошибок агента SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> Сейчас в [управляемом экземпляре базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) поддерживается большинство функций агента SQL Server (но не все). Подробные сведения см. в статье [Различия T-SQL между управляемым экземпляром базы данных SQL Azure и SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Агент создает журнал ошибок, в который по умолчанию записываются предупреждения и ошибки. В журнале отображаются следующие предупреждения и ошибки:  
  
-   Предупреждающие сообщения, содержащие сведения о потенциальных проблемах, например "Задание \<*имя_задания*> удалено в процессе выполнения".  
  
-   Сообщения об ошибках, обычно требующих вмешательства системного администратора, например «Невозможно начать почтовый сеанс». Сообщения об ошибках могут отправляться конкретному пользователю или на конкретный компьютер с помощью команды **net send**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает до девяти журналов ошибок агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Каждый архивируемый журнал снабжается расширением, указывающим относительный срок давности журнала. Например, расширение .1 указывает на новейший архивированный журнал ошибок, а расширение .9 — на наиболее старый.  
  
По умолчанию сообщения трассировки выполнения не записываются в журнал ошибок агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так как они могут его переполнить. При заполнении журнала ошибок снижается возможность выбора и анализа более сложных ошибок. Так как ведение журнала увеличивает нагрузку на сервер, важно правильно оценить эффект, получаемый при захвате сообщений трассировки выполнения в журнал ошибок. В общем случае захват всех сообщений будет наилучшим вариантом только при отладке конкретной проблемы.  
  
Когда агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] остановлен, размещение журнала ошибок агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно изменить. Если журнал ошибок пустой, открыть его невозможно. Журнал агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно в любое время циклически перезаписывать без остановки агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Просмотр журнала ошибок агента SQL Server**  
  
-   [Просмотр журнала ошибок агента SQL Server (среда SQL Server Management Studio)](../../ssms/agent/view-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**Переименование журнала ошибок агента SQL Server**  
  
-   [Переименование журнала ошибок агента SQL Server (среда SQL Server Management Studio)](../../ssms/agent/rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**Отправка сообщений об ошибках агента SQL Server**  
  
-   [Send SQL Server Agent Error Messages](../../ssms/agent/send-sql-server-agent-error-messages.md)  
  
**Запись сообщений трассировки выполнения в журнал ошибок агента SQL Server**  
  
-   [Запись сообщений трассировки выполнения в журнал ошибок агента SQL Server (среда SQL Server Management Studio)](../../ssms/agent/write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
