---
title: Субъекты (ядро СУБД) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.selectroll.f1
- sql12.swb.databaseuser.permissions.user.f1--May use common.permissions
helpviewer_keywords:
- certificates [SQL Server], principals
- roles [SQL Server], principals
- permissions [SQL Server], principals
- '##MS_SQLAuthenticatorCertificate##'
- principals [SQL Server]
- '##MS_SQLResourceSigningCertificate##'
- groups [SQL Server], principals
- '##MS_AgentSigningCertificate##'
- authentication [SQL Server], principals
- schemas [SQL Server], principals
- principals [SQL Server], about principals
- security [SQL Server], principals
- users [SQL Server], principals
- '##MS_SQLReplicationSigningCertificate##'
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 54aab33e754331482ef154d9172f0e41cd251db0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011915"
---
# <a name="principals-database-engine"></a>Субъекты (компонент Database Engine)
  *Субъекты* — это сущности, которые могут запрашивать ресурсы [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Как и другие компоненты модели авторизации [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , участников можно иерархически упорядочить. Область влияния участника зависит от области определения участника: Windows, сервер, база данных; и того, коллективный это участник или коллекции. Имя входа Windows является примером индивидуального (неделимого) субъекта, а группа Windows — коллективного. Каждый субъект имеет идентификатор безопасности (SID).  
  
 **Субъекты уровня Windows**  
  
-   Имя входа домена Windows  
  
-   Локальное имя входа Windows  
  
 **Субъекты**-**уровня** **principals**  
  
-   Имя входа [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Роль сервера  
  
 **Участники уровня базы данных**  
  
-   Пользователь базы данных  
  
-   Роль базы данных  
  
-   Роль приложения  
  
## <a name="the-sql-server-sa-login"></a>Имя входа «sa» SQL Server  
 Имя входа [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sa является субъектом уровня сервера. По умолчанию оно создается при установке экземпляра. Начиная с версии [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]базой данных для имени входа sa по умолчанию является master. Это поведение было изменено по сравнению с предыдущими версиями [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="public-database-role"></a>Роль базы данных public  
 Каждый пользователь базы данных является членом роли базы данных public. Если пользователю не были предоставлены или запрещены особые разрешения на доступ к защищаемому объекту, то он наследует для него разрешения роли public.  
  
## <a name="informationschema-and-sys"></a>INFORMATION_SCHEMA и sys  
 Каждая база данных включает в себя две сущности, которые отображаются как пользователи в представлениях каталога: INFORMATION_SCHEMA и sys. Они необходимы для работы [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; эти пользователи не являются субъектами и не могут быть изменены или удалены.  
  
## <a name="certificate-based-sql-server-logins"></a>Имена входа SQL Server на основе сертификата  
 Субъекты уровня сервера, имеющие имена, заключенные в хэш-символы (##), — только для внутреннего системного пользования. Следующие участники создаются из сертификатов при установке [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и не должны удаляться.  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## <a name="the-guest-user"></a>Пользователь-гость  
 Каждая база данных включает в себя пользователя **guest**. Разрешения, предоставленные пользователю **guest** , наследуются пользователями, которые имеют доступ к базе данных, но не обладают учетной записью пользователя в ней. **Гостевой** пользователя нельзя удалить, но его можно отключить, отменив его в `CONNECT` разрешение. `CONNECT` Разрешение можно отменить, выполнив `REVOKE CONNECT FROM GUEST` в любой базе данных, кроме master или tempdb.  
  
## <a name="client-and-database-server"></a>Клиент и сервер базы данных  
 По определению клиент и сервер базы данных являются защищаемыми субъектами безопасности. Данные сущности могут пройти взаимную проверку подлинности перед установкой безопасного сетевого соединения. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] поддерживает [Kerberos](https://go.microsoft.com/fwlink/?LinkId=100758) протокола проверки подлинности, который определяет, как клиенты взаимодействуют со службой проверки подлинности в сети.  
  
## <a name="related-tasks"></a>Связанные задачи  
 Данный раздел электронной документации по [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] содержит следующие подразделы.  
  
-   [Инструкции по управлению именами входа, пользователями и схемами](managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [Роли уровня сервера](server-level-roles.md)  
  
-   [Роли уровня базы данных](database-level-roles.md)  
  
-   [Роли приложений](application-roles.md)  
  
## <a name="see-also"></a>См. также  
 [Обеспечение безопасности SQL Server](../securing-sql-server.md)   
 [sys.database_principals (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)   
 [sys.server_principals (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)   
 [sys.sql_logins (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)   
 [sys.database_role_members (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)   
 [Роли уровня сервера](server-level-roles.md)   
 [Роли уровня базы данных](database-level-roles.md)  
  
  
