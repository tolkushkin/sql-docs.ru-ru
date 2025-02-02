---
title: Включение или исключение строк (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- included rows
- search conditions [SQL Server], HAVING clause
- search criteria [SQL Server], including rows
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- search conditions [SQL Server], WHERE clause
- row included in search [SQL Server]
- excluding rows
ms.assetid: ba4e1202-31a2-444d-8365-c68a530ef223
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: dfb60ac381570489fe5fdb5d8ac0b6ec75e15cd0
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65096805"
---
# <a name="include-or-exclude-rows-visual-database-tools"></a>Включение или исключение строк (визуальные инструменты для баз данных)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Чтобы ограничить число строк, возвращаемых запросом SELECT, создают условия поиска или критерии фильтрации. В языке SQL условия поиска появляются в предложении инструкций WHERE или, если запрос статистический, в предложении HAVING.  
  
> [!NOTE]  
> Можно также использовать условия поиска, чтобы задать, какие строки будут изменены запросами обновления, вставки результатов и значений, удаления или создания таблиц.  
  
При выполнении запроса компонент [!INCLUDE[ssDE](../../includes/ssde_md.md)] проверяет и применяет условия поиска к каждой строке таблиц, где осуществляется поиск. Если строка соответствует условиям, она включается в запрос. Например, условие поиска всех сотрудников в определенном регионе может быть таким:  
  
```  
region = 'UK'  
```  
  
Чтобы задать критерий включения строки в результат, можно применять несколько условий поиска. Например, следующий критерий состоит из двух условий поиска. Запрос включает строку в результирующий набор только в том случае, если она удовлетворяет обоим условиям.  
  
```  
region = 'UK' AND product_line = 'Housewares'  
```  
  
Эти условия можно комбинировать с помощью ключевых слов AND и OR. В предыдущем примере использовался AND. В следующем критерии, напротив, используется OR. Результирующий набор будет включать в себя все строки, удовлетворяющие любому из условий поиска или обоим:  
  
```  
region = 'UK' OR product_line = 'Housewares'  
```  
  
Можно даже комбинировать условия поиска по одному столбцу. Например, следующий критерий сочетает два условия поиска по столбцу region:  
  
```  
region = 'UK' OR region = 'US'  
```  
  
Дополнительные сведения о сочетании условий поиска см. в следующих подразделах:  
  
-   [Обозначения для условий комбинированного поиска на панели критериев (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
  
-   [Указание нескольких условий поиска для одного столбца (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md)  
  
-   [Указание нескольких условий поиска для нескольких столбцов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
  
-   [Объединение условий, если приоритет имеет оператор AND (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
  
-   [Соединение условий, если приоритет имеет оператор OR (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
  
## <a name="examples"></a>Примеры  
Несколько примеров запросов с использованием различных операторов и критериев фильтрации строк.  
  
-   **Литерал** . Текстовое, численное, логическое значение или значение даты. В следующем примере литерал используется для поиска всех сотрудников, работающих в Великобритании:  
  
    ```  
    WHERE region = 'UK'  
    ```  
  
-   **Ссылка на столбец** . Сравнение значений одного столбца со значениями в другом. В следующем примере в таблице `products` ищутся все строки, где стоимость производства ниже стоимости доставки:  
  
    ```  
    WHERE prod_cost < ship_cost  
    ```  
  
-   **Функция** . Ссылка на функцию, которую серверная часть базы данных может разрешить для вычисления значения, использующегося в поиске. Это может быть функция, определенная сервером базы данных, или определяемая пользователем функция, возвращающая скалярное значение. В следующем примере ищутся все заказы, сделанные сегодня (функция GETDATE( ) возвращает текущую дату):  
  
    ```  
    WHERE order_date = GETDATE()  
    ```  
  
-   **NULL** . В следующем примере в таблице `authors` ищутся все авторы, имя которых сохранено в файле:  
  
    ```  
    WHERE au_fname IS NOT NULL  
    ```  
  
-   **Вычисление** . Результат вычисления, в котором могут участвовать литералы, ссылки на столбцы и другие выражения. В следующем примере в таблице `products` ищутся все строки, где розничная цена в два раза превышает стоимость производства:  
  
    ```  
    WHERE sales_price > (prod_cost * 2)  
    ```  
  
## <a name="see-also"></a>См. также:  
[Разделы по конструированию запросов и представлений (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Определение критериев поиска (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Запрос с параметрами (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
