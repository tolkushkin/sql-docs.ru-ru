---
title: Детализация диалоговое окно «» (средство просмотра моделей интеллектуального анализа данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.drillthrough.f1
ms.assetid: 42b78399-143d-4f44-90e0-b545ffb79e10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c065e36dd20646312d04379ea61b96d37a47a262
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081485"
---
# <a name="drill-through-dialog-box-mining-model-viewer"></a>Диалоговое окно «Детализация» (средство просмотра моделей интеллектуального анализа данных)
  При просмотре модели интеллектуального анализа данных с помощью вкладки **Средство просмотра моделей интеллектуального анализа данных** конструктора интеллектуального анализа данных можно раскрывать более подробные сведения о данных вариантов, предоставляемые моделью с включенной детализацией. Более того, если для базовой структуры интеллектуального анализа данных включена детализация, также можно просматривать столбцы в структуре интеллектуального анализа данных, даже если эти столбцы не включены в модель интеллектуального анализа данных. В списке столбцов столбцы структуры имеют префикс в виде метки "Structure.".  
  
> [!NOTE]  
>  Для существующей структуры интеллектуального анализа данных нельзя включить детализацию. Вместо этого следует создать повторно структуру интеллектуального анализа данных и включить детализацию в процессе создания.  
  
 Дополнительные сведения о доступе к данным вариантов из каждого средства просмотра моделей интеллектуального анализа данных, в которых поддерживается детализация, **см. в разделе** [Выполнение детализации до данных вариантов из модели интеллектуального анализа данных](data-mining/drill-through-to-case-data-from-a-mining-model.md).  
  
## <a name="options"></a>Параметры  
 **Варианты систематизированы как**  
 Отображает определение правила, набора элементов и кластера, содержащихся в выбранном узле.  
  
 **Список столбцов**  
 Отображает столбцы модели, за которыми следуют столбцы структуры.  
  
 **ПРИМЕЧАНИЕ.** Столбцы структуры отображаются, только если в структуре интеллектуального анализа данных включена детализация и выбран параметр **Столбцы модели и структуры**. Более того, чтобы просмотреть столбцы необходимо обладать разрешениями на детализацию как для модели, так и для структуры интеллектуального анализа данных.  
  
 Столбцы структуры, которые не находятся в модели отображаются как **структуры.\< Имя столбца >**.  
  
> [!NOTE]  
>  Чтобы скопировать данные детализации в буфер обмена в формате с разделителями — знаками табуляции, можно щелкнуть правой кнопкой мыши любое место сетки столбцов и выбрать команду **Копировать все**. Будут скопированы только данные вариантов, но не определение узла.  
  
 **Воспроизведение**  
 Нажмите кнопку с зеленой стрелкой, чтобы обновить данные.  
  
## <a name="see-also"></a>См. также  
 [Запросы детализации (интеллектуальный анализ данных)](data-mining/drillthrough-queries-data-mining.md)   
 [Средства просмотра моделей интеллектуального анализа данных (конструктор моделей интеллектуального анализа данных)](mining-model-viewers-data-mining-model-designer.md)   
 [Задачи и инструкции по средству просмотра моделей интеллектуального анализа данных](data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
