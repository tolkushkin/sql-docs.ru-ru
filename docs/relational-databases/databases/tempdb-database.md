---
title: База данных tempdb | Документация Майкрософт
description: В этой статье приводятся подробные сведения о настройке и использовании базы данных tempdb в SQL Server и базе данных SQL Azure.
ms.custom: P360
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.reviewer: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 86c030eabfe3b18f544ca43f3e493bcd90f5e5ca
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994238"
---
# <a name="tempdb-database"></a>База данных tempdb

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Системная база данных **tempdb** — это глобальный ресурс, доступный всем пользователям, подключенным к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или базе данных SQL. База данных tempdb служит для хранения следующих объектов:  
  
- Временные **пользовательские объекты**, созданные явно, такие как глобальные или локальные временные таблицы и индексы, временные хранимые процедуры, табличные переменные, таблицы, возвращаемые функциями с табличными значениями, и курсоры.  
- **Внутренние объекты**, созданные ядром СУБД. К ним относятся следующие объекты.
  - Рабочие таблицы, хранящие промежуточные результаты буферов, курсоры, сортировки и временное хранилище больших объектов (LOB).
  - рабочие файлы для операций хэш-соединения или статистических хэш-выражений;
  - промежуточные результаты сортировки при таких операциях, как создание или перестроение индексов (если указан параметр SORT_IN_TEMPDB), либо определенных запросах GROUP BY, ORDER BY или UNION.

  > [!NOTE]
  > Каждый внутренний объект использует минимум девять страниц: страницу IAM и восьмистраничный экстент. Дополнительные сведения о страницах и экстентах см. в разделе [Страницы и экстенты](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).
  > [!IMPORTANT]
  > Отдельные базы данных и эластичные пулы Базы данных SQL Azure поддерживают глобальные временные таблицы и глобальные временные хранимые процедуры, которые хранятся в базе данных tempdb и областью действия которых является база данных. Глобальные временные таблицы и глобальные временные хранимые процедуры являются общими для всех сеансов пользователей в рамках одной базы данных SQL Azure. Сеансы пользователей, связанные с другими базами данных SQL Azure, не имеют доступа к глобальным временным таблицам. Дополнительные сведения см. в разделе [Глобальные временные таблицы (база данных SQL Azure) в области базы данных](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database). [Управляемый экземпляр Базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)) поддерживает те же временные объекты, что и SQL Server.
  > Для отдельных баз данных и эластичных пулов Базы данных SQL Azure используются только базы данных master и tempdb. Дополнительные сведения см. в разделе [Что являет собою сервер Базы данных SQL Azure?](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server). Описание базы данных tempdb в контексте отдельных баз данных и эластичных пулов Базы данных SQL Azure см. в разделе [База данных tempdb в базе данных SQL](#tempdb-database-in-sql-database). Для Управляемого экземпляра Базы данных Azure SQL применяются все системные базы данных.

- **Хранилища версий** — это коллекции страниц данных, содержащих строки данных, которые необходимы для поддержки возможностей, применяющих управление версиями строк. Существует два хранилища версий: общее хранилище версий и хранилище версий построения индексов в сети. Хранилища версий содержат следующее:
  - версии строк, сформированные транзакциями изменения данных в базе данных, в которой используются транзакции изоляции моментальных снимков с зафиксированным чтением и транзакции изоляции моментальных снимков;  
  - версии строк, создаваемые транзакциями изменения данных для таких функций, как операции с индексами в сети, функции режима MARS и триггеры AFTER.  
  
Операции в базе данных **tempdb** регистрируются минимально, что позволяет откатывать транзакции. База данных**tempdb** пересоздается при каждом запуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , чтобы система всегда запускалась с чистой копией базы данных. Временные таблицы и хранимые процедуры удаляются автоматически при отключении, и при выключении системы нет активных соединений. Поэтому в базе данных **tempdb** ничего не сохраняется от одного сеанса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] до следующего. Операции резервного копирования и восстановления базы данных **tempdb**запрещены.  
  
## <a name="physical-properties-of-tempdb-in-sql-server"></a>Физические свойства базы данных tempdb в SQL Server

В приведенной ниже таблице описывается исходная конфигурация данных и файлов журналов базы данных **tempdb**, которая основывается на значениях по умолчанию для шаблона базы данных. Размеры этих файлов могут немного изменяться в зависимости от выпуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Файл|Логическое имя|Физическое имя|Начальный размер|Увеличение размера файлов|  
|----------|------------------|-------------------|------------------|-----------------|  
|Первичные данные|tempdev|tempdb.mdf|8 МБ|Автоматическое увеличение на 64 МБ до заполнения диска.|  
|Вторичные файлы данных*.|temp#|tempdb_mssql_ # .ndf|8 МБ|Автоматическое увеличение на 64 МБ до заполнения диска.|  
|Журнал|templog|templog.ldf|8 МБ|Автоматическое увеличение на 64 МБ до максимального размера в 2 ТБ.|  
  
\* Количество файлов зависит от числа (логических) процессоров на компьютере. Как правило, если число логических процессоров меньше или равно восьми, используйте равное ему число файлов данных. Если число логических процессоров больше восьми, используйте восемь файлов данных, а затем, если состязание сохраняется, увеличивайте число файлов данных на значение, кратное 4, пока состязание не уменьшится до приемлемого уровня, или внесите изменения в рабочую нагрузку или код.

> [!NOTE]
> Количество файлов данных по умолчанию основано на общих рекомендациях, приведенных в статье [KB 2154845](https://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>Перемещение данных и файлов журналов базы данных tempdb в SQL Server

Сведения о перемещении файлов данных и журналов базы данных **tempdb** см. в разделе [Перемещение системных баз данных](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>Параметры базы данных tempdb в SQL Server

Следующая таблица описывает значения по умолчанию всех параметров базы данных **tempdb** и условия их изменения. Чтобы просмотреть текущие настройки этих параметров, используйте представление каталога [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Параметр базы данных|Значение по умолчанию|Можно ли изменить|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Да|  
|ANSI_NULL_DEFAULT|OFF|Да|  
|ANSI_NULLS|OFF|Да|  
|ANSI_PADDING|OFF|Да|  
|ANSI_WARNINGS|OFF|Да|  
|ARITHABORT|OFF|Да|  
|AUTO_CLOSE|OFF|нет|  
|AUTO_CREATE_STATISTICS|ON|Да|  
|AUTO_SHRINK|OFF|нет|  
|AUTO_UPDATE_STATISTICS|ON|Да|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Да|  
|CHANGE_TRACKING|OFF|нет|  
|CONCAT_NULL_YIELDS_NULL|OFF|Да|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Да|  
|CURSOR_DEFAULT|GLOBAL|Да|  
|Параметры доступности базы данных|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|нет<br /><br /> нет<br /><br /> нет|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Да|  
|DB_CHAINING|ON|нет|  
|ENCRYPTION|OFF|нет|  
|MIXED_PAGE_ALLOCATION|OFF|нет|  
|NUMERIC_ROUNDABORT|OFF|Да|  
|PAGE_VERIFY|Значение CHECKSUM для новых установок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Значение NONE для обновлений [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Да|  
|PARAMETERIZATION|SIMPLE|Да|  
|QUOTED_IDENTIFIER|OFF|Да|  
|READ_COMMITTED_SNAPSHOT|OFF|нет|  
|RECOVERY|SIMPLE|нет|  
|RECURSIVE_TRIGGERS|OFF|Да|  
|Параметры компонента Service Broker|ENABLE_BROKER|Да|  
|TRUSTWORTHY|OFF|нет|  
  
Описание этих баз данных см. в статье [Параметры ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="tempdb-database-in-sql-database"></a>База данных tempdb в базе данных SQL

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>Размеры базы данных tempdb для уровней служб на основе DTU

|SLO|Максимальный размер файла данных Tempdb (ГБ)|Число файлов данных tempdb|Максимальный размер данных tempdb (ГБ)|
|---|---:|---:|---:|
|Basic|13|1|13|
|S0|13|1|13|
|S1|13|1|13|
|S2|13|1|13|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13|12|156|
|P2|13|12|156|
|P4|13|12|156|
|P6|13|12|156|
|P11|13|12|156|
|P15|13|12|156|
|Эластичные пулы уровня "Премиум" (все конфигурации DTU)|13|12|156|
|Эластичные пулы ценовой категории "Стандартный" (S0–S2)|13|12|156|
|Эластичные пулы ценовой категории "Стандартный" (S3 и выше) |32|12|384|
|Эластичные пулы уровня "Базовый" (все конфигурации DTU)|13|12|156|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>Размеры базы данных tempdb для уровней служб на основе виртуальных ядер

См. [пределы для ресурсов на основе виртуальных ядер](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits)

## <a name="restrictions"></a>Ограничения

В базе данных **tempdb** нельзя выполнить следующие операции.  
  
- добавление файловых групп;
- резервное копирование и восстановление базы данных;
- Изменение параметров сортировки. (параметрами сортировки по умолчанию являются параметры сортировки сервера);
- Изменение владельца базы данных. (владельцем **tempdb** является **sa**);
- Создание моментального снимка базы данных
- удаление базы данных;
- удаление пользователя **guest** из базы данных;
- включение отслеживания измененных данных;
- участие в зеркальном отображении базы данных;
- удаление первичной файловой группы, первичного файла данных или файла журнала;
- переименование базы данных или первичной файловой группы;
- выполнение инструкции DBCC CHECKALLOC;
- выполнение инструкции DBCC CHECKCATALOG;
- перевод базы данных в режим "вне сети" (OFFLINE);
- перевод базы данных или первичной файловой группы в режим "только для чтения" (READ_ONLY).
  
## <a name="permissions"></a>Разрешения

Любой пользователь может создавать временные объекты в базе данных tempdb. Если не предоставлены какие-либо дополнительные разрешения, то пользователи могут производить доступ только к тем объектам, которыми они владеют. Существует возможность отменить разрешение на соединение с базой данных tempdb, чтобы пользователь не мог ею пользоваться, но этого делать не рекомендуется, так как база данных tempdb необходима для некоторых стандартных операций.  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>Оптимизация производительности базы данных tempdb в SQL Server

Размер и физическое размещение базы данных tempdb может влиять на производительность системы. Например, если для базы данных tempdb установлен слишком малый размер, часть системной нагрузки может приходиться на автоувеличение базы данных tempdb до размера, требуемого для поддержки рабочей нагрузки при каждом перезапуске экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Если возможно, используйте [мгновенную инициализацию файлов базы данных](../../relational-databases/databases/database-instant-file-initialization.md), чтобы улучшить производительность операций увеличения файлов данных.

Заранее выделите место для всех файлов tempdb, установив размер файла в значение, достаточное, чтобы гарантировать обычную рабочую нагрузку в среде. Предварительное выделение предотвращает слишком частое расширение tempdb, которое может повлиять на производительность. Следует установить автоувеличение для базы данных tempdb, но это следует сделать, чтобы увеличить место на диске для незапланированных исключений.

Файлы данных внутри каждой [файловой группы](../../relational-databases/databases/database-files-and-filegroups.md#filegroups) должны иметь одинаковый размер, поскольку [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] использует алгоритм пропорционального заполнения, который повышает вероятность выделения памяти в файлах с большим объемом свободного пространства. Разделение базы данных tempdb на несколько файлов данных равного размера обеспечивает высокую степень параллельной эффективности операций, использующих базу данных tempdb.

Установите шаг увеличения размера файла на приемлемую величину, чтобы избежать слишком малого увеличения размера файлов базы данных tempdb. Если увеличение размера файла будет идти слишком медленно по сравнению с объемом записываемых в базу tempdb данных, база данных tempdb может требовать постоянного расширения, что сказывается на производительности.

Чтобы проверить текущий размер и параметры роста базы данных tempdb, используйте следующий запрос:

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

Поместите базу данных tempdb на быструю подсистему ввода-вывода. Если имеется много непосредственно присоединенных дисков, то используйте чередование дисков. Отдельные файлы данных tempdb или их группы необязательно должны располагаться на разных дисках или шпинделях, за исключением случаев, когда наблюдаются узкие места, связанные с производительностью операций ввода-вывода.

Расположите базу данных tempdb на дисках, отличных от используемых пользовательскими базами данных.

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>Увеличение производительности базы данных tempdb в SQL Server

Начиная с версии [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], производительность базы данных **tempdb** дополнительно оптимизируется следующими способами:  
  
- Временные таблицы и табличные переменные кэшируются. Кэширование позволяет операциям по удалению и созданию временных объектов выполняться очень быстро и снижает число состязаний из-за выделения страниц.  
- Усовершенствован протокол кратковременных блокировок выделения страниц для снижения количества используемых кратковременных блокировок UP (обновление).  
- Снижены затраты на ведение журнала базы данных **tempdb**. При этом снижается потребление пропускной способности подсистемы ввода-вывода файлом журнала **tempdb**.  
- Программа установки добавляет несколько файлов данных tempdb при установке нового экземпляра. Эту задачу можно выполнить с помощью нового элемента управления вводом в разделе **Настройка ядра СУБД** пользовательского интерфейса и параметра командной строки /SQLTEMPDBFILECOUNT. По умолчанию программа установки добавляет число файлов данных tempdb, равное количеству логических процессоров, либо восемь файлов в зависимости от того, какое значение меньше.  
- Если существует несколько файлов данных **tempdb**, размер всех файлов автоматически увеличивается в одно и то же время и на одинаковое значение в зависимости от параметров увеличения. Флаг трассировки 1117 больше не требуется.  
- Для всех операций выделения в **tempdb** используются единообразные экстенты. [Флаг трассировки 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) больше не требуется.  
- Для первичной файловой группы свойство AUTOGROW_ALL_FILES включено и не может быть изменено.

Дополнительные сведения об улучшениях производительности в базе данных tempdb см. в следующей статье блога:

[TEMPDB — Files and Trace Flags and Updates, Oh My!](https://blogs.msdn.microsoft.com/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my/) (TEMPDB — файлы, флаги трассировки и обновления)

## <a name="memory-optimized-tempdb-metadata"></a>Оптимизированные для памяти метаданные TempDB

Состязание метаданных TempDB всегда было узким местом для масштабируемости многих рабочих нагрузок, выполняющихся в SQL Server. В [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] появилась новая функция оптимизированных для памяти метаданных tempdb, входящая в семейство функций [выполняющейся в памяти базы данных](../in-memory-database.md). Она эффективно устраняет эту проблему и открывает новый уровень масштабируемости для рабочих нагрузок, активно использующих tempdb. В [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] системные таблицы, связанные с управлением метаданными временной таблицы, можно переместить в неустойчивые таблицы без кратковременной блокировки, оптимизированные для памяти. Чтобы согласиться на эту новую функцию, используйте следующий скрипт:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON 
```

Чтобы это изменение конфигурации вступило в силу, нужно перезапустить службу.

У этой реализации имеются некоторые ограничения, которые нужно учитывать:

1. Включение и отключение функции не является динамическим. Из-за внутренних изменений, которые необходимо внести в структуру tempdb, для включения или отключения этой функции требуется перезапуск.
2. Отдельная транзакция не может обратиться к оптимизированным для памяти таблицам в более чем одной базе данных.  Это означает, что все транзакции, связанные с оптимизированной для памяти таблицей в пользовательской базе данных, не смогут обратиться к системным представлениям TempDB в той же транзакции.  Если вы попытаетесь обратиться к системным представлениям TempDB в той же транзакции, где участвует оптимизированная для памяти таблица в пользовательской базе данных, произойдет следующая ошибка:
    ```
    A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
    ```
    Пример
    ```
    BEGIN TRAN
    SELECT *
    FROM tempdb.sys.tables  -----> Creates a user In-Memory OLTP Transaction on Tempdb
    INSERT INTO <user database>.<schema>.<mem-optimized table>
    VALUES (1)  ----> Attempts to create user In-Memory OLTP transaction but will fail
    COMMIT TRAN
    ```
3. Запросы к таблицам, оптимизированным для памяти, не поддерживают указания блокировки и изоляции, поэтому запросы к представлениям каталога оптимизированной для памяти TempDB не будут учитывать указания блокировки и изоляции. Как и в случае с другими системными представлениями каталога в SQL Server, все транзакции для системных представлений будут находиться в изоляции READ COMMITTED (или READ COMMITTED SNAPSHOT в данном случае).
4. При включении оптимизированных для памяти метаданных tempdb возможны некоторые проблемы с индексами columnstore во временных таблицах. В этом предварительном выпуске рекомендуется избегать индексов columnstore во временных таблицах при использовании оптимизированных для памяти метаданных tempdb.

> [!NOTE] 
> Эти ограничения действуют только при ссылке на системные представления TempDB, при необходимости вы сможете создать временную таблицу в той же транзакции, где обращаетесь к оптимизированной для памяти таблице в пользовательской базе данных.

Вы можете проверить, является ли TempDB оптимизированной для памяти, используя следующую команду T-SQL:
```
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized')
```

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>Планирование размера базы данных tempdb в SQL Server

Определение требуемого размера базы данных tempdb в рабочей среде SQL Server зависит от множества факторов. Как описано выше в этой статье, эти факторы включают текущую рабочую нагрузку и используемые компоненты [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Рекомендуется проанализировать текущую рабочую нагрузку, выполнив следующие задачи в среде тестирования SQL Server:

- Установите автоувеличение для базы данных tempdb.
- Запустите отдельные запросы или файлы трассировки рабочей нагрузки и следите за использованием диска базой данных tempdb.
- Выполните операции обслуживания индексов, например перестроение индексов, и следите за использованием диска базой данных tempdb.
- Используйте сведения об используемом месте из предыдущих шагов для прогнозирования общей рабочей нагрузки, скорректируйте полученное значение с учетом планируемой параллельной обработки и задайте соответствующий размер базы данных tempdb.

## <a name="how-to-monitor-tempdb-use"></a>Мониторинг использования базы данных tempdb

Нехватка места на диске для базы данных tempdb может привести к существенным сбоям рабочей среды [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и помешать работающим приложениям завершить операции. Для контроля места на диске, используемого в файлах базы данных tempdb, можно применить динамическое административное представление [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md):

```sql
 -- Determining the Amount of Free Space in tempdb
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount Space Used by the Version Store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by Internal Objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by User Objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

Кроме того, для контроля деятельности по выделению и освобождению страниц в базе данных tempdb на уровне сеанса или задачи можно использовать динамические административные представления [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) и [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md). Эти представления могут быть использованы для определения больших запросов, временных таблиц или табличных переменных, которые используют много места на диске базы данных tempdb. Также предусмотрено несколько соответствующих счетчиков, которые можно использовать для отслеживания свободного места в базе данных tempdb и ресурсов, использующих базу данных tempdb. Дополнительные сведения см. в следующем разделе.

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>См. также

- [Параметр SORT_IN_TEMPDB для индексов](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
- [Системные базы данных](../../relational-databases/databases/system-databases.md)  
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
- [Перемещение файлов базы данных](../../relational-databases/databases/move-database-files.md)  
  
## <a name="see-also"></a>См. также:

- [Работа с базой данных tempdb в SQL Server 2005](https://technet.microsoft.com/library/cc966545.aspx)  
- [Устранение неполадок, связанных с нехваткой места на диске для базы данных tempdb](https://msdn.microsoft.com/library/ms176029.aspx)
