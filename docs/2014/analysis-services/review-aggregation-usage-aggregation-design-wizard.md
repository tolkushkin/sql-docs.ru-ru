---
title: Просмотр использования статистической обработки (мастер статистических схем) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.aggregationdesignwizard.reviewusage.f1
ms.assetid: 107ee872-3df2-4931-b56c-af11e38f6745
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f52ec05ddadc6bb23968f6b5f8ee7fda9adc65a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070220"
---
# <a name="review-aggregation-usage-aggregation-design-wizard"></a>Просмотр использования статистической обработки (мастер статистических схем)
  Используйте страницу **Просмотр использования статистической обработки** для настройки параметров статистической обработки.  
  
## <a name="options"></a>Параметры  
 **Default**  
 Выберите, чтобы присвоить параметру статистической обработки атрибута значение «По умолчанию». Используя данный параметр, конструктор применяет правило по умолчанию, основанное на типе атрибута и измерения.  
  
 `Full`  
 Выберите, чтобы присвоить параметру статистической обработки атрибута значение `Full`. При использовании данного параметра, каждый агрегат для куба должен включать данный атрибут или связанный атрибут, находящийся ниже в цепочке атрибутов. Если атрибут содержит большое количество элементов, следует избегать использования параметра статистической обработки `Full`. При назначении нескольким атрибутам или атрибутам, включающим множество элементов, данный параметр может привести к тому, что агрегат не будет создан из-за избыточного размера.  
  
 **None**  
 Выберите, чтобы присвоить параметру статистической обработки атрибута значение «Нет». При использовании этого параметра, ни одна статистическая обработка для куба не может включать данный атрибут.  
  
 `Unrestricted`  
 Выберите, чтобы присвоить параметру статистической обработки атрибута значение `Unrestricted`. При использовании этого параметра к конструктору агрегатов не применяются никакие ограничения; тем не менее необходимо провести оценку, может ли этот атрибут использоваться в качестве агрегата.  
  
 **Задать все значения по умолчанию**  
 Выберите, чтобы присвоить для всех атрибутов настройки статистической обработки по умолчанию.  
  
## <a name="see-also"></a>См. также  
 [Справка F1 мастера статистических схем](aggregation-design-wizard-f1-help.md)   
 [Мастера служб Analysis Services &#40;многомерных данных&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
