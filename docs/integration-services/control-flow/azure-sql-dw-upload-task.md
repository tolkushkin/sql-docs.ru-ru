---
title: Задача отправки информации в хранилище данных SQL Azure | Документы Майкрософт
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPDWUPTASK.F1
- sql14.dts.designer.afpdwuptask.f1
ms.assetid: eef82c89-228a-4dc7-9bd0-ea00f57692f5
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.openlocfilehash: 96be54415e3a2892da2ec892a0e90c02c5365e90
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727931"
---
# <a name="azure-sql-dw-upload-task"></a>Задача отправки информации в хранилище данных SQL Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



**Задача отправки информации в хранилище данных SQL Azure** позволяет пакету служб SSIS копировать табличные данные в хранилище данных SQL Azure из файловой системы или хранилища BLOB-объектов Azure.
Для повышения производительности в задаче используется подход PolyBase, описанный в статье [Azure SQL Data Warehouse Loading Patterns and Strategies](https://blogs.msdn.microsoft.com/sqlcat/2017/05/17/azure-sql-data-warehouse-loading-patterns-and-strategies/)(Стратегии и шаблоны загрузки хранилища данных SQL Azure).
В настоящее время в качестве формата исходного файла данных поддерживается текст с разделителями в кодировке UTF-8.
В процессе копирования из файловой системы данные сначала будут переданы на промежуточное хранение в хранилище BLOB-объектов Azure, а затем в хранилище данных SQL Azure. Поэтому требуется учетная запись хранилища BLOB-объектов Azure.

**Задача отправки информации в хранилище данных SQL Azure** входит в состав [пакета дополнительных компонентов SQL Server Integration Services (SSIS) для Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Чтобы добавить **задачу отправки информации в хранилище данных SQL Azure**, перетащите ее из панели элементов служб SSIS на холст конструктора и дважды щелкните ее (или щелкните ее правой кнопкой мыши), а затем выберите команду **Изменить** , чтобы открыть диалоговое окно редактора задач.

На странице **Общие** настройте следующие свойства.

В свойстве **SourceType** указывается тип источника данных. Выберите один из следующих вариантов:

* **FileSystem:** исходные данные находятся в локальной файловой системе.
* **BlobStorage:** исходные данные находятся в хранилище BLOB-объектов Azure.

Ниже указаны свойства для каждого типа источника.

### <a name="filesystem"></a>FileSystem

Поле|Описание
-----|-----------
LocalDirectory|Указывает локальный каталог с файлами данных для отправки.
Рекурсивно|Указывает, выполнять ли рекурсивный поиск в подкаталогах.
FileName|Указывает фильтр имен для выбора файлов с определенным именем. Пример: при указании MySheet*.xls\* будут выбраны такие файлы, как MySheet001.xls и MySheetABC.xlsx.
RowDelimiter|Указывает символы, обозначающие конец строки.
ColumnDelimiter|Указывает символы, обозначающие конец столбца. Пример: &#124; (вертикальная черта), \t (табуляция), ' (одинарная кавычка), " (двойная кавычка) и 0x5c (обратная косая черта).
IsFirstRowHeader|Указывает, содержит ли первая строка каждого файла данных названия столбцов, а не фактические данные.
AzureStorageConnection|Указывает диспетчер подключений службы хранилища Azure.
BlobContainer|Задает название контейнера больших двоичных объектов, в который будут переданы локальные данные (и который будет использоваться для их ретрансляции в хранилище данных Azure через PolyBase). Если контейнер не существует, он будет создан.
BlobDirectory|Задает название каталога больших двоичных объектов (виртуальной иерархической структуры), в который будут переданы локальные данные (и который будет использоваться для их ретрансляции в хранилище данных Azure через PolyBase).
RetainFiles|Указывает, следует ли сохранить файлы, переданные в службу хранилища Azure.
CompressionType|Указывает формат сжатия, используемый при передаче файлов в службу хранилища Azure. Сжатие не влияет на локальный источник.
CompressionLevel|Указывает уровень сжатия, используемый в рамках формата сжатия.
AzureDwConnection|Указывает диспетчер соединений ADO.NET для хранилища данных SQL Azure.
TableName|Указывает название целевой таблицы. Выберите существующую таблицу или создайте новую, выбрав пункт **\<Создать таблицу ...>**.
TableDistribution|Указывает метод распределения данных для новой таблицы. Применяется, если для **TableName**указано название новой таблицы.
HashColumnName|Указывает столбец, используемый для распределения данных посредством хэш-таблицы. Применяется, если для **TableDistribution** указано значение **HASH**.

### <a name="blobstorage"></a>BlobStorage

Поле|Описание
-----|-----------
AzureStorageConnection|Указывает диспетчер подключений службы хранилища Azure.
BlobContainer|Указывает имя контейнера больших двоичных объектов, в котором находится источник данных.
BlobDirectory|Указывает каталог больших двоичных объектов (виртуальную иерархическую структуру), в котором находится источник данных.
RowDelimiter|Указывает символы, обозначающие конец строки.
ColumnDelimiter|Указывает символы, обозначающие конец столбца. Пример: &#124; (вертикальная черта), \t (табуляция), ' (одинарная кавычка), " (двойная кавычка) и 0x5c (обратная косая черта).
CompressionType|Указывает формат сжатия, используемый для источника данных.
AzureDwConnection|Указывает диспетчер соединений ADO.NET для хранилища данных SQL Azure.
TableName|Указывает название целевой таблицы. Выберите существующую таблицу или создайте новую, выбрав пункт **\<Создать таблицу ...>**.
TableDistribution|Указывает метод распределения данных для новой таблицы. Применяется, если для **TableName**указано название новой таблицы.
HashColumnName|Указывает столбец, используемый для распределения данных посредством хэш-таблицы. Применяется, если для **TableDistribution** указано значение **HASH**.

Содержимое страницы **Сопоставления** изменяется в зависимости от того, в какую таблицу копируются данные — в новую или существующую.
В первом случае необходимо будет настроить сопоставляемые исходные столбцы и соответствующие им названия целевых столбцов в создаваемой целевой таблице.
Во втором случае необходимо сопоставить исходные и целевые столбцы.

На странице **Столбцы** необходимо настроить свойства типов данных для каждого исходного столбца.

На странице **T-SQL** отображается код T-SQL, используемый для передачи данных из хранилища BLOB-объектов Azure в хранилище данных SQL Azure.
Этот код создается автоматически на основе параметров конфигурации, выбранных на других страницах, и будет исполняться в ходе выполнения задачи.
Вы можете вручную изменить созданный код T-SQL, если нужно, нажав кнопку **Изменить** .
Чтобы позже вернуться к исходному коду (первоначально созданному автоматически), нажмите кнопку **Сброс** .
