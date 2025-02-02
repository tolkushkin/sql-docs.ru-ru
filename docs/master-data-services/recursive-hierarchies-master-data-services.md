---
title: Рекурсивные иерархии (Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- recursive hierarchies [Master Data Services]
- hierarchies [Master Data Services], recursive hierarchies
ms.assetid: 9408c6ea-d9c4-4a0b-8a1b-1457fb6944af
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 82f45235ac82b3aada6ad85a25d21e4bbfa3a101
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65485933"
---
# <a name="recursive-hierarchies-master-data-services"></a>Рекурсивные иерархии (службы Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]рекурсивная иерархия — это производная иерархия, которая содержит рекурсивную связь. Рекурсивная связь возникает, когда у сущности есть атрибут, который базируется на самой сущности, на основе домена.  
  
## <a name="recursive-hierarchy-example"></a>Образец рекурсивной иерархии  
 Типичным примером рекурсивной иерархии может служить организационная структура. В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]для этого создается сущность «Сотрудник» с основанным на домене атрибутом «Менеджер». Атрибут «Менеджер» заполняется из списка сотрудников. В организации, взятой для образца, все сотрудники могут быть менеджерами.  
  
 ![mds_conc_recursive_table_w_data](../master-data-services/media/mds-conc-recursive-table-w-data.gif "mds_conc_recursive_table_w_data")  
  
 Можно создать производную иерархию, в которой выделяется связь между сущностью «Сотрудник» и атрибутом «Менеджер» на основе домена.  
  
 ![mds_conc_recursive_UI_structure](../master-data-services/media/mds-conc-recursive-ui-structure.gif "mds_conc_recursive_UI_structure")  
  
 Чтобы включить каждый элемент в иерархию только один раз, можно закрепить нулевые связи. При этом элементы с пустыми значениями атрибутов на основе домена отображаются на высшем уровне иерархии.  
  
 ![mds_conc_recursive_UI_example_anchored](../master-data-services/media/mds-conc-recursive-ui-example-anchored.gif "mds_conc_recursive_UI_example_anchored")  
  
 Если не закрепить нулевые связи, то элементы будут включаться несколько раз. Все элементы отображаются на высшем уровне. Они также отображаются под теми элементами, атрибутами которых являются.  
  
 ![mds_conc_recursive_UI_example_nonanchored](../master-data-services/media/mds-conc-recursive-ui-example-nonanchored.gif "mds_conc_recursive_UI_example_nonanchored")  
  
 В данном примере Марсия находится на высшем уровне. Она не является менеджером ни для кого из сотрудников, поскольку она не используется как значение атрибута на основе домена для какого-либо другого элемента сущности «Сотрудник». У Роберта, с другой стороны, есть более низкий уровень, поскольку для Марсии Роберт является значением ее атрибута «Менеджер».  
  
## <a name="rules"></a>Правила  
  
-   Производная иерархия не может содержать более одной рекурсивной связи. Однако эта иерархия может содержать другие производные связи (например, производная иерархия, содержащая рекурсивную связь «Менеджер-Сотрудник», также может иметь связи «Страна-Менеджер» и «Сотрудник-Магазин»).  
  
-   Нельзя назначать разрешения элементам (на вкладке **Элементы иерархии** ) в рекурсивной иерархии.  
  
-   В рекурсивные иерархии не могут включаться циклические связи. Например, Катерина не может быть менеджером Сэндип, если Сэндип — ее менеджер. Также Катерина не может быть своим собственным менеджером.  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Создание производной иерархии.|[Создание производной иерархии (службы Master Data Services)](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Изменение имени существующей производной иерархии.|[Изменение имени производной иерархии (службы Master Data Services)](../master-data-services/change-a-derived-hierarchy-name-master-data-services.md)|  
|Удаление существующей производной иерархии.|[Удаление производной иерархии (службы Master Data Services)](../master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
  
## <a name="related-content"></a>См. также  
  
-   [Атрибуты на основе домена (службы Master Data Services)](../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [Производные иерархии (службы Master Data Services)](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
