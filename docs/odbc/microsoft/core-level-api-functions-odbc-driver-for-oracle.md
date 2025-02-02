---
title: Основные функции уровня API (драйвер ODBC для Oracle) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2e77ffd4fe892bc2f3d9a944c79d6b702d5e671
ms.sourcegitcommit: 36c5f28d9fc8d2ddd02deb237937c9968d971926
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354587"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Функции API основного уровня (драйвер ODBC для Oracle)
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Вместо этого используйте драйвер ODBC, предоставляемого корпорацией Oracle.  
  
 Функции на этом уровне включают минимальный уровень соответствия интерфейс для драйверов ODBC.  
  
|API-функция|Примечания|  
|------------------|-----------|  
|**SQLAllocConnect**|Выделяет память для дескриптора соединения, *hdbc*, в среду, определяемую по *henv*. Диспетчер драйверов обрабатывает этот вызов и вызывает драйвер **SQLAllocConnect** каждый раз, когда функция **SQLConnect**, **SQLBrowseConnect**, или  **SQLDriverConnect** вызывается.|  
|**SQLAllocEnv**|Отображает диалоговое окно, указав требование для клиентского программного обеспечения Oracle, а затем возвращает значение SQL_NULL_HANDLE. Если клиентское по Oracle не установлен, эта функция выделяет память для дескриптора среды, *henv*и инициализирует интерфейс уровня вызова ODBC для использования приложением.|  
|**SQLAllocStmt**|Выделяет память для дескриптора инструкции и связывает дескриптора инструкции с подключением, определяемое hdbc. Диспетчер драйверов передает этот вызов к драйверу, который выделяет память для структуры hstmt.|  
|**SQLBindCol**|Назначает дискового пространства для столбца результатов и указывает тип результата.|  
|**SQLCancel**|Отменяет обработку на дескриптор инструкции, hstmt. В некоторых случаях Oracle не поддерживает отмену выполнения инструкции. Это означает, что выполнение инструкции будут выполняться до Oracle завершает процесс, после чего результаты инструкций отменяются драйвером ODBC для Oracle.|  
|**SQLColAttributes**|Возвращает данные дескриптора для столбца в результирующем наборе. Сведения о дескрипторе возвращается как символьная строка, значение дескриптора зависит от 32-разрядной или целочисленное значение.|  
|**SQLConnect**|Подключается к источнику данных. Чтобы использовать проверку подлинности операционной системы Oracle, укажите «/» как *szUID* параметр и «» как *szAuthStr* параметра.|  
|**SQLDescribeCol**|Возвращает имя, тип, точность, масштаб и допустимость значений NULL столбца данного результата. **Примечание.  SQLDescribeCol** сообщает вычисляемые столбцы в виде SQL_VARCHAR.|  
|**SQLDisconnect**|Закрывает соединение. Если включено использование пулов соединений для совместно используемой среде, и приложение вызывает **SQLDisconnect** для подключения в этой среде, соединение возвращается в пул подключений и по-прежнему доступен для других компонентов, с помощью одной общей среде.|  
|**SQLError**|Возвращает сведения об ошибках и состоянии о последней ошибке. Драйвер поддерживает стека или список ошибок, которые могут быть возвращены для *hstmt*, *hdbc*, и *henv* аргументами, в зависимости от того, как вызов **SQLError**  выполняется. В очередь ошибок очищается после каждой инструкции. Обычно получает сообщение об ошибке Oracle, а в противном случае будет пустым.|  
|**SQLExecDirect**|Выполняет инструкцию SQL новый, неподготовленных. Драйвер использует текущие значения переменных маркера параметра, если существует любые параметры в инструкции. Если на таблицу, представление или имена полей содержат пробелы, заключите имя назад кавычка метки. Например, если база данных содержит таблицу с именем *My Table* и поле *Мое поле*, заключите каждый элемент идентификатора следующим образом:<br /><br /> ВЫБЕРИТЕ \`таблицы\`. \`Мои Field1\`, \`Таблицы\`.\` Мои Field2\` FROM \`таблицы\`|  
|**SQLExecute**|Выполняет подготовленную инструкцию SQL (инструкцию, уже созданные **SQLPrepare**). Драйвер использует текущие значения переменных маркера параметра, если существует любые параметры в инструкции.|  
|**SQLFetch**|Получает одну строку из результирующего набора в расположениях, указанных предыдущие обращения для **SQLBindCol**. Подготавливает драйвер для вызова **SQLGetData** для несвязанных столбцов.|  
|**SQLFreeConnect**|Освобождает дескриптор соединения и освобождает всей памяти, выделенной для дескриптора.|  
|**SQLFreeEnv**|Драйвер ODBC для Oracle закрывает и освобождает всю память, связанные с драйвером.|  
|**SQLFreeStmt**|Останавливает обработку, связанные с определенной hstmt, закрывает все открытые курсоры, связанные с hstmt, отменяет ожидающие результаты и при необходимости освобождает все ресурсы, связанные с дескриптором инструкции.|  
|**SQLGetCursorName**|Возвращает имя курсора, связанный с данной hstmt.|  
|**SQLNumResultCols**|Возвращает количество столбцов в курсор результирующего набора.|  
|**SQLPrepare**|Подготавливает инструкцию SQL, Планирование способов оптимизации и выполните инструкцию. Инструкция SQL компилируется для исполнения **SQLExecDirect**.<br /><br /> Если на таблицу, представление или имена полей содержат пробелы, заключите имя назад кавычка метки. Например, если база данных содержит таблицу с именем *My Table* и поле *Мое поле*, заключите каждый элемент идентификатора следующим образом:<br /><br /> ВЫБЕРИТЕ \`таблицы\`.\` Мое поле\` FROM \`таблицы\`<br /><br /> Сведения об использовании результирующих наборов, содержащий массивов в качестве формальных параметров, см. в разделе [возврат параметров массива из хранимых процедур](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle не предоставляет способ определить количество строк в результирующем наборе, пока после извлечения последней строки, поэтому он возвращает значение -1.|  
|**SQLSetCursorName**|Связывает имя курсора с дескриптором активный оператор, *hstmt*.|  
|**SQLSetParam**|Заменить SQLBindParameter в ODBC 2. *x*.|  
|**SQLTransact**|Запрашивает операцию commit или rollback для всех активных операций на все дескрипторы инструкций (hstmts), ассоциированные с соединением, или для всех подключений, связанных с дескриптором среды, *henv*. Если фиксация завершается неудачей, если в ручном режиме, транзакция остается активным; Вы можете выполнить откат транзакции или повторите операцию фиксации. При сбое операции фиксации в режиме автоматической транзакции, транзакция откатывается автоматически. транзакция не может быть неактивной.|
