---
title: Метаданные каталога | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- metadata [ODBC]
- catalog metadata [ODBC]
ms.assetid: b82665be-8cb1-4ad3-ac15-2e590bdc1815
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2784b7915d96665cae814e0dff46b2f2135bc52
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62511528"
---
# <a name="catalog-metadata"></a>Метаданные каталога
  В этом разделе описаны метаданные столбцов, возвращаемые функциями `SQLColumns` и `SQLProcedureColumns`, а также метаданные для типов данных, возвращаемые функцией `SQLGetTypeInfo`.  
  
## <a name="remarks"></a>Примечания  
 Функции `SQLColumns` и `SQLProcedureColumns` возвращают следующие значения столбцов для типов данных даты-времени.  
  
|Тип параметра|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|6|10|16|16|16|20|  
|DECIMAL_DIGITS|0|0..7|0|3|1..7|1..7|  
|SQL_DATA_TYPE|SQL_DATETIME|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TYPE_TIMESTAMPOFFSET|  
|SQL_DATETIME_SUB|SQL_CODE_DATE|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|  
|CHAR_OCTET_LENGTH|NULL|NULL|NULL|NULL|NULL|NULL|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
  
 Функция `SQLGetTypeInfo` возвращает следующие значения столбцов для типов данных даты-времени.  
  
|Тип параметра|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|масштаб|NULL|NULL|масштаб|масштаб|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULL|NULL|NULL|NULL|NULL|NULL|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|0|0|0|3|0|0|  
|MAXIMUM_SCALE|0|7|0|3|7|7|  
|SQL_DATA_TYPE|SQL_DATETIME|SQL_SS_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TYPE_TIMESTAMPOFFSET|  
|SQL_DATETIME_SUB|SQL_CODE_DATE|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|  
|NUM_PREC_RADIX|NULL|NULL|NULL|NULL|NULL|NULL|  
|INTERVAL_PRECISION|NULL|NULL|NULL|NULL|NULL|NULL|  
|USERTYPE|0|0|12|22|0|0|  
  
## <a name="see-also"></a>См. также  
 [Метаданные &#40;ODBC&#41;](../../database-engine/dev-guide/metadata-odbc.md)  
  
  
