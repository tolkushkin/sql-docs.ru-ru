---
title: Группы атрибутов (службы Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services]
- attribute groups [Master Data Services], about attribute groups
ms.assetid: 648b3d0b-e15a-45f9-8292-3a54a072e62c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 63664133370cb001fd4ee20e54f57819bde4a500
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478614"
---
# <a name="attribute-groups-master-data-services"></a>Группы атрибутов (службы Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]группы атрибутов помогают организовать атрибуты в сущности. Если сущность имеет множество атрибутов, то использование групп атрибутов улучшает отображение сущности в веб-приложении [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
## <a name="how-attribute-groups-change-the-display"></a>Изменение отображения при использовании групп атрибутов  
 Группы атрибутов отображаются как вкладки над сеткой в функциональной области **обозревателя** в веб-приложении [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Если атрибутов у сущности много и эта сущность просматривается в сетке в **Обозревателе**, то для их просмотра нужно прокручивать экран вправо. Чтобы не нужно было прокручивать экран, можно объединить атрибуты в группы.  
  
-   Группы атрибутов всегда автоматически включают атрибуты «Имя» и «Код».  
  
-   Каждый атрибут сущности может принадлежать к нескольким группам.  
  
-   Все атрибуты автоматически включаются во вкладку **Все атрибуты** в **обозревателе**.  
  
-   Нельзя скрыть вкладку **Все атрибуты** .  
  
 Управление группами атрибутов осуществляется в функциональной области **Администрирование системы** в веб-приложении [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="show-or-hide-attribute-groups"></a>Отображение или скрытие групп атрибутов  
 При создании группы атрибутов она автоматически скрыта от всех пользователей, кроме того, кто ее создал. Дополнительные сведения о назначении видимости группе см. в разделе [Превращение группы атрибутов в видимую для пользователей &#40;службы Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md).  
  
 При необходимости скрыть определенный атрибут внутри группы вы можете назначить атрибуту разрешение **Запрещено** . Дополнительные сведения см. в разделе [Разрешения конечного элемента (службы Master Data Services)](../master-data-services/leaf-permissions-master-data-services.md).  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Создание новой группы атрибутов и добавление к ней атрибутов.|[Создание группы атрибутов (службы Master Data Services)](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Превращение группы атрибутов в видимую для пользователей|[Превращение группы атрибутов в видимую для пользователей (службы Master Data Services)](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)|  
|Изменение имени существующей группы атрибутов.|[Изменение имени группы атрибутов (службы Master Data Services)](../master-data-services/change-an-attribute-group-name-master-data-services.md)|  
|Удаление существующей группы атрибутов.|[Удаление группы атрибутов (службы Master Data Services)](../master-data-services/delete-an-attribute-group-master-data-services.md)|  
  
## <a name="related-content"></a>См. также  
  
-   [Атрибуты (службы Master Data Services)](../master-data-services/attributes-master-data-services.md)  
  
  
