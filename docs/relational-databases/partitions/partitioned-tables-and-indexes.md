---
title: Секционированные таблицы и индексы | Документация Майкрософт
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- partitioned tables [SQL Server], about partitioned tables
- partitioned indexes [SQL Server], architecture
- partitioned tables [SQL Server], architecture
- partitioned indexes [SQL Server], about partitioned indexes
- index partitions
ms.assetid: cc5bf181-18a0-44d5-8bd7-8060d227c927
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d5e5a00bbe461062412882124a6419cc804c5721
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65713312"
---
# <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает секционирование таблиц и индексов. Данные секционированных таблиц и индексов подразделяются на блоки, которые могут быть распределены по нескольким файловым группам в базе данных. Данные секционируются горизонтально, поэтому группы строк сопоставляются с отдельными секциями. Все секции одного индекса или таблицы должны находиться в одной и той же базе данных. Таблица или индекс рассматриваются как единая логическая сущность при выполнении над данными запросов или обновлений. До версии [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 секционированные таблицы и индексы были доступны не в каждом выпуске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Сведения о функциях, поддерживаемых различными выпусками [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], см. в статье [Возможности, поддерживаемые различными выпусками SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
> [!IMPORTANT]  
> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] поддерживает по умолчанию до 15 000 секций. В версиях, предшествующих [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], количество секций по умолчанию было равно 1000. В системах с архитектурой x86 создание таблицы или индекса с количеством секций более 1,000 возможно, но не поддерживается.  
  
## <a name="benefits-of-partitioning"></a>Преимущества секционирования  
 Секционирование больших таблиц или индексов может дать следующие преимущества в управляемости и производительности.  
  
-   Это позволяет быстро и эффективно переносить подмножества данных и обращаться к ним, сохраняя при этом целостность набора данных. Например, такая операция, как загрузка данных из OLTP в систему OLAP, выполняется за секунды, а не за минуты и часы, как в случае несекционированных данных.  
  
-   Операции обслуживания можно выполнять быстрее с одной или несколькими секциями. Операции более эффективны, так как выполняются только с поднаборами данных, а не со всей таблицей. Например, можно сжать данные в одну или несколько секций или перестроить одну или несколько секций индекса.  
  
-   Можно повысить скорость выполнения запросов в зависимости от запросов, которые часто выполняются в вашей конфигурации оборудования. Например, оптимизатор запросов может быстрее выполнять запросы на эквисоединение двух и более секционированных таблиц, если столбцы секционирования те же, что и столбцы для объединения таблиц. См. подробнее о [запросах](#queries).
  
В процессе сортировки данных для операций ввода-вывода в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] сначала проводится сортировка данных по секциям. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может одновременно обращаться только к одному диску, что может снизить производительность. Для ускорения сортировки данных рекомендуется распределить файлы данных в секциях по нескольким жестким дискам, создав RAID. Таким образом, несмотря на сортировку данных по секциям, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] сможет одновременно осуществлять доступ ко всем жестким дискам каждой секции.  
  
Кроме того, можно повысить производительность, применяя блокировки на уровне секций, а не всей таблицы. Это может уменьшить количество конфликтов блокировок для таблицы. Чтобы снизить состязание блокировок с помощью применения укрупнения блокировок к секциям, задайте для параметра `LOCK_ESCALATION` инструкции `ALTER TABLE` значение AUTO. 
  
## <a name="components-and-concepts"></a>Компоненты и основные понятия  
Следующие термины относятся к секционированию таблиц и индексов.  
  
### <a name="partition-function"></a>Функция секционирования  
Объект базы данных, который определяет распределение строк таблицы или индекса по секциям на основе значений определенных столбцов, называемых столбцами секционирования. То есть функция секционирования определяет количество разделов в таблице и как будут определены границы разделов. Например, таблицу, содержащую данные заказов на продажу, может потребоваться разделить на 12 месячных секций по значениям столбца **datetime** , например по дате продаж.  
  
### <a name="partition-scheme"></a>Схема секционирования 
Объект базы данных, который сопоставляет секции функции секционирования набору файловых групп. Главная причина, по которой секции разделяются по разным файловым группам, заключается в необходимости независимого резервного копирования этих секций, поскольку оно всегда выполняется отдельно для каждой из файловых групп.  
  
### <a name="partitioning-column"></a>Столбец секционирования  
Столбец таблицы или индекса, используемый функцией секционирования для секционирования таблицы или индекса. Вычисляемые столбцы, участвующие в функции секционирования, должны быть явно помечены как PERSISTED. Все типы данных, допустимые для использования в качестве индексных столбцов, могут использоваться как столбцы секционирования, за исключением **timestamp**. Типы данных **ntext**, **text**, **image**, **xml**, **varchar(max)**, **nvarchar(max)** или **varbinary(max)** указать нельзя. Также нельзя указать определяемый пользователем тип данных среды Microsoft .NET Framework CLR и столбцы типа данных псевдонима.  
  
### <a name="aligned-index"></a>Выровненный индекс  
Индекс, созданный на основе той же схемы секционирования, что и соответствующая таблица. Когда таблица и ее индексы выровнены, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может при обслуживании структуры секционирования как таблицы, так и индексов быстро и эффективно переключать секции. Для выравнивания с базовой таблицей индексу необязательно использовать функцию секционирования с тем же именем. Тем не менее функции секционирования индекса и базовой таблицы не должны существенно различаться, то есть:
 1. аргументы функции секционирования должны иметь один и тот же тип данных;
 2. функции должны определять одинаковое количество секций;
 3. функции должны определять для секций одинаковые граничные значения.  

#### <a name="partitioning-clustered-indexes"></a>Секционирование кластеризованных индексов
При секционировании кластеризованного индекса столбец секционирования должен содержаться в ключе кластеризации. При секционировании неуникального кластеризованного индекса, если столбец секционирования не указан явно в ключе кластеризации, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] по умолчанию добавляет столбец секционирования в список ключей кластеризованного индекса. Если кластеризованный индекс является уникальным, для него следует явным образом задать наличие столбца секционирования в ключе кластеризованного индекса.        

#### <a name="partitioning-nonclustered-indexes"></a>Секционирование некластеризованных индексов
При секционировании уникального некластеризованного индекса столбец секционирования должен содержаться в ключе индекса. При секционировании неуникального некластеризованного индекса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] по умолчанию добавляет столбец секционирования как неключевой (включенный) столбец индекса, чтобы обеспечить выравнивание индекса с базовой таблицей. Если столбец секционирования уже присутствует в индексе, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] его не добавляет. 

### <a name="non-aligned-index"></a>Невыровненный индекс  
Индекс, секционированный независимо от соответствующей таблицы. Т. е. индекс имеет другую схему секционирования или находится не в той файловой группе, где находится базовая таблица. Создание невыровненного секционированного индекса может быть полезно в следующих случаях:  
-   Базовая таблица не секционирована.  
-   Ключ индекса является уникальным и не содержит столбца секционирования таблицы.  
-   Требуется участие базовой таблицы в выровненных соединениях с таблицами, использующими другие столбцы соединения.  

### <a name="partition-elimination"></a>Устранение секций
Процесс, в ходе которого оптимизатор запросов обращается только к определенным секциям в соответствии с фильтром запроса.  

## <a name="performance-guidelines"></a>Рекомендации по производительности  
 Более высокое новое максимальное количество секций (15 000) влияет на память, операции с секционированными индексами, команды DBCC и запросы. В этом разделе показано, как влияет на производительность создание более 1 000 секций и как обойти проблемы. Увеличение максимального количества секций до 15 000 позволяет дольше хранить данные. Однако рекомендуется хранить данные ровно столько времени, сколько требуется, и поддерживать баланс между производительностью и количеством секций.  
  
### <a name="processor-cores-and-number-of-partitions-guidelines"></a>Рекомендации относительно процессорных ядер и числа секций  
 Чтобы добиться максимальной производительности с помощью параллельных операций, рекомендуется, чтобы число секций и процессорных ядер совпадало, но не превышало 64 (это максимальное число параллельных процессоров, которые [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может использовать).  
  
### <a name="memory-usage-and-guidelines"></a>Использование памяти и рекомендации  
 При большом количестве используемых секций рекомендуется использовать ОЗУ не менее 16 ГБ. Если у системы недостаточно памяти, возможен сбой инструкций языка обработки данных (DML), инструкций языка описания данных (DDL) и других операций из-за нехватки памяти. В системах с ОЗУ 16 ГБ и большим количеством процессов, интенсивно использующих память, возможны сбои операций, работающих на большом количестве секций, из-за нехватки памяти. Поэтому чем больше у вас памяти сверх 16 МБ, тем меньше вероятность проблем с производительностью и памятью.  
  
 Ограничения оперативной памяти могут повлиять на производительность [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] при построении секционированного индекса и даже на саму возможность его построения. Такое случается, например, когда индекс не выровнен со своей базовой таблицей или со своим кластеризованным индексом, если такой существует в таблице. В этом случае может оказаться полезным увеличить параметр конфигурации сервера index create memory. Дополнительные сведения см. в статье [Настройка параметра конфигурации сервера index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md). 
  
### <a name="partitioned-index-operations"></a>Операции с секционированными индексами  
Создание и перестройка невыровненных индексов для таблицы, количество секций в которой превышает 1000, возможны, но не поддерживаются. Это может привести к снижению производительности или чрезмерному потреблению памяти во время таких операций.  
  
Создание и перестройка выровненных индексов может занимать больше времени по мере увеличения количества секций. Не рекомендуется выполнять одновременно несколько команд создания и перестройки индекса, так как возможны проблемы с производительностью и памятью.  
  
 При сортировке, выполняемой при построении секционированных индексов, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] сначала создает для каждой секции по одной таблице сортировки.  Затем либо в соответствующей файловой группе каждой секции, либо в **tempdb**, если задан параметр индекса SORT_IN_TEMPDB, производится построение таблиц сортировки. Для всех таблиц сортировки требуется минимальный объем оперативной памяти. При построении секционированного индекса, выровненного со своей базовой таблицей, таблицы сортировки создаются по одной за раз, экономно расходуя оперативную память. Однако при построении невыровненного секционированного индекса таблицы сортировки создаются одновременно. В результате необходим достаточный объем оперативной памяти, чтобы параллельно их обрабатывать. Чем больше число секций, тем больше требуется оперативной памяти. Для каждой из секций размер таблицы сортировки составляет не менее 40 страниц, по 8 килобайт каждая. Например, для невыровненного секционированного индекса, разбитого на 100 секций, потребуется объем оперативной памяти для одновременной сортировки 4 000 страниц (40*100). Если такой объем памяти доступен, операция создания будет выполнена успешно, но может пострадать производительность. Если же такой объем памяти недоступен, операция построения завершится ошибкой. Для выровненного секционированного индекса, разбитого на 100 секций, для сортировки потребуется всего 40 страниц, поскольку сортировки осуществляются не одновременно.  
  
 Как для выровненных, так и для невыровненных индексов может потребоваться больший объем оперативной памяти, если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] применяет степени параллелизма для выполнения данной операции на многопроцессорном компьютере. Чем больше степень параллелизма, тем больше требуется оперативной памяти. Например, если для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] определена степень параллелизма 4, то невыровненному секционированному индексу, содержащему 100 секций, потребуется такой объем памяти, чтобы четыре процессора могли одновременно отсортировать по 4 000 страниц, то есть 16 000 страниц. Если секционированный индекс выровнен, требования оперативной памяти снижаются до 40 страниц для каждого из четырех процессоров, то есть 160 страниц (4*40). С помощью параметра индекса MAXDOP можно вручную снизить степень параллелизма.  

### <a name="dbcc-commands"></a>Команды DBCC  
При большем количестве секций выполнение команд DBCC может занимать больше времени по мере увеличения количества секций.  
  
### <a name="queries"></a>Запросы  
Запросы, использующие функцию устранения секций, могут иметь сопоставимую или более высокую производительность с большим числом секций. Запросы, не использующие функцию устранения секций, могут занимать больше времени по мере увеличения количества секций.  
  
Предположим, таблица имеет 100 миллионов строк и столбцов `A`, `B`и `C`. 
-  В примере 1 таблица делится на 1000 секций по столбцу `A`. 
-  В примере 2 таблица делится на 10,000 секций по столбцу `A`. Запрос к таблице, включающий предложение `WHERE` с фильтром по столбцу `A`, выполнит функцию устранения секций и просканирует одну секцию. Тот же самый запрос может быть выполнен быстрее в примере 2, так как в секции меньше строк для сканирования. Запрос, включающий предложение `WHERE` с фильтром по столбцу B, будет сканировать все секции. В примере 1 этот запрос может быть выполнен быстрее, чем в примере 2, так как в этом случае меньше секций для сканирования.  

Запросы, в которых используются такие операторы, как TOP или MAX/MIN, в столбцах, отличных от столбца секционирования, могут столкнуться со снижением производительности при секционировании, поскольку вычисляться должны все секции.  

При частом выполнении запросов на эквивалентное соединение двух и более секционированных таблиц, их секционированные столбцы должны совпадать со столбцами, по которым производится соединение. Дополнительно: таблицы или их индексы должны быть упорядочены. Это означает, что в них используется либо общая именованная функция секционирования, либо разные, но дающие одинаковый результат. То есть:
-  Указанные таблицы секционированы по одинаковому количеству параметров, имеющих одинаковый тип данных.
-  В указанных таблицах имеется одинаковое количество секций.
-  В указанных таблицах секции имеют одинаковые граничные значения.
При выполнении указанных условий оптимизатор запросов проводит операцию соединения гораздо быстрее, так как в этом случае могут быть соединены сами секции. Если запрос проводит соединение двух неупорядоченных таблиц, либо таблиц, не секционированных для соединения, наличие секционирования в таблице может замедлить выполнение запроса вместо его ускорения.

## <a name="behavior-changes-in-statistics-computation-during-partitioned-index-operations"></a>Изменения в поведении при статистических вычислениях во время операций с секционированным индексом  
 Начиная с выпуска [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] статистические данные не создаются путем сканирования всех строк таблицы при создании или перестроении секционированного индекса. Вместо этого оптимизатор запросов использует для создания статистики алгоритм выборки по умолчанию. После обновления базы данных с секционированными индексами можно заметить разницу в гистограммах для этих индексов. Это изменение в поведении может не влиять на время выполнения запросов. Для получения статистики по секционированным индексам путем сканирования всех строк таблицы используйте инструкции `CREATE STATISTICS` или `UPDATE STATISTICS` с предложением `FULLSCAN`.  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|||  
|-|-|  
|**Задания**|**Раздел**|  
|Описано, как создать функции секционирования и схемы секционирования и применить их к таблице или индексу.|[Создание секционированных таблиц и индексов](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)|  
|||  
  
## <a name="related-content"></a>См. также  
 Следующие публикации по стратегиям секционированных таблиц и индексов и примеры внедрения могут оказаться полезными.  
-   [Partitioned Table and Index Strategies Using SQL Server 2008](https://msdn.microsoft.com/library/dd578580\(SQL.100\).aspx)    
-   [How to Implement an Automatic Sliding Window in a Partitioned Table on SQL Server 2005](https://msdn.microsoft.com/library/aa964122\(SQL.90\).aspx)    
-   [Массовая загрузка в секционированную таблицу](https://msdn.microsoft.com/library/cc966380.aspx)    
-   [Проект REAL. Жизненный цикл данных — секционирование](https://technet.microsoft.com/library/cc966424.aspx)    
-   [Улучшенные возможности обработки запросов для секционированных таблиц и индексов](https://msdn.microsoft.com/library/ms345599.aspx)    
-   [10 лучших методов для построения реляционного хранилища данных в больших масштабах](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/SQLCAT's%20Guide%20to%20Relational%20Engine.pdf) в _руководстве SQLCAT по реляционному проектированию_
  
  
