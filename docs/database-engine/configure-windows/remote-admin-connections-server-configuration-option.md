---
title: Параметр конфигурации сервера "remote admin connections" | Документы Майкрософт
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- administrator connections [SQL Server]
- DAC
- connections [SQL Server], dedicated administrator
- remote admin connections option
- dedicated administrator connections [SQL Server]
ms.assetid: bf32b60a-7a48-401f-b6be-b5e2e46c413f
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 43fc46517ffbf639cfc9328510ad4550e048cbc9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772064"
---
# <a name="remote-admin-connections-server-configuration-option"></a>Параметр конфигурации сервера «remote admin connections»
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляет выделенное административное соединение (DAC). Такое подключение позволяет администратору получать доступ к серверу для выполнения диагностических функций или инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] или решения проблем на сервере, даже когда сервер заблокирован или работает в аварийном состоянии и не отвечает на соединение компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . По умолчанию выделенные административные соединения доступны только с клиента на сервер. Чтобы разрешить клиентским приложениям на удаленных компьютерах подключение DAC, используйте параметр remote admin connections хранимой процедуры sp_configure.  
  
 По умолчанию DAC ожидает соединения только на IP-адресе обратной связи (127.0.0.1), порт 1434. Если TCP-порт 1434 недоступен, то TCP-порт динамически назначается при запуске компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Если на компьютере установлено более одного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , необходимо проверить номер TCP-порта в журнале ошибок.  
  
 В следующей таблице приведены возможные значения параметра remote admin connections.  
  
|Значение|Описание|  
|-----------|-----------------|  
|0|Означает, что разрешены только локальные соединения через DAC.|  
|1|Означает, что разрешены удаленные соединения через DAC.|  
  
## <a name="example"></a>Пример  
 В следующем примере показано подключение через DAC с удаленного компьютера.  
  
```  
sp_configure 'remote admin connections', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [Диагностическое соединение для администраторов баз данных](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
