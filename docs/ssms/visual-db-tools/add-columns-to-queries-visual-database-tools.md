---
title: Добавление столбцов в запросы (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2ae2ace318d49ff524379c3f825d8da272674755
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65088847"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>Добавление столбцов в запросы (визуальные инструменты для баз данных)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Для использования столбца в запросе его необходимо туда добавить. Можно добавлять столбцы для отображения в результатах выполнения запроса, для использования при сортировке, поиска или обобщения их содержимого. Выбрать, какие используемые в запросе столбцы необходимо включить на панель результатов, можно при выполнении запроса. Дополнительные сведения см. в разделе [Удаление столбцов из результатов запроса (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md).  
  
> [!NOTE]  
> Для просмотра типа данных столбца в конструкторе запросов и представлений выберите таблицу или возвращающий табличное значение объект на **панели диаграммы** , а затем щелкните "Список столбцов" в окне свойств. После этого нажмите кнопку с многоточием **(...)**, чтобы открыть диалоговое окно **Список столбцов**.  
  
При работе со столбцами в запросе можно также применять выражение, состоящее из любого сочетания столбцов, литералов, операторов и функций.  
  
### <a name="to-add-an-individual-column"></a>Добавление отдельного столбца  
  
-   На **панели диаграммы**установите флажок рядом со столбцом, который требуется включить.  
  
    -или-  
  
-   На **панели критериев**перейдите на первую пустую строку сетки, щелкните поле в столбце **Столбец** и выберите имя столбца из раскрывающего списка.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>Добавление всех столбцов одной таблицы или возвращающего табличное значение объекта  
  
-   На **панели диаграммы**установите флажок **#42;(все столбцы)**.  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>Добавление всех столбцов всех таблиц и табличных объектов  
  
1.  Убедитесь, что строки соединения не выбраны на **панели операций с таблицей** .  
  
2.  Щелкните правой кнопкой мыши пустую область окна проектирования и выберите пункт **Свойства** из контекстного меню.  
  
3.  В окне "Свойства" щелкните **Выводить все столбцы** и выберите **Да** или **Нет** из раскрывающегося списка.  
  
## <a name="see-also"></a>См. также:  
[Удаление столбцов из результатов запроса (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[Удаление столбцов из запросов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[Определение критериев поиска (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Резюмирование результатов запросов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Выполнение основных операций с запросами (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
