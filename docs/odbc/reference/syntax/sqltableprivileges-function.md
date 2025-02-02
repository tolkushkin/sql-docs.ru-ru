---
title: Функция SQLTablePrivileges | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTablePrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTablePrivileges
helpviewer_keywords:
- SQLTablePrivileges function [ODBC]
ms.assetid: 8cfdb64f-64c5-47e6-ad57-0533ac630afa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81659ae2cab2343a7fcf03327cbdc89c0db6c8c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536307"
---
# <a name="sqltableprivileges-function"></a>Функция SQLTablePrivileges
**Соответствие стандартам**  
 Представленные версии: Соответствие стандартам 1.0 ODBC: интерфейс ODBC  
  
 **Сводка**  
 **SQLTablePrivileges** возвращает список таблиц и права, связанные с каждой таблицей. Драйвер возвращает сведения, на указанной инструкции в виде результирующего набора.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
  
SQLRETURN SQLTablePrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3);  
```  
  
## <a name="arguments"></a>Аргументы  
 *StatementHandle*  
 [Вход] Дескриптор инструкции.  
  
 *CatalogName*  
 [Вход] Каталог таблицы. Если драйвер поддерживает каталоги для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, пустая строка ("») обозначает этих таблиц, у которых нет каталогов. *CatalogName* не может содержать шаблон поиска строки.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *CatalogName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *CatalogName* обычный аргумент; интерпретируется буквально, а также его регистр имеет значения. Дополнительные сведения см. в разделе [аргументов в функции работы с каталогами](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Вход] Длина в символах **CatalogName*.  
  
 *SchemaName*  
 [Вход] Строка шаблона поиска для имен схемы. Если драйвер поддерживает схемы, для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, пустая строка ("») обозначает этих таблиц, у которых нет схемы.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *SchemaName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *SchemaName* — это аргумент значения шаблона; интерпретируется буквально, а также его регистр имеет значения.  
  
 *NameLength2*  
 [Вход] Длина в символах **SchemaName*.  
  
 *TableName*  
 [Вход] Строка, шаблон поиска для имен таблиц.  
  
 Если атрибут инструкции SQL_ATTR_METADATA_ID имеет значение SQL_TRUE, *TableName* рассматривается как идентификатор и его регистр не имеет значения. Если это значение SQL_FALSE, *TableName* — это аргумент значения шаблона; интерпретируется буквально, а также его регистр имеет значения.  
  
 *NameLength3*  
 [Вход] Длина в символах **TableName*.  
  
## <a name="returns"></a>Возвращает  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR, or SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Диагностика  
 Когда **SQLTablePrivileges** возвращает значение SQL_ERROR или SQL_SUCCESS_WITH_INFO, а связанное значение SQLSTATE может быть получен путем вызова **SQLGetDiagRec** с *HandleType* значение SQL_HANDLE_STMT и *обрабатывать* из *StatementHandle*. В следующей таблице перечислены значения SQLSTATE, обычно возвращаемые **SQLTablePrivileges** и объясняется каждый из них в контексте этой функции; описания SQLSTATE, возвращаемых диспетчером драйверов предшествует обозначение «(DM)» . Возвращается связанный с каждого значения SQLSTATE значение SQL_ERROR, если не указано иное.  
  
|SQLSTATE|Ошибка|Описание|  
|--------------|-----------|-----------------|  
|01000|Общее предупреждение|Специфические для драйвера информационное сообщение. (Функция возвращает значение SQL_SUCCESS_WITH_INFO).|  
|08S01|Отказ канала связи|Сбой в канале связи между драйвером и источника данных, к которому был подключен драйвер перед обработкой функции было завершено.|  
|24000|Недопустимое состояние курсора|Курсор был открыт на *StatementHandle*, и **SQLFetch** или **SQLFetchScroll** бы вызывалась. Если эта ошибка возвращается диспетчером драйверов **SQLFetch** или **SQLFetchScroll** не вернула значение SQL_NO_DATA и возвращается с помощью драйвера, если **SQLFetch** или **SQLFetchScroll** вернула значение SQL_NO_DATA.<br /><br /> Курсор был открыт на *StatementHandle*, но **SQLFetch** или **SQLFetchScroll** не был вызван.|  
|40001|Сбой сериализации|Выполнен откат транзакции из-за взаимоблокировки ресурсов с другой транзакцией.|  
|40003|Состояние транзакции неизвестно|Не удалось выполнить связанное соединение во время выполнения этой функции и не удается определить состояние транзакции.|  
|HY000|Общая ошибка|Произошла ошибка, для которой было нет конкретных SQLSTATE и SQLSTATE не зависящие от реализации, который был определен. Сообщение об ошибке, возвращенные **SQLGetDiagRec** в  *\*MessageText* буфера описывает ошибку и его причины.|  
|HY001|Ошибка выделения памяти|Драйвер не удалось выделить память, необходимую для поддержки выполнения или завершения функции.|  
|HY008|Операция отменена|Асинхронная обработка была включена для *StatementHandle*. **SQLTablePrivileges** была вызвана функция, и до его завершения выполнения, **SQLCancel** или **SQLCancelHandle** был вызван для  *StatementHandle*. Затем **SQLTablePrivileges** функция была вызвана снова на *StatementHandle*.<br /><br /> **SQLTablePrivileges** была вызвана функция, и до его завершения выполнения, **SQLCancel** или **SQLCancelHandle** был вызван для  *StatementHandle* из другого потока в многопоточных приложениях.|  
|HY009|Недопустимое использование пустого указателя|Атрибут инструкции SQL_ATTR_METADATA_ID было установлено значение SQL_TRUE, *CatalogName* аргумент был пустым указателем, а также SQL_CATALOG_NAME *InfoType* возвращает этот каталога имена поддерживаются.<br /><br /> (DM) атрибут инструкции SQL_ATTR_METADATA_ID было установлено значение SQL_TRUE и *SchemaName* или *TableName* аргумент был пустым указателем.|  
|HY010|Ошибка последовательности функций|(DM) был вызван асинхронно выполняемой функции для дескриптора соединения, связанный с *StatementHandle*. Если по-прежнему выполнении асинхронной функции **SQLTablePrivileges** была вызвана функция.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, или **SQLMoreResults** был вызван для *StatementHandle* и возвращается SQL_PARAM_DATA_ ДОСТУПНО. Прежде чем данные были получены для всех параметров потоковой вызове этой функции.<br /><br /> (DM) асинхронно выполняемой функции (не такой) был вызван для *StatementHandle* и еще выполнялась при вызове этой функции.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, или **SQLSetPos** был вызван для  *StatementHandle* и возвращается значение SQL_NEED_DATA. Эта функция был вызван перед отправкой данных для всех параметров данных времени выполнения или столбцов.|  
|HY013|Ошибка управления памятью|Не удалось обработать вызов функции, так как базовые объекты памяти оказываются недоступны, возможно из-за нехватки памяти.|  
|HY090|Недопустимая длина строки или буфера|(DM) значение одного из аргументов длина имени меньше 0, но не равно SQL_NTS.<br /><br /> Значение одного из аргументов длина имени превышает значение максимальной длины для соответствующих квалификатор или имени.|  
|HY117|Подключение будет приостановлена из-за состояние транзакции неизвестно. Только отключиться и разрешены функции, доступные только для чтения.|(DM) Дополнительные сведения о приостановленном состоянии, см. в разделе [функция SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Дополнительная возможность не реализована|Был указан каталог, а драйверу или источнику данных не поддерживает каталоги.<br /><br /> Указано схему и драйверу или источнику данных не поддерживает схемы.<br /><br /> Для схемы таблицы, имя таблицы или имени столбца указан шаблон поиска строки, а источник данных не поддерживает шаблоны поиска для одного или нескольких из этих аргументов.<br /><br /> Сочетание текущие значения атрибутов инструкции SQL_ATTR_CONCURRENCY и SQL_ATTR_CURSOR_TYPE не поддерживается драйвером или источником данных.<br /><br /> Атрибут инструкции SQL_ATTR_USE_BOOKMARKS было присвоено SQL_UB_VARIABLE и атрибут инструкции SQL_ATTR_CURSOR_TYPE было присвоено тип курсора, для которого драйвер не поддерживает закладки.|  
|HYT00|Время ожидания истекло|Время ожидания запроса истекло раньше, чем источник данных вернул результирующий набор. Период ожидания задается с помощью **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Время ожидания подключения истекло|Время ожидания подключения истекло раньше, чем ответил на запрос источника данных. Период времени ожидания задается с помощью **SQLSetConnectAttr**, sql_attr_connection_timeout не учитывается.|  
|IM001|Драйвер не поддерживает эту функцию|Драйвер (DM), связанные с *StatementHandle* не поддерживает функцию.|  
|IM017|Опрос недоступен в режиме асинхронное уведомление|Каждый раз, когда используется модель уведомлений, отключен опроса.|  
|IM018|**SQLCompleteAsync** не был вызван для завершения предыдущей асинхронной операции на этот дескриптор.|Если предыдущий вызов функции в дескриптор возвращает SQL_STILL_EXECUTING, и если включен режим уведомлений, **SQLCompleteAsync** должен вызываться с дескриптором постобработки и завершить операцию.|  
  
## <a name="comments"></a>Комментарии  
 *SchemaName* и *TableName* аргументы принимают шаблонов поиска. Дополнительные сведения о шаблонах допустимым поиска см. в разделе [аргументы значения шаблона](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 **SQLTablePrivileges** возвращает результаты в виде стандартных результирующий набор, упорядоченный по TABLE_CAT, по значениям TABLE_SCHEM, TABLE_NAME, прав и у УЧАСТНИКА.  
  
 Чтобы определить фактический длин столбцов TABLE_CAT, по значениям TABLE_SCHEM и TABLE_NAME, приложение может вызвать **SQLGetInfo** с параметрами SQL_MAX_CATALOG_NAME_LEN SQL_MAX_SCHEMA_NAME_LEN и SQL_MAX_TABLE_NAME_LEN.  
  
> [!NOTE]  
>  Дополнительные сведения о общего использования, аргументы и возвращаемые данные функций каталога ODBC, см. в разделе [функций каталога](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Следующие столбцы были переименованы для ODBC 3 *.x*. Изменения имен столбцов не влияют на обратную совместимость так, как выполнить привязку приложения, номер столбца.  
  
|Столбец ODBC 2.0|ODBC 3 *.x* столбца|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 В следующей таблице перечислены столбцы в результирующем наборе. Дополнительные столбцы вслед за столбец 7 (IS_GRANTABLE) можно определить с помощью драйвера. Приложения должны получить доступ к от драйвера, отсчет от конца результирующего набора, вместо указания явной порядковый номер. Дополнительные сведения см. в разделе [данные, возвращаемые функциями каталога](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Имя столбца|Номер столбца|Тип данных|Комментарии|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Имя каталога; Значение NULL, если не применим к источнику данных. Если драйвер поддерживает каталоги для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, возвращается пустая строка ("») для этих таблиц, у которых нет каталогов.|  
|TABLE_SCHEM  (ODBC 1.0)|2|Varchar|Имя схемы; Значение NULL, если не применим к источнику данных. Если драйвер поддерживает схемы для некоторых таблиц, но не для других пользователей, например, когда драйвер извлекает данные из разных СУБД, возвращается пустая строка ("») для этих таблиц, у которых нет схемы.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar not NULL|Имя таблицы.|  
|ОБЪЕКТ, ПРЕДОСТАВЛЯЮЩИЙ РАЗРЕШЕНИЕ (ODBC 1.0)|4|Varchar|Имя пользователя, который предоставил права; Значение NULL, если не применим к источнику данных.<br /><br /> Для всех строк, в которых значение в столбце участника, КОТОРОМУ владелец объекта столбец GRANTOR будет «_SYSTEM».|  
|УЧАСТНИК (ODBC 1.0)|5|Varchar not NULL|Имя пользователя, которому предоставлено право доступа.|  
|ПРАВ ДОСТУПА (ODBC 1.0)|6|Varchar not NULL|Права доступа к таблице. Может быть одним из следующих или привилегии зависящие от источника данных.<br /><br /> ВЫБЕРИТЕ: Получатель прав может получить данные для одного или нескольких столбцов таблицы.<br /><br /> ВСТАВЬТЕ: Получатель прав может вставлять новые строки, содержащий данные для одного или нескольких столбцов в таблицу.<br /><br /> ОБНОВЛЕНИЕ: Получатель прав может обновлять данные в один или несколько столбцов таблицы.<br /><br /> УДАЛЕНИЕ: Получатель прав может удалить строки данных из таблицы.<br /><br /> ССЫЛКИ: Участник может ссылаться на один или несколько столбцов таблицы в пределах ограничение (например, уникальный, данных, или проверочное ограничение таблицы).<br /><br /> Область действий, допускаемой участнику права доступа к заданной таблице — зависит от источника данных. Например права доступа UPDATE могут разрешить пользователю grantee обновлять все столбцы в таблице на один источник данных и только те столбцы, для которых пользователь grantor имеет права доступа UPDATE с другим источником данных.|  
|IS_GRANTABLE (ODBC 1.0)|7|Varchar|Указывает, разрешено ли участнику предоставлять права другим пользователям; «YES», «Нет», или значение NULL, если неизвестно или неприменимо к источнику данных.<br /><br /> Привилегия является предоставляемым либо не предоставляемых, но не оба. Результирующий набор, возвращаемый **SQLColumnPrivileges** никогда не будет содержать две строки, для которых все столбцы, кроме столбца IS_GRANTABLE содержат одинаковое значение.|  
  
## <a name="code-example"></a>Пример кода  
 Пример кода ту же функцию, см. в разделе [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Связанные функции  
  
|Сведения о|См.|  
|---------------------------|---------|  
|Привязка к столбцу в результирующем наборе буфер|[Функция SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Отмена обработка инструкций|[Функция SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Возвращает привилегии для столбца или столбцов|[Функция SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Возврат столбцов в таблице или таблицах|[Функция SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Выборка одной строки или блока данных в направлении только вперед|[Функция SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Блока данных или прокрутке результирующего набора|[Функция SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Возврат статистики таблиц и индексов|[Функция SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Возвращает список таблиц в источнике данных|[Функция SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>См. также  
 [Справочник по API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Файлы заголовков ODBC](../../../odbc/reference/install/odbc-header-files.md)
