---
title: Восстановление базы данных master (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 823a6455616b412a41179d831b565e10b3286fb7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875141"
---
# <a name="restore-the-master-database-transact-sql"></a>восстановить базу данных master (Transact-SQL)
  Этот раздел посвящен восстановлению базы данных **master** из полной резервной копии.  
  
### <a name="to-restore-the-master-database"></a>Восстановление базы данных master  
  
1.  Запустите экземпляр сервера в однопользовательском режиме.  
  
     Дополнительные сведения об указании параметра запуска в однопользовательском режиме (**-m**) см. в разделе [Настройка параметров запуска сервера (диспетчер конфигурации SQL Server)](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
2.  Чтобы восстановить полную резервную копию базы данных **master**, используйте следующую инструкцию [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `RESTORE DATABASE master FROM`  *<устройство_резервного_копирования>*  `WITH REPLACE`  
  
     Если задан параметр REPLACE, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] восстанавливает указанную базу данных, даже если база данных с таким же именем уже существует. Существующая база данных в таком случае будет удалена. В однопользовательском режиме рекомендуется вводить инструкцию RESTORE DATABASE в [программе sqlcmd](../../tools/sqlcmd-utility.md). Дополнительные сведения см. в статье [Программа sqlcmd](../scripting/sqlcmd-use-the-utility.md).  
  
    > [!IMPORTANT]  
    >  После восстановления базы данных **master** экземпляр [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] завершает работу и останавливает процесс **sqlcmd** . Перед перезапуском экземпляра сервера удалите параметр запуска однопользовательского режима. Дополнительные сведения см. в разделе [Настройка параметров запуска сервера (диспетчер конфигурации SQL Server)](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
3.  Перезапустите экземпляр сервера и выполните остальные шаги восстановления из копии, такие как восстановление других баз данных, присоединение баз данных и исправление несовпадающих данных пользователей.  
  
## <a name="example"></a>Пример  
 Следующий пример восстанавливает базу данных `master` в определенном по умолчанию экземпляре сервера. В этом примере предполагается, что экземпляр сервера уже работает в однопользовательском режиме. В примере запускается `sqlcmd` и выполняется инструкция `RESTORE DATABASE` , которая восстанавливает полную резервную копию базы данных `master` с дискового устройства: `Z:\SQLServerBackups\master.bak`.  
  
> [!NOTE]
>  Для именованного экземпляра команда **sqlcmd** должна задавать параметр **-S**_\<имя_компьютера>_\\*\<имя_экземпляра>*.  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>См. также  
 [Выполнение полного восстановления базы данных (простая модель восстановления)](complete-database-restores-simple-recovery-model.md)   
 [Выполнение полного восстановления базы данных (модель полного восстановления)](complete-database-restores-full-recovery-model.md)   
 [Диагностика пользователей, утративших связь с учетной записью (SQL Server)](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Присоединение и отсоединение базы данных (SQL Server)](../databases/database-detach-and-attach-sql-server.md)   
 [Перестроение системных баз данных](../databases/system-databases.md)   
 [Параметры запуска службы Database Engine](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [Диспетчер конфигурации SQL Server](../sql-server-configuration-manager.md)   
 [Резервное копирование и восстановление системных баз данных (SQL Server)](back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Запуск SQL Server в однопользовательском режиме](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
