---
title: Переходы подключения | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f808460a1421a9ab4cb3a76c2810d810b9636b11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224507"
---
# <a name="connection-transitions"></a>Переходы подключения
Подключения ODBC иметь следующие состояния.  
  
|Штат|Описание|  
|-----------|-----------------|  
|C0|Нераспределенное среды, нераспределенное подключения|  
|C1|Выделенной среды, нераспределенное подключения|  
|C2|Выделенные среды, выделенные подключения|  
|C3|Функция подключения должна данных|  
|C4|Подключенные подключения|  
|C5|Подключенные подключения, выделенной инструкции|  
|C6|Подключенные подключения во время выполнения транзакции. Вполне возможно, для подключения находится в состоянии C6 без операторов, выделенные при соединении. Например предположим, подключение находится в режиме ручной фиксации и находится в состоянии C4. Если инструкция является выделенной, выполняется (запуск транзакции) и этого освобождается, транзакция остается активной, но нет инструкций в соединении.|  
  
 В следующих таблицах показано, как каждая функция ODBC влияет на состояние соединения.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> Нет Env.|Нераспределенное C1|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1 [1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH) [3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH) [4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] в этой строке показаны переходы при *HandleType* был SQL_HANDLE_ENV.  
  
 [2] в этой строке показаны переходы при *HandleType* было установленным в значение sql_handle_stmt.  
  
 [3] в этой строке показаны переходы при *HandleType* был значение SQL_HANDLE_STMT.  
  
 [4] в этой строке показаны переходы при *HandleType* был SQL_HANDLE_DESC.  
  
 [5] вызова **SQLAllocHandle** с *OutputHandlePtr* указывает на допустимый дескриптор перезаписывает этот дескриптор, без учета предыдущих ofthat дескриптор содержимого и может привести к проблемам для драйверов ODBC. Это неправильный программирования приложений ODBC для вызова **SQLAllocHandle** дважды с той же переменной приложения, определенные для  *\*OutputHandlePtr* без вызова  **SQLFreeHandle** для освобождения дескриптора перед ее перераспределения. Перезапись ODBC дескрипторы таким образом, может привести к непредсказуемому поведению или ошибок со стороны драйверы ODBC.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 C3 [d] [s]|--C2 [d] [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5[2]|  
  
 [1] соединение было в режиме ручной фиксации.  
  
 [2] подключение было в режиме автоматической фиксации.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns, SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges и SQLTables  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] подключение находилась в режиме автоматической фиксации или источника данных не удалось начать транзакцию.  
  
 [2] подключение находилась в режиме ручной фиксации и источника данных начала транзакции.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField, SQLGetDescRec, SQLSetDescField и SQLSetDescRec  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] в этом состоянии только дескрипторов, доступных приложению явным образом выделяются дескрипторов.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources и SQLDrivers  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|S C4 - n [f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--[3]|--[3]|--[3]|--|--|--[4] или ([5], [6] и [8]) C4 [5] и [7] C5 [5], [6] и [9]|  
|(IH) [2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] в этой строке показаны переходы при *HandleType* был SQL_HANDLE_ENV.  
  
 [2] в этой строке показаны переходы при *HandleType* было установленным в значение sql_handle_stmt.  
  
 [3], так как подключение не находится в подключенном состоянии, не влияет на транзакцию.  
  
 [4 commit или rollback при подключении не пройдена. Функция возвращает значение SQL_ERROR в данном случае.  
  
 [5 commit или rollback успешно выполнена на подключение. Функция возвращает значение SQL_ERROR, если commit или rollback не удалось выполнить на другое соединение или функция возвращает значение SQL_SUCCESS, если фиксация или откат выполнен успешно для всех соединений.  
  
 [6] была хотя бы один оператор, выделенные при соединении.  
  
 [7] произошли никакие инструкции, выделенные при соединении.  
  
 [8] подключение было по крайней мере одну инструкцию, для которого существует был открытого курсора, и источника данных сохраняет курсоры при транзакции фиксируются или откатываются назад, в зависимости от ситуации (в зависимости от того *CompletionType* был SQL_ ФИКСАЦИЯ или SQL_ROLLBACK). Дополнительные сведения см. в разделе атрибутов SQL_CURSOR_COMMIT_BEHAVIOR и SQL_CURSOR_ROLLBACK_BEHAVIOR [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] Если соединение было все инструкции, для которых были открытые курсоры, курсоры не были сохранены после фиксации или откат транзакции.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect и SQLExecute  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2] C6[3]|--|  
  
 [1] подключение находилась в режиме автоматической фиксации и не было выполненной инструкции *курсор* *спецификации* (например, SELECT); или соединение установлено в режим ручной фиксации и инструкции выполнить не удалось начать транзакцию.  
  
 [2] подключение находилась в режиме автоматической фиксации, а инструкцией, выполненной была *курсор* *спецификации* (например, SELECT).  
  
 [3] подключение находилась в режиме ручной фиксации и источника данных начала транзакции.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|C4 [5], [6]|--C4 [7] [5] и [8] C5 [6] и [8]|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] в этой строке показаны переходы при *HandleType* был SQL_HANDLE_ENV.  
  
 [2] в этой строке показаны переходы при *HandleType* было установленным в значение sql_handle_stmt.  
  
 [3] в этой строке показаны переходы при *HandleType* был значение SQL_HANDLE_STMT.  
  
 [4] в этой строке показаны переходы при *HandleType* был SQL_HANDLE_DESC.  
  
 [5] была только одна инструкция, выделенные при соединении.  
  
 [6] было несколько инструкций, выделенные при соединении.  
  
 [7] соединение было в режиме ручной фиксации.  
  
 [8] соединение было в режиме автоматической фиксации.  
  
## <a name="sqlfreestmt"></a>Функция SQLFreeStmt  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|(IH)|(IH)|(IH)|(IH)|--|C5 [3], [4]|  
|(IH) [2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] Эта строка показывает транзакции при *параметр* аргумент является SQL_CLOSE.  
  
 [2] Эта строка показывает транзакции при *параметр* аргументом является SQL_UNBIND или SQL_RESET_PARAMS.  
  
 [3] подключение находилась в режиме автоматической фиксации, и никакие курсоры были открыты на инструкции, за исключением этого.  
  
 [4] подключение находилась в режиме ручной фиксации, или она находилась в режиме автоматической фиксации и курсор был открыт на хотя бы одну инструкцию.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--|--|--|  
  
 [1] *атрибут* аргумент был SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE или SQL_ATTR_TRACEFILE, или значение было значение для атрибута соединения.  
  
 [2] *атрибут* аргумент не SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE или SQL_ATTR_TRACEFILE, и значение не было задано для подключения атрибут.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>Функция SQLGetDiagField и SQLGetDiagRec  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH) [1]|--|--|--|--|--|--|  
|(IH) [2]|(IH)|--|--|--|--|--|  
|(IH) [3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH) [4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] в этой строке показаны переходы при *HandleType* был SQL_HANDLE_ENV.  
  
 [2] в этой строке показаны переходы при *HandleType* было установленным в значение sql_handle_stmt.  
  
 [3] в этой строке показаны переходы при *HandleType* был значение SQL_HANDLE_STMT.  
  
 [4] в этой строке показаны переходы при *HandleType* был SQL_HANDLE_DESC.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|08003|--|--|--|  
  
 [1] *InfoType* аргумент был SQL_ODBC_VER.  
  
 [2] *InfoType* аргумент не SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--C5 [3] [1]|  
  
 [1] подключение было в режиме автоматической фиксации, а при вызове **SQLMoreResults** обработки результирующего набора курсора спецификации не инициализирован.  
  
 [2] подключение было в режиме автоматической фиксации, а при вызове **SQLMoreResults** инициализации обработки результирующего набора курсора спецификации.  
  
 [3] соединение было в режиме ручной фиксации.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] подключение находилась в режиме автоматической фиксации или источника данных не удалось начать транзакцию.  
  
 [2] подключение находилась в режиме ручной фиксации и источника данных начала транзакции.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--[3] 08002[4] HY011[5]|--[3] 08002[4] HY011[5]|--[3] и [6] C5 [8] [4] HY011 08002 [5] или [7]|  
  
 [1] *атрибут* аргумент не настройки SQL_ATTR_TRANSLATE_LIB или SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] *атрибут* аргумент был настройки SQL_ATTR_TRANSLATE_LIB или SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] *атрибут* аргумент не SQL_ATTR_ODBC_CURSORS или SQL_ATTR_PACKET_SIZE.  
  
 [4] *атрибут* аргумент был SQL_ATTR_ODBC_CURSORS.  
  
 [5] *атрибут* аргумент был SQL_ATTR_PACKET_SIZE.  
  
 [6] *атрибут* аргумент не SQL_ATTR_AUTOCOMMIT, или *атрибут* аргумент был SQL_ATTR_AUTOCOMMIT и установка для данного атрибута не удалось зафиксировать транзакцию.  
  
 [7] *атрибут* аргумент был SQL_ATTR_TXN_ISOLATION.  
  
 [8] *атрибут* аргумент был SQL_ATTR_AUTOCOMMIT, и установка для данного атрибута фиксации транзакции.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Все остальные функции ODBC  
  
|C0<br /><br /> Нет Env.|C1<br /><br /> Не выделено|C2<br /><br /> выделено|C3<br /><br /> Требуются данные|C4<br /><br /> Подключен|C5<br /><br /> .|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
