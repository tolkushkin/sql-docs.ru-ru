---
title: Интервал функции, даты и времени | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1303ca724ef6790ae7bcf218ab8ed0e5da4ed38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735090"
---
# <a name="time-date-and-interval-functions"></a>Функции даты, времени и интервалов
В следующей таблице перечислены функций даты и времени, которые включены в набор скалярные функции ODBC. Приложение может определить, какие функции даты и времени поддерживаются драйвером, вызвав **SQLGetInfo** с *тип сведений* из SQL_TIMEDATE_FUNCTIONS.  
  
 Аргументы обозначается как *timestamp_exp* может быть именем столбца, результат другой скалярной функцией, или *-время-escape-последовательность ODBC*, *-Дата-escape-последовательность ODBC*, или *-Timestamp-escape-последовательность ODBC*, где базовый тип данных может быть представлено как SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE или SQL_TYPE_TIMESTAMP.  
  
 Аргументы обозначается как *выражение_даты* может быть именем столбца, результат другой скалярной функцией, или *-Дата-escape-последовательность ODBC* или *-timestamp-escape-последовательность ODBC*, где базовый тип данных может быть представлено как SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE или SQL_TYPE_TIMESTAMP.  
  
 Аргументы обозначается как *выражение_времени* может быть именем столбца, результат другой скалярной функцией, или *-время-escape-последовательность ODBC* или *-timestamp-escape-последовательность ODBC*, где базовый тип данных может быть представлено как SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME и SQL_TYPE_TIMESTAMP.  
  
 Функция CURRENT_DATE, CURRENT_TIME и CURRENT_TIMESTAMP timedate скалярные функции были добавлены в ODBC 3.0 в соответствии со стандартом SQL-92.  
  
|Компонент|Описание|  
|--------------|-----------------|  
|**(ФУНКЦИЯ CURRENT_DATE)** (ODBC 3.0)|Возвращает текущую дату.|  
|**CURRENT_TIME [(** *точность_в_секундах* **)]** (ODBC 3.0)|Возвращает текущее время. *Точность_в_секундах* аргумент определяет секунды значения типа возвращаемого значения.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *timestamp точности* **)]** (ODBC 3.0)|Возвращает текущую локальную дату и местное время как значение отметки времени. *Timestamp точности* аргумент определяет точность секунды возвращаемой отметки времени.|  
|**(ФУНКЦИЯ CURDATE)** (ODBC 1.0)|Возвращает текущую дату.|  
|**(ФУНКЦИЯ CURTIME)** (ODBC 1.0)|Возвращает текущее время.|  
|**Функция DAYNAME (** *выражение_даты* **)** (ODBC 2.0)|Возвращает символьную строку, содержащую имя зависящие от источника данных дня (например, от Sunday до Saturday или от Sun. до Sat., для источника данных использует английский язык, либо от Sonntag до samstag, если для источника данных использует немецкий) для части дня *выражение_даты*.|  
|**DAYOFMONTH (** *выражение_даты* **)** (ODBC 1.0)|Возвращает день месяца, основываясь на поле «месяц» в *выражение_даты* виде целочисленного значения в диапазоне от 1 до 31.|  
|**DAYOFWEEK (** *выражение_даты* **)** (ODBC 1.0)|Возвращает день недели, исходя из поля недели в *выражение_даты* виде целочисленного значения в диапазоне 1 – 7, где 1 соответствует воскресенью.|  
|**DAYOFYEAR (** *выражение_даты* **)** (ODBC 1.0)|Возвращает день года, основываясь на поле года в *выражение_даты* виде целочисленного значения в диапазоне от 1 до 366.|  
|**EXTRACT(** *extract-field FROM* *extract-source* **)** (ODBC 3.0)|Возвращает *извлечение поля* часть *источника извлечения*. *Источника извлечения* аргументом является выражение даты-времени или интервал. *Извлечение поля* аргумент может принимать одно из следующих ключевых слов:<br /><br /> ГОД МЕСЯЦ СЕКУНДЫ МИНУТЫ ЧАСА ДНЯ<br /><br /> Точность возвращаемого значения определяется реализацией. Масштаб равен 0, если не указано во-ВТОРЫХ, в этом случае масштаб не меньше, чем точность значения долей секунды *источника извлечения* поля.|  
|**HOUR(** *time_exp* **)** (ODBC 1.0)|Возвращает час из поля часа в *выражение_времени* виде целочисленного значения в диапазоне от 0 до 23.|  
|**MINUTE(** *time_exp* **)** (ODBC 1.0)|Возвращает минуту поля минуты в *выражение_времени* виде целочисленного значения в диапазоне от 0 до 59.|  
|**МЕСЯЦ (** *выражение_даты* **)** (ODBC 1.0)|Возвращает месяца, основываясь на поле «месяц» в *выражение_даты* виде целочисленного значения в диапазоне от 1 до 12.|  
|**MONTHNAME (** *выражение_даты* **)** (ODBC 2.0)|Возвращает строку символов, содержащая зависящие от источника данных название месяца (например, January до December или Jan. до Dec., если источник данных использует английский язык, либо от Januar до Dezember, если для источника данных использует немецкий) для части месяца *выражение_даты*.|  
|**(ТЕПЕРЬ)** (ODBC 1.0)|Возвращает текущую дату и время как значение отметки времени.|  
|**QUARTER(** *date_exp* **)** (ODBC 1.0)|Возвращает квартал в *выражение_даты* виде целочисленного значения в диапазоне от 1 до 4, где 1 представляет 1 января по 31 марта.|  
|**SECOND(** *time_exp* **)** (ODBC 1.0)|Возвращает секунду на второе поле в *выражение_времени* виде целочисленного значения в диапазоне от 0 до 59.|
|**TIMESTAMPADD (** *интервал*, *целое_выражение*, *timestamp_exp* **)** (ODBC 2.0)|Возвращает метку времени, рассчитывается путем сложения *целое_выражение* интервалы типа *интервал* для *timestamp_exp*. Допустимые значения *интервал* являются следующие ключевые слова:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> где долей секунды, выражаются в миллиардных долей секунды. Например следующая инструкция SQL возвращает имя каждого сотрудника и его срок окончания действия один год:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Если *timestamp_exp* — это значение времени и *интервал* указывает дней, недель, месяцев, кварталов или лет, части даты *timestamp_exp* имеет значение текущей даты до Вычисление итоговый отметка времени.<br /><br /> Если *timestamp_exp* является значением даты и *интервал* указывает доли секунды, секунд, минут или часов, а часть времени *timestamp_exp* имеет значение 0 перед Вычисление итоговый отметка времени.<br /><br /> Приложение определяет, какие интервалы, поддерживаемый источником данных, вызвав **SQLGetInfo** с параметром SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF (** *интервал*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|Возвращает целое число интервалов типа *интервал* , на который *timestamp_exp2* больше, чем *timestamp_exp1*. Допустимые значения *интервал* являются следующие ключевые слова:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> где долей секунды, выражаются в миллиардных долей секунды. Например следующая инструкция SQL возвращает имя каждого сотрудника и количества лет, он или она принят на работу:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Если любое из выражений отметка времени — это значение времени и *интервал* указывает дней, недель, месяцев, кварталов или лет, части даты этой метки времени имеет значение текущей даты до Вычисление разности между метками времени.<br /><br /> Если любое из выражений метка времени представляет собой значение даты и *интервал* указывает доли секунды, секунд, минут или часов, промежуток времени этой метки времени имеет значение 0 перед Вычисление разности между метками времени.<br /><br /> Приложение определяет, какие интервалы, поддерживаемый источником данных, вызвав **SQLGetInfo** с параметром SQL_TIMEDATE_DIFF_INTERVALS.|  
|**НЕДЕЛЯ (** *выражение_даты* **)** (ODBC 1.0)|Возвращает неделю года, основываясь на поля недели в *выражение_даты* виде целочисленного значения в диапазоне от 1-53.|  
|**ГОД (** *выражение_даты* **)** (ODBC 1.0)|Возвращает год по полю "год" в *выражение_даты* виде целочисленного значения. Диапазон не зависит от источника данных.|
