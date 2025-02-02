---
title: 'C в SQL: Символ | Документация Майкрософт'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0158da62ed360e926cdb5382b89b1491c0723550
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201627"
---
# <a name="c-to-sql-character"></a>C в SQL: Символ
Идентификаторы для символов типа данных ODBC C следующие:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 Следующая таблица показывает ODBC SQL типы данных, к которым могут преобразовываться C символьные данные. Описание столбцов и условия в таблице, см. в разделе [преобразование данных из C в типы данных SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
> [!NOTE]  
>  При преобразовании данных SQL Юникода C символьных данных, длину данных в Юникоде должен быть четным числом.  
  
|Идентификатор типа SQL|Тест|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Байтовая длина данных < = длина столбца.<br /><br /> Длину данных в байтах > длина столбца.|н/д<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Длина данных < = длина столбца.<br /><br /> Длина данных символьной > длина столбца.|н/д<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Данные, преобразованные без усечения<br /><br /> Данные преобразуются с помощью усечения цифр дробной части [e]<br /><br /> Преобразование данных приведет к потере разрядов (в отличие от долей) [e]<br /><br /> Значение данных не *числовой литерал*|н/д<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Данные не выходят за диапазон типа данных, в который преобразуется значение<br /><br /> Данных находится вне диапазона типа данных, в который преобразуется значение<br /><br /> Значение данных не *числовой литерал*|н/д<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|Данные являются 0 или 1<br /><br /> Данные больше 0, меньше 2 и не равно 1<br /><br /> Данных меньше 0 или больше или равно 2<br /><br /> Данные не *числовой литерал*|н/д<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Длину в байтах данных) / 2 < = длина столбца в байтах<br /><br /> (Длину в байтах данных) / 2 > длина столбца в байтах<br /><br /> Значение данных не является шестнадцатеричным значением|н/д<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|Значение является допустимым *ODBC-литерал даты*<br /><br /> Значение является допустимым *ODBC-timestamp-literal*; время часть равна нулю<br /><br /> Значение является допустимым *ODBC-timestamp-literal*; части времени задается ненулевое значение [a]<br /><br /> Значение данных не является допустимым *ODBC-литерал даты* или *ODBC-timestamp-literal*|н/д<br /><br /> н/д<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|Значение является допустимым *ODBC-литерал времени*<br /><br /> Значение является допустимым *ODBC-timestamp-literal*; дробная часть секунд является ноль [b]<br /><br /> Значение является допустимым *ODBC-timestamp-literal*; дробная часть секунд — ненулевое значение [b]<br /><br /> Значение данных не является допустимым *ODBC-литерал времени* или *ODBC-timestamp-literal*|н/д<br /><br /> н/д<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|Значение является допустимым *ODBC-timestamp-literal*; дробная часть секунд не усекаются<br /><br /> Значение является допустимым *ODBC-timestamp-literal*; дробной части с обозначением секунды усекаются<br /><br /> Значение является допустимым *ODBC-литерал даты*[c]<br /><br /> Значение является допустимым *ODBC-литерал времени*[d]<br /><br /> Значение данных не является допустимым *ODBC-литерал даты*, *ODBC-литерал времени*, или *ODBC-timestamp-literal*|н/д<br /><br /> 22008<br /><br /> н/д<br /><br /> н/д<br /><br /> 22018|  
|Все типы интервала SQL|Значение является допустимым *значение интервала*; усечение не происходит<br /><br /> Значение является допустимым *значение интервала*; значение в одно из полей будет усечено<br /><br /> Значение не является допустимое значение литерала интервала|н/д<br /><br /> 22015<br /><br /> 22018|  
  
 [a] усекается части времени отметки времени.  
  
 [b] в части даты отметки времени учитывается.  
  
 [c] части времени отметки времени, равным нулю.  
  
 [d] в части даты отметки времени имеет значение текущей даты.  
  
 [e] источник данных и драйвера эффективно ожидает, пока не будет принят всю строку (даже если символьные данные отправляется по частям при вызове **SQLPutData**) прежде чем пытаться выполнить преобразование.  
  
 Когда символ C данные преобразуются в числовые, даты, времени или данных timestamp SQL, начальные и завершающие пробелы учитываются.  
  
 При C символьные данные преобразуются в двоичные данные SQL, каждый два байта символьные данные преобразуются в один байт (8 бит) двоичных данных. Каждый двух байт символьных данных представляет число в виде шестнадцатеричного числа. Например «01» преобразуется в двоичный 00000001, и «FF» преобразуется в двоичное 11111111.  
  
 Драйвер всегда преобразует пар шестнадцатеричных цифр в отдельных байтов и игнорирует байтов конечное значение null. Из-за этого Если длина символьной строки является нечетным, последний байт строки (за исключением байт конечное значение null, если таковые имеются) не преобразуется.  
  
> [!NOTE]  
>  Разработчикам приложений не рекомендуется привязка данных символа C на двоичный тип данных SQL. Это преобразование обычно является неэффективным и медленно.
