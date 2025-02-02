---
title: Оценка требований к объему памяти для таблиц, оптимизированных для памяти | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 15b3b27f859b2ea2ed3008d33f19a682aeef833b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157960"
---
# <a name="estimate-memory-requirements-for-memory-optimized-tables"></a>Оценка требований к объему памяти для таблиц, оптимизированных для памяти
  При создании нового [!INCLUDE[hek_2](../../includes/hek-2-md.md)] оптимизированной для памяти таблицы или переносе существующей таблицы на диске в оптимизированных для памяти таблицу, важно иметь оценку требований к памяти для каждой таблицы, поэтому можно оставить на сервере достаточно объем памяти. В этом разделе описывается, как определить объем памяти, необходимый для хранения данных в таблице, оптимизированной для памяти.  
  
 Если вы рассматриваете переход от дисковых таблиц к таблицам, оптимизированным для памяти, то перед продолжением чтения посмотрите в разделе [Определение, должна ли таблица или хранимая процедура быть перенесена в In-Memory OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) сведения о том, какие таблицы лучше всего подходят для миграции. Все разделы статьи [Миграция в In-Memory OLTP](migrating-to-in-memory-oltp.md) содержат руководство по миграции дисковых таблиц в оптимизированные для памяти.  
  
## <a name="sections-in-this-topic"></a>Подразделы этого раздела  
  
-   [Пример оптимизированной для памяти таблицы](#bkmk_ExampleTable)  
  
-   [Память для таблицы](#bkmk_MemoryForTable)  
  
-   [Память для индексов](#bkmk_IndexMeemory)  
  
-   [Память для управления версиями строк](#bkmk_MemoryForRowVersions)  
  
-   [Память для табличных переменных](#bkmk_TableVariables)  
  
-   [Память под будущее увеличение](#bkmk_MemoryForGrowth)  
  
##  <a name="bkmk_ExampleTable"></a> Пример оптимизированной для памяти таблицы  
 Рассмотрим следующую схему таблицы, оптимизированной для памяти:  
  
```sql  
  
CREATE TABLE t_hk (  
col1 int NOT NULL PRIMARY KEY NONCLUSTERED,  
col2 int NOT NULL INDEX t1c2_index   
     HASH WITH (bucket_count = 5000000),  
col3 int NOT NULL INDEX t1c3_index   
     HASH WITH (bucket_count = 5000000),  
col4 int NOT NULL INDEX t1c4_index   
     HASH WITH (bucket_count = 5000000),  
col5 int NOT NULL INDEX t1c5_index NONCLUSTERED,  
col6 char (50) NOT NULL,  
col7 char (50) NOT NULL,   
col8 char (30) NOT NULL,   
col9 char (50) NOT NULL  
     WITH (memory_optimized = on)  
GO  
  
```  
  
 С помощью этой схемы мы определим минимальный объем памяти, необходимый для оптимизированной для памяти таблицы.  
  
##  <a name="bkmk_MemoryForTable"></a> Память для таблицы  
 Строка оптимизированной для памяти таблицы состоит из 3 частей:  
  
-   **Метки времени**   
    Заголовок строки или метки времени = 24 байта.  
  
-   **Указатели индекса**   
    Для каждого хэш-индекса в таблице каждая строка содержит 8-байтный адресный указатель на следующую строку в индексе.  Поскольку имеются 4 индекса, каждая строка выделит 32 байта для указателей индекса (указатель для каждого индекса занимает 8 байт).  
  
-   **Данные**   
    Размер данных в строке определяется путем суммирования размера типа данных для каждого столбца данных.  В нашей таблице имеется пять 4-байтных целых чисел, три 50-байтных символьных столбцов и один 30-байтный символьный столбец.  Поэтому часть данных в каждой строке — это 4 + 4 + 4 + 4 + 4 + 50 + 50 + 30 + 50 или 200 байт.  
  
 Далее приведено вычисление размера для 5 миллионов строк в таблице, оптимизированной для памяти. Общий объем памяти, используемой строками данных, вычисляется следующим образом:  
  
 **Память для строк таблицы**  
  
 Из вышеуказанных вычислений, размер каждой строки в таблице, оптимизированной для памяти, будет 24 + 32 + 200 или 256 байт.  Поскольку мы имеем 5 миллионов строк, таблица использует 5 000 000 * 256 байт или 1 280 000 000 байт — примерно 1,28 ГБ.  
  
##  <a name="bkmk_IndexMeemory"></a> Память для индексов  
 **Объем памяти для каждого хэш-индекса**  
  
 Каждый хэш-индекс — это хэш-массив, состоящий из 8-байтных указателей адреса.  Размер массива лучше всего определяется количеством уникальных значений индекса в нем, то есть количество уникальных значений Col2 будет хорошей отправной точкой для подсчета размера массива t1c2_index. Слишком большой хэш-массив занимает много памяти.  Слишком маленький хэш-массив снижает производительность, поскольку будет слишком много конфликтов индексных значений, которые хэшируются в один и тот же индекс.  
  
 В хэш-индексах скорость поиска совпадений очень высока:  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE Col2 = 3  
  
```  
  
 Некластеризованные индексы будут быстрее при поиске диапазона, например:  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE Col2 >= 3  
  
```  
  
 При переносе дисковой таблицы можно использовать следующий критерий для определения количества уникальных значений в индексе t1c2_index.  
  
```sql  
  
SELECT COUNT(DISTINCT [Col2])  
  FROM t_hk  
  
```  
  
 При создании новой таблицы необходимо оценить размер массива или собрать данные путем теста еще до развертывания.  
  
 Сведения о принципах работы хэш-индексов в оптимизированных для памяти таблицах [!INCLUDE[hek_2](../../includes/hek-2-md.md)] см. в разделе [Хэш-индексы](../../database-engine/hash-indexes.md).  
  
 **Примечание.** Невозможно изменить размер массива хэш-индекса в режиме реального времени. Чтобы изменить размер массива хэш-индекса, нужно удалить таблицу, изменить значение bucket_count и повторно создать таблицу.  
  
 **Параметр размер массива хэш-индекса**  
  
 Размер хэш-массива задается `(bucket_count= <value>)` где \<значение > является целым значением, отличным от нуля. Если \<значение > не является степенью 2, фактическое значение bucket_count округляется вверх до следующего ближайшей степени числа 2.  В нашем примере таблицы (bucket_count = 5000000), так как 5 000 000 не является степенью числа 2, фактическое число контейнеров округляется до 8 388 608 (2<sup>23</sup>).  Необходимо использовать это число, а не 5 000 000, при вычислении объема памяти, необходимого для хэш-массива.  
  
 Таким образом, в нашем примере для хэш-массива потребуется памяти:  
  
 8 388 608 * 8 = 2<sup>23</sup> \* 8 = 2<sup>23</sup> \* 2<sup>3</sup> = 2<sup>26</sup> = 67 108 864 или приблизительно 64 МБ.  
  
 Поскольку мы имеем 3 хэш-индекса, память, требуемая для хэш-индексов, — 64 МБ * 3 = 192 МБ.  
  
 **Память для некластеризованных индексов**  
  
 Некластеризованные индексы реализуются в виде B-деревьев, внутренние узлы которых содержат значения индекса и указатели на последующие узлы.  Листовые узлы содержат значение индекса и указатель на строку таблицы в памяти.  
  
 В отличие от хэш-индексов некластеризованные индексы не имеют фиксированный размер контейнера. Индекс динамически увеличивается и уменьшается вместе с данными.  
  
 Объем памяти, требуемый для некластеризованных индексов, можно вычислить следующим образом:  
  
-   **Память, выделенная для неконечных узлов**   
    В стандартной конфигурации объем памяти, выделенный для неконечных узлов, составляет небольшой процент от общей памяти, занятой индексом. Это слишком мало, поэтому этот объем можно спокойно опустить.  
  
-   **Память для конечных узлов**   
    Конечные узлы содержат по одной строке для каждого уникального ключа в таблице, и она указывает на строки данных с этим уникальным ключом.  При наличии нескольких строк с одинаковым ключом (т. е. имеется неуникальный некластеризованный индекс) будет только одна строка в конечном узле индекса, указывающая на одну из строк, а другие строки будут связаны между собой.  Таким образом, общую память можно примерно вычислить следующим образом:   
    memoryForNonClusteredIndex = (pointerSize + sum(keyColumnDataTypeSizes)) * rowsWithUniqueKeys  
  
 Некластеризованные индексы наилучшим образом подходят для поиска по диапазону, как показано в примере следующего запроса:  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE c2 > 5  
```  
  
##  <a name="bkmk_MemoryForRowVersions"></a> Память для управления версиями строк  
 Чтобы избежать блокировок, модуль In-Memory OLTP использует оптимистический параллелизм при обновлении или удалении строк. Это означает, что при обновлении строки создается ее дополнительная версия. Система держит предыдущие версии до тех пор, пока все транзакции, которые теоретически могут использовать одну из версий, не завершатся. При удалении строки система действует точно так же, как и при обновлении, сохраняя версию до тех пор, пока она больше не понадобится. Операции считывания и вставки не создают версии дополнительных строк.  
  
 Поскольку в любой момент в памяти может находиться некоторое количество дополнительных строк, ожидающих цикла сборки мусора для освобождения памяти, необходимо иметь достаточный объем памяти, чтобы учесть эти дополнительные строки.  
  
 Число дополнительных строк может быть получено путем подсчета пикового количества обновлений и удалений строк в секунду, которое затем умножается на число секунд, которое занимает самая длинная транзакция (минимум 1 секунда).  
  
 Затем это значение умножается на размер строки, что дает число байтов, необходимых для управления версиями строк.  
  
 `rowVersions = durationOfLongestTransactionInSeconds * peakNumberOfRowUpdatesOrDeletesPerSecond`  
  
 Затем вычисляется нужный памяти для старых строк путем умножения количества старых строк на размер строки в таблице, оптимизированной для памяти (см. в разделе [память для таблицы](#bkmk_MemoryForTable) выше).  
  
 `memoryForRowVersions = rowVersions * rowSize`  
  
##  <a name="bkmk_TableVariables"></a> Память для табличных переменных  
 Память, отведенная для табличных переменных, освобождается только в тех случаях, когда табличная переменная покидает область действия. Удаленные строки, включая строки, удаленные как часть обновления, из табличной переменной, не подвергаются сборке мусора. Ресурсы памяти не освобождаются до того момента, пока существует область табличных переменных.  
  
 Табличные переменные, определенные в большом пакете SQL, в отличие от области действия процедур, используемых в нескольких транзакциях, могут потреблять большой объем памяти. Так как для них не применяется сборка мусора, удаленные строки в табличной переменной могут занимать большой объем памяти и, следовательно, могут снизить производительность, т. к. операции считывания должны сканировать эти удаленные строки.  
  
##  <a name="bkmk_MemoryForGrowth"></a> Память под будущее увеличение  
 Указанные выше вычисления дают оценку потребного объема памяти для таблицы в том виде, в котором она существует в данный момент. В дополнение к этому объему памяти необходимо оценить увеличение размера таблицы и предоставить достаточно памяти для ее будущего роста.  Например, если предполагается рост размера в 10 %, то следует умножить полученные ранее результаты на 1,1. Это и даст общую оценку объема памяти для таблицы.  
  
## <a name="see-also"></a>См. также:  
 [Миграция в In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
