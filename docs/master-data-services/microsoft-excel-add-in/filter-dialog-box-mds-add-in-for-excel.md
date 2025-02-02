---
title: Диалоговое окно "Фильтр" (надстройка MDS для Excel) | Документы Майкрософт
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 879ee3d55a178e2ef5fc7feca3f6ef475e683a8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65477166"
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>Диалоговое окно «Фильтр» (надстройка MDS для Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]воспользуйтесь диалоговым окном **Фильтр** , чтобы сузить список данных, управляемых MDS, прежде чем загружать их в Excel.  
  
 Это диалоговое окно содержит три раздела: **Столбцы**, **строк**, и **Сводка**.  
  
## <a name="columns"></a>Столбцы  
 В разделе **Столбцы** можно определить атрибуты (столбцы), которые должны отображаться в Excel.  
  
|Имя элемента управления|Описание|  
|------------------|-----------------|  
|Тип атрибута|Тип атрибута описывает тип элементов, с которыми вы собираетесь работать. В большинстве случаев это **Конечный элемент**. Дополнительные сведения о типах элементов см. в разделе [Элементы (службы Master Data Services)](../../master-data-services/members-master-data-services.md).|  
|Явная иерархия|При выборе типа атрибута **Объединены** нужно также выбрать иерархию, к которой относятся консолидированные элементы. Дополнительные сведения см. в разделе [Явные иерархии (службы Master Data Services)](../../master-data-services/explicit-hierarchies-master-data-services.md).|  
|Группы атрибутов|Группы атрибутов представляют собой способ группирования подмножеств атрибутов. Выберите группу атрибутов, если необходимо показать подмножество доступных атрибутов. Дополнительные сведения о группах атрибутов см. в разделе [Группы атрибутов (службы Master Data Services)](../../master-data-services/attribute-groups-master-data-services.md).|  
|Выделить все|Нажмите, чтобы выбрать все атрибуты, показанные в списке.|  
|Очистить все|Нажмите, чтобы очистить выбранные атрибуты, показанные в списке.<br /><br /> Нельзя очистить атрибуты **Имя** и **Код**.|  
|СТРЕЛКА ВВЕРХ или СТРЕЛКА ВНИЗ|Нажмите, чтобы переместить выбранный атрибут вверх или вниз в списке. Порядок сверху вниз соответствует порядку отображения столбцов на листе слева направо.|  
  
## <a name="rows"></a>Строки  
 В разделе **Строки** можно определить элементы (строки), которые нужно отображать в Excel. Это делается путем определения условия фильтрации строк для отображения.  
  
|Имя элемента управления|Описание|  
|------------------|-----------------|  
|attribute|Отображает атрибут, по которому необходимо фильтровать. Если в списке нет атрибутов, это означает, что они не добавлены.<br /><br /> Примечание. Можно фильтровать по атрибутам, которые не планируется показывать на листе.|  
|Оператор|Содержит операторы, соответствующие типу выбранного атрибута. Дополнительные сведения см. в разделе [Операторы фильтров (службы Master Data Services)](../../master-data-services/filter-operators-master-data-services.md).|  
|Критерии|Условие, по которому нужно выполнить фильтрацию.|  
|Обновить сводку|При открытии больших баз данных щелкните, чтобы выбрать обновление в разделе **Сводка** сведений об объемах данных, которые будут загружены.|  
|Добавить|Если щелкнуть атрибут в разделе **Столбцы** , а затем нажать кнопку **Добавить**, то этот атрибут будет добавлен в список фильтров.|  
|Удалить все|Удаляет все фильтры из указанного списка.|  
|Удалить|Удаляет выбранный фильтр из списка.|  
  
## <a name="summary"></a>Сводка  
 В разделе **Сводка** можно просмотреть сведения об объемах данных, которые будут загружены, прежде чем выполнять загрузку.  
  
|Имя элемента управления|Описание|  
|------------------|-----------------|  
|Модель|Имя модели.|  
|Версия|Имя версии.|  
|Сущность|Имя сущности.|  
|Строки|Число строк, которые будут загружены в Excel, исходя из фильтров, примененных в разделе **Строки** .|  
|Столбцы|Число столбцов, которые будут загружены в Excel, исходя из атрибутов, примененных в разделе **Столбцы** .|  
  
## <a name="see-also"></a>См. также:  
 [Фильтрация данных перед их экспортом (надстройка MDS для Excel)](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)   
 [Обзор: экспорт данных в Excel (надстройка MDS для Excel)](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
