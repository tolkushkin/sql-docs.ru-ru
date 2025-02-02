---
title: Создание связей | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.createrelationships.f1
ms.assetid: 6ebd305f-ffd2-4a1d-b24c-e28c151b94f5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 647fa27d872829a60d32c0cdc7686938ae796f2a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770380"
---
# <a name="create-relationships"></a>Создание связей
  Используйте диалоговое окно **Создание связей** , чтобы изменить сопоставления между исходными столбцами и столбцами таблицы уточняющих запросов, настроенные в редакторе преобразования «Нечеткий уточняющий запрос», в редакторах преобразования «Уточняющий запрос» и «Уточняющий запрос термина».  
  
> [!NOTE]  
>  Диалоговое окно **Создание связей** отображает только списки **Входной столбец** и **Столбец подстановок** , если вызвано из редактора преобразования "Уточняющий запрос термина".  
  
 Дополнительные сведения о преобразованиях, использующих диалоговое окно **Создание связей** см. в разделах [Fuzzy Lookup Transformation](lookup-transformation.md), [Lookup Transformation](lookup-transformation.md)и [Term Lookup Transformation](term-lookup-transformation.md).  
  
## <a name="options"></a>Параметры  
 **Входной столбец**  
 Выберите входной столбец из списка имеющихся входных столбцов.  
  
 **Столбец подстановок**  
 Выберите из списка доступных столбцов подстановок.  
  
 **Тип сопоставления**  
 Выберите нечеткое или четкое соответствие.  
  
 При использовании нечеткого соответствия строки рассматриваются как дубликаты, если они в значительной степени совпадают по всем столбцам, имеющим нечеткий тип соответствия. Для получения лучших результатов от нечеткого соответствия можно указать, чтобы некоторые столбцы использовали четкое соответствие вместо нечеткого. Например, если известно, что конкретный столбец не содержит ошибок или противоречий, то возможно указать для этого столбца четкое соответствие, таким образом, чтобы в качестве дубликатов рассматривались лишь те строки, которые содержат идентичные значения в этом столбце. Это увеличивает степень точности нечеткого соответствия по другим столбцам.  
  
 **Флаги сравнения**  
 Дополнительные сведения о параметрах сравнения строк см. в разделе [Сравнение строковых данных](../comparing-string-data.md).  
  
 **Минимальное подобие**  
 Установите порог подобия на уровне столбцов, используя ползунок. Чем ближе это значение к 1, тем ближе должно быть сходство между значением уточняющего столбца и исходным значением, чтобы они считались соответствующими. Увеличение этого порога может повысить скорость нахождения совпадений, так как количество рассматриваемых потенциальных записей будет меньше.  
  
 **Псевдоним выхода подобия**  
 Укажите имя для нового выходного столбца, который является подобным выбранному столбцу. Если оставить это значение пустым, то выходной столбец не будет создан.  
  
## <a name="see-also"></a>См. также  
 [Справочник по сообщениям об ошибках служб Integration Services](../../integration-services-error-and-message-reference.md)   
 [Редактор преобразования "Нечеткий уточняющий запрос" (вкладка "Столбцы")](../../fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Редактор преобразования "Уточняющий запрос" (страница "Столбцы")](../../lookup-transformation-editor-columns-page.md)   
 [Редактор преобразований "Уточняющий запрос термина" (вкладка "Уточняющий запрос термина")](../../term-lookup-transformation-editor-term-lookup-tab.md)  
  
  
