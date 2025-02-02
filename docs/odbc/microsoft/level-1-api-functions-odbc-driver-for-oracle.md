---
title: Функции API уровня 1 (драйвер ODBC для Oracle) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a70116fb0e8ef1236b18cb478184e96fe08fce5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262232"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Функции API уровня 1 (драйвер ODBC для Oracle)
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Вместо этого используйте драйвер ODBC, предоставляемого корпорацией Oracle.  
  
 Поддерживает функции на этом уровне обеспечивают соответствие основного интерфейса, а также дополнительные функции, такие как транзакции.  
  
|API-функция|Примечания|  
|------------------|-----------|  
|**SQLColumns**|Создает результирующий набор для таблицы, которую представляет собой список столбцов для указанной таблицы или таблиц. При запросе столбцов для ОТКРЫТОГО синонима, необходимо задать атрибут соединения SYNONYMCOLUMNS и указан пустую строку в качестве *szTableOwner* аргумент. При возвращении столбцов для ОБЩИХ синонимов, драйвер устанавливает значение столбца ИМЕНИ таблицы на пустую строку. Результирующий набор содержит дополнительный столбец, порядковый номер ПОЗИЦИИ, в конце каждой строки. Это значение является порядковый номер столбца в таблице.|  
|**SQLDriverConnect**|Подключается к источнику данных. Дополнительные сведения см. в разделе [формат строки подключения и атрибуты](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**SQLGetConnectOption**|Возвращает текущее значение параметра соединения. Эта функция поддерживается частично. Драйвер поддерживает все значения для *fOption* аргумент, но не поддерживает некоторые *vParam* значений в параметре *fOption* аргумент [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Дополнительные сведения см. в разделе [параметров подключения](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Получает значение из одного поля в текущей записи данного результирующего набора.|  
|**SQLGetFunctions**|Возвращает значение TRUE для всех поддерживаемых функций. Реализован диспетчером драйверов.|  
|**SQLGetInfo**|Возвращает сведения, включая SQLHDBC, SQLUSMALLINT, указатель SQLPOINTER, SQLSMALLINT и SQLSMALLINT \*, о драйвере ODBC для Oracle и источника данных связан дескриптор соединения *hdbc*.|  
|**SQLGetStmtOption**|Возвращает текущее значение параметра инструкции. Дополнительные сведения см. в разделе [параметров инструкции](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Возвращает сведения о типах данных, поддерживаемых источником данных. Драйвер возвращает сведения в результирующем наборе SQL.|  
|**SQLParamData**|Используется в сочетании с **SQLPutData** для указания параметра данных во время выполнения инструкции.|  
|**SQLPutData**|Позволяет приложению отправлять данные для параметра или столбца к драйверу во время выполнения инструкции.|  
|**SQLSetConnectOption**|Предоставляет доступ к параметрам, которые управляют аспектах соединения. Эта функция поддерживается частично: Драйвер поддерживает все значения для *fOption* аргумент, но не поддерживает некоторые *vParam* значений в параметре *fOption* аргумент [SQL_TXN_ISOLATION ](../../odbc/microsoft/connect-options.md). Дополнительные сведения см. в разделе [параметров подключения](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOption**|Задает параметры, связанные с дескриптор инструкции *hstmt*. Дополнительные сведения см. в разделе [параметров инструкции](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Возвращает оптимальный набор столбцов, уникально определяющий строку в таблице.|  
|**SQLStatistics**|Извлекает список статистику о одной таблицы и индексы или имена тегов, связанные с таблицей. Драйвер возвращает данные в виде результирующего набора.|  
|**SQLTables**|Возвращает список имен таблиц, указанного в параметре в **SQLTables** инструкции. Если параметр не указан, возвращает имена таблиц, хранимых в текущем источнике данных. Драйвер возвращает данные в виде результирующего набора.<br /><br /> Перечисления типа вызывает метод не получит запись результирующего набора для представления удаленного или локального параметризованных представлений. Тем не менее вызов **SQLTables** с уникальной таблицы спецификатор имени будет найти совпадения для такого представления, если он имеется, с таким же именем; благодаря этому API для проверки конфликтов имени до создания новой таблицы.<br /><br /> ОТКРЫТЫЙ синонимы возвращаются со значением TABLE_OWNER «».<br /><br /> ПРЕДСТАВЛЕНИЯ, принадлежащие SYS или системы, определяются как СИСТЕМНОЕ ПРЕДСТАВЛЕНИЕ.|
