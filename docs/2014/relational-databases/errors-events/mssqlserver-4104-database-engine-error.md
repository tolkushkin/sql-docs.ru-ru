---
title: MSSQLSERVER_4104 | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4104 (Database Engine error)
ms.assetid: 52dc32d8-97ad-4ef0-834d-2e68f215d007
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fd364a08781c00eaaf42eb0b1c15e7e5011ed432
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868001"
---
# <a name="mssqlserver4104"></a>MSSQLSERVER_4104
    
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|4104|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя|ALG_MULTI_ID_BAD|  
|Текст сообщения|Не удалось выполнить привязку составного идентификатора "%.*ls".|  
  
## <a name="explanation"></a>Объяснение  
 Имя сущности в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] определяется ее *идентификатором*. Идентификаторы используются, например, всегда при ссылках на сущности путем указания в запросе имен столбца и таблицы. Составной идентификатор содержит один или несколько квалификаторов, являющихся префиксом для идентификатора. Например, перед идентификатором таблицы можно указывать такие квалификаторы, как имя базы данных и имя схемы, в которых содержится таблица, а перед идентификатором столбца могут находиться такие квалификаторы, как имя таблицы или псевдоним таблицы.  
  
 Ошибка 4104 указывает, что заданный составной идентификатор не может быть сопоставлен существующей сущности. Эта ошибка может быть возвращена при следующих условиях.  
  
-   Квалификатор, заданный в качестве префикса для имени столбца, не совпадает ни с одним именем таблицы или псевдонима, используемым в запросе.  
  
     Например, в следующей инструкции псевдоним таблицы (`Dept`) используется как префикс столбца, но в предложении FROM нет ссылки на псевдоним таблицы.  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department;  
    ```  
  
     В следующих инструкциях составной идентификатор столбца `TableB.KeyCol` задан в предложении WHERE как часть условия JOIN между двумя таблицами, но в запросе нет явной ссылки на таблицу `TableB`.  
  
    ```  
    DELETE FROM TableA WHERE TableA.KeyCol = TableB.KeyCol;  
    ```  
  
    ```  
    SELECT 'X' FROM TableA WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   Имя псевдонима для таблицы указывается в предложении FROM, но квалификатор, указанный для столбца, является именем таблицы. Например, в следующей инструкции имя таблицы (`Department`) используется как префикс столбца; но у таблицы есть псевдоним (`Dept`), ссылка на который содержится в предложении FROM.  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department AS Dept;  
    ```  
  
     Когда используется псевдоним, имя таблицы не может использоваться в других частях инструкции.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не может определить, указывает ли составной идентификатор на столбец, предваряемый таблицей, или на определяемый пользователем тип данных CLR, предваряемый столбцом. Это происходит потому, что ссылка на свойства столбцов определяемых пользователем типов задается с использованием точки (.) в качестве разделителя между именем столбца и именем свойства, так же как имя столбца предваряется именем таблицы. В следующем примере создается две таблицы, `a` и `b`. Таблица `b` содержит столбец `a`, в котором в качестве типа данных используется определяемый пользователем тип данных CLR `dbo.myudt2`. Инструкция SELECT содержит составной идентификатор `a.c2`.  
  
    ```  
    CREATE TABLE a (c2 int);   
    GO  
    ```  
  
    ```  
    CREATE TABLE b (a dbo.myudt2);   
    GO  
    ```  
  
    ```  
    SELECT a.c2 FROM a, b;   
    ```  
  
     Если определяемый пользователем тип данных `myudt2` не имеет свойства с именем `c2`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не сможет определить, указывает ли идентификатор `a.c2` на столбец `c2` в таблице `a` или на столбец `a`, свойство `c2` в таблице `b`.  
  
## <a name="user-action"></a>Действие пользователя  
  
-   Префиксы столбцов должны быть согласованы с именами таблиц или псевдонимами, указанными в предложении FROM запроса. Если псевдоним определен для имени таблицы в предложении FROM, то псевдоним можно использовать только как квалификатор для столбцов, связанных с этой таблицей.  
  
     Приведенные выше инструкции, которые содержат ссылки на таблицу `HumanResources.Department`, можно исправить следующим образом:  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department AS Dept;  
    GO  
    ```  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department;  
    GO  
    ```  
  
-   Проверьте, что все таблицы указаны в запросе и условия JOIN между таблицами заданы верно. Инструкция DELETE выше может быть исправлена следующим образом:  
  
    ```  
    DELETE FROM dbo.TableA  
    WHERE TableA.KeyCol = (SELECT TableB.KeyCol   
                            FROM TableB   
                            WHERE TableA.KeyCol = TableB.KeyCol);  
    GO  
    ```  
  
     Приведенная выше инструкция SELECT для таблицы `TableA` может быть исправлена следующим образом:  
  
    ```  
    SELECT 'X' FROM TableA, TableB WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
     или диспетчер конфигурации служб  
  
    ```  
    SELECT 'X' FROM TableA INNER JOIN TableB ON TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   Используйте для идентификаторов уникальные, понятные имена. В результате будет проще читать и исправлять исходный текст, и снижается опасность неоднозначных ссылок на несколько сущностей.  
  
## <a name="see-also"></a>См. также  
 [MSSQLSERVER_107](mssqlserver-107-database-engine-error.md)   
 [Идентификаторы баз данных](../databases/database-identifiers.md)  
  
  
