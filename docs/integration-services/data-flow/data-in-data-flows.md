---
title: Данные потоков данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- comparing data
- data types [Integration Services], data flow
- parsing [Integration Services]
- string comparisons
- data flow [Integration Services], data options
ms.assetid: 8a9d6186-eb52-48e3-997e-021f24d458a3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2ae28de186f1f411792b1f20b728c473e6df4bca
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727015"
---
# <a name="data-in-data-flows"></a>Данные потоков данных

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] предоставляют набор типов данных, используемых в потоках данных.  
  
## <a name="data-type-conversion"></a>Преобразование типов данных  
 Источник, который добавляется в поток данных, преобразовывает исходные данные в типы данных служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Последующие преобразования могут преобразовать данные в различные типы данных служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , и в зависимости от типа хранилища данных, в который загружаются данные, назначения могут преобразовать конечный тип данных [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] в тип данных, необходимый целевому хранилищу данных. Дополнительные сведения см. в разделе [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Для преобразования данных в тип данных [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] компонент потока данных производит синтаксический анализ данных. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] предусматривают два типа синтаксического анализа данных: быстрый и стандартный. Большинство компонентов потока данных могут использовать только стандартный анализ; однако, источник неструктурированного файла и преобразование «Конвертация данных» могут использовать как быстрый, так и стандартный синтаксический анализ. Дополнительные сведения см. в статье [Parsing Data](../../integration-services/data-flow/parsing-data.md).  
  
## <a name="data-type-comparison"></a>Сравнение типов данных  
 Многие преобразования сравнивают значения данных. Например, преобразование «Статистическая обработка» сравнивает значения с целью статистической обработки значений в наборе строк данных, преобразование «Сортировка» сравнивает значения с целью их сортировки, а преобразование «Уточняющий запрос» сравнивает значения со значениями в отдельной ссылочной таблице. Для определения способа сравнения строк преобразование включает ряд параметров сравнения, таких как использование чувствительности к регистру, способ обработки знаков кана в японском тексте и использование разделителей в строке. Дополнительные сведения см. в разделе [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).  
  
 Средство оценки выражений при вычислении сравнивает также значения данных, используемых переменными, элементами управления очередностью и преобразованиями.  
  
## <a name="data-flow-troubleshooting"></a>Устранение неполадок в потоке данных  
 После развертывания пакета в каталоге служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] можно проанализировать поток данных, возникающий во время выполнения пакета, для проверки производительности или обнаружения других проблем. Доступны стандартные отчеты, позволяющие просматривать состояние пакета и журнал событий. Можно также запросить представления базы данных, которые содержат подробные сведения о выполнении пакета. Также можно динамически добавлять и удалять отводы данных во время выполнения пакета, чтобы получить сведения о конкретных компонентах пакета. Дополнительные сведения см. в статье [Отладка потока данных](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
  
