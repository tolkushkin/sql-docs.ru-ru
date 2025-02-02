---
title: 'C в SQL: Числовые | Документация Майкрософт'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 816394bb8469148504c1b2b416e77fec814bef8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191735"
---
# <a name="c-to-sql-numeric"></a>C в SQL: Numeric
Идентификаторы для числовых типов данных ODBC C следующие:  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 Следующая таблица показывает ODBC SQL типы данных, к которым можно преобразовать числовые данные C. Описание столбцов и условия в таблице, см. в разделе [преобразование данных из C в типы данных SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Идентификатор типа SQL|Тест|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Число цифр или символов < = длина столбца в байтах<br /><br /> Число цифр или символов > длина столбца в байтах|н/д<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Число символов < = длина столбца символов<br /><br /> Число символов > длины столбца символов|н/д<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|Данные преобразуются без усечения, или усекается цифр дробной части<br /><br /> Данные преобразуются с помощью усечение целой части|н/д<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Данные не выходят за диапазон типа данных, в который преобразуется значение<br /><br /> Данных находится вне диапазона типа данных, в который преобразуется значение|н/д<br /><br /> 22003|  
|SQL_BIT|Данные являются 0 или 1<br /><br /> Данные больше 0, меньше 2 и не равно 1<br /><br /> Данных меньше 0 или больше или равно 2|н/д<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE[a]<br /><br /> SQL_INTERVAL_SECOND [a]|Данные не усекаются.<br /><br /> Усечение данных.|н/д<br /><br /> 22015|  
  
 [a] Эти преобразования поддерживаются только для точных числовых типов данных (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG или SQL_C_NUMERIC). Они не поддерживаются для приблизительных числовых типов данных (SQL_C_FLOAT или SQL_C_DOUBLE). Точные числовые типы данных C нельзя преобразовать тип SQL, точности которого интервала не состоит из одного поля интервала.  
  
 [b] для варианта «н/д» драйвер может при необходимости возвращают значение SQL_SUCCESS_WITH_INFO и 01S07 при отсутствии частичное усечение.  
  
 Драйвер не учитывает значение длины и индикатора, при преобразовании данных из числовых типов данных C и предполагается, что размер буфера данных является размером числового типа данных C. Значение длины и индикатора, переданное в *StrLen_or_Ind* аргумента в **SQLPutData** и в указанный буфер с *StrLen_or_IndPtr* аргумента в **SQLBindParameter**. Буфер данных указывается с помощью *DataPtr* аргумента в **SQLPutData** и *ParameterValuePtr* аргумента в **SQLBindParameter**.
