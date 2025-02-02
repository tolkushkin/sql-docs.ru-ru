---
title: Подсчет строк в таблице (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- totals [SQL Server], row counts
- row counts [SQL Server]
- column values [SQL Server]
- number of rows
- number of values
- counting rows
ms.assetid: dda4296a-1d16-4e77-8d6f-e295f6dd4e87
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 68e4d3787e1ad71673ddecfbcf94abb9b97afc6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65089483"
---
# <a name="count-rows-in-a-table-visual-database-tools"></a>подсчитать строки в таблице (визуальные инструменты для баз данных)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Строки в таблице можно подсчитать, чтобы определить:  
  
-   общее число строк в таблице, например подсчет всех книг в таблице `titles` ;  
  
-   количество строк в таблице, удовлетворяющих определенному условию (например количество книг одного издателя в таблице `titles` );  
  
-   количество значений в определенном столбце.  
  
При подсчете значений в столбце значения NULL не учитываются. Например можно подсчитать количество книг в таблице `titles` , имеющих значения в столбце `advance` . По умолчанию подсчет включает все значения, а не только уникальные.  
  
Процедуры выполнения для всех трех типов похожи.  
  
### <a name="to-count-all-the-rows-in-a-table"></a>Подсчет всех строк в таблице  
  
1.  Убедитесь, что таблица, по которой необходимо подвести итог, уже имеется на панели диаграмм.  
  
2.  Щелкните правой кнопкой мыши фон панели диаграммы и выберите из контекстного меню пункт **Добавить Group By** . [Конструктор запросов и представлений](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) добавляет столбец **Группировать** в сетку на панели критериев.  
  
3.  В прямоугольнике, представляющем таблицу или возвращающем табличное значение объект, выберите **&#42; (все столбцы)** .  
  
    Конструктор запросов и представлений автоматически заносит значение **Подсчет** в столбец **Group By** на панели критериев и присваивает столбцу, по которому подводится итог, псевдоним столбца. Псевдоним, созданный автоматически, можно заменить более содержательным псевдонимом. Дополнительные сведения см. в разделе [Создание псевдонимов столбцов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
4.  Выполните запрос.  
  
### <a name="to-count-all-the-rows-that-meet-a-condition"></a>Подсчет всех строк, удовлетворяющих условию  
  
1.  Убедитесь, что таблица, по которой необходимо подвести итог, уже имеется на панели диаграмм.  
  
2.  Щелкните правой кнопкой мыши фон панели диаграммы и выберите из контекстного меню пункт **Добавить Group By** . Конструктор запросов и представлений добавляет столбец **Группировать** в сетку на панели критериев.  
  
3.  В прямоугольнике, представляющем таблицу или возвращающем табличное значение объект, выберите **&#42(все столбцы)** .  
  
    Конструктор запросов и представлений автоматически заносит значение **Подсчет** в столбец **Group By** на панели критериев и присваивает столбцу, по которому подводится итог, псевдоним столбца. О создании более содержательного заголовка столбца в выводе запроса см. в разделе [Создание псевдонимов столбцов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
4.  Добавьте столбец данных, по которому необходимо произвести поиск, затем снимите флажок в столбце **Вывод**.  
  
    Конструктор запросов и представлений автоматически заносит значение **Группировать** в столбец сетки **Group By** .  
  
5.  Замените значение **Группировать** в столбце **Group By** на значение **Куда**.  
  
6.  В столбце **Фильтр** введите условие для выполнения поиска по столбцу данных.  
  
7.  Выполните запрос.  
  
### <a name="to-count-the-values-in-a-column"></a>Подсчет значений в столбце  
  
1.  Убедитесь, что таблица, по которой необходимо подвести итог, уже имеется на панели диаграмм.  
  
2.  Щелкните правой кнопкой мыши фон панели диаграммы и выберите из контекстного меню пункт **Добавить Group By** . Конструктор запросов и представлений добавляет столбец **Группировать** в сетку на панели критериев.  
  
3.  Добавьте столбец, по которому необходимо подвести итог, на панели критериев.  
  
    Конструктор запросов и представлений автоматически заносит значение **Группировать** в столбец сетки **Group By** .  
  
4.  Замените значение **Группировать** в столбце **Group By** на значение **Подсчет**.  
  
    > [!NOTE]  
    > Чтобы подсчитать только уникальные значения, выберите **Count Distinct**.  
  
5.  Выполните запрос.  
  
## <a name="see-also"></a>См. также:  
[Результаты запросов сортировки и группирования (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Резюмирование результатов запросов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
