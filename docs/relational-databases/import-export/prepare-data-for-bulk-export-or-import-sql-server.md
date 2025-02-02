---
title: Подготовка данных к массовому экспорту или импорту (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], planning
- bulk importing [SQL Server], from a CSV file
- data formats [SQL Server], planning operations
- CSV files [SQL Server]
- quoted fields in CSV files [SQL Server]
ms.assetid: 783fd581-2e5f-496b-b79c-d4de1e09ea30
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3489ef2c55de4ce332f53bccc167f2ff052f19d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "64946153"
---
# <a name="prepare-data-for-bulk-export-or-import-sql-server"></a>Подготовка данных к массовому экспорту или импорту (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  В этом разделе рассматриваются факторы, которые следует учитывать при планировании операций массового экспорта, и требования для операций массового импорта.  
  
> [!NOTE]  
>  Если вы не уверены в том, как следует форматировать файл данных для массового импорта, то для экспорта данных из таблицы в файл данных можно использовать служебную программу **bcp** . Форматирование каждого поля данных в этом файле соответствует необходимому формату для массового импорта данных в соответствующий столбец таблицы. Используйте то же самое форматирование для полей своего файла данных.  
  
## <a name="data-file-format-considerations-for-bulk-export"></a>Замечания по формату файлов данных для массового экспорта  
 Прежде чем выполнить операцию массового экспорта с помощью команды **bcp** , примите во внимание следующее.  
  
-   При экспорте данных в файл команда **bcp** автоматически создает файл данных, используя указанное имя файла. Если это имя файла уже используется, то в процессе массового копирования в файл данных существующее содержимое файла перезаписывается.  
  
-   Для массового экспорта из таблицы или представления в файл данных необходимо разрешение SELECT в таблице или представлении, над которым производится операция массового копирования.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может использовать параллельный просмотр для получения данных. Поэтому обычно не гарантируется определенный порядок размещения в файле данных строк таблицы, над которыми была выполнена операция массового экспорта из экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Чтобы строки таблицы для массового экспорта размещались в файле данных в определенном порядке, примените параметр **queryout** для массового экспорта из запроса и укажите предложение ORDER BY.  
  
## <a name="data-file-format-requirements-for-bulk-import"></a>Требования к формату файлов данных для массового импорта  
 Файл, из которого необходимо импортировать данные, должен отвечать следующим основным требованиям.  
  
-   Данные должны быть представлены в формате строк и столбцов.  
  
> [!NOTE]  
>  Структура файла данных необязательно должна быть идентична структуре таблицы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так как столбцы можно пропускать и переупорядочивать в процессе массового импорта.  
  
-   Данные в файле данных должны быть в поддерживаемом формате, например символьном или исходном.  
  
-   Данные могут быть в символьном или исходном двоичном формате, включая Юникод.  
  
-   Для импорта данных с использованием команды **bcp**, инструкции BULK INSERT или инструкции INSERT… SELECT * FROM OPENROWSET(BULK...), целевая таблица должна уже существовать.  
  
-   Каждое поле в файле данных должно быть совместимо с соответствующим столбцом в целевой таблице. Например, поле типа **int** нельзя загрузить в столбец типа **datetime** . Дополнительные сведения см. в статьях [Форматы данных для массового экспорта или импорта (SQL Server)](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md) и [Указание форматов данных для совместимости с помощью программы bcp (SQL Server)](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
    > [!NOTE]  
    >  Указать для импорта из файла данных не весь файл, а подмножество строк можно с помощью команды **bcp** с параметром **-F** *first_row* и (или) параметром **-L** *last_row*. Дополнительные сведения см. в разделе [bcp Utility](../../tools/bcp-utility.md).  
  
-   Чтобы импортировать данные из файлов данных фиксированной длины или с полями фиксированной ширины, используйте файл форматирования. Дополнительные сведения см. в разделе [XML-файлы форматирования (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md).  
  
-   CSV-Файлы с разделителями-запятыми не поддерживаются в операциях массового импорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Однако в некоторых случаях CSV-файл можно использовать в качестве файла данных для массового импорта данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Обратите внимание, что признаком конца поля CSV-файла не обязательно должна быть запятая. CSV-файл, который можно использовать в качестве файла данных для массового импорта, должен соответствовать следующим условиям.  
  
    -   Поля данных не должны содержать признак конца поля.  
  
    -   Или никакие, или все значения в полях данных должны заключаться в кавычки ("").  
  
     Чтобы выполнить массовый импорт данных из файла [!INCLUDE[msCoName](../../includes/msconame-md.md)] FoxPro, таблицы Visual FoxPro (DBF) или листа [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] (XLS), данные необходимо преобразовать в CSV-файл, который соответствует описанным ранее ограничениям. Этот файл обычно имеет расширение CSV. Затем его можно использовать как файл данных в операции массового импорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     На 32-разрядных системах возможно импортировать данные CSV в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] без оптимизации массового импорта с помощью параметра [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) с поставщиком OLE DB для Jet. Поставщик Jet обрабатывает текстовые файлы как таблицы со схемой, определенной в файле schema.ini, который расположен в том же каталоге, что и источник данных.  Для CSV-данных одним из параметров в файле schema.ini будет «FORMAT=CSVDelimited». Чтобы использовать такое решение, нужно представлять принципы работы поставщика Jet Test IISAMm: знать синтаксис строки соединения, правила использования schema.ini, параметры реестра и т. д.  Лучшими источниками для получения таких сведений служат справка Microsoft Access и статьи базы знаний. Дополнительные сведения см. в разделах [Инициализация драйвера текстового источника данных](https://msdn.microsoft.com/library/office/ff834391.aspx), [Как использовать распределенный запрос SQL Server 7.0 со связанным сервером для защищенных баз данных Access](https://go.microsoft.com/fwlink/?LinkId=128504), [Как использовать поставщик Jet OLE DB 4.0 для подключения к базам данных ISAM](https://go.microsoft.com/fwlink/?LinkId=128505) (на английском языке) и [Как открыть текстовые файлы с разделителями с помощью драйвера Text IIsam поставщика Jet](https://go.microsoft.com/fwlink/?LinkId=128501) (на английском языке).  
  
 Кроме того, для массового импорта данных из файла данных в таблицу необходимо следующее.  
  
-   Пользователи должны иметь разрешения INSERT и SELECT в таблице. Пользователи также должны иметь разрешение ALTER TABLE в случае использования параметров, требующих операций DDL, например отмены ограничений.  
  
-   При массовом импорте данных с использованием инструкций BULK INSERT или INSERT ... SELECT * FROM OPENROWSET(BULK...), файл данных должен быть доступен для операций чтения из профиля безопасности процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (если пользователь регистрируется с именем входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) или из процедуры входа [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, выполняемой с делегированными полномочиями безопасности. В дополнение пользователь должен иметь разрешение ADMINISTER BULK OPERATIONS для чтения файла.  
  
> [!NOTE]  
>  Массовый импорт в секционированное представление не поддерживается, и попытки массового импорта данных в секционированное представление завершаются неудачно.  
  
## <a name="external-resources"></a>Внешние ресурсы  
 [Импорт данных из Excel в SQL Server](https://support.microsoft.com/kb/321686)  
  
## <a name="change-history"></a>Журнал изменений  
  
|Обновленное содержимое|  
|---------------------|  
|Добавлены сведения об использовании поставщика OLE DB для Jet при импорте данных с разделителями-запятыми.|  
  
## <a name="see-also"></a>См. также:  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Типы данных (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [Использование символьного формата для импорта и экспорта данных (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)   
 [Использование собственного формата для импорта и экспорта данных (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
  
