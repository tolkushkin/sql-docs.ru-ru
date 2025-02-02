---
title: Предложение INTO (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 05/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INTO_TSQL
- INSERT_INTO_TSQL
- INSERT INTO
- INTO
- INTO clause
- INTO_clause_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- copying data [SQL Server], into a new table
- INTO clause
- moving data, to a new table
- table creation [SQL Server], INTO clause
- SELECT INTO statement
- inserting rows
- clauses [SQL Server], INTO
- row additions [SQL Server], INTO clause
ms.assetid: b48d69e8-5a00-48bf-b2f3-19278a72dd88
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4246ac153e28393db2bfaefd443f85235e8cf6db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705646"
---
# <a name="select---into-clause-transact-sql"></a>Предложение SELECT ...INTO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Инструкция SELECT…INTO создает новую таблицу в файловой группе по умолчанию и вставляет в нее результирующие строки из запроса. Полный синтаксис SELECT см. в разделе [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md).  
  
![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
[ INTO new_table ]
[ ON filegroup ]
```  
  
## <a name="arguments"></a>Аргументы  
 *new_table*   
 Указывает имя новой таблицы, создаваемой на основе столбцов, указанных в списке выбора, и строк, выбираемых из источника данных.  
 
 Формат аргумента *new_table* определяется путем расчета выражений, указанных в списке выбора. Столбцы в таблице, указанной в аргументе *new_table*, создаются в порядке, соответствующем списку выбора. Все столбцы таблицы, указанной в аргументе *new_table*, получают такие же имена, значения, типы данных и свойства допустимости значений NULL, которые указаны в соответствующем выражении в списке выбора. Свойство IDENTITY столбца переносится за исключением случаев, когда наступают условия, описанные в подразделе «Примечания» раздела «Работа со столбцами идентификаторов».  
  
 Для того чтобы создать таблицу в другой базе данных в этом же экземпляре службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], определите *new_table* в качестве полного имени в форме *database.schema.table_name*.  
  
 *new_table* нельзя создать на удаленном сервере, однако *new_table* можно заполнить из удаленного источника данных. Для создания таблицы *new_table* из удаленного источника таблицы определите источник таблицы, используя четырехчастное имя в форме *linked_server*.*catalog*.*schema*.*object* в предложении FROM инструкции SELECT. Для указания удаленного источника данных также можно использовать функцию [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) или функцию [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) в предложении FROM.  
 
 *filegroup*    
 Указывает имя файловой группы, в которой будет создана таблица. Указанная файловая группа должна существовать в базе данных, в противном случае обработчик SQL Server создает ошибку.   
 
 **Применимо к:** с [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] с пакетом обновления 2 (SP2) по [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="data-types"></a>Типы данных  
 Атрибут FILESTREAM не переносится в новую таблицу. Объекты BLOB FILESTREAM копируются и хранятся в новой таблице как объекты BLOB типа **varbinary(max)** . Без атрибута FILESTREAM тип данных **varbinary(max)** имеет ограничение в 2 ГБ. Если размер большого двоичного объекта FILESTREAM превышает это значение, происходит ошибка 7119 и инструкция прекращает работу.  
  
 При выборе существующего столбца идентификаторов в новой таблице новый столбец наследует свойство IDENTITY, если не выполняется ни одно из следующих условий.  
  
-   Инструкция SELECT содержит соединение.  
  
-   несколько инструкций SELECT соединены при помощи UNION;  
  
-   столбец идентификаторов встречается более чем один раз в списке выбора;  
  
-   столбец идентификаторов является частью выражения;  
  
-   столбец идентификаторов получен из удаленного источника данных.  
  
Если любое из этих условий выполняется, столбец создается как NOT NULL и не наследует свойство IDENTITY. Если в новой таблице необходим столбец идентификаторов, но такой столбец недоступен или необходимо изменить начальное значение или шаг приращения по сравнению с исходным столбцом идентификаторов, определите столбец в списке выбора с помощью функции IDENTITY. См. подраздел «Создание столбца идентификаторов с помощью функции IDENTITY» далее в разделе «Примеры».  

## <a name="remarks"></a>Remarks  
Инструкция `SELECT...INTO` работает в два этапа — создается новая таблица, затем вставляются строки.  Это означает, что если произойдет сбой операций вставки, все они откатываются, но новая таблица остается (пустая).  Если вам нужно гарантировать успех или неуспех всей операции целиком, используйте [явную транзакцию](../language-elements/begin-transaction-transact-sql.md).
  
## <a name="limitations-and-restrictions"></a>Ограничения  
 В качестве новой таблицы нельзя указывать табличную переменную или возвращающий табличное значение параметр.  
  
 Инструкцию `SELECT...INTO` нельзя использовать для создания секционированной таблицы, даже если исходная таблица является секционированной. Инструкция `SELECT...INTO` не использует схему секционирования исходной таблицы. Вместо этого новая таблица создается в файловой группе по умолчанию. Для вставки строк в секционированную таблицу необходимо сначала создать секционированную таблицу, а затем использовать инструкцию `INSERT INTO...SELECT...FROM`.  
  
 Индексы, ограничения и триггеры, определенные в исходной таблице, не переносятся в новую таблицу, их также нельзя указывать в инструкции `SELECT...INTO`. Если эти объекты нужны для дальнейшей работы, их можно создать после выполнения инструкции `SELECT...INTO`.  
  
 Указание предложения `ORDER BY` не гарантирует, что строки будут вставлены в указанном порядке.  
  
 Если в список выбора входит разреженный столбец, то свойство разреженного столбца не передается столбцу в новой таблице. Если это свойство необходимо в новой таблице, измените определение столбца после выполнения инструкции SELECT...INTO для включения этого свойства.  
  
 Если в список выбора входит вычисляемый столбец, соответствующий столбец новой таблицы не будет вычисляемым. Значениями нового столбца становятся значения, вычисленные при выполнении инструкции `SELECT...INTO`.  
  
## <a name="logging-behavior"></a>Режим ведения журнала  
 Объем информации, записываемой в журнал для операции `SELECT...INTO`, зависит от модели восстановления, действующей для базы данных. В модели восстановления с неполным протоколированием и в простой модели массовые операции минимально протоколируются. При минимальном ведении журнала использование инструкции `SELECT...INTO` может оказаться более эффективным, чем создание таблицы и заполнение ее инструкцией INSERT. Дополнительные сведения см. в статье [Журнал транзакций (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
## <a name="permissions"></a>Разрешения  
 Требуется разрешение CREATE TABLE в целевой базе данных.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-creating-a-table-by-specifying-columns-from-multiple-sources"></a>A. Создание таблицы путем указания столбцов из нескольких источников  
 В следующем примере таблица `dbo.EmployeeAddresses` создается в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] с помощью выбора семи столбцов из различных таблиц, содержащих сведения о сотрудниках и адресах.  
  
```sql  
SELECT c.FirstName, c.LastName, e.JobTitle, a.AddressLine1, a.City,   
    sp.Name AS [State/Province], a.PostalCode  
INTO dbo.EmployeeAddresses  
FROM Person.Person AS c  
    JOIN HumanResources.Employee AS e   
    ON e.BusinessEntityID = c.BusinessEntityID  
    JOIN Person.BusinessEntityAddress AS bea  
    ON e.BusinessEntityID = bea.BusinessEntityID  
    JOIN Person.Address AS a  
    ON bea.AddressID = a.AddressID  
    JOIN Person.StateProvince as sp   
    ON sp.StateProvinceID = a.StateProvinceID;  
GO  
```  
  
### <a name="b-inserting-rows-using-minimal-logging"></a>Б. Вставка строк с применением минимального протоколирования  
 В следующем примере создается таблица `dbo.NewProducts`, а затем вставляются строки из таблицы `Production.Product`. В примере предполагается, что для базы данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] выбрана модель восстановления FULL. Чтобы убедиться, что применяется минимальное протоколирование, модель восстановления базы данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] устанавливается в значение BULK_LOGGED перед вставкой строк и возвращается в значение FULL после инструкции SELECT...INTO. Эта процедура обеспечивает минимальное использование журнала транзакций инструкцией SELECT...INTO и ее эффективное выполнение.  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
  
SELECT * INTO dbo.NewProducts  
FROM Production.Product  
WHERE ListPrice > $25   
AND ListPrice < $100;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-creating-an-identity-column-using-the-identity-function"></a>В. Создание столбца идентификаторов с помощью функции IDENTITY  
 В следующем примере используется функция IDENTITY для создания столбца идентификаторов в новой таблице `Person.USAddress` в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Это необходимо, поскольку инструкция SELECT, которая определяет таблицу, содержит соединение, и в результате свойство IDENTITY не переносится в новую таблицу. Обратите внимание, что начальное значение и шаг приращения, заданные в функции IDENTITY, отличаются от значений в столбце `AddressID` исходной таблицы `Person.Address`.  
  
```sql  
-- Determine the IDENTITY status of the source column AddressID.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
  
-- Create a new table with columns from the existing table Person.Address. 
-- A new IDENTITY column is created by using the IDENTITY function.  
SELECT IDENTITY (int, 100, 5) AS AddressID,   
       a.AddressLine1, a.City, b.Name AS State, a.PostalCode  
INTO Person.USAddress   
FROM Person.Address AS a  
INNER JOIN Person.StateProvince AS b 
  ON a.StateProvinceID = b.StateProvinceID  
WHERE b.CountryRegionCode = N'US';   
  
-- Verify the IDENTITY status of the AddressID columns in both tables.  
SELECT OBJECT_NAME(object_id) AS TableName, name AS column_name, 
  is_identity, seed_value, increment_value  
FROM sys.identity_columns  
WHERE name = 'AddressID';  
```  
  
### <a name="d-creating-a-table-by-specifying-columns-from-a-remote-data-source"></a>Г. Создание таблицы путем указания столбцов из удаленного источника данных  
 В следующем примере показаны три метода создания новой таблицы на локальном сервере из удаленного источника данных. Пример начинается с создания ссылки на удаленный источник данных. Затем задается имя связанного сервера (`MyLinkServer,`) в предложении FROM первой инструкции SELECT...INTO и в функции OPENQUERY второй инструкции SELECT...INTO. В третьей инструкции SELECT...INTO используется функция OPENDATASOURCE, которая непосредственно задает удаленный источник данных, не указывая имя связанного сервера.  
  
 **Применимо к**: с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_name\instance_name'.  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  

USE AdventureWorks2012;  
GO  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.Departments  
FROM MyLinkServer.AdventureWorks2012.HumanResources.Department  
GO  
-- Use the OPENQUERY function to access the remote data source.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenQuery  
FROM OPENQUERY(MyLinkServer, 'SELECT *  
               FROM AdventureWorks2012.HumanResources.Department');   
GO  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_name\instance_name.  
SELECT DepartmentID, Name, GroupName, ModifiedDate  
INTO dbo.DepartmentsUsingOpenDataSource  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=server_name;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department;  
GO  
```  
  
### <a name="e-import-from-an-external-table-created-with-polybase"></a>Д. Импорт из внешней таблицы, созданной с помощью PolyBase  
 Вы можете импортировать данные из Hadoop или службы хранилища Azure в SQL Server для постоянного хранения. Чтобы импортировать данные, на которые ссылается внешняя таблица, следует использовать `SELECT INTO`. Оперативно создайте реляционную таблицу, а затем индекс хранилища столбца на основе таблицы, описанной на втором шаге.  
  
 **Применимо к:** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql
-- Import data for car drivers into SQL Server to do more in-depth analysis.  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome;  
```  
### <a name="f-creating-a-new-table-as-a-copy-of-another-table-and-loading-it-a-specified-filegroup"></a>Е. Создание новой таблицы в качестве копии другой таблицы и ее загрузка в указанную файловую группу
В следующем примере показано создание новой таблицы в качестве копии другой таблицы и ее загрузка в указанную файловую группу, отличную от файловой группы по умолчанию для пользователя.

 **Применимо к:** с [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] с пакетом обновления 2 (SP2) по [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

```sql
ALTER DATABASE [AdventureWorksDW2016] ADD FILEGROUP FG2;
ALTER DATABASE [AdventureWorksDW2016]
ADD FILE
(
NAME='FG2_Data',
FILENAME = '/var/opt/mssql/data/AdventureWorksDW2016_Data1.mdf'
)
TO FILEGROUP FG2;
GO
SELECT * INTO [dbo].[FactResellerSalesXL] ON FG2 FROM [dbo].[FactResellerSales];
```
  
## <a name="see-also"></a>См. также:  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [Примеры использования инструкции SELECT (Transact-SQL)](../../t-sql/queries/select-examples-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [IDENTITY (функция) (Transact-SQL)](../../t-sql/functions/identity-function-transact-sql.md)  
  
  
