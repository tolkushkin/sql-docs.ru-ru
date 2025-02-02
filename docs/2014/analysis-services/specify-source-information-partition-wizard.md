---
title: Определение исходных сведений (мастер секционирования) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifydsvandfacttables.f1
ms.assetid: b6c13587-c690-45d9-af90-b3d652afc55b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aca14c9462d847d91ae2b51dfdf179650ee06732
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068173"
---
# <a name="specify-source-information-partition-wizard"></a>Определение исходных сведений (мастер секционирования)
  С помощью страницы **Определение исходных сведений** можно выбрать группу мер, в которой создается секция, а также представление источника данных, и отфильтровать таблицы для секции.  
  
> [!CAUTION]  
>  Если из списка **Доступные таблицы** выбирается таблица, которая используется другой секцией, необходимо предоставить запрос на странице **Ограничение на строки** , иначе возникнет риск повторения данных в кубе.  
  
## <a name="options"></a>Параметры  
 **Группа мер**  
 Выберите группу мер для этой секции.  
  
 **Look in**  
 Выберите источник данных или представление источника данных, содержащие исходные таблицы для этой секции. По умолчанию выбирается представление источника данных, используемое группой мер.  
  
 **Фильтровать таблицы**  
 Введите строку, которая будет использоваться для ограничения имен таблиц, отображаемых в списке **Доступные таблицы**.  
  
 **Поиск таблиц**  
 Выберите, чтобы обновить список таблиц **Доступные таблицы**, еще более ограничивая его, если в поле **Фильтровать таблицы**введено значение.  
  
 **Доступные таблицы**  
 Выбор таблиц, используемых в качестве исходных таблиц для секционирования. **Мастер секционирования** создает одну секцию для каждой таблицы, выбранной из списка **Доступные таблицы**.  
  
 Если в поле **Фильтровать таблицы**не задан фильтр, этот список будет содержать все таблицы из источника данных или представления источников данных, определенного параметром **Искать в** , а также таблицы, аналогичные по структуре таблице фактов, используемой группой мер, определенной параметром **Группа мер**.  
  
 Если в поле **Фильтровать таблицы**указан фильтр, список еще более ограничивается в результате сравнения фильтра с именами таблиц, удовлетворяющими предыдущему критерию. Отображаются только те таблицы, которые содержат строку, указанную в поле **Фильтровать таблицы** .  
  
> [!NOTE]  
>  Если выбирается несколько таблиц, страницу **Ограничение на строки** невозможно отобразить, и нельзя ограничить строки для секций, созданных из выбранных таблиц. Для ограничения строк во всех секциях мастер секционирования должен выполняться по одному разу для каждой таблицы, из которых должна создаваться секция.  
  
## <a name="see-also"></a>См. также  
 [Секции (службы Analysis Services — многомерные данные)](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
