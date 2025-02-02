---
title: Загрузка с помощью службы Integration Services — Parallel Data Warehouse | Документация Майкрософт
description: Предоставляет ссылки и информация о развертывании для загрузки данных в Parallel Data Warehouse (PDW) с помощью пакетов служб SQL Server Integration Services (SSIS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b8a1ca0ec3662dddb2baa5fbac5fe01ed4d4f2e5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213376"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>Загрузка данных с помощью служб Integration Services для Parallel Data Warehouse
Предоставляет ссылки и информация о развертывании для загрузки данных в SQL Server Parallel Data Warehouse с помощью пакетов служб SQL Server Integration Services (SSIS).  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>Основные сведения  
Службы Integration Services — это компонент SQL Server для высокопроизводительного извлечения, преобразования и загрузки (ETL) данных и обычно используется для заполнения и обновления хранилища данных.  
  
Адаптер загрузки данных PDW — это компонент службы Integration Services, которое служит для загрузки данных в PDW с помощью dtsx-пакетов служб Integration Services. В рабочем процессе пакета для SQL ServerPDW можно загружать и объединять данные из нескольких источников и загрузки данных в несколько назначений. Загрузки происходят параллельно как внутри пакета, так и среди нескольких параллельно выполняющихся пакетов; параллельно в одном устройстве может выполняться до 10 загрузок.  
  
Кроме задач, описанных в этом разделе можно использовать другие функции служб Integration Services для фильтрации, преобразование, анализ и очистка данных перед загрузкой в хранилище данных. Кроме того, можно повышать производительность рабочих процессов пакета путем запуска инструкций SQL, запуска дочерних пакетов или отправки почты.  
  
Полный комплект документации служб Integration Services, см. в разделе [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).  
  
## <a name="HowToDeployPackage"></a>Методы для выполнения пакета служб Integration Services  
Используйте один из этих методов для запуска пакета служб Integration Services.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Запуск из SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)  
Чтобы запустить пакет в BIDS, щелкните пакет правой кнопкой мыши и выберите **выполнение пакета**.  
  
По умолчанию BIDS выполняется пакетов с помощью 64-разрядных двоичных файлов. Это определяется параметром **Run64BitRuntime** упаковать свойство. Чтобы задать это свойство, перейдите на **обозревателе решений**, щелкните правой кнопкой мыши проект и выберите **свойства**. На **страницы свойств Integration Services**, перейдите в меню **свойства конфигурации** и выберите **Отладка**. Вы увидите **Run64BitRuntime** свойства в разделе **параметры отладки**. Чтобы использовать 32-разрядных средах выполнения, задайте значение **False**. Чтобы использовать 64-разрядных средах выполнения, задайте значение **True**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Запустите из SQL Server 2012 SQL Server Data Tools  
Чтобы запустить пакет из в SQL Server Data Tools, щелкните пакет правой кнопкой мыши и выберите **выполнение пакета**.  
  
### <a name="run-from-powershell"></a>Запустить с помощью PowerShell  
Чтобы запустить пакет из Windows PowerShell, с помощью **dtexec** служебной программы: `dtexec /FILE <packagePath>`  
  
Например `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`   
  
### <a name="run-from-a-windows-command-prompt"></a>Командная строка для запуска из Windows 
Чтобы запустить пакет из командной строки Windows, с помощью **dtexec** служебной программы: `dtexec /FILE <packagePath>`  
  
Например: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>Типы данных  
При использовании служб Integration Services для загрузки данных из источника данных в базу данных SQL Server PDW, данные сначала сопоставляется из источника данных в типы данных служб Integration Services. Это позволяет сопоставлять данные из нескольких источников с общим набором типов данных.  
  
Затем сопоставления данных из служб Integration Services в типы данных SQL Server PDW. Для каждого типа данных SQL Server PDW в следующей таблице перечислены типы данных служб Integration Services, которые могут быть преобразованы в тип данных SQL Server PDW.  
  
|Тип данных PDW|Типы данных Integration Services (s), которые сопоставляются с типом данных PDW|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|FLOAT|DT_R4, DT_R8|  
|INT|DT_I1, DTI2, DT_I4, DT_UI1, DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|NVARCHAR|DT_WSTR, DT_STR|  
|real|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1, DT_I2, DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**Ограниченная поддержка точности типа данных**  
  
PDW выдает ошибку проверки, если выполнить сопоставление входного столбца DT_NUMERIC или DT_DECIMAL, который содержит значение с точностью больше 28.  
  
**Неподдерживаемые типы данных**  
  
SQL Server PDW не поддерживает следующие типы данных служб Integration Services:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Чтобы загрузить столбцов, содержащих данные из этих типов в SQL Server PDW, необходимо добавить вышестоящий источник «Конвертация данных» в потоке данных для преобразования данных в совместимый тип данных.  
  
## <a name="permissions"></a>Разрешения  
Чтобы запустить пакет служб Integration Services нагрузки, вам потребуется:  
  
-   Разрешение загрузки в базе данных.  
  
-   Применимые INSERT, UPDATE, DELETE разрешения для целевой таблицы.  
  
-   Если используется промежуточную базу данных, разрешение CREATE в промежуточной базе данных. Это необходимо для создания временной таблицы.  
  
-   Если промежуточная база данных не используется, разрешение CREATE в целевой базе данных. Это необходимо для создания временной таблицы.  
  
## <a name="GenRemarks"></a>Общие замечания  
Если в пакете служб Integration Services имеет несколько назначений SQL Server PDW под управлением, и одно из подключений прерывается, службы Integration Services прекращает передачу во всех адресов назначения SQL Server PDW.  
  
## <a name="Limits"></a>Пределы и ограничения  
Число назначений SQL Server PDW для одного источника данных для пакета служб Integration Services ограничивается максимальное количество активных нагрузок. Это максимальное значение — стандартное и не предназначено для настройки пользователем. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Пункт назначения пакета служб Integration Services для одного источника данных считается как одна нагрузка при выполнении пакета. Например, предположим, что максимальное количество активных нагрузок равно 10. Пакет не будет запущен, если попытается открыть 11 или больше назначений для одного источника данных.  
  
Несколько пакетов могут работать параллельно при условии, что каждый пакет использует не больше максимального количества активных нагрузок. Например, если максимальное количество активных нагрузок составляет 10, то можно одновременно запускать два пакета по 10 назначений в каждом. Пока один пакет будет выполняться, второй будет ожидать в очереди нагрузок.  
  
Если количество нагрузок в очереди нагрузок превысит максимальное количество нагрузок в очереди, пакет не запустится. Например, если максимальное количество нагрузок составляет 10 на устройство, и максимальное количество нагрузок в очереди равно 40 на устройство, то можно одновременно запускать пяти пакетов служб Integration Services, каждая 10 назначений. Если произойдет попытка запустить шестой пакет, он не запустится.  

> [!IMPORTANT]
> Адаптер загрузки данных PDW, используя источник данных OLE DB в службах SSIS, может привести к повреждению данных, если исходная таблица содержит столбцы char и varchar с параметрами сортировки SQL. Мы рекомендуем использовать источник ADO.NET, если исходная таблица содержит столбцы типа char или varchar с параметрами сортировки SQL. 

  
## <a name="Locks"></a>Режим блокировки  
При загрузке данных с помощью служб Integration Services, SQL ServerPDW использует блокировки уровня строк для обновления данных в целевой таблице. Это означает, что каждая строка будет недоступна для чтения и записи на время обновления. Строки в целевой таблице не блокируются, пока данные загружаются в промежуточную таблицу.  
  
## <a name="Examples"></a>Примеры  
  
### <a name="Walkthrough"></a>. Простой нагрузочный из неструктурированного файла  
Следующий пример демонстрирует использование служб Integration Services для загрузки данных неструктурированного файла в SQL Server PDW Appliance нагрузки простых данных.  В этом примере предполагается, что на клиентском компьютере уже установлены службы интеграции, и будет установлен SQL Server PDW назначения, как описано выше.  
  
В этом примере мы будет загружена в `Orders` таблицу, которая имеет следующий DDL. `Orders` Таблица является частью `LoadExampleDB` базы данных.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
Ниже приведен загрузки данных.  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
В процессе подготовки для загрузки, создание неструктурированного файла `exampleLoad.txt`, содержащий данные нагрузки:  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
Во-первых создайте в пакете служб Integration Services, выполнив следующие действия:  
  
1.  В SQL Server Data Tools \(SSDT\)выберите **файл**, **New**, а затем **проекта**. Выберите **проект служб Integration Services** из перечисленных параметров. Назовите этот проект `ExampleLoad`и нажмите кнопку **ОК**.  
  
2.  Нажмите кнопку **поток управления** вкладке, а затем перетащите **задача потока данных** из **элементов** для **поток управления** области.  
  
3.  Нажмите кнопку **потока данных** вкладке, а затем перетащите **Flat File Source** из **элементов** для **потока данных** области. Дважды щелкните поле, вы только что создали для открытия **Редактор источника неструктурированного файла**.  
  
4.  Нажмите кнопку **диспетчер соединений** и нажмите кнопку **New**.  
  
5.  В **имя диспетчера соединений** введите понятное имя для соединения. В этом примере `Example Load Flat File CM`.  
  
6.  Нажмите кнопку **Обзор** и выберите `ExampleLoad.txt` файл с локального компьютера.  
  
7.  Поскольку неструктурированного файла содержит строку с именами столбцов, щелкните **имена столбцов в первой строке данных** поле.  
  
8.  Нажмите кнопку **столбцы** в левом столбце и предварительный просмотр данных, которые будут загружены, чтобы убедиться, что имена столбцов и данных были правильной интерпретации.  
  
9. Нажмите кнопку **Дополнительно** в левом столбце. Щелкните имя каждого столбца, чтобы просмотреть тип данных, связанный с данными. Внесите изменения в поле так, чтобы типы данных, загружаемых данных совместима с типами столбца назначения.  
  
10. Нажмите кнопку **ОК** сохранить диспетчера соединений.  
  
11. Нажмите кнопку **ОК** для выхода из **Редактор источника неструктурированного файла**.  
  
Укажите назначение для потока данных.  
  
1.  Перетащите **назначение SQL Server PDW** из **элементов** для **потока данных** области.  
  
2.  Дважды щелкните поле, вы только что создали для загрузки **Редактор назначения SQL Server PDW**.  
  
3.  Щелкните стрелку вниз рядом с полем **диспетчер соединений**.  
  
4.  Выберите **создайте новое соединение**.  
  
5.  Заполните сведения для базы данных сервера, пользователя, пароль и назначение содержимым, относящимся к устройству. (Ниже приведены примеры). Затем нажмите кнопку **ОК**.  
  
    Для соединения InfiniBand **имя сервера**: Введите < имя устройства >-SQLCTL01 17001.  
  
    Для подключения Ethernet **имя сервера**: Введите IP-адрес узла кластера управления, запятая, порт 17001. Например 10.192.63.134,17001.  
  
    **Пользователь:**`user1`  
  
    **Пароль:**`password1`  
  
    **Целевая база данных:**`LoadExampleDB`  
  
6.  Выберите целевую таблицу: `Orders`.  
  
7.  Выберите **Append** режим загрузки и нажмите кнопку **ОК**.  
  
Укажите поток данных из источника в место назначения.  
  
1.  На **потока данных** панели перетащите зеленую стрелку от **Flat File Source** поле для **назначение SQL Server PDW** поле.  
  
2.  Дважды щелкните **назначение SQL Server PDW** поле, чтобы увидеть **Редактор назначения SQL Server PDW** еще раз. Имена столбцов из неструктурированного файла в левой части, должны отображаться в списке **несопоставленные входные столбцы**. Имена столбцов из целевой таблицы в правой части, должны отображаться в списке **несопоставленные целевые столбцы**. Сопоставьте столбцы путем перетаскивания или двойным щелчком имен соответствующих столбцов в **несопоставленные входные столбцы** и **несопоставленные целевые столбцы** списки для **сопоставленные столбцы**поле. Нажмите кнопку **ОК** для сохранения параметров.  
  
3.  Сохранить пакет, нажав кнопку **Сохранить** в **файл** меню.  
  
Запустите пакет на компьютере службы Integration Services.  
  
1.  В службах Integration Services**обозревателе решений** (правый столбец), щелкните правой кнопкой мыши `Package.dtsx` и выберите **Execute**.  
  
2.  Пакет запустится и будет показан ход выполнения, а также все ошибки на **ход выполнения** области. Используйте клиент SQL, чтобы подтвердить загрузку или отслеживанию нагрузки через консоль администратора SQL Server PDW.  
  
## <a name="see-also"></a>См. также  
[Создание задачи «скрипт», который использует адаптер загрузки данных PDW служб SSIS](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[Проектирование и разработка пакетов (службы Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[Учебник. Создание основного пакета с помощью мастера](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[Приступая к работе (службы Integration Services)](https://go.microsoft.com/fwlink/?LinkId=202412)  
[Пример формирования динамических пакетов](https://go.microsoft.com/fwlink/?LinkId=202413)  
[Проектирование пакетов служб SSIS для параллелизма (видеоматериал SQL Server)](https://msdn.microsoft.com/library/dd795221.aspx)  
[Примеры сообщества Microsoft SQL Server: Службы Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[Повышение эффективности добавочной загрузки измененных данных](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[Преобразование "Медленно изменяющееся измерение"](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[Задача «Массовая вставка»](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
