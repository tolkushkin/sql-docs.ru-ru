---
title: STUFF (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 11/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STUFF
- STUFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 88745cf6d143436dcce84d20a4253266843d6c8e
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947463"
---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Функция STUFF вставляет одну строку в другую. Она удаляет указанное количество символов первой строки в начальной позиции и вставляет на их место вторую строку.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>Аргументы  
 *character_expression*  
 [Выражение](../../t-sql/language-elements/expressions-transact-sql.md) символьного типа данных. Аргумент *character_expression* может быть константой, переменной или столбцом символьных или двоичных данных.  
  
 *start*  
 Целочисленное значение, определяющее место начала удаления и вставки. Если аргумент *start* отрицателен или равен нулю, то возвращается пустая строка. Если значение аргумента *start* превышает длину первого аргумента *character_expression*, возвращается значение NULL. *start* может иметь тип **bigint**.  
  
 *length*  
 Целочисленное выражение, которое определяет, какое количество символов следует удалить. Если аргумент *length* отрицателен, то возвращается пустая строка. Если значение аргумента *length* превышает длину первого аргумента *character_expression*, удаляются все символы вплоть до последнего в последнем аргументе *character_expression*.  Если аргумент *length* равен нулю, вставка производится перед первым символом в строке. *length* может иметь тип **bigint**.

 *replaceWith_expression*  
 [Выражение](../../t-sql/language-elements/expressions-transact-sql.md) символьного типа данных. Аргумент *character_expression* может быть константой, переменной или столбцом символьных или двоичных данных. Это выражение заменяет *length* символов выражения *character_expression*, начиная с позиции *start*. Если указать `NULL` в качестве значения *replaceWith_expression*, символы удаляются, причем вставка не производится.   
  
## <a name="return-types"></a>Типы возвращаемых данных  
 Возвращает символьные данные, если *character_expression* имеет один из поддерживаемых символьных типов данных. Возвращает двоичные данные, если аргумент *character_expression* имеет один из поддерживаемых двоичных типов данных.  
  
## <a name="remarks"></a>Remarks  
 Если начальная позиция или число удаляемых символов отрицательны или если начальная позиция превышает длину первой строки, возвращается пустая строка. Если начальная позиция равна 0, то возвращается значение NULL. Если число удаляемых символов превышает длину первой строки, удаление выполняется до первого символа первой строки.  

Ошибка, которая возникает, если результат больше, чем максимальное значение, поддерживаемое типом возвращаемого параметра.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Дополнительные символы (суррогатные пары)  
 При использовании параметров сортировки SC как выражение *character_expression*, так и выражение *replaceWith_expression* могут содержать суррогатные пары. Параметр длины будет рассматривать каждый суррогат в *character_expression* как один символ.  
  
## <a name="examples"></a>Примеры  
 Следующий пример иллюстрирует создание строки `abcdef` после удаления из нее трех символов, начиная с позиции `2`, с символа `b` и вставки второй строки в место удаления.  
  
```  
SELECT STUFF('abcdef', 2, 3, 'ijklmn');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
aijklmnef   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>См. также:  
 [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS (Transact-SQL)](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE (Transact-SQL)](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME (Transact-SQL)](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE (Transact-SQL)](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE (Transact-SQL)](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG (Transact-SQL)](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE (Transact-SQL)](../../t-sql/functions/string-escape-transact-sql.md)  
 [TRANSLATE (Transact-SQL)](../../t-sql/functions/translate-transact-sql.md)  
 [Типы данных (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [Строковые функции (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
