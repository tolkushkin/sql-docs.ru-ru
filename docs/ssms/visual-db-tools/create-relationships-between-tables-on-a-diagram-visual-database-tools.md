---
title: Создание связей между таблицами на диаграмме | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a6722dcbc9f9052803ef32a3b1bdb75a9e06de31
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090023"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>Создание связи между таблицами на диаграмме (визуальные инструменты для баз данных)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Можно создавать связи между столбцами разных таблиц в конструкторе диаграмм, перетаскивая столбцы между таблицами.  
  
### <a name="to-create-a-relationship-graphically"></a>Графическое создание связи  
  
1.  В конструкторе баз данных щелкните селектор строк для одного или более столбцов базы данных, которые необходимо связать со столбцом в другой таблице.  
  
2.  Перетащите выбранные столбцы в связанную таблицу.  
  
3.  Отобразятся два диалоговых окна: **Связь по внешнему ключу** и **Таблицы и столбцы**, второе отображается на переднем плане.  
  
4.  **Имя связи** устанавливается системой в формате FK_*локальная_таблица*\_*таблица_внешнего_ключа*. Можно изменить это значение.  
  
5.  Убедитесь, что **Таблица первичного ключа** правильно задает таблицу.  
  
6.  Сетка содержит локальные столбцы и соответствующие им внешние столбцы. Можно добавить или удалить столбцы таблицы, либо изменить сопоставления.  
  
7.  Нажмите кнопку **ОК**.  
  
    Открывается диалоговое окно **Связь по внешнему ключу** . **Выбранная связь** отображает созданную связь.  
  
8.  Измените свойства связи в сетке.  
  
9. Нажмите кнопку **OК** , чтобы создать связь.  
  
    Конструктор баз данных отображает связь между выбранными столбцами.  
  
## <a name="see-also"></a>См. также:  
[Диалоговое окно "Таблицы и столбцы" (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/tables-and-columns-dialog-box-visual-database-tools.md)  
[Работа с ограничениями (визуальные инструменты для баз данных)](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)  
[Работа с таблицами в диаграммах базы данных (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  
