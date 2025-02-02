---
title: Заполнение таблицы существующими иерархическими данными | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: fd943d84-dbe6-4a05-912b-c88164998d80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b2614d090bce0ecf0c61db5c9a5222ec6b10951
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66110166"
---
# <a name="populating-a-table-with-existing-hierarchical-data"></a>Заполнение таблицы существующими иерархическими данными
  В этой задаче создается таблица и заполняется данными из таблицы **EmployeeDemo**. Эта задача включает следующие шаги.  
  
-   Создание новой таблицы, содержащей столбец типа данных `hierarchyid`. Этот столбец может заменить существующие столбцы **EmployeeID** и **ManagerID** . Однако эти столбцы нужно сохранить. Это нужно для того, чтобы существующие приложения могли ссылаться на эти столбцы, а также для помощи при распознавании данных после передачи. Определение таблицы задает столбец **OrgNode** как первичный ключ, следовательно, этот столбец должен содержать уникальные значения. В кластеризованном индексе на основе столбца **OrgNode** будут храниться данные в последовательности ключа **OrgNode** .  
  
-   Создание временной таблицы, которая будет использована для слежения за тем, сколько сотрудников напрямую подчиняются каждому менеджеру.  
  
-   Заполнение новой таблицы данными из таблицы **EmployeeDemo** .  
  
### <a name="to-create-a-new-table-named-neworg"></a>Создание новой таблицы с именем NewOrg  
  
-   В окне редактора запросов запустите приведенный ниже код, чтобы создать таблицу с именем **HumanResources.NewOrg**.  
  
    ```  
    CREATE TABLE NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="to-create-a-temporary-table-named-children"></a>Создание новой таблицы с именем #Children  
  
1.  Создайте временную таблицу с именем **#Children** . В ней должен быть столбец **Num** , который должен содержать количество потомков каждого узла:  
  
    ```  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  Добавьте индекс, который значительно ускорит работу запроса, заполняющего таблицу **NewOrg** :  
  
    ```  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="to-populate-the-neworg-table"></a>Заполнение таблицы NewOrg  
  
1.  Рекурсивные запросы запрещают использование вложенных запросов со статистическими выражениями. Вместо этого заполните таблицу **#Children** с помощью следующего кода, который использует метод [ROW_NUMBER()](/sql/t-sql/functions/row-number-transact-sql) для заполнения столбца **Num** :  
  
    ```  
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM EmployeeDemo  
    GO  
  
    ```  
  
2.  Просмотрите таблицу **#Children** . Обратите внимание, что в столбце **Num** содержатся последовательные номера для каждого менеджера.  
  
    ```  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
     `EmployeeID ManagerID Num`  
  
     `---------- --------- ---`  
  
     `1        NULL       1`  
  
     `2         1         1`  
  
     `3         1         2`  
  
     `4         2         1`  
  
     `5         2         2`  
  
     `6         2         3`  
  
     `7         3         1`  
  
     `8         3         2`  
  
     `9         4         1`  
  
     `10        4         2`  
  
3.  Заполнение таблицы **NewOrg** . Используйте методы GetRoot и ToString для объединения **Num** значения в `hierarchyid` форматирования, а затем обновите **OrgNode** столбец результирующий иерархическими значениями:  
  
    ```  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   
  
    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO  
  
    ```  
  
4.  Столбец типа данных `hierarchyid` становится более понятным, если его преобразовать в символьный формат. Просмотрите данные в таблице **NewOrg** , выполнив следующий код, содержащий два представления столбца **OrgNode** :  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM NewOrg   
    ORDER BY LogicalNode;  
    GO  
  
    ```  
  
     **LogicalNode** преобразует столбец `hierarchyid` столбца в более доступную текстовую форму, которая представляет иерархию. В оставшихся задачах для представления логического формата столбцов типа данных `hierarchyid` также следует использовать метод `ToString()`.  
  
5.  Удалите временную таблицу, она больше не понадобится:  
  
    ```  
    DROP TABLE #Children  
    GO  
    ```  
  
 Следующая задача создаст индексы для поддержки иерархической структуры.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
 [Оптимизация таблицы NewOrg](lesson-1-3-optimizing-the-neworg-table.md)  
  
  
