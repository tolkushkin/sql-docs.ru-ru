---
title: Группа доступности не готова для автоматического перехода на другой ресурс
description: Определение возможных причин, по которым группа доступности Always On может быть не готова к переходу на другой ресурс.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp3autofailover.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 28261014-342c-442a-bd89-6d04b8d4e8b7
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 2107137f9b50a289e056042446c2d763f0b7cd23
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800125"
---
# <a name="always-on-availability-group-is-not-ready-for-automatic-failover"></a>Группа доступности Always On не готова к автоматическому переходу на другой ресурс
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Введение  
  
|||  
|-|-|  
|**Имя политики**|Готовность группы доступности к автоматическому переходу на другой ресурс при сбое|  
|**Проблема**|Группа доступности не готова к автоматическому переходу на другой ресурс.|  
|**Категория**|**Критическая**|  
|**Аспект**|группа доступности|  
  
## <a name="description"></a>Описание  
 Эта политика проверяет наличие в группе доступности хотя бы одной вторичной реплики, готовой к переходу на другой ресурс. Политика находится в нерабочем состоянии и, если для первичной реплики настроен автоматический режим перехода на другой ресурс, но ни одна из вторичных реплик в группе доступности не готова к переходу на другой ресурс, формируется предупреждение.  
  
 Политика находится в рабочем состоянии, если по крайней мере одна вторичная реплика готова к автоматическому переходу на другой ресурс.  
  
> [!NOTE]  
>  Для этого выпуска [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]сведения о возможных причинах проблем и решениях доступны в разделе [Группа доступности не готова для автоматического перехода на другой ресурс](https://go.microsoft.com/fwlink/p/?LinkId=220851) в TechNet Wiki.  
  
## <a name="possible-causes"></a>Возможные причины  
 Группа доступности не готова к автоматическому переходу на другой ресурс. Для первичной реплики настроен автоматический переход на другой ресурс. Однако вторичная реплика не готова к автоматическому переходу на другой ресурс. Вторичная реплика, настроенная для автоматического перехода на другой ресурс, может быть недоступна, или ее состояние синхронизации данных в настоящий момент отлично от SYNCHRONIZED.  
  
## <a name="possible-solutions"></a>Возможные решения  
 Ниже перечислены возможные решения этой проблемы:  
  
-   Убедитесь, что по крайней мере для одной вторичной реплики настроен автоматический переход на другой ресурс. При отсутствии вторичных реплик, для которых настроен автоматический переход на другой ресурс, обновите конфигурацию вторичной реплики для настройки ее в качестве целевой реплики для автоматического перехода на другой ресурс с синхронной фиксацией.  
  
-   Используйте политику, чтобы убедиться, что данные находятся в состоянии синхронизации, и что у целевого узла автоматического перехода на другой ресурс имеется состояние SYNCHRONIZED, а затем устраните проблему в реплике доступности.  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Использование панели мониторинга AlwaysOn (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
