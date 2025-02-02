---
title: Назначения ролей | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- users [Reporting Services]
- roles [Reporting Services]
- role-based security [Reporting Services], role assignments
- groups [Reporting Services]
- security [Reporting Services], role assignments
ms.assetid: 600e112c-1897-48a6-93c0-6e9f3f12dc01
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 556abc4ff00df4393c756f62072254e417653f40
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101866"
---
# <a name="role-assignments"></a>Назначения ролей
  В службах [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] *назначения ролей* определяют доступ к сохраненным элементам и к самому серверу отчетов. Назначение ролей состоит из следующих частей.  
  
-   Защищаемый элемент, доступом к которому нужно управлять. Примеры защищаемых элементов — это папки, отчеты и ресурсы.  
  
-   Учетная запись пользователя или группы, которая может быть проверена службой безопасности Windows или другим механизмом проверки подлинности.  
  
-   Определение ролей, которые определяют набор задач. Примеры определения ролей: **Системный администратор**, **Диспетчер содержимого**и **Издатель**.  
  
 Назначения ролей наследуются в иерархии папок. Назначение ролей, заданное для папки, будет автоматически унаследовано всеми отчетами, общими источниками данных, ресурсами и вложенными папками этой папки. Можно заменить унаследованные параметры безопасности, определив назначения ролей для отдельных элементов. Все части иерархии папок должны быть защищены, по меньшей мере, одним назначением роли. Нельзя создать незащищенный элемент или задать настройки так, чтобы получился незащищенный элемент.  
  
 Следующая диаграмма показывает назначение ролей, которое сопоставляет группу и отдельного пользователя с ролью **Издатель** для папки В.  
  
 ![Диаграмма назначения ролей](../media/report-securityarch.gif "Диаграмма назначения ролей")  
Диаграмма назначения ролей  
  
## <a name="system-level-and-item-level-role-assignments"></a>Назначение ролей на уровне системы и на уровне элемента  
 Безопасность служб [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] на основе ролей организована на нескольких уровнях.  
  
-   Назначения ролей на уровне элемента управляют доступом к отчетам, папкам, моделям отчетов, общим источникам данных и ресурсам в иерархии папок сервера отчетов. Назначения ролей на уровне элемента определяются при создании назначения роли отдельному элементу или корневой папке.  
  
-   Назначения системных ролей разрешают операции, применяемые к серверу в целом (например, управление задачами системного уровня). Назначение системной роли не эквивалентно назначению роли системного администратора. Оно не предоставляет разрешений на полное управление сервером отчетов.  
  
 Назначение системной роли не дает доступа к элементам иерархии папок. Защищенность системы и элемента взаимно исключают друг друга. Для любого данного пользователя или группы может потребоваться создать одновременно назначения роли на уровне системы и на уровне элемента, чтобы предоставить адекватный доступ к серверу отчетов.  
  
## <a name="users-and-groups-in-role-assignments"></a>Пользователи и группы в назначении ролей  
 Учетные записи пользователей и групп, указанные в назначениях ролей, — это доменные учетные записи. Сервер отчетов ссылается (но не создает и не изменяет) на пользователей и группы домена [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (или иной модели безопасности, если используется настраиваемый модуль безопасности).  
  
 Среди всех назначений ролей, применяемых к данному элементу, никакие два не могут указывать одного и того же пользователя или группу. Если учетная запись пользователя входит в учетную запись группы, и существуют назначения ролей для них обеих, пользователю будет доступен комбинированный набор задач для обоих назначений.  
  
 Когда пользователь добавляется в группу, которая уже принимает участие в назначении ролей, необходимо перезагрузить службы IIS, чтобы новые назначения ролей подействовали на этого пользователя.  
  
## <a name="predefined-role-assignments"></a>Предопределенное назначение ролей  
 По умолчанию применяются предопределенные назначения ролей, что позволяет локальным администраторам управлять сервером отчетов. Чтобы предоставить доступ другим пользователям, нужно добавить дополнительные назначения ролей.  
  
 Дополнительные сведения о стандартных назначениях ролей, обеспечивающих безопасность по умолчанию, см. в разделе [Стандартные роли](role-definitions-predefined-roles.md).  
  
## <a name="see-also"></a>См. также  
 [Создание, удаление и изменение ролей (среда Management Studio)](role-definitions-create-delete-or-modify.md)   
 [Предоставление пользователям доступа к серверу отчетов (диспетчер отчетов)](grant-user-access-to-a-report-server.md)   
 [Изменение или удаление назначения ролей (диспетчер отчетов)](role-assignments-modify-or-delete.md)   
 [Задание разрешений для элементов сервера отчетов на сайте SharePoint (службы Reporting Services в режиме интеграции с SharePoint)](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Предоставление разрешений на сервер отчетов в собственном режиме](granting-permissions-on-a-native-mode-report-server.md)  
  
  
