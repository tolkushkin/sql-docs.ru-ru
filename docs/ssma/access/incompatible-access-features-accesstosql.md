---
title: Несовместимые компоненты Access (AccessToSQL) | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 29b5225f95c6b2cb04f42c0e67c504ac2cb20e53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740909"
---
# <a name="incompatible-access-features-accesstosql"></a>Несовместимые компоненты Access (AccessToSQL)
Не все функции доступа к базе данных совместимы с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Например [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и доступа имеют разные наборы зарезервированные ключевые слова. Проблемы, такие, как они могут помешать успешной миграции для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Используйте следующую таблицу, чтобы узнать о возможных проблемы миграции и возможностях о них.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>Параметры базы данных или функции, которые могут повлиять на миграцию  
  
|Доступ к параметру базы данных или функции|Вопросы миграции|  
|--------------------------------------|-------------------|  
|Доступ к таблицам, не имеют уникальные индексы.|Если таблицу, которая не имеет уникального индекса переносится в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], невозможно изменить таблицу после миграции. Это может привести к проблемам совместимости приложений.<br /><br />При преобразовании объектов базы данных Access, в окне вывода будут отображаться любой доступ к таблицам, которые не имеют уникальные индексы.<br /><br />Можно настроить доступ, чтобы добавить первичный ключ на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] таблицы во время преобразования. Дополнительные сведения см. в разделе [параметры проекта (преобразование)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388).|  
|Доступ к таблицам столбцами репликации.|Если в таблице Access, который включает в себя столбцы системы репликации переносится в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], функциональные возможности репликации Jet будет нарушена после миграции.<br /><br />После миграции, рассмотрите возможность использования [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] репликации, чтобы поддерживать синхронизированные копии базы данных.|  
|Доступ к таблицам, которые имеют уникальные индексы содержат значения null.|Доступ к таблицам, которые имеют уникальные индексы с несколькими значениями null не могут быть переданы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], так как в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], уникальные индексы запретить несколько значений NULL. Миграция завершится ошибкой для этих таблиц.<br /><br />SSMA будет сообщать эту проблему в отчетах оценки. Чтобы создать отчет об оценке, см. в разделе [оценка объектов базы данных Access для преобразования](assessing-access-database-objects-for-conversion-accesstosql.md).<br /><br />Если существует проблема, необходимо убедиться в том, что первичный ключ не имеет повторяющиеся значения null. Или, необходимо удалить первичный ключ и уникальные индексы, содержащих несколько значений null.|  
|Доступ к таблицам содержат значения даты из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] диапазона.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Datetime** принимает тип даты в диапазоне от 1 января 1753 года до 31 декабря 9999 года только. Допускается ввод даты в диапазоне от 1 января 100 до 31 декабря 9999 года.<br /><br />SSMA будет сообщать эту проблему в отчетах оценки. Чтобы создать отчет об оценке, см. в разделе [оценка объектов базы данных Access для преобразования](assessing-access-database-objects-for-conversion-accesstosql.md).<br /><br />Можно настроить как SSMA разрешает дат, которые из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] диапазона. Дополнительные сведения см. в разделе [параметры проекта (миграция)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).|  
|Длина индекса в Access превышать 900 байт.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] индексы имеют 900-байтовый предел на общий размер ключевых столбцов индекса. Если ваш доступ к таблицам использования больших индексов, SSMA отобразит предупреждение.<br /><br />Если продолжить перенос данных, перенос может завершиться сбоем.|  
|Имена объектов доступа являются [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ключевые слова, или содержать специальные символы.|Доступ и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имеет разные наборы зарезервированные ключевые слова и специальные символы. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] принимает объекты, которые имеют имена с помощью [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ключевые слова или содержащие специальные символы, если вы используете идентификаторы, заключенные в скобки или заключенные в кавычки, например «select» или [выберите] .p. Дополнительные сведения см. в разделе «Идентификаторы с разделителями (компонент Database Engine)» в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.<br /><br />**ПРИМЕЧАНИЕ.** Использование кавычек для выделения идентификаторов, параметр SET QUOTED_IDENTIFIER должен иметь значение ON.<br /><br />Например `CREATE TABLE [schema](c1 [FOR])` является корректной инструкцией, даже если **схемы** и **для** являются зарезервированными ключевыми словами. Кроме того `CREATE TABLE [xxx*yyy](c1 x&y)` является корректной инструкцией, несмотря на то, что имя таблицы и столбца содержать специальные символы  **\&#42;** и **&amp;**.<br /><br />Все запросы, которые ссылаются на эти объекты также необходимо использовать имена с квадратные скобки или кавычки. Например, запрос `SELECT * FROM schema` завершится ошибкой. Правильный запрос: `SELECT * FROM [schema]`.<br /><br />При преобразовании объектов базы данных Access, на панели вывода будут отображаться любой доступ к таблицам, которые используют ключевые слова или специальные символы. Можно изменить таблицы в режиме доступа и затем удалить и снова добавить базу данных или можно изменять запросы, которые ссылаются на эти объекты, благодаря чему запросы использовать квадратные скобки или кавычки для выделения идентификаторов. Если вы не меняете запросов, приложений на базе Access может возвращать ошибки или возникают другие проблемы.|  
|Размеры полей отличаются связи первичного/внешнего ключа.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не поддерживает функцию Jet связывания столбцов, имеющих различные типы данных или размеры с ограничениями внешнего ключа.<br /><br />При преобразовании объектов базы данных Access, окно вывода отображает первичный ключ/ограничений внешнего ключа, которые не будут преобразовываться в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Типы данных и размеры столбцов доступа можно изменить, чтобы они совпадают, а затем удалите и повторно добавить базу данных Access. Или можно выполнить перенос данных, несмотря на то, что эти ограничения не создаются в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Ссылочные таблицы в связи доступа имеют первичный ключ, ни уникальный индекс.|Доступ принимает связи между таблицами, где ссылочная таблица не имеет первичного ключа или уникального индекса. Тем не менее, это не поддерживается [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br />При преобразовании объектов базы данных Access, в окне вывода будут отображаться все таблицы, связи, но не имеют первичный ключ или уникальный индекс. Может изменять таблицы для добавления первичные ключи или уникальные индексы, а затем удалите и повторно добавить базу данных Access. Или можно выполнить перенос данных, несмотря на то, что связь между таблицами будет нарушена.|  
|Доступ к таблицам столбцами гиперссылки.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не поддерживает **hyperlink** столбцов. Вместо этого все столбцы обрабатываются как столбцы типа memo доступа. По умолчанию эти столбцы будут преобразовываться в **nvarchar(max)** столбцов в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Вы можете настроить сопоставление. Дополнительные сведения см. в разделе [сопоставление исходного и целевого типов данных](mapping-source-and-target-data-types-accesstosql.md).|  
|По умолчанию или проверки выражения правила содержат функции доступа, которые нельзя преобразовать в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или SQL Azure.|Выражения доступа по умолчанию или правила проверки могут включать системные функции доступа или определяемые пользователем функции, которые не сопоставляются [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или SQL Azure. С помощью функций, которые не сопоставляются [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или SQL Azure будут препятствовать загрузке выражения по умолчанию или правила проверки в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или SQL Azure.|  
  
## <a name="see-also"></a>См. также  
[Подготовка к миграции базы данных Access](preparing-access-databases-for-migration-accesstosql.md)  
[Миграция баз данных Access в SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
