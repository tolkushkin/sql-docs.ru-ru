---
title: Панель результатов (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- result sets [SQL Server], queries
- synchronization [SQL Server], query results with definition
- displaying query results in grid
- grid showing query results [SQL Server]
- showing query results in grid
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- viewing query results
- queries [SQL Server], results
- Results pane
ms.assetid: 6309a1bc-a628-4141-8bb5-b35924bd19f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 87bfaef1ad5dc4c9b1f907c27955ca3f156038a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63067810"
---
# <a name="results-pane-visual-database-tools"></a>Панель результатов (визуальные инструменты для баз данных)
  панель результатов отображает результаты самого последнего выполненного запроса SELECT (результаты запросов других типов отображаются в окнах сообщений). Чтобы открыть панель результатов, откройте или создайте запрос или представление или получите данные таблицы. Если панель результатов не отображается по умолчанию, в меню **Конструктор запросов** выберите пункт **Панель**и щелкните **Результаты**.  
  
## <a name="what-you-can-do-in-the-results-pane"></a>Что можно делать на панели результатов:  
  
-   Просматривать результирующие наборы самого последнего выполненного запроса SELECT в виде табличной сетки.  
  
-   Для запросов или представлений, показывающих данные из отдельной таблицы или представления, можно редактировать значения отдельных столбцов результирующего набора, добавлять новые строки и удалять существующие.  
  
## <a name="limitations-in-the-results-pane"></a>Ограничения, относящиеся к панели результатов  
  
-   Результаты функций, возвращающих табличное значение, можно обновлять только в некоторых случаях.  
  
-   Невозможно обновить запросы или представления, включающие столбцы из нескольких таблиц или представлений.  
  
-   Нельзя обновлять результаты, возвращаемые хранимой процедурой.  
  
-   Нельзя обновлять запросы или представления, содержащие предложения GROUP BY или DISTINCT  
  
## <a name="navigating-in-the-results-pane"></a>Перемещение по панели результатов  
 Используя панель навигации в нижней части области результатов, можно быстро перемещаться по записям.  
  
 На панели имеются кнопки для перехода к первой и последней записи, к следующей и предыдущей записи, а также для перехода к конкретной записи.  
  
 Чтобы перейти к конкретной записи, наберите соответствующий номер строки в текстовом поле на панели навигации, а затем нажмите клавишу ВВОД.  
  
 Сведения об использовании сочетаний клавиш в конструкторе запросов и представлений см. в разделе [Навигация по конструктору запросов и представлений (визуальные инструменты для баз данных)](visual-database-tools.md).  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Синхронизация наборов результатов с определением запроса  
 Во время работы с результатами запроса или представления существует вероятность, что записи на панели результатов окажутся не синхронизированы с определением запроса. Например, при выполнении запроса для четырех из пяти столбцов таблицы и последующего добавления пятого столбца к определению запроса на панели диаграмм, данные этого пятого столбца не будут автоматически добавлены на панель результатов. Чтобы на панели результатов отображалось новое определение запроса, необходимо запустить запрос снова.  
  
 Если запрос изменился, в правом нижнем углу панели результатов появляется значок предупреждения и текст «Запрос изменен». Изображение значка появляется также в левом верхнем углу панели.  
  
## <a name="see-also"></a>См. также  
 [Создание запросов &#40;визуальных инструментах баз данных&#41;](create-queries-visual-database-tools.md)   
 [Выполнение запросов &#40;визуальных инструментах баз данных&#41;](run-queries-visual-database-tools.md)   
 [Проектирование запросов и представлений инструкции &#40;визуальных инструментах баз данных&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Панель диаграмм &#40;визуальных инструментах баз данных&#41;](diagram-pane-visual-database-tools.md)   
 [Панель критериев &#40;визуальных инструментах баз данных&#41;](criteria-pane-visual-database-tools.md)   
 [Работа с данными на панели результатов (визуальные инструменты для баз данных)](results-pane-visual-database-tools.md)  
  
  
