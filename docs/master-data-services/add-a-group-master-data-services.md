---
title: Добавление группы (службы Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- groups [Master Data Services], adding
- adding groups [Master Data Services]
ms.assetid: c7a88381-3b2c-4af7-9cf7-3a930c1abdee
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 236596354139971c6fcceebff759a57f807cdefa
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484860"
---
# <a name="add-a-group-master-data-services"></a>Добавление группы (службы Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Чтобы начать процесс назначения разрешений для веб-приложения, нужно добавить группу в список **Группы** служб [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Прежде чем пользователь группы сможет получить доступ к [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], группе необходимо предоставить разрешения для одной или нескольких функциональных областей и объектов модели.  
  
## <a name="prerequisites"></a>предварительные требования  
 Для выполнения этой процедуры:  
  
-   необходимо иметь разрешение на доступ к функциональной области **Разрешения пользователей и групп** ;  
  
### <a name="to-add-a-group"></a>Добавление группы  
  
1.  В среде [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]щелкните **Разрешения пользователей и групп**.  
  
2.  На панели меню страницы **Пользователи** нажмите кнопку **Управление группами**.  
  
3.  Нажмите кнопку **Добавить группы**.  
  
4.  Введите имя группы, предваряемое именем домена Active Directory либо именем сервера в виде *домен\имя_группы* или *компьютер\имя_группы*.  
  
5.  По желанию нажмите кнопку **Проверить имена**.  
  
6.  Нажмите кнопку **ОК**.  
  
    > [!NOTE]  
    >  После первого обращения пользователя к [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]имя пользователя добавляется в список пользователей [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
## <a name="next-steps"></a>Следующие шаги  
  
-   [Назначение разрешений для функциональной области (службы Master Data Services)](../master-data-services/assign-functional-area-permissions-master-data-services.md)  
  
## <a name="see-also"></a>См. также  
 [Безопасность (службы Master Data Services)](../master-data-services/security-master-data-services.md)  
  
  
