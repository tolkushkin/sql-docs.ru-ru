---
title: Преобразование "Процентная выборка" | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtrans.f1
helpviewer_keywords:
- testing mining models
- sampling seeds [Integration Services]
- data mining [Analysis Services], sample data sets
- Percentage Sampling transformation
- sample data sets [Integration Services]
- datasets [Integration Services], sample
- training mining models
ms.assetid: 59767e52-f732-4b3f-8602-be50d0a64ef2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 27d3ff9ef1c6296a6bec2040f9caefd477568bfa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900150"
---
# <a name="percentage-sampling-transformation"></a>преобразование «Процентная выборка»
  Преобразование «Процентная выборка» создает образец набора данных извлечением некоторого процента входных строк преобразования. Данные выборки извлекаются случайным образом из входа преобразования. За счет этого достигается репрезентативность выборки.  
  
> [!NOTE]  
>  Помимо заданного количества процентов преобразование «Процентная выборка» использует алгоритм, определяющий возможность включения строки в результирующую выборку. Это означает, что количество строк в выборке может не соответствовать точно заданному количеству процентов. Например, определив 10 процентов от входного набора данных, содержащего 25000 строк, можно получить выборку, содержащую немного больше или немного меньше, чем 2500 строк.  
  
 Преобразование «Процентная выборка» особенно полезно для интеллектуального анализа данных. С помощью этого преобразования можно случайным образом разделить набор данных на два набора: один — для изучения модели интеллектуального анализа данных, другой — для тестирования этой модели.  
  
 Преобразование «Процентная выборка» также полезно для создания образца набора данных, используемого при разработке пакета. Применяя преобразование «Процентная выборка» к потоку данных, можно уменьшить размер набора данных, сохраняя его статистические характеристики. Тестовый пакет можно выполнить быстрее, потому что он содержит меньший, но репрезентативный набор данных.  
  
## <a name="configuration-the-percentage-sampling-transformation"></a>Настройка преобразования «Процентная выборка»  
 Можно изменить начальное значение генератора случайных чисел, используемого для выборки строк. Если всегда использовать одинаковое начальное значение для генератора, то результирующая выборка, при прочих равных условиях, будет тоже всегда одинаковая. Если начальное значение для создания случайного номера не указано, преобразование использует счетчик тактов операционной системы. Поэтому можно выбрать постоянное начальное значение для генератора во время отладки и случайное значение при передаче пакета в производственную эксплуатацию.  
  
 Это преобразование немного схоже с преобразованием «Выборка строк», которое создает выборку с заданным количеством строк. Дополнительные сведения см. в статье [Row Sampling Transformation](row-sampling-transformation.md).  
  
 Преобразование «Процентная выборка» содержит пользовательское свойство `SamplingValue`. Это свойство может быть обновлено выражением свойства при загрузке пакета. Дополнительные сведения см. в разделах [Выражения служб Integration Services (SSIS)](../../expressions/integration-services-ssis-expressions.md), [Использование выражений свойств в пакетах](../../expressions/use-property-expressions-in-packages.md) и [Пользовательские свойства преобразований](transformation-custom-properties.md).  
  
 Преобразование имеет один вход и два выхода. Вывод ошибок не поддерживается.  
  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно установить в диалоговом окне **Редактор преобразования «Процентная выборка»** , см. в разделе [Percentage Sampling Transformation Editor](../../percentage-sampling-transformation-editor.md).  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](../../common-properties.md)  
  
-   [Пользовательские свойства преобразований](transformation-custom-properties.md)  
  
 Дополнительные сведения о настройке свойств см. в разделе [Установление свойств компонента потока данных](../set-the-properties-of-a-data-flow-component.md).  
  
  
