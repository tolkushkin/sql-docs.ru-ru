---
title: CREATE EXTERNAL FILE FORMAT (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 02/20/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4018857b93a828e5ed756a80ba23f425a26790c8
ms.sourcegitcommit: 982a1dad0b58315cff7b54445f998499ef80e68d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66175026"
---
# <a name="create-external-file-format-transact-sql"></a>CREATE EXTERNAL FILE FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Создает объект формата внешнего файла, определяя внешние данные, которые сохранены в Hadoop, хранилище BLOB-объектов Azure или хранилище озера данных Azure. Создание формата внешнего файла — обязательное условие для создания внешней таблицы. Создавая формат внешнего файла, вы указываете фактическую структуру данных, на которые ссылается внешняя таблица.  
  
 PolyBase поддерживает следующие форматы файлов:
  
-   Текстовый файл с разделителями  
  
-   Hive RCFile  
  
-   Hive ORC
  
-   Parquet  
  
Инструкции по созданию внешней таблицы см. в разделе [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md).
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис
  
```
-- Create an external file format for PARQUET files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = PARQUET  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.GzipCodec'      }  
    ]);  
  
--Create an external file format for ORC files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = ORC  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.DefaultCodec'      }  
    ]);  
  
--Create an external file format for RCFILE.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = {  
        'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
      | 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'  
    }  
    [ , DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec' ]);  
  
--Create an external file format for DELIMITED TEXT files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT  
    [ , FORMAT_OPTIONS ( <format_options> [ ,...n  ] ) ]  
    [ , DATA_COMPRESSION = {  
           'org.apache.hadoop.io.compress.GzipCodec'  
         | 'org.apache.hadoop.io.compress.DefaultCodec'  
        }  
     ]);  
  
<format_options> ::=  
{  
    FIELD_TERMINATOR = field_terminator  
    | STRING_DELIMITER = string_delimiter 
    | First_Row = integer -- ONLY AVAILABLE SQL DW
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>Аргументы  
 *file_format_name*  
 Задает имя формата внешнего файла.
  
 FORMAT_TYPE = [ PARQUET | ORC | RCFILE | DELIMITEDTEXT] Задает формат внешних данных.
  
   -   PARQUET Задает формат Parquet.
  
   -   ORC  
   Задает формат ORC. Для использования этого параметра во внешнем кластере Hadoop требуется Hive версии 0.11 или выше. В Hadoop формат файла ORC обеспечивает более качественное сжатие и более высокую производительность, чем формат файла RCFILE.

   -   RCFILE (в сочетании с SERDE_METHOD = *SERDE_method*) Задает формат файла RcFile. Этот параметр требует задания метода сериализации и десериализации куч (SerDe). То же требование действует при использовании Hive/HiveQL в Hadoop для отправки запросов файлам RC. Обратите внимание, что метод SerDe учитывает регистр.

   Примеры задания RCFile с двумя методами SerDe, которые поддерживаются PolyBase.

    -   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'

    -   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'

   -   DELIMITEDTEXT Задает формат текста с разделителями столбцов (которые также называются признаками конца поля).
  
 FIELD_TERMINATOR = *field_terminator*  
Применяется только для текстовых файлов с разделителями. Признак конца поля задает один или несколько символов, отмечающих окончание каждого поля (столбца) в файле с разделителями текста. По умолчанию используется вертикальная черта (|). Для гарантированной поддержки рекомендуется использовать один или несколько символов ascii.
  
  
 Примеры:  
  
-   FIELD_TERMINATOR = '|'  
  
-   FIELD_TERMINATOR = ' '  
  
-   FIELD_TERMINATOR = ꞌ\tꞌ  
  
-   FIELD_TERMINATOR = '~|~'  
  
 STRING_DELIMITER = *string_delimiter*  
Задает признак конца поля для данных типа "строка" в файле с разделителями текста. Разделитель строк имеет длину один или несколько символов и заключен в одинарные кавычки. По умолчанию используется пустая строка "". Для гарантированной поддержки рекомендуется использовать один или несколько символов ascii.
 
  
 Примеры:  

-   STRING_DELIMITER = '"'

-   STRING_DELIMITER = '0x22' — шестнадцатеричная двойная кавычка
  
-   STRING_DELIMITER = '*'  
  
-   STRING_DELIMITER = ꞌ,ꞌ  
  
-   STRING_DELIMITER = '0x7E0x7E' — две тильды (например, ~~)
 
 FIRST_ROW = *First_row_int*  
Задает номер строки, которая читается первой во всех файлах во время загрузки PolyBase. Этот параметр может принимать значения 1–15. Если задано значение 2, первая строка в каждом файле (строка заголовка) при загрузке данных пропускается. Строки пропускаются по признакам конца строк (/r/n, /r, /n). Если для экспорта используется этот вариант, строки добавляются в данные, чтобы гарантировать возможность прочтения файла без потери данных. Если задано значение больше 2, первой экспортируется строка с названиями столбцов внешней таблицы.

 DATE\_FORMAT = *datetime_format*  
Задает пользовательский формат для всех данных о дате и времени, которые могут отображаться в текстовом файле с разделителями. Если исходный файл использует стандартные форматы даты и времени, этот параметр не является обязательным. Можно использовать не более одного пользовательского формата даты и времени на файл. Невозможно указать для файла более одного пользовательского формата даты и времени. Однако можно использовать несколько форматов даты и времени, если каждый из них является форматом по умолчанию для соответствующего типа данных в определении внешней таблицы.

PolyBase использует пользовательский формат даты только для импорта данных. Для записи данных во внешний файл пользовательский формат не используется.

 Если параметр DATE_FORMAT не задан или является пустой строкой, PolyBase использует следующие форматы по умолчанию:
  
-   DateTime: 'yyyy-MM-dd HH:mm:ss'  
  
-   SmallDateTime: 'yyyy-MM-dd HH:mm'  
  
-   Date: 'yyyy-MM-dd'  
  
-   DateTime2: 'yyyy-MM-dd HH:mm:ss'  
  
-   DateTimeOffset: 'yyyy-MM-dd HH:mm:ss'  
  
-   Time: 'HH:mm:ss'  
  
**Примеры форматов даты** приводятся в следующей таблице:
  
Примечания об этой таблице:  
  
-   Год, месяц и день могут иметь различные форматы и порядок. В таблице показан только формат **ymd**. Месяц может обозначаться одной или двумя цифрами или тремя символами. День может обозначаться одной или двумя цифрами. Год может обозначаться двумя или четырьмя цифрами.
  
-   Миллисекунды (fffffff) не требуются.
  
-   Указание времени суток (tt) не является обязательным. По умолчанию используется время AM (до полудня).
  
|Тип данных|Пример|Описание|  
|---------------|-------------|-----------------|  
|DateTime|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fff'|Кроме года, месяца и дня этот формат данных включает 00-24 часа, 00-59 минут, 00-59 секунд и трехзначное обозначение миллисекунд.|  
|DateTime|DATE_FORMAT = 'yyyy-MM-dd hh:mm:ss.ffftt'|Кроме года, месяца и дня этот формат данных включает 00-12 часов, 00-59 минут, 00-59 секунд и трехзначное обозначение миллисекунд и указание времени суток: AM, am, PM или pm. |  
|SmallDateTime|DATE_FORMAT =  'yyyy-MM-dd HH:mm'|Кроме года, месяца и дня этот формат данных включает 00-23 часа, 00-59 минут.|  
|SmallDateTime|DATE_FORMAT =  'yyyy-MM-dd hh:mmtt'|Кроме года, месяца и дня этот формат данных включает 00-11 часов, 00-59 минут и указание времени суток: AM, am, PM или pm. Секунды не указаны.|  
|Дата|DATE_FORMAT =  'yyyy-MM-dd'|Год, месяц и день. Элемент времени не включен.|  
|Дата|DATE_FORMAT = 'yyyy-MMM-dd'|Год, месяц и день. Если используется трехзначное обозначение месяца, входящее значение — это одна из строк янв, фев, мар, апр, май, июн, июл, авг, сен, окт, ноя или дек.|  
|datetime2|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fffffff'|Кроме года, месяца и дня этот формат данных включает 00-23 часа, 00-59 минут, 00-59 секунд и семизначное обозначение миллисекунд.|  
|datetime2|DATE_FORMAT = 'yyyy-MM-dd hh:mm:ss.ffffffftt'|Кроме года, месяца и дня этот формат данных включает 00-11 часов, 00-59 минут, 00-59 секунд и семизначное обозначение миллисекунд и указание времени суток: AM, am, PM или pm.|  
|DateTimeOffset|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fffffff zzz'|Кроме года, месяца и дня этот формат данных включает 00-23 часа, 00-59 минут, 00-59 секунд, семизначное обозначение миллисекунд и смещение часового пояса, которое указывается во входящем файле в виде `{+&#124;-}HH:ss`. Например, так как время в Лос-Анджелесе без перехода на летнее время на 8 часов отстает от времени UTC, значение -08:00 во входящем файле задает часовой пояс для Лос-Анджелеса.|  
|DateTimeOffset|DATE_FORMAT = 'yyyy-MM-dd hh:mm:ss.ffffffftt zzz'|Кроме года, месяца и дня этот формат данных включает 00-11 часов, 00-59 минут, 00-59 секунд и семизначное обозначение миллисекунд, указание времени суток (AM, am, PM или pm) и смещение часового пояса. См. в описании в предыдущей строке.|  
|Time|DATE_FORMAT = 'HH:mm:ss'|Нет значения даты, только 00-23 часа 00-59 минут и 00-59 секунд.|  
  
 Все поддерживаемые форматы даты:
  
|DATETIME|smalldatetime|Дата|datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm[:00][tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm[:00][tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
 Сведения.  
  
-   Для разделения значений месяца, дня и года можно использовать символы "-", "/" или ".". Для простоты в таблице используется только разделитель "-".
  
-   Чтобы указать месяц в виде текста, используйте три и более символов. Обозначения месяца из одного или двух символов интерпретируются как число.
  
-   Для разделения значений времени используйте символ ":".
  
-   Буквы в квадратных скобках необязательны.
  
-   Буквы tt обозначают время суток [AM|PM|am|pm]. По умолчанию используется AM. Если задано значение tt, значение часа (hh) должно находиться в диапазоне от 0 до 12.
  
-   Буквы zzz обозначают смещение часового пояса для текущего часового пояса системы в формате {+ |-} HH:ss].
  
 USE_TYPE_DEFAULT = { TRUE | **FALSE** }  
 Указывает способ обработки отсутствующих значений в текстовых файлах с разделителями, когда PolyBase извлекает данные из текстового файла.
  
 TRUE  
 При извлечении данных из текстового файла сохраните каждое отсутствующее значение, воспользовавшись значением по умолчанию для типа данных в соответствующем столбце в определении внешней таблицы. Например, замените отсутствующее значение следующим:  
  
-   0, если столбец определен как числовой. Столбцы decimal не поддерживаются и приводят к ошибке.
  
-   Пустая строка "", если столбец является строковым.
  
-   1900-01-01, если столбец является столбцом дат.
  
 FALSE  
 Сохраните все отсутствующие значения как NULL. Любые значения NULL, сохраненные с использованием слова NULL в текстовом файле с разделителями, импортируются в качестве строки NULL.
  
   Encoding = {'UTF8' | 'UTF16'}  
 В Хранилище данных SQL Azure и PDW (APS CU7.4) PolyBase может читать текстовые файлы с разделителями в кодировке UTF8 и UTF16-LE. В SQL Server PolyBase не поддерживает чтение файлов в кодировке UTF16.
  
 DATA_COMPRESSION = *data_compression_method*  
 Задает метод сжатия данных для внешних данных. Если параметр DATA_COMPRESSION не задан, по умолчанию используются несжатые данные.
 Для правильной работы сжатые Gzip файлы должны иметь файловое расширение .gz.
 
 Тип формата DELIMITEDTEXT поддерживает следующие методы сжатия:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'

 Тип формата RCFILE поддерживает следующий метод сжатия:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
 Тип файлового формата ORC поддерживает следующие методы сжатия:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
 Тип файлового формата PARQUET поддерживает следующие методы сжатия:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
## <a name="permissions"></a>Разрешения  
 Требуется разрешение ALTER ANY EXTERNAL FILE FORMAT.
  
## <a name="general-remarks"></a>Общие замечания
 Формат внешнего файла действует на уровне баз данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Он действует на уровне сервера в [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 Все варианты форматов являются необязательными и применяются только к текстовым файлам с разделителями.  
  
 Если данные хранятся в одном из сжатых форматов, PolyBase сначала распаковывает данные и только потом возвращает записи данных.
  
## <a name="limitations-and-restrictions"></a>Ограничения
  
 Разделитель строк в текстовых файлах с разделителями должен поддерживаться объектом LineRecordReader в Hadoop. То есть необходимо использовать следующие разделители: \r, \n или \r\n. Эти разделители не настраиваются пользователем.
  
 Сочетания поддерживаемых методов SerDe с RCFiles, а также поддерживаемые методы сжатия данных перечислены ранее в этой статье. Поддерживаются не все комбинации.
  
 Максимальное число одновременно выполняющихся процессов PolyBase — 32. При выполнении 32 параллельных запросов каждый запрос может прочитать не более 33 000 файлов из внешнего файлового расположения. Корневая папка и каждая вложенная папка тоже считаются файлами. Если степень параллелизма меньше 32, внешнее файловое расположение может содержать более 33 000 файлов.
  
 Из-за ограничения на количество файлов во внешней таблице рекомендуется хранить не более 30 000 файлов в корневой и вложенных папках внешнего файлового расположения. Кроме того, рекомендуется не создавать много вложенных папок в корневом каталоге. При ссылке на слишком большое число файлов может возникнуть исключение, связанное с нехваткой памяти на виртуальной машине Java.
  
  При экспорте данных в Hadoop или хранилище BLOB-объектов Azure с помощью PolyBase передаются только данные без имен столбцов (метаданных), как определено в команде CREATE EXTERNAL TABLE.

## <a name="locking"></a>Блокировка  
 Принимает совмещаемую блокировку на объекте EXTERNAL FILE FORMAT.
  
## <a name="performance"></a>Производительность
 При использовании сжатых файлов всегда приходится идти на компромисс: перенести меньше данных между внешним источником данных и SQL Server, но увеличить использование ресурсов ЦП для сжатия и распаковывания данных.
  
 Сжатые текстовые файлы Gzip разделить невозможно. Чтобы повысить производительность сжатых текстовых файлов Gzip, рекомендуется создать несколько хранимых в одном каталоге файлов во внешнем источнике данных. Такая файловая структура позволяет PolyBase читать и распаковывать данные быстрее, используя несколько процессов чтения и распаковывания. Оптимальное количество сжатых файлов — максимальное число процессов чтения данных на вычислительном узле. В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] максимальное число процессов чтения данных на узел составляет 8 для каждого узла. В хранилище данных SQL Azure 2-го поколения это число составляет 20. В [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] максимальное число процессов чтения данных на узел варьируется в зависимости от SLO. См. подробные сведения в разделе [Стратегии и шаблоны загрузки хранилища данных SQL Azure](https://blogs.msdn.microsoft.com/sqlcat/2017/05/17/azure-sql-data-warehouse-loading-patterns-and-strategies/).  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>A. Создание формата внешнего файла DELIMITEDTEXT  
 В этом примере создается формат внешнего файла *textdelimited1* для текстового файла с разделителями. Параметры, заданные для FORMAT\_OPTIONS, указывают, что поля в файле необходимо разделять вертикальной чертой (|). Текстовый файл также сжимается с помощью кодека Gzip. Если параметр DATA\_COMPRESSION не задан, сжатие текстового файла не выполняется.
  
 Для текстового файла с разделителями в качестве метода сжатия данных может использоваться либо кодек по умолчанию (org.apache.hadoop.io.compress.DefaultCodec), либо кодек Gzip (org.apache.hadoop.io.compress.GzipCodec).
  
```  
CREATE EXTERNAL FILE FORMAT textdelimited1  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,  
    FORMAT_OPTIONS (  
        FIELD_TERMINATOR = '|',  
        DATE_FORMAT = 'MM/dd/yyyy' ),  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
);  
```  
  
### <a name="b-create-an-rcfile-external-file-format"></a>Б. Создание формата внешнего файла RCFile  
 В этом примере создается формат внешнего файла для RCFile, использующего метод сериализации/десериализации org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe. Кроме того, указано, что в качестве метода сжатия данных необходимо использовать кодек по умолчанию. Если параметр DATA_COMPRESSION не задан, по умолчанию сжатие не выполняется.
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>В. Создание формата внешнего файла ORC  
 В этом примере создается формат внешнего файла для файла ORC, который сжимает данные с помощью метода сжатия данных org.apache.io.compress.SnappyCodec. Если параметр DATA_COMPRESSION не задан, по умолчанию сжатие не выполняется.
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>Г. Создание формата внешнего файла PARQUET  
 В этом примере создается формат внешнего файла для файла Parquet, который сжимает данные с помощью метода сжатия данных org.apache.io.compress.SnappyCodec. Если параметр DATA_COMPRESSION не задан, по умолчанию сжатие не выполняется.  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
### <a name="e-create-a-delimited-text-file-skipping-header-row-azure-sql-dw-only"></a>Д. Создание текстового файла с разделителями с пропуском строки заголовка (только для хранилища данных SQL Azure)
 В этом примере создается формат внешнего файла для файла CSV с одной строкой заголовка. 
  
```  
CREATE EXTERNAL FILE FORMAT skipHeader_CSV
WITH (FORMAT_TYPE = DELIMITEDTEXT,
      FORMAT_OPTIONS(
          FIELD_TERMINATOR = ',',
          STRING_DELIMITER = '"',
          FIRST_ROW = 2, 
          USE_TYPE_DEFAULT = True)
)
```   

## <a name="see-also"></a>См. также:
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT (хранилище данных SQL Azure)](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
