---
title: SQLStatistics, функция | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4277c6606392c91ffb3de40ace658cd68461f01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536272"
---
# <a name="sqlstatistics-function"></a>SQLStatistics, функция
**Соответствие стандартам**  
 Представленные версии: Соответствие стандартам 1.0 ODBC: ISO-92  
  
 **Сводка**  
 **SQLStatistics** извлекает список статистических данных о одной таблицы и индексы, связанные с таблицей. Драйвер возвращает данные в виде результирующего набора.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>Аргументы  
 *StatementHandle*  
 [Вход] Дескриптор инструкции.  
  
 *CatalogName*  
 [Вход] Имя каталога. Если драйвер поддерживает каталоги для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, пустая строка ("») указывает, эти таблицы, у которых нет каталогов. *CatalogName* не может содержать шаблон поиска строки.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *CatalogName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *CatalogName* обычный аргумент; интерпретируется буквально, а также его регистр имеет значения. Дополнительные сведения см. в разделе [аргументов в функции работы с каталогами](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Вход] Длина в символах **CatalogName*.  
  
 *SchemaName*  
 [Вход] Имя схемы. Если драйвер поддерживает схемы, для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, пустая строка ("») указывает, эти таблицы, у которых нет схемы. *SchemaName* не может содержать шаблон поиска строки.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *SchemaName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *SchemaName* обычный аргумент; интерпретируется буквально, а также его регистр имеет значения.  
  
 *NameLength2*  
 [Вход] Длина в символах **SchemaName*.  
  
 *TableName*  
 [Вход] Имя таблицы. Этот аргумент не может быть пустым указателем. *SchemaName* не может содержать шаблон поиска строки.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *TableName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *TableName* обычный аргумент; интерпретируется буквально, а также его регистр имеет значения.  
  
 *NameLength3*  
 [Вход] Длина в символах **TableName*.  
  
 *Уникальный*  
 [Вход] Тип индекса: SQL_INDEX_UNIQUE или SQL_INDEX_ALL.  
  
 *Reserved*  
 [Вход] Показывает важность количестве ЭЛЕМЕНТОВ и СТРАНИЦАХ столбцов в результирующем наборе. Следующие параметры, влияющие на возвращение количества ЭЛЕМЕНТОВ и СТРАНИЦАХ только столбцы; сведения об индексе возвращается в том случае, даже если количество ЭЛЕМЕНТОВ и СТРАНИЦАХ не возвращаются.  
  
 SQL_ENSURE запросов, что драйвер безусловно получения статистики. (Драйверы, которые соответствуют стандарту Open Group и не поддерживаем расширения ODBC не будет поддерживать SQL_ENSURE.)  
  
 SQL_QUICK запросов, что драйвер получить количество ЭЛЕМЕНТОВ и СТРАНИЦАХ только в том случае, если они доступны с сервера. В этом случае драйвер не гарантирует актуальность значений. (Приложения, написанные в стандарте Open Group будет всегда получают значение SQL_QUICK из ODBC 3 *.x*-совместимые драйверы.)  
  
## <a name="returns"></a>Возвращает  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR, or SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Диагностика  
 Когда **SQLStatistics** возвращает значение SQL_ERROR или SQL_SUCCESS_WITH_INFO, а связанное значение SQLSTATE можно получить, вызвав **SQLGetDiagRec** с *HandleType* из SQL_ HANDLE_STMT и *обрабатывать* из *StatementHandle*. В следующей таблице перечислены значения SQLSTATE, обычно возвращаемые при помощи **SQLStatistics** и объясняется каждый из них в контексте этой функции; описания SQLSTATE, возвращаемых диспетчером драйверов предшествует обозначение «(DM)». Возвращается связанный с каждого значения SQLSTATE значение SQL_ERROR, если не указано иное.  
  
|SQLSTATE|Ошибка|Описание|  
|--------------|-----------|-----------------|  
|01000|Общее предупреждение|Специфические для драйвера информационное сообщение. (Функция возвращает значение SQL_SUCCESS_WITH_INFO).|  
|08S01|Отказ канала связи|Сбой в канале связи между драйвером и источника данных, к которому был подключен драйвер перед обработкой функции было завершено.|  
|24000|Недопустимое состояние курсора|Курсор был открыт на *StatementHandle*, и **SQLFetch** или **SQLFetchScroll** бы вызывалась. Если эта ошибка возвращается диспетчером драйверов **SQLFetch** или **SQLFetchScroll** не вернула значение SQL_NO_DATA и возвращается с помощью драйвера, если **SQLFetch** или **SQLFetchScroll** вернула значение SQL_NO_DATA.<br /><br /> Курсор был открыт на *StatementHandle*, но **SQLFetch** или **SQLFetchScroll** не был вызван.|  
|40001|Сбой сериализации|Выполнен откат транзакции из-за взаимоблокировки ресурсов с другой транзакцией.|  
|40003|Состояние транзакции неизвестно|Не удалось выполнить связанное соединение во время выполнения этой функции и не удается определить состояние транзакции.|  
|HY000|Общая ошибка|Произошла ошибка, для которой было нет конкретных SQLSTATE и SQLSTATE не зависящие от реализации, который был определен. Сообщение об ошибке, возвращенные **SQLGetDiagRec** в  *\*MessageText* буфера описывает ошибку и его причины.|  
|HY001|Ошибка выделения памяти|Драйвер не удалось выделить память, необходимая для поддержки выполнения или завершения функции.|  
|HY008|Операция отменена|Асинхронная обработка была включена для *StatementHandle*. Функция была вызвана, и до его завершения выполнения, **SQLCancel** или **SQLCancelHandle** был вызван для *StatementHandle*, и затем вызова функции еще раз на *StatementHandle*.<br /><br /> Функция была вызвана, и до его завершения выполнения, **SQLCancel** или **SQLCancelHandle** был вызван для *StatementHandle* из другого потока в многопоточные приложения.|  
|HY009|Недопустимое использование пустого указателя|*TableName* аргумент был пустым указателем.<br /><br /> Атрибут инструкции SQL_ATTR_METADATA_ID было установлено значение SQL_TRUE, *CatalogName* аргумент был пустым указателем, а также SQL_CATALOG_NAME *InfoType* возвращает этот каталога имена поддерживаются.<br /><br /> (DM) атрибут инструкции SQL_ATTR_METADATA_ID было установлено значение SQL_TRUE и *SchemaName* аргумент был пустым указателем.|  
|HY010|Ошибка последовательности функций|(DM) был вызван асинхронно выполняемой функции для дескриптора соединения, связанный с *StatementHandle*. Если по-прежнему выполнении асинхронной функции **SQLStatistics** была вызвана функция.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, или **SQLMoreResults** был вызван для *StatementHandle* и возвращается SQL_PARAM_DATA_ ДОСТУПНО. Прежде чем данные были получены для всех параметров потоковой вызове этой функции.<br /><br /> (DM) асинхронно выполняемой функции (не такой) был вызван для *StatementHandle* и еще выполнялась при вызове этой функции.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, или **SQLSetPos** был вызван для  *StatementHandle* и возвращается значение SQL_NEED_DATA. Эта функция был вызван перед отправкой данных для всех параметров данных времени выполнения или столбцов.|  
|HY013|Ошибка управления памятью|Не удалось обработать вызов функции, так как базовые объекты памяти оказываются недоступны, возможно из-за нехватки памяти.|  
|HY090|Недопустимая длина строки или буфера|(DM) значение одного из аргументов длина имени меньше 0, но не равно SQL_NTS.<br /><br /> Значение одного из аргументов длина имени превышает значение максимальной длины для соответствующего имени.|  
|HY100|Тип параметра Uniqueness за пределами диапазона|(DM) указан недопустимый *Unique* было указано значение.|  
|HY101|Тип параметра accuracy за пределами диапазона|(DM) указан недопустимый *зарезервированный* было указано значение.|  
|HY117|Подключение будет приостановлена из-за состояние транзакции неизвестно. Только отключиться и разрешены функции, доступные только для чтения.|(DM) Дополнительные сведения о состоянии приостановки, см. в разделе [функция SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Дополнительная возможность не реализована|Был указан каталог, а драйверу или источнику данных не поддерживает каталоги.<br /><br /> Указано схему и драйверу или источнику данных не поддерживает схемы.<br /><br /> Сочетание текущие значения атрибутов инструкции SQL_ATTR_CONCURRENCY и SQL_ATTR_CURSOR_TYPE не поддерживается драйвером или источником данных.<br /><br /> Атрибут инструкции SQL_ATTR_USE_BOOKMARKS было присвоено SQL_UB_VARIABLE и атрибут инструкции SQL_ATTR_CURSOR_TYPE было присвоено тип курсора, для которого драйвер не поддерживает закладки.|  
|HYT00|Время ожидания истекло|Истекло время ожидания запроса перед источника данных, возвращаемого набора требуемого результата. Период ожидания задается с помощью **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Время ожидания подключения истекло|Время ожидания подключения истекло раньше, чем ответил на запрос источника данных. Период времени ожидания задается с помощью **SQLSetConnectAttr**, sql_attr_connection_timeout не учитывается.|  
|IM001|Драйвер не поддерживает эту функцию|Драйвер (DM), связанные с *StatementHandle* не поддерживает функцию.|  
|IM017|Опрос недоступен в режиме асинхронное уведомление|Каждый раз, когда используется модель уведомлений, отключен опроса.|  
|IM018|**SQLCompleteAsync** не был вызван для завершения предыдущей асинхронной операции на этот дескриптор.|Если предыдущий вызов функции в дескриптор возвращает SQL_STILL_EXECUTING, и если включен режим уведомлений, **SQLCompleteAsync** должен вызываться с дескриптором постобработки и завершить операцию.|  
  
## <a name="comments"></a>Комментарии  
 **SQLStatistics** возвращает сведения об одной таблицы, как стандартный результирующий набор, упорядоченный по NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME и ТИПА ORDINAL_POSITION. Результирующий набор объединяет статистические данные (в количестве ЭЛЕМЕНТОВ и СТРАНИЦАХ столбцы результирующего набора) для таблицы с информацией о каждом индексе. Сведения о том, как эта информация может использоваться, см. в разделе [использует данные из каталога](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Чтобы определить фактический длин столбцов TABLE_CAT, по значениям TABLE_SCHEM, TABLE_NAME и COLUMN_NAME, приложение может вызвать **SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN, и SQL_MAX_COLUMN_NAME_LEN параметры.  
  
> [!NOTE]  
>  Дополнительные сведения о общего использования, аргументы и возвращаемые данные функций каталога ODBC, см. в разделе [функций каталога](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Следующие столбцы были переименованы для ODBC 3 *.x*. Изменения имен столбцов не влияют на обратную совместимость так, как выполнить привязку приложения, номер столбца.  
  
|Столбец ODBC 2.0|ODBC 3 *.x* столбца|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 В следующей таблице перечислены столбцы в результирующем наборе. Дополнительные столбцы вслед за столбца 13 (условие_фильтрации) можно определить с помощью драйвера. Приложение должно получить доступ к от драйвера, отсчет от конца результирующего набора вместо указания явной порядковый. Дополнительные сведения см. в разделе [данные, возвращаемые функциями каталога](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Имя столбца|Номер столбца|Тип данных|Комментарии|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Имя каталога таблицы, к которому применяется статистики или индекс; Значение NULL, если не применим к источнику данных. Если драйвер поддерживает каталоги для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, возвращается пустая строка ("») для этих таблиц, у которых нет каталогов.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Имя схемы таблицы, к которому применяется статистики или индекс; Значение NULL, если не применим к источнику данных. Если драйвер поддерживает схемы для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, возвращается пустая строка ("») для этих таблиц, у которых нет схемы.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|Имя таблицы, таблицы, к которому применяется статистики или индекса.|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|Указывает, является ли индекс не допускает повторяющиеся значения:<br /><br /> SQL_TRUE, если значения индекса может быть неуникальным.<br /><br /> Значение SQL_FALSE, если значение индекса должно быть уникальным.<br /><br /> Если тип является SQL_TABLE_STAT, возвращается значение NULL.|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|Идентификатор, который используется для определения индекса назовите это **DROP INDEX**; Если квалификатор индекса не поддерживается источником данных, или если тип является SQL_TABLE_STAT, возвращается значение NULL. Если в этом столбце возвращается значение отличное от null, он должен использоваться для указания имени индекса на **DROP INDEX** оператор; в противном случае по значениям TABLE_SCHEM должен использоваться для указания имени индекса.|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|Имя индекса; Если тип является SQL_TABLE_STAT, возвращается значение NULL.|  
|ТИП (ODBC 1.0)|7|Smallint, не NULL|Тип возвращаемых данных:<br /><br /> SQL_TABLE_STAT указывает статистику для таблицы (в столбце количества ЭЛЕМЕНТОВ или СТРАНИЦАХ).<br /><br /> SQL_INDEX_BTREE указывает индекс сбалансированного дерева.<br /><br /> SQL_INDEX_CLUSTERED указывает кластеризованного индекса.<br /><br /> SQL_INDEX_CONTENT указывает индекс содержимого.<br /><br /> SQL_INDEX_HASHED указывает хэшированное индекса.<br /><br /> SQL_INDEX_OTHER указывает другой тип индекса.|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|Порядковый номер столбца в индексе (начиная с 1); Если тип является SQL_TABLE_STAT, возвращается значение NULL.|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|Имя столбца. Если столбец основан на выражении, например Зарплата + ПРЕИМУЩЕСТВА, возвращается выражение; Если выражение не может быть определен, возвращается пустая строка. Если тип является SQL_TABLE_STAT, возвращается значение NULL.|  
|ASC_OR_DESC (ODBC 1.0)|10|char(1)|Последовательность сортировки для столбца: «» Для по возрастанию; «D», по убыванию; Если порядок сортировки столбцов не поддерживается источником данных, или если тип является SQL_TABLE_STAT, возвращается значение NULL.|  
|КОЛИЧЕСТВО ЭЛЕМЕНТОВ (ODBC 1.0)|11|Целочисленный|Количество элементов таблицы или индекса; количество строк в таблице, если тип является SQL_TABLE_STAT; количество уникальных значений в индексе, если тип не является SQL_TABLE_STAT; Если значение источника данных недоступен, возвращается значение NULL.|  
|СТРАНИЦЫ (ODBC 1.0)|12|Целочисленный|Число страниц, используемый для хранения индекса или таблицы. количество страниц для таблицы, если тип является SQL_TABLE_STAT; количество страниц индекса, если тип не является SQL_TABLE_STAT; Если значение источника данных недоступен или не применим к источнику данных, возвращается значение NULL.|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|Если индекс является отфильтрованным, это условие фильтра, например Зарплата > 30000; Если не удается определить условие фильтра, это пустая строка.<br /><br /> Значение NULL, если индекс не является отфильтрованный индекс, не удается определить, является ли индекс отфильтрованный индекс, или тип — SQL_TABLE_STAT.|  
  
 Если строки в результирующем наборе соответствует таблице, драйвер устанавливает тип в SQL_TABLE_STAT и NON_UNIQUE, INDEX_QUALIFIER, INDEX_NAME, ORDINAL_POSITION, COLUMN_NAME и ASC_OR_DESC присваивается значение NULL. Если количество ЭЛЕМЕНТОВ или страницы не доступны из источника данных, драйвер устанавливает их в значение NULL.  
  
## <a name="code-example"></a>Пример кода  
 Пример кода ту же функцию, см. в разделе [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Связанные функции  
  
|Сведения о|См.|  
|---------------------------|---------|  
|Привязка к столбцу в результирующем наборе буфер|[Функция SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Отмена обработка инструкций|[Функция SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Выборка одной строки или блока данных в направлении только вперед.|[Функция SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Блока данных или прокрутке результирующего набора|[Функция SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Возврат столбцов внешних ключей|[Функция SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|Возврат столбцов первичного ключа|[Функция SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>См. также  
 [Справочник по API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Файлы заголовков ODBC](../../../odbc/reference/install/odbc-header-files.md)
