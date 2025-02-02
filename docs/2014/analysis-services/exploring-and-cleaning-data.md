---
title: Исследование и очистка данных | Документация Майкрософт
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79d356aa1b14ac30ba5bc9a8f579fc66ddebea92
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081271"
---
# <a name="exploring-and-cleaning-data"></a>Исследование и очистка данных
  Подготовка данных — это не просто очистка данных. Помните, что качество подготовки данных в конечном итоге влияет на интерпретацию результатов. Подготовка данных включает в себя следующие задачи:  
  
-   анализ и проверка распределения данных;  
  
-   очистка недействительных записей и выбор столбцов для интеллектуального анализа данных;  
  
-   правильная обработка значений NULL;  
  
-   группировка или статистическая обработка значений с различными временными блоками;  
  
-   добавление меток для повышения удобства использования результатов;  
  
-   преобразование типов данных или классификации значений, если это необходимо для анализа.  
  
 Если вы не знакомы с моделированием, мы рекомендуем прочитать связанной статье [контрольный список Preparation for Data Mining](checklist-of-preparation-for-data-mining.md).  
  
## <a name="data-preparation-tools"></a>Средства подготовки данных  
 Надстройки интеллектуального анализа данных для Office представляют следующие средства для очистки и подготовки данных:  
  
### <a name="explore-data"></a>Просмотр данных  
 Используйте **Просмотр данных** мастера для этих задач подготовки данных:  
  
-   Предварительный просмотр данных и определение ошибок, которые нужно исправить перед анализом.  
  
-   Сбор статистических данных, которые могут оказаться полезными для понимания баланса данных и необходимых задач очистки.  
  
-   Определение столбцов, полезных для анализа, и планирование этапа моделирования данных.  
  
 [Просмотр данных &#40;надстройки интеллектуального анализа данных SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md).  
  
### <a name="detect-and-handle-outliers"></a>Определение и обработка выбросов  
 **Выбросы** мастер графическое представление распределения значений в данных и позволяет удалить крайние значения. Используйте **выбросы** средство для выполнения следующих задач подготовки данных:  
  
-   Определение надежности отдельных значений на основе закономерностей, обнаруженных в данных.  
  
-   Изучение необычных значений и последующее их удаление или замена.  
  
-   Определение области действия модели для определенного диапазона значений. Например, если известно, что в одном магазине присутствуют выбросы, можно устранить эти значения и получить модель, которая создает более эффективные прогнозы для других магазинов.  
  
 [Выбросы &#40;надстройки интеллектуального анализа данных SQL Server&#41;](outliers-sql-server-data-mining-add-ins.md).  
  
### <a name="relabel-and-bin-data"></a>Переразметка и преобразование данных в двоичные  
 **Переразметка** мастер группирует данные по значениям, таким образом, можно изменить метки данных. Используйте средство «Переразметка» для выполнения следующих задач подготовки данных:  
  
-   Изменение числовых кодов, используемых в результатах опроса, для текстового описания значения числовых кодов.  
  
     Например, можно заменить такие входные данные, как «пол = 1» на «пол = женский».  
  
-   Двоичные данные путем создания групп, представляющих диапазоны чисел.  
  
     Например, может потребоваться заменить столбец чисел дохода метки подобной **доход — Средний** и **дохода — высокий**.  
  
-   Распределение дискретных значений по категориям.  
  
     Например, если имеется слишком много отдельных продуктов, чтобы обнаружить закономерность среди покупок, можно попробовать сгруппировать продукты в более общие категории.  
  
 [Переразметка &#40;надстройки интеллектуального анализа данных SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>Очистка данных  
 Очистка данных включает различные действия, большая часть которых поддерживается надстройками  
  
-   Распознает значения NULL и определяет, должны они быть заменены на действительные значения или обработаны как значения `Missing`.  
  
-   Обнаружение отсутствующих значений и их удаление или аппроксимация (например, использование среднего значения, NULL или другого значения).  
  
 [Просмотр данных &#40;надстройки интеллектуального анализа данных SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [Переразметка &#40;надстройки интеллектуального анализа данных SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [Заполнение по примеру](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>Образец данных  
 Мастер образцов данных предоставляет два метода создания сбалансированных наборов данных для обучения и проверки моделей  
  
-   **Случайная выборка.** Используйте этот параметр, чтобы извлечь репрезентативный набор данных из большего набора данных для использования в обучении или тестировании. Надстройки интеллектуального анализа данных используют *стратифицированная выборка* для убедитесь, что для каждой переменной выборки получается Сбалансированный набор значений.  
  
-   **Избыточная выборка.** Используйте этот параметр, если данных меньше, чем требуется для целевого результата, и нужно назначить этим данным больший вес. Например, мошенничество может происходить редко, но по имеющимся случаям можно сформировать избыточную выборку для моделирования.  
  
 [Образец данных &#40;надстройки интеллектуального анализа данных SQL Server&#41;](sample-data-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>См. также  
 [Создание модели интеллектуального анализа данных](creating-a-data-mining-model.md)   
 [Проверка моделей и использование моделей для прогнозирования &#40;интеллектуального анализа данных надстройки для Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Развертывание и масштабирование моделей интеллектуального анализа данных &#40;интеллектуального анализа данных надстройки для Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
