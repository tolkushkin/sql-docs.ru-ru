---
title: Поддержка правил, триггеры, значения по умолчанию и хранимых процедур | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47795998b019df22b01852519f75f6e8d3d274dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269868"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Поддержка правил, триггеров, значений по умолчанию и хранимых процедур (драйвер ODBC для Visual FoxPro)
Не удается создать правила Visual FoxPro, триггеры, значения по умолчанию или хранимых процедур с помощью драйвера ODBC для Visual FoxPro. Тем не менее приложение может взаимодействовать с существующие правила, триггеры, значения по умолчанию или хранимых процедур, как он вставляет, обновляются или удаляются из базы данных Visual FoxPro.  
  
 Ниже перечислены команды Visual FoxPro и функций, поддерживаемых драйвером ODBC для Visual FoxPro, если команды или функции в правила, триггеры, значения по умолчанию или хранимых процедур.  
  
 Если ваше приложение взаимодействует с данными, правила, триггеры, значения по умолчанию, или хранимые процедуры вызова других Visual FoxPro команд или функций, драйвер выдает ошибку. См. в разделе [неподдерживаемые команды Visual FoxPro и функции](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) список команд и функций, не поддерживается драйвером.  
  
> [!TIP]  
>  Если вы хотите вставить условный код в правила, триггеров или хранимых процедур, которые определяют команды для выполнения при вызове с помощью драйвера, можно использовать **(версии)** функции. **(Версии)** возвращает «драйвер ODBC для Visual FoxPro  *\<версии >*"при вызове с помощью драйвера.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Команды Visual FoxPro и функций, поддерживаемых правил, триггеры, значения по умолчанию и хранимых процедур  
  
||||  
|-|-|-|  
|Оператор $|%-Оператор|& Команды|  
|& & Команда|* Команда|= Команда|  
  
## <a name="a"></a>Объект  
  
||||  
|-|-|-|  
|Функция ABS)|ACOPY ()-функция|Команда ADD TABLE|  
|ADATABASES ()-функция|ADBOBJECTS ()-функция|AERROR ()-функция|  
|ЭДЕЛЬ ()-функция|AELEMENT ()-функция|ALEN ()-функция|  
|AFIELDS ()-функция|СТАТЬЕ ()-функция|ALTER TABLE (команда SQL)|  
|ПСЕВДОНИМ ()-функция|ALLTRIM ()-функция|ДОБАВЛЕНИЕ КОМАНДЫ МАССИВА|  
|И оператор|ДОБАВЬТЕ команду|ДОБАВЬТЕ команду MEMO|  
|ДОБАВЛЕНИЕ КОМАНДЫ|ДОБАВЬТЕ команду Общие|ASCAN ()-функция|  
|ДОБАВЬТЕ команду ПРОЦЕДУРЫ|ASC ()-функция|ASUBSCRIPT ()-функция|  
|Функция ASIN)|ASORT ()-функция|Функция ATAN)|  
|В функции)|AT_C ()-функция|ATCLINE ()-функция|  
|ATC ()-функция|ATCC ()-функция|AUSED ()-функция|  
|ATLINE ()-функция|ATN2 ()-функция||  
|Среднее команды|Функция ACOS)||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Команда BEGIN TRANSACTION|МЕЖДУ ()-функция|BITNOT ()-функция|  
|BITCLEAR ()-функция|BITLSHIFT ()-функция|Функция битовом МАССИВЕ)|  
|Функция BITOR)|BITRSHIFT ()-функция|ПУСТОЙ команды|  
|BITTEST ()-функция|BITXOR ()-функция||  
|Функция BOF)|Функция BITAND)||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|ВЫЧИСЛИТЬ команду|Функциям-КАНДИДАТАМ)|Функция CHR)|  
|CDX ()-функция|Функция CEILING)|ЗАКРЫТЬ команды|  
|CHRTRAN ()-функция|CHRTRANC ()-функция|СКОПИРУЙТЕ команду ИНДЕКСОВ|  
|CMONTH ()-функция|По-ПРЕЖНЕМУ команды|СКОПИРУЙТЕ команду EXTENDED СТРУКТУРЫ|  
|СКОПИРУЙТЕ команду ПРОЦЕДУРЫ|СКОПИРУЙТЕ команду СТРУКТУРЫ|СКОПИРУЙТЕ КОМАНДУ|  
|СКОПИРУЙТЕ команду ТЕГА|СКОПИРУЙТЕ КОМАНДУ МАССИВА|CPCONVERT ()-функция|  
|COS ()-функция|Команды COUNT|CTOD ()-функция|  
|CPCURRENT ()-функция|CPDBF ()-функция|CURSORSETPROP ()-функция|  
|CTOT ()-функция|CURSORGETPROP ()-функция||  
|CURVAL ()-функция|CDOW ()-функция||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Функция DATE)|Функции даты и времени)|Функция DAY)|  
|Двухбайтовые Символы ()-функция|() DBF-функция|DBGETPROP ()-функция|  
|DBUSED ()-функция|DELETE (команда SQL)|Команда DELETE|  
|Команда DELETE TAG|(УДАЛЕННЫЕ)-функция|По УБЫВАНИЮ ()-функция|  
|Функция DIFFERENCE)|Команда ИЗМЕРЕНИЯ|Места на диске ()-функция|  
|ДМГ ()-функция|СДЕЛАЙТЕ ВАРИАНТ... Команда ENDCASE|Команды|  
|DO WHILE... Команда ENDDO|DOW ()-функция|DTOC ()-функция|  
|DTOR ()-функция|Объекты передачи данных ()-функция|DTOT ()-функция|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|(Пустой)-функция|ВЫЧИСЛИТЬ функцию)|Команда ВЫХОДА|  
|Ошибка ()-функция|Функция EXP)||  
|Команда END TRANSACTION|EOF ()-функция||  
  
## <a name="f"></a>Ж  
  
||||  
|-|-|-|  
|FCOUNT ()-функция|FDATE ()-функция|ПОЛЯ ()-функция|  
|ФАЙЛ ()-функция|Функции ФИЛЬТРА)|FLDLIST ()-функция|  
|FLOCK ()-функция|Функция FLOOR)|Команда ОЧИСТКИ|  
|FOR... Команда ENDFOR|ДЛЯ функции)|НАЙТИ ()-функция|  
|Команда свободного TABLE|FSIZE ()-функция|Функция FTIME)|  
|FULLPATH ()-функция|ФУНКЦИИ-команда|Аргумент ()-функция|  
  
## <a name="g"></a>Ж  
  
||||  
|-|-|-|  
|СОБЕРИТЕ команду|GETNEXTMODIFIED ()-функция|Команда GO/GOTO|  
|GETFLDSTATE ()-функция|GOMONTH ()-функция||  
|GETCP ()-функция|GETENV ()-функция||  
  
## <a name="h"></a>З  
  
|||  
|-|-|  
|Заголовок ()-функция|Функция HOUR)|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE ()-функция|IF... ENDIF-команда|Функция IIF)|  
|INDBC ()-функция|Команда INDEX|INLIST ()-функция|  
|Команде INSERT SQL|Функция INT)|ISALPHA ()-функция|  
|Функция ISBLANK)|ISDIGIT ()-функция|ISEXCLUSIVE ()-функция|  
|Isleadbyte-функция)|ISLOWER ()-функция|Функция ISNULL)|  
|ISREADONLY ()-функция|ISUPPER ()-функция||  
  
## <a name="k"></a>Л  
  
||||  
|-|-|-|  
|Функция ключа)|KEYMATCH ()-функция||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|(СЛЕВА)-функция|LEFTC ()-функция|LIKEC ()-функция|  
|LENC ()-функция|ПОДОБНО функции)|БЛОКИРОВКА ()-функция|  
|ЛОКАЛЬНЫЕ команды|НАЙТИ команду|Функция LOOKUP)|  
|Функция LOG)|Функция LOG10)|Функция LTRIM)|  
|Функция LOWER)|Команда LPARAMETERS||  
|LUPDATE ()-функция|Функция LEN)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE системной памяти переменной|Функция MAX)|Функция многомерных Выражений)|  
|MDY (МДГ) ()-функция|MEMLINES ()-функция|СООБЩЕНИЕ ()-функция|  
|Функция MIN)|Функции (минуты)|MLINE ()-функция|  
|Функция MOD)|МЕСЯЦ ()-функция|MTON ()-функция|  
  
## <a name="n"></a>Нет  
  
||||  
|-|-|-|  
|Как NDX ()-функция|НОРМАЛИЗОВАТЬ ()-функция|Оператор NOT|  
|Команда Примечание|NTOM ()-функция|NVL ()-функция|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|ПРОИСХОДИТ ()-функция|OLDVAL ()-функция|Ошибка КОМАНДЫ|  
|Основные КОМАНДЫ|НА ()-функция|Команда ОТКРЫТЬ базу данных|  
|ИЛИ оператор|ПОРЯДОК ()-функция|ОС ()-функция|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Команды PACK|Параметры ()-функция|ОПЛАТЫ ()-функция|  
|ПАРАМЕТРЫ команды|(ОСНОВНОЙ)-функция|Команда PRIVATE|  
|Функция PI)|ПРОГРАММЫ ()-функция|ПРАВИЛЬНЫЙ ()-функция|  
|Команда ПРОЦЕДУРЫ|PV ()-функция||  
|ОТКРЫТЫЙ команды|PADL( ) &#124; PADR( ) &#124; PADC( ) Functions||  
  
## <a name="r"></a>Чтение  
  
||||  
|-|-|-|  
|Функция RAND)|RAT ()-функция|RATC ()-функция|  
|RATLINE ()-функция|ОТОЗВАТЬ команду|RECCOUNT ()-функция|  
|RECNO ()-функция|(): RECSIZE-функция|РЕГИОНАЛЬНЫЕ команды|  
|СВЯЗЬ ()-функция|УДАЛИТЬ команду таблицы|ЗАМЕНИТЕ команду|  
|ЗАМЕНИТЕ КОМАНДЫ МАССИВА|РЕПЛИКАЦИИ ()-функция|ПОВТОРИТЕ команду|  
|ВОЗВРАЩАЕТ команду|Функция (СПРАВА)|RIGHTC ()-функция|  
|RLOCK ()-функция|Команда ROLLBACK|Функция ROUND)|  
|RTOD ()-функция|RTRIM ()-функция||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|ПРОВЕРКА... Команда ENDSCAN|Точечная диаграмма команды|СЕК ()-функция|  
|СЕКУНДЫ ()-функция|ПОИСК команды|Поиск ()-функция|  
|ВЫБЕРИТЕ команду|ВЫБЕРИТЕ ()-функция|Команда SELECT-SQL|  
|Команда SET BLOCKSIZE|Команда SET ВЫПОЛНЕНИЯ|Команда SET ВЕКЕ|  
|Команда SET COLLATE|Команда SET базы данных|Команда SET-DATE|  
|Команда SET по умолчанию|Команда SET DELETED|Команда SET EXACT|  
|Команда SET EXCLUSIVE|Команда SET FDOW|Команда SET поля|  
|Команда SET-ФИЛЬТРА|Основные команды SET|Команда SET FULLPATH|  
|Команда SET FWEEK|Команды ЗАДАЙТЕ часов|Команда SET ИНДЕКСА|  
|Команда SET БЛОКИРОВКИ|Команда MULTILOCKS SET|ЗАДАТЬ КОМАНДЫ|  
|Команда SET NOCPTRANS|Команда SET-уведомление|Команда SET NULL|  
|Команда SET-ОПТИМИЗАЦИЯ|Команда SET ЗАКАЗА|Команда SET PATH|  
|Команда SET-ПРОЦЕДУРЫ|Команда SET отношения|НАБОР отношения OFF команда|  
|Команда SET REPROCESS|Команда SKIP SET|Команда SET UDFPARMS|  
|Команда SET UNIQUE|Команда SET тома|НАБОР ()-функция|  
|SETFLDSTATE ()-функция|Функция SIGN)|Функция SIN)|  
|Команда SKIP|Команда SORT|Функция SPACE)|  
|Функция SQRT)|Команда ХРАНИЛИЩА|STR ()-функция|  
|(). Функция STRCONV|STRTRAN ()-функция|Функция STUFF)|  
|STUFFC ()-функция|SUBSTR ()-функция|SUBSTRC ()-функция|  
|Команда SUM|Функция sys(2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY системной памяти переменной|_TRIGGERLEVEL системной памяти переменной|TAGCOUNT ()-функция|  
|TABLEUPDATE ()-функция|ТЕГ ()-функция|Целевой объект ()-функция|  
|TAGNO ()-функция|Функция TAN)|TRIM ()-функция|  
|ВРЕМЯ ()-функция|Всего команд|TXNLEVEL ()-функция|  
|TTOC ()-функция|TTOD ()-функция||  
|Функция ТИПА)|TABLEREVERT ()-функция||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|(УНИКАЛЬНЫЙ)-функция|UNLOCK, команда|Используйте команду|  
|Команда UPDATE|(Верхний)-функция||  
|ИСПОЛЬЗОВАТЬ ()-функция|UPDATE (команда SQL)||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Функция VAL)|ВЕРСИИ ()-функция||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|НЕДЕЛЯ ()-функция|||  
  
## <a name="y"></a>Да  
  
||||  
|-|-|-|  
|Функция YEAR)|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Команда ZAP|||
