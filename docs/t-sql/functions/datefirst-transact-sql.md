---
title: '@@DATEFIRST (Transact-SQL) | Документы Майкрософт'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SET DATEFIRST
- first day of week [SQL Server]
- dates [SQL Server], first day of week
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- date and time [SQL Server], DATEFIRST
- DATEFIRST option [SQL Server]
- date and time [SQL Server], @@DATEFIRST
- weekdays [SQL Server]
- '@@DATEFIRST function [SQL Server]'
- functions [SQL Server], date and time
- options [SQL Server], date
ms.assetid: a178868e-49d5-4bd5-a5e2-1283409c8ce6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c748a75fa9264cce7282f2a9af7b5d183c75cdb5
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65943640"
---
# <a name="x40x40datefirst-transact-sql"></a>&#x40;&#x40;DATEFIRST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Эта функция возвращает текущее значение параметра [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) для определенного сеанса.
  
Обзор всех типов данных и функций даты и времени в языке [!INCLUDE[tsql](../../includes/tsql-md.md)] см. в статье [Типы данных и функции даты и времени (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Синтаксис  
  
```
@@DATEFIRST  
```  
  
## <a name="return-type"></a>Тип возвращаемых данных  
**tinyint**
  
## <a name="remarks"></a>Remarks  
Инструкция SET DATEFIRST *n* задает первый день недели (понедельник, вторник, среда и т. д.). Значение *n* лежит в диапазоне от 1 до 7.

```sql
SET DATEFIRST 3;
GO  
SELECT @@DATEFIRST; -- 3 (Wednesday)
GO
```  

Для региональных настроек "Английский (США)" значением @@DATEFIRST по умолчанию является 7 (воскресенье).
  
Эта языковая настройка влияет на интерпретацию символьных строк при их преобразовании сервером SQL Server в значения дат для хранения в базе данных. Она также влияет на отображение дат, хранящихся в базе данных. Она не влияет на формат хранения дат.

В приведенном ниже примере сначала задается язык `Italian`. Инструкция `SELECT @@DATEFIRST;` возвращает значение `1`. Следующая инструкция задает язык `us_english`. В последней инструкции `SELECT @@DATEFIRST;` возвращает значение `7`.
  
```sql
SET LANGUAGE Italian;  
GO  
SELECT @@DATEFIRST;  
GO  
SET LANGUAGE us_english;  
GO  
SELECT @@DATEFIRST;  
```  
  
## <a name="examples"></a>Примеры  
В приведенном ниже примере в качестве первого дня недели задается `5` (пятница) и предполагается, что текущий день `Today` приходится на субботу. Инструкция `SELECT` возвращает значение `DATEFIRST` и номер текущего дня недели.
  
```sql
SET DATEFIRST 5;  
SELECT @@DATEFIRST AS 'First Day'  
    ,DATEPART(dw, SYSDATETIME()) AS 'Today';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
First Day         Today  
----------------  --------------  
5                 2  
```  
  
## <a name="example"></a>Пример
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>См. также раздел
[Функции настройки (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  

