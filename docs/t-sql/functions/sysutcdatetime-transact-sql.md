---
title: SYSUTCDATETIME (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 12/01/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SYSUTCDATETIME
- SYSUTCDATETIME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- date and time [SQL Server], SYSUTCDATETIME
- SYSUTCDATETIME function [SQL Server]
- time [SQL Server], system
ms.assetid: f14fc2cd-9ea8-4daf-88f4-418cf523ab55
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2cdac555a12724f8ef1574b369324a5f0a16bcc3
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948572"
---
# <a name="sysutcdatetime-transact-sql"></a>SYSUTCDATETIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает значение типа **datetime2**, которое содержит дату и время компьютера, на котором запущен экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Возвращаемые дата и время отображаются в формате UTC. Точность дробной части значения секунд может быть задана в диапазоне от 1 до 7 цифр. Точность по умолчанию составляет 7 цифр.  
  
> [!NOTE]  
>  SYSDATETIME и SYSUTCDATETIME имеют большую точность в долях секунды, чем GETDATE и GETUTCDATE. SYSDATETIMEOFFSET включает смещение часового пояса, заданное в системе. SYSDATETIME, SYSUTCDATETIME и SYSDATETIMEOFFSET можно присваивать переменным любого типа даты и времени.  
  
 Обзор всех типов данных и функций даты и времени в языке [!INCLUDE[tsql](../../includes/tsql-md.md)] см. в статье [Типы данных и функции даты и времени](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
SYSUTCDATETIME ( )  
```  
  
## <a name="return-type"></a>Тип возвращаемых данных  
 **datetime2**  
  
## <a name="remarks"></a>Remarks  
 Функция SYSUTCDATETIME может использоваться в инструкциях [!INCLUDE[tsql](../../includes/tsql-md.md)] везде, где допустимо использование выражений **datetime2**.  
  
 Тип SYSUTCDATETIME является недетерминированным. Невозможно проиндексировать представления и выражения, ссылающиеся на эту функцию в столбце.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] получает значения даты и времени с помощью функции GetSystemTimeAsFileTime() Windows API. Точность зависит от физического оборудования и версии Windows, в которой запущен экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Точность возвращаемых значений этого API-интерфейса задана равной 100 нс. Точность может быть определена с помощью метода GetSystemTimeAdjustment() интерфейса API Windows.  
  
## <a name="examples"></a>Примеры  
 В следующих примерах с помощью шести системных функций [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], которые возвращают текущую дату и время, происходит возврат даты, времени или и того и другого. Значения возвращаются последовательно и поэтому могут различаться на доли секунды.  
  
### <a name="a-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>A. Отображение форматов, которые возвращаются функциями даты и времени  
 В следующем примере показаны различные идентификаторы, возвращаемые функциями даты и времени.  
  
```  
SELECT SYSDATETIME() AS [SYSDATETIME()]  
    ,SYSDATETIMEOFFSET() AS [SYSDATETIMEOFFSET()]  
    ,SYSUTCDATETIME() AS [SYSUTCDATETIME()]  
    ,CURRENT_TIMESTAMP AS [CURRENT_TIMESTAMP]  
    ,GETDATE() AS [GETDATE()]  
    ,GETUTCDATE() AS [GETUTCDATE()];  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
SYSDATETIME()      2007-04-30 13:10:02.0474381
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047
GETDATE()          2007-04-30 13:10:02.047
GETUTCDATE()       2007-04-30 20:10:02.047
```  
  
### <a name="b-converting-date-and-time-to-date"></a>Б. Преобразование даты и времени в дату  
 В следующем примере показано, как преобразовать значения даты и времени в тип `date`.  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
```  
  
### <a name="c-converting-date-and-time-values-to-time"></a>В. Преобразование значений даты и времени во время  
 В следующем примере показано, как преобразовать значения даты и времени в тип `time`.  
  
 ```
DECLARE @DATETIME DATETIME = GetDate();
DECLARE @TIME TIME
SELECT @TIME = CONVERT(time, @DATETIME)
SELECT @TIME AS 'Time', @DATETIME AS 'Date Time'
```
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Time             Date Time  
13:49:33.6330000 2009-04-22 13:49:33.633
```  
  
## <a name="see-also"></a>См. также:  
 [Функции CAST и CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Типы данных и функции даты и времени (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE (Transact-SQL)](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


