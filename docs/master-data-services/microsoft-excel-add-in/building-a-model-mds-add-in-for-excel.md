---
title: Построение модели (надстройка MDS для Excel) | Документы Майкрософт
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e3a946626223a464b63b2099912c0f89d95ff32b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488923"
---
# <a name="building-a-model-mds-add-in-for-excel"></a>Построение модели (надстройка MDS для Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]администраторы могут выполнять сокращенный набор административных функций, доступных в веб-приложении [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
 Администраторы могут выполнять следующие задачи по созданию моделей в [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] :  
  
-   Создание сущностей. Дополнительные сведения о сущностях см. в разделе [Сущности (службы Master Data Services)](../../master-data-services/entities-master-data-services.md).  
  
-   Создание атрибутов всех типов, включая атрибуты на основе домена. Дополнительные сведения об атрибутах см. в разделах [Атрибуты (службы Master Data Services)](../../master-data-services/attributes-master-data-services.md) и [Атрибуты на основе домена (службы Master Data Services)](../../master-data-services/domain-based-attributes-master-data-services.md).  
  
 Администратор должен создавать модель с помощью веб-приложения [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или веб-службы. Затем с помощью [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] можно создавать сущности и атрибуты в модели. Дополнительные сведения об объектах модели см. в разделе [Модели (службы Master Data Services)](../../master-data-services/models-master-data-services.md).  
  
## <a name="related-tasks"></a>Связанные задачи  
 Однако большинство административных задач все равно необходимо выполнять в веб-приложении [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или с помощью веб-службы. В следующей таблице показаны средства, с помощью которых администраторы могут выполнять задачи в MDS.  
  
|Описание задачи|Инструмент|Раздел|  
|----------------------|----------|-----------|  
|Создание моделей.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или веб-служба|[Создание модели (службы Master Data Services)](../../master-data-services/create-a-model-master-data-services.md)|  
|Создание сущности.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , веб-служба или [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[Создание сущности (надстройка MDS для Excel)](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|Создание атрибута на основе домена.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , веб-служба или [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[Создание атрибута на основе домена (надстройка MDS для Excel)](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Создание групп атрибутов.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или веб-служба|[Создание группы атрибутов (службы Master Data Services)](../../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Создание бизнес-правил.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или веб-служба|[Создание и публикация бизнес-правила (службы Master Data Services)](../../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Создание представлений подписки.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или веб-служба|[Создание представления подписки для экспорта данных (службы Master Data Services)](../../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Создание иерархий.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или веб-служба|[Создание производной иерархии (службы Master Data Services)](../../master-data-services/create-a-derived-hierarchy-master-data-services.md)<br /><br /> [Создание явной иерархии (службы Master Data Services)](../../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Создание коллекций.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или веб-служба|[Создание коллекции (службы Master Data Services)](../../master-data-services/create-a-collection-master-data-services.md)|  
|Создание версий данных.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] или веб-служба|[Блокировка версии (службы Master Data Services)](../../master-data-services/lock-a-version-master-data-services.md)|  
|Развертывание моделей.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , веб-служба или средство MDSModelDeploy.|[Создание пакета развертывания модели при помощи MDSModelDeploy](../../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a>См. также  
  
-   [Модели (службы Master Data Services)](../../master-data-services/models-master-data-services.md)  
  
-   [Сущности (службы Master Data Services)](../../master-data-services/entities-master-data-services.md)  
  
-   [Атрибуты (службы Master Data Services)](../../master-data-services/attributes-master-data-services.md)  
  
-   [Атрибуты на основе домена (службы Master Data Services)](../../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [Группы атрибутов (службы Master Data Services)](../../master-data-services/attribute-groups-master-data-services.md)  
  
-   [Бизнес-правила (службы Master Data Services)](../../master-data-services/business-rules-master-data-services.md)  
  
-   [Обзор: экспорт данных (службы Master Data Services)](../../master-data-services/overview-exporting-data-master-data-services.md)  
  
-   [Иерархии (службы Master Data Services)](../../master-data-services/hierarchies-master-data-services.md)  
  
-   [Коллекции (службы Master Data Services)](../../master-data-services/collections-master-data-services.md)  
  
-   [Версии (службы Master Data Services)](../../master-data-services/versions-master-data-services.md)  
  
-   [Безопасность (службы Master Data Services)](../../master-data-services/security-master-data-services.md)  
  
-   [Развертывание моделей (службы Master Data Services)](../../master-data-services/deploying-models-master-data-services.md)  
  
  
