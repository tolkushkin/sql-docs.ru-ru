---
title: Иерархии (Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services]
- hierarchies [Master Data Services], about hierarchies
ms.assetid: 70dbb1fc-ead7-45be-9552-a45e3ccd8d21
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d0e7abd1443af69fdcb2df26071f7bf29a216255
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65477133"
---
# <a name="hierarchies-master-data-services"></a>Иерархии (службы основных данных)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Иерархия в [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]— древовидная структура, которую можно использовать:  
  
-   для группировки схожих элементов с целью систематизации;  
  
-   объединения и сведения элементов для отчетов или анализа.  
  
## <a name="what-hierarchies-contain"></a>Что содержится в иерархиях  
 Каждая иерархия содержит элементы из одной или нескольких сущностей. При добавлении, изменении или удалении элемента все иерархии обновляются. Это гарантирует, что данные будут точными во всех иерархиях. Иерархии также гарантируют, что каждый элемент будет учитываться ровно один раз.  
  
 Если необходимо создать группирование подмножества элементов, рассмотрите возможность использования коллекции. Дополнительные сведения см. в разделе [Коллекции (службы Master Data Services)](../master-data-services/collections-master-data-services.md).  
  
## <a name="kinds-of-hierarchies"></a>Виды иерархий  
 Можно создавать разные иерархии для просмотра и систематизации элементов разными способами. Можно создавать:  
  
-   Неоднородные иерархии из единой сущности, которые называются явными иерархиями. Дополнительные сведения см. в разделе [Явные иерархии (службы Master Data Services)](../master-data-services/explicit-hierarchies-master-data-services.md).  
  
-   Иерархии на основе уровней, состоящие из многих сущностей и основанные на существующих связях между сущностями и их атрибутами, которые называются производными иерархиями. Дополнительные сведения см. в разделе [Derived Hierarchies &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md).  
  
> [!NOTE]  
>  Все элементы в иерархии должны быть в одной модели.  
  
## <a name="hierarchies-are-not-taxonomies"></a>Иерархии не являются классификациями  
 Иерархия отличается от классификации. В классификации элементы упорядочены в соответствии с несколькими атрибутами одновременно, а в иерархии — только по одному атрибуту. Классификации может включать один элемент несколько раз, а иерархия имеет только одно вхождение элемента.  
  
 Например, один велосипед может быть упомянут в классификации дважды: один раз, потому что его цвет красный, и один раз, потому что его размер равен 38. В иерархии велосипед включен только один раз, поэтому нужно определить, в соответствии с чем он будет отображаться: с цветом или размером.  
  
## <a name="hierarchy-example"></a>Пример иерархии  
 В следующем примере в иерархии элементы продуктов группируются по элементам подкатегории.  
  
 ![Пример иерархии, сгруппированной по подкатегориям](../master-data-services/media/mds-conc-hierarchy.gif "Пример иерархии, сгруппированной по подкатегориям")  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Создание явной иерархии.|[Создание явной иерархии (службы Master Data Services)](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Создание производной иерархии.|[Создание производной иерархии (службы Master Data Services)](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Скрытие или удаление уровней в существующей производной иерархии.|[Скрытие или удаление уровней в производной иерархии (службы Master Data Services)](../master-data-services/hide-or-delete-levels-in-a-derived-hierarchy-master-data-services.md)|  
  
## <a name="related-content"></a>См. также  
  
-   [Явные иерархии (службы Master Data Services)](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Производные иерархии (службы Master Data Services)](../master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [Рекурсивные иерархии (службы Master Data Services)](../master-data-services/recursive-hierarchies-master-data-services.md)  
  
-   [Производные иерархии с явными ограничениями (службы Master Data Services)](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)  
  
-   [Коллекции (службы Master Data Services)](../master-data-services/collections-master-data-services.md)  
  
  
