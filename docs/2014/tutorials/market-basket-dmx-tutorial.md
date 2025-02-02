---
title: Учебник расширений интеллектуального анализа данных потребительской корзины | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- market basket analysis [Analysis Services]
- tutorials [Data Mining]
- tutorials [DMX]
ms.assetid: 6e262a1d-c89e-4033-8368-46cf25168ef5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe12f1c4ca1c0946572c61e89f4f4edb8ba9a762
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185643"
---
# <a name="market-basket-dmx-tutorial"></a>Учебник по расширениям интеллектуального анализа данных потребительской корзины
  С помощью данного учебника вы научитесь создавать, обучать и исследовать модели интеллектуального анализа данных при помощи языка запросов расширения интеллектуального анализа данных (DMX). После этого вы будете использовать модели интеллектуального анализа данных для создания прогнозов, описывающих, какие продукты будут покупаться с наибольшей вероятностью.  
  
 Модели интеллектуального анализа данных будут созданы на основе данных, содержащихся в образце базы данных [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], где хранятся данные вымышленной компании [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] является крупной транснациональной производственной организацией. Компания изготавливает и продает велосипеды из металла и композитных материалов в Северной Америке, а также на европейском и азиатском рынках. Основное производство расположено в городе Ботель, штат Вашингтон, и имеет 290 служащих; существуют несколько региональных групп продаж, расположенных на территории рынков сбыта.  
  
## <a name="tutorial-scenario"></a>Сценарий учебника  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] приняла решение создать пользовательское приложение с применением функциональности интеллектуального анализа данных, чтобы предсказать, какие типы продуктов наиболее вероятно будут покупаться клиентами. Целью приложения является возможность определить набор продуктов и предсказать, какие дополнительные продукты будут покупаться вместе с другими продуктами. После этого [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] будет использовать полученные сведения, чтобы добавить на веб-сайт новую функцию — «Предложение», а также лучше предоставлять информацию клиентам.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] предоставляют ряд средств, которые могут использоваться для выполнения этой задачи.  
  
-   Язык DMX-запросов  
  
-   [Алгоритм взаимосвязей (Майкрософт)](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)  
  
-   Редактор запросов в среде [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 Расширения интеллектуального анализа данных представляют собой язык запросов, предоставляемый службами [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] и используемый для создания и работы с моделями интеллектуального анализа данных. [!INCLUDE[msCoName](../includes/msconame-md.md)] Алгоритм взаимосвязей Майкрософт создает модели, которые могут предсказывать продукты, которые, скорее всего, будут приобретены вместе.  
  
 Целью данного учебника является описание запросов расширений интеллектуального анализа данных, которые используются в описанном выше приложении.  
  
 **Дополнительные сведения см. в следующих разделах:** [Решения для интеллектуального анализа данных](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>Структура и модели интеллектуального анализа данных  
 Перед созданием инструкций для расширения интеллектуального анализа данных важно понять, какие основные объекты служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] используются для создания моделей интеллектуального анализа данных. *Структуры интеллектуального анализа данных* — это структура данных, определяющая домен данных, на основе которого строятся модели интеллектуального анализа данных. Структура интеллектуального анализа данных может содержать несколько *моделей интеллектуального анализа данных* , общий доступ к тому же домену. Модель интеллектуального анализа данных применяет алгоритм интеллектуального анализа к данным, представленным структурой интеллектуального анализа данных.  
  
 Строительными блоками структуры интеллектуального анализа являются столбцы, которые описывают данные, содержащиеся в источнике данных. Эти столбцы содержат такие сведения, как тип данных, тип содержимого и способы распределения данных.  
  
 Модели интеллектуального анализа данных должны включать ключевой столбец, описанный в структуре интеллектуального анализа данных, а также набор оставшихся столбцов. Модель интеллектуального анализа данных определяет использование каждого столбца и определяет алгоритм, используемый для создания этой модели. Например, в расширении интеллектуального анализа данных можно указать столбец в качестве ключевого или столбца типа PREDICT. Если столбец не указан, он считается входным столбцом.  
  
 В расширении интеллектуального анализа данных существует два способа создания моделей интеллектуального анализа данных. Можно либо создать структуру интеллектуального анализа данных и связанную модель интеллектуального анализа данных вместе с помощью инструкции `CREATE MINING MODEL`, либо вначале создать структуру интеллектуального анализа данных с помощью инструкции `CREATE MINING STRUCTURE`, а затем добавить к структуре модель интеллектуального анализа данных с помощью инструкции `ALTER STRUCTURE`. Эти методы описаны ниже.  
  
 `CREATE MINING MODEL`  
 Эта инструкция используется для одновременного создания структуры интеллектуального анализа данных и связанной с ней модели интеллектуального анализа данных с одним и тем же именем. К имени модели интеллектуального анализа данных добавляется слово «Structure», чтобы отличить ее от структуры интеллектуального анализа данных.  
  
 Эта инструкция полезна, если создается структура интеллектуального анализа данных, которая будет содержать только одну модель интеллектуального анализа данных.  
  
 Дополнительные сведения см. в статье [CREATE MINING MODEL (расширения интеллектуального анализа данных)](/sql/dmx/create-mining-model-dmx).  
  
 CREATE MINING STRUCTURE  
 Эта инструкция используется для создания новой структуры интеллектуального анализа данных без использования моделей.  
  
 При использовании CREATE MINING STRUCTURE можно также создать набор контрольных данных, который может быть использован для проверки моделей, основанных на той же структуры интеллектуального анализа данных.  
  
 Дополнительные сведения см. в статье [CREATE MINING STRUCTURE (DMX)](/sql/dmx/create-mining-structure-dmx).  
  
 `ALTER MINING STRUCTURE`  
 Эта инструкция используется для добавления модели интеллектуального анализа данных к уже существующей на сервере структуре интеллектуального анализа данных.  
  
 Есть несколько причин, почему может понадобиться добавить несколько моделей интеллектуального анализа данных в структуру интеллектуального анализа данных. Например, можно создать несколько моделей интеллектуального анализа данных, которые используют разные алгоритмы, чтобы выяснить, какой из них самый лучший. При помощи одного и того же алгоритма можно создать несколько различных моделей и установить для них различные настройки определенного параметра, чтобы выяснить, какое значение параметра является наилучшим.  
  
 Дополнительные сведения см. в разделе [ALTER MINING STRUCTURE &#40;расширений интеллектуального анализа данных&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016).  
  
 В этом учебнике создается структура интеллектуального анализа данных, которая содержит несколько моделей, поэтому в учебнике используется второй метод.  
  
 **Дополнительные сведения**  
  
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; ссылку](/sql/dmx/data-mining-extensions-dmx-reference), [основные сведения о расширениях интеллектуального анализа данных инструкция "Select"](/sql/dmx/understanding-the-dmx-select-statement), [структура и методы использования прогнозирующих запросов расширений интеллектуального анализа данных](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>Обзор учебника  
 Учебник содержит следующие занятия:  
  
 [Занятие 1. Создание структуры интеллектуального анализа данных потребительской корзины](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)  
 На этом занятии рассматривается использование инструкции `CREATE` для создания структур интеллектуального анализа данных.  
  
 [Занятие 2. Добавление моделей интеллектуального анализа данных к структуре интеллектуального анализа данных потребительской корзины](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
 На этом занятии рассматривается использование инструкции `ALTER` для добавления моделей интеллектуального анализа данных в структуру интеллектуального анализа данных.  
  
 [Занятие 3. Обработка структуры интеллектуального анализа данных потребительской корзины](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
 На этом занятии рассматривается использование инструкции `INSERT INTO` для обработки структур интеллектуального анализа данных и связанных с ними моделей интеллектуального анализа данных.  
  
 [Занятие 4. Выполнение прогнозов потребительской корзины](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
 На этом занятии рассматривается использование инструкции `PREDICTION JOIN` для создания прогнозов по моделям интеллектуального анализа данных.  
  
## <a name="requirements"></a>Требования  
 Прежде чем выполнять задания этого учебника, убедитесь, что установлены следующие компоненты:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   База данных [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]  
  
 В целях повышения безопасности образцы баз данных по умолчанию не установлены. Чтобы установить официальные образцы баз данных для [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], перейдите в меню [ http://www.CodePlex.com/MSFTDBProdSamples ](https://go.microsoft.com/fwlink/?LinkId=88417) или на домашней странице Microsoft SQL Server Samples and Community Projects в разделе Microsoft SQL Server Product Samples. Нажмите кнопку **баз данных**, нажмите кнопку **выпуски** вкладку и выберите нужные базы данных.  
  
> [!NOTE]  
>  При просмотре учебников рекомендуется добавить **следующий раздел** и **предыдущий раздел** кнопок панели инструментов средства просмотра документов.  
  
## <a name="see-also"></a>См. также  
 [Bike Buyer расширений интеллектуального анализа данных учебника](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [Учебник по основам интеллектуального анализа данных](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Занятие 3. Построение сценария потребительской корзины &#40;средний уровень учебник по интеллектуальному анализу данных&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
