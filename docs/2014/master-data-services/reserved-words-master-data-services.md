---
title: Зарезервированные слова (службы Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5435c2a48417156abd6d4f831bf61c9ba6440fab
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482574"
---
# <a name="reserved-words-master-data-services"></a>Зарезервированные слова (службы Master Data Services)
  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]при создании элементов и объектов модели нельзя использовать некоторые слова. В противном случае могут возникнуть ошибки.  
  
> [!NOTE]  
>  Кроме того, следует ограничить использование специальных знаков (особых символов, знаков переноса и т. п.).  
  
-   [Модели](#models)  
  
-   [Сущности](#entities)  
  
-   [Явные иерархии](#exhierarchies)  
  
-   [Атрибуты](#attributes)  
  
-   [Члены](#members)  
  
##  <a name="models"></a> Модели  
 При создании модели с именем **имя**, не устанавливайте **создать сущность с именем модели** поскольку **имя** не может использоваться в качестве имени сущности.  
  
##  <a name="entities"></a> Сущности  
 В качестве имен сущностей нельзя указывать **Name** и **Code**.  
  
##  <a name="exhierarchies"></a> Явные иерархии  
 В качестве имен явных иерархий нельзя указывать **Name** и **Code**.  
  
##  <a name="attributes"></a> Атрибуты  
  
-   **Идентификатор**  
  
-   **Code**  
  
-   **Name**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> Члены  
 Для элементов нельзя использовать **MDMMemberStatus** или **КОРНЕВОЙ** для **код** значение атрибута.  
  
## <a name="see-also"></a>См. также  
 [Общие сведения о службах Master Data Services](master-data-services-overview-mds.md)  
  
  
