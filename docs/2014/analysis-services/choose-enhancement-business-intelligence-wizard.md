---
title: Выбор расширения (мастер бизнес-аналитики) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.bienhancement.f1
ms.assetid: 39e2f36c-2c02-4a71-af8f-5dbd373190dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 687f7fb96ee5a2b96d80562c20d536eeeb308379
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088119"
---
# <a name="choose-enhancement-business-intelligence-wizard"></a>Выбор расширения (мастер бизнес-аналитики)
  Страница **Выбор расширения** используется для выбора расширения бизнес-аналитики для добавления к кубу или измерению.  
  
## <a name="options"></a>Параметры  
 **Имеющиеся расширения**  
 Выберите расширение бизнес-аналитики для добавления. В следующей таблице перечислены имеющиеся расширения.  
  
|Расширение|Описание|  
|-----------------|-----------------|  
|**Определение логики операций со временем**|Добавить дополнительные представления времени для выбранной иерархии. Они включают представления периода на дату, представления скользящего среднего и представления между периодами.<br /><br /> Примечание. Этот параметр доступен только для кубов.|  
|**Определение операций со счетами**|Присвойте стандартную бухгалтерскую классификацию, например доходы или расходы, элементам атрибута счета.<br /><br /> Если статистическая функция для мер установлена в состояние *ByAccount*, то экземпляр служб [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] использует бухгалтерскую классификацию для статистической обработки мер по элементам атрибута счета по времени.|  
|**Определить логику операций с измерениями**|Логика операций с измерениями используется для присвоения стандартного бизнес-типа для измерения и для задания допустимых типов для атрибутов измерения. Клиентские приложения могут использовать эти характеристики типа при анализе данных.|  
|**Определение унарного оператора**|Укажите унарный оператор для замены статистической функции по умолчанию, которое связано с элементами иерархии типа «родители-потомки», включаемой в куб.<br /><br /> Примечание. Этот параметр доступен только для кубов.|  
|**Создание нестандартной формулы элемента**|Создайте нестандартную формулу элементов для замены статистической функции по умолчанию, связанной с элементом измерения с другим оператором.|  
|**Задать сортировку атрибута**|Задайте, как упорядочиваются элементы выбранного атрибута. Элементы могут упорядочиваться по имени или ключу выбранного атрибута, или по имени или ключу атрибута, относящегося к выбранному атрибуту. По умолчанию элементы упорядочиваются по имени выбранного атрибута.|  
|**Включение обратной записи в измерение**|Включите ручное изменение структуры измерения. Обновления измерений, доступных для записи, записываются прямо в таблицу измерения.|  
|**Определение полуаддитивного режима**|Определите статистический метод для отдельных мер или элементов атрибута типа счета вручную. Если в кубе содержится измерение счетов, можно использовать параметр **Определить логику операций со счетами** для автоматической установки полуаддитивной функциональности на основе типа счета.<br /><br /> Примечание. Этот параметр доступен только для кубов.|  
|**Определение конвертации валюты**|Определите правила для конвертации и анализа многонациональных данных в кубе. Правила конвертации применяются к кубу с использованием скрипта многомерных выражений, сформированного мастером бизнес-аналитики.<br /><br /> Примечание. Этот параметр доступен только для кубов.|  
  
 **Описание**  
 Предоставляет краткое описание выбранного расширения бизнес-аналитики.  
  
## <a name="see-also"></a>См. также  
 [Справка F1 мастера бизнес-аналитики](business-intelligence-wizard-f1-help.md)   
 [Конструктор кубов &#40;службы Analysis Services — многомерные данные&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Конструктор измерений &#40;службы Analysis Services — многомерные данные&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
