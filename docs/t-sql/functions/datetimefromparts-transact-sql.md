---
title: DATETIMEFROMPARTS (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIMEFROMPARTS_TSQL
- DATETIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEFROMPARTS function
ms.assetid: 6008148b-bf75-4c98-9392-68a89fa0711c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 505b1ac04eae49c58a4166fcceba8ec9bf53a66a
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945722"
---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Эта функция возвращает значение **datetime** для указанных аргументов даты и времени.
  
![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Синтаксис  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
```  
  
## <a name="arguments"></a>Аргументы  
*year*  
Целочисленное выражение, задающее год.
  
*month*  
Целочисленное выражение, задающее месяц.
  
*day*  
Целочисленное выражение, задающее день.
  
*hour*  
Целочисленное выражение, задающее часы.
  
*minute*  
Целочисленное выражение, задающее минуты.
  
*секунд*  
Целочисленное выражение, задающее секунды.
  
*milliseconds*  
Целочисленное выражение, задающее миллисекунды.
  
## <a name="return-types"></a>Типы возвращаемых данных
**datetime**
  
## <a name="remarks"></a>Remarks  
Функция `DATETIMEFROMPARTS` возвращает полностью инициализированное значение типа **datetime**. Функция `DATETIMEFROMPARTS` вызывает ошибку, если по крайней мере один обязательный аргумент имеет недопустимое значение. Функция `DATETIMEFROMPARTS` возвращает NULL, если по крайней мере один обязательный аргумент имеет значение NULL.
  
Эта функция поддерживает удаленное взаимодействие с серверами [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] и более поздних версий. Она не поддерживает удаленное взаимодействие с серверами версий ниже [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Примеры  
  
```sql
SELECT DATETIMEFROMPARTS ( 2010, 12, 31, 23, 59, 59, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>См. также раздел
[datetime (Transact-SQL)](../../t-sql/data-types/datetime-transact-sql.md)
  
  

