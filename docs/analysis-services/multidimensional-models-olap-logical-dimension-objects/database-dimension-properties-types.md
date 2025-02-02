---
title: Типы измерений | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 663c26ac169c11e5ab2d9b90285419cf4145368c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025767"
---
# <a name="database-dimension-properties---types"></a>Свойства измерений базы данных — типы
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  **Тип** предоставляет сведения о содержимом измерения серверу и клиентским приложениям. В некоторых случаях **тип** параметр содержит рекомендации для клиентских приложений и является необязательным. В других случаях таких как **учетные записи** или **время** измерений, **тип** значения свойств для измерения и его атрибуты определяют конкретные режимы сервера и может быть необходимой для реализации определенных режимов куба. Например **тип** свойству измерения может быть присвоено **учетные записи** для указания для клиентских приложений, что в стандартном измерении содержатся атрибуты счетов. Дополнительные сведения о времени, счетов и измерениях валют см. в разделе [Создание измерения типа Date](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [Создание учетной записи Finance с измерением типа родители потомки](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), и [Создание валюты Введите измерения](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 Значение по умолчанию для типа измерения можно **регулярных**, что делает никаких предположений о содержимом измерения. Это параметр по умолчанию для всех измерений при первоначальном определении измерения, если не указать **время** при определении измерения с помощью мастера измерений. Необходимо также оставить **регулярных** как тип измерения, если мастер измерений не содержит соответствующего типа для типа измерения.  
  
## <a name="available-dimension-types"></a>Доступные типы измерений  
 В следующей таблице описаны типы измерений, доступных в [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Тип измерения|Описание|  
|--------------------|-----------------|  
|Regular|Измерение, тип которого не был изменен на специальный тип измерения.|  
|Time|Измерение, атрибуты которого представляют периоды времени, например годы, семестры, кварталы, месяцы и дни.|  
|Organization|Измерение, атрибуты которого представляют сведения об организации, например сотрудниках или филиалах.|  
|Geography|Измерение, атрибуты которого представляют географические сведения, например города или почтовые индексы.|  
|Измерение ведомости материалов|Измерение, атрибуты которого представляют сведения по описи или производственные данные, например списки деталей для изделий.|  
|Измерение счетов|Измерение, атрибуты которого представляют диаграмму счетов для финансовой отчетности.|  
|Заказчики|Измерение, атрибуты которого представляют сведения о заказчиках или контактные данные.|  
|Измерение продуктов|Измерение, атрибуты которого представляют сведения о продуктах.|  
|Сценарий|Измерение, атрибуты которого представляют сведения о планах или данные о стратегическом анализе.|  
|Количественное измерение|Измерение, атрибуты которого представляют количественные данные.|  
|Служебная программа|Измерение, атрибуты которого представляют прочие сведения.|  
|Currency|Измерение, атрибуты которого содержат данные валюты и метаданные.|  
|Изменения курсов|Измерение, атрибуты которого представляют данные о курсе обмена валюты.|  
|Channel|Измерение, атрибуты которого представляют данные о каналах.|  
|Promotion|Измерение, атрибуты которого представляют сведения об акциях по продвижению.|  
  
## <a name="see-also"></a>См. также  
 [Создание измерения с помощью существующей таблицы](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Измерения (службы Analysis Services — многомерные данные)](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
