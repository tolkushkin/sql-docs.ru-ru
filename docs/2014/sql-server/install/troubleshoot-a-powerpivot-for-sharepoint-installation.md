---
title: Устранение неполадок с PowerPivot для SharePoint | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fc6e01ff69850cb4faf9240c9dc0247ba0d01f11
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091774"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Устранение неполадок установки PowerPivot для SharePoint
  Если вместо ожидаемых страниц и компонентов выдаются ошибки, выполните следующие действия.  
  
-   Откройте заметки о выпуске SharePoint и [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , чтобы выяснить, какие существуют способы решения известных проблем установки. Заметки о выпуске доступны на установочном носителе или на сайте Майкрософт, с которого было загружено программное обеспечение.  
  
    -   [Заметки о выпуске SQL Server 2014](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx).  
  
-   См. раздел [Устранение неполадок установки PowerPivot (и других надстроек)](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx)портала TechNet Wiki.  
  
## <a name="issues"></a>Проблемы  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>Миниатюрные изображения в галерее PowerPivot отображаются в виде красного x  
 Одной из возможных причин **Интеграция функций PowerPivot для семейства веб-сайтов** не активна. Выполните следующие действия.  
  
1.  В библиотеке PowerPivot Gallery, выберите **параметры сайта** из меню значка с шестеренкой ![параметры SharePoint](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "параметры SharePoint") или **домашней** списка.  
  
2.  Щелкните **Компоненты семейства веб-сайтов** в разделе **Администрирование семейства веб-сайтов**.  
  
3.  Щелкните **Компоненты коллекции сайтов**.  
  
4.  Убедитесь, что значение **Функции интеграции с PowerPivot для семейств веб-сайтов** равно **Активны**.  
  
 Дополнительные причин этой проблемы, см. в разделе [Галерея PowerPivot отображается красная x для значков](https://support.microsoft.com/kb/2361559) (https://support.microsoft.com/kb/2361559).  
  
  
