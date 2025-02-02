---
title: Создание проверочного набора (мастер интеллектуального анализа данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.holdout.f1
ms.assetid: d0a44b59-ffbd-45fc-baa8-6b8046b1a2f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f0e4d1a384995c0c49c346102f8fddbcdf47f68
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086791"
---
# <a name="create-testing-set-data-mining-wizard"></a>Создание проверочного набора (Мастер интеллектуального анализа данных)
  На странице **Создание проверочного набора** указывается, какая часть данных должна использоваться для обучения, а какая должна быть зарезервирована для применения в качестве проверочного набора. Благодаря разделению данных на обучающий и проверочный наборы при создании структуры интеллектуального анализа становится намного проще оценить точность моделей интеллектуального анализа данных, создаваемых в дальнейшем.  
  
 Можно указать количество проверочных данных в процентах или задать число, чтобы ограничить количество вариантов, используемых для проверки. Если указаны и процентная доля, и максимальное количество вариантов, используемых для проверки, то сравниваются оба параметра и в набор проверочных данных включается меньшее из двух значений количества вариантов. По умолчанию используется 30 процентов данных для проверки, 70 процентов — для обучения, и максимальное количество проверочных вариантов не устанавливается.  
  
 По умолчанию в службах [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] формируется числовое начальное значение, которое используется для запуска секционирования. Это начальное значение определяется на основе имени структуры интеллектуального анализа данных. Если необходимо, чтобы секции оставались неизменными даже при изменении имени структуры интеллектуального анализа, можно указать величину начального значения, указав свойство HoldoutSeed структуры интеллектуального анализа данных. Если это начальное контрольное значение изменится, обработка структуры должна быть выполнена повторно.  
  
 Если позже вы хотите изменить количество проверочных или обучающих данных, можно изменить `HoldoutMaxCases` и `HoldoutMaxPercent` свойства структуры интеллектуального анализа данных с помощью **свойства** окна. Однако после такого изменения необходимо выполнить повторную обработку структуры интеллектуального анализа и всех связанных с ней моделей интеллектуального анализа данных. Также действуют следующие ограничения.  
  
-   Секционирование структуры интеллектуального анализа данных поддерживается только в том случае, если структура интеллектуального анализа данных хранится в [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Более ранние версии служб [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] не поддерживают кэширование данных секций для структур интеллектуального анализа данных.  
  
-   Секционирование структуры интеллектуального анализа данных невозможно, если структура интеллектуального анализа содержит ключевой столбец времени, который требуется для моделей интеллектуального анализа данных с временными рядами.  
  
-   Секционировать данные невозможно, если предпринимается попытка прогнозирования значения, которое хранится во вложенной таблице.  
  
 **Дополнительные сведения:** [Тестирование и проверка &#40;интеллектуального анализа данных&#41;](data-mining/testing-and-validation-data-mining.md), [Создание реляционной структуры](data-mining/create-a-relational-mining-structure.md), [учебник интеллектуального анализа данных](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
## <a name="options"></a>Параметры  
 **Процент проверочных данных**  
 Нажимайте кнопки со стрелками вверх и вниз, чтобы увеличить или уменьшить процентную долю данных, предназначенных для использования в качестве обучающего множества, или введите значение от 0 до 100 в текстовом поле.  
  
 **Максимальное число вариантов в наборе проверочных данных**  
 Введите число, ограничивающее количество вариантов, которые могут использоваться для проверки.  
  
 Если указано число, превышающее фактическое количество вариантов в данных, будут использоваться все варианты.  
  
 Значение по умолчанию — NULL. Это означает отсутствие какого-либо предела.  
  
## <a name="see-also"></a>См. также  
 [Справка F1 мастера интеллектуального анализа данных &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Предложение связанных столбцов &#40;мастер интеллектуального анализа данных&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Определение типов таблиц &#40;мастер интеллектуального анализа данных&#41;](specify-table-types-data-mining-wizard.md)   
 [Определение содержимого и типа данных столбца &#40;мастер интеллектуального анализа данных&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
