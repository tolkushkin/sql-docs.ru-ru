---
title: Настройка веб-сайта и базы данных для служб Master Data Services | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 478dea9095fe22a437aecf138c22374b5a70885b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054094"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>Настройка базы данных и веб-сайта для служб Master Data Services
  Использование [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] для настройки базы данных и веб-сайта для [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS)  
  
 Чтобы настроить базу данных и веб-сайт, выполните следующие задачи.  
  
1.  Создание базы данных при помощи **базы данных конфигурации** странице в [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].  
  
     Сведения см. в разделе [страница базы данных конфигурации &#40;диспетчер конфигурации Master Data Services&#41; ](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md) и [мастер создания базы данных &#40;диспетчер конфигурации Master Data Services&#41; ](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
2.  Создайте новый веб-сайт, выберите веб-сайт по умолчанию или выберите другой существующий веб-сайт с помощью **веб-конфигурация** странице в [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Затем свяжите базу данных MDS с создаваемым или выбранным веб-приложением.  
  
     Сведения см. в разделе [веб-страницы конфигурации &#40;диспетчер конфигурации Master Data Services&#41; ](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) и [создать диалоговое окно веб-сайт &#40;диспетчер конфигурации Master Data Services&#41; ](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
3.  (Необязательно) Включение интеграции со службами Data Quality Services с помощью **веб-конфигурация** странице в [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].  
  
     Дополнительные сведения см. в разделе [веб-страницы конфигурации &#40;диспетчер конфигурации Master Data Services&#41; ](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) и [включить службы интеграции служб Data Quality со службами Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md).  
  
 Также можно использовать [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] для указания параметров веб-приложений и служб, связанных с базой данных MDS. К примеру, можно указать, как часто загружаются данные или как часто отправляются сообщения проверки. Дополнительные сведения см. в разделе [Системные параметры (службы Master Data Services)](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>См. также  
 [База данных служб Master Data Services](../../2014/master-data-services/master-data-services-database.md)   
 [Веб-приложение диспетчера основных данных](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
