---
title: TODATETIMEOFFSET (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26a8299165eea6a2a8f1b8d69f87dc92f9bf12b6
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65949063"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает значение **datetimeoffset**, преобразованное из выражения **datetime2**.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>Аргументы  
 *expression*  
 [Выражение](../../t-sql/language-elements/expressions-transact-sql.md), которое разрешается в значение [datetime2](../../t-sql/data-types/datetime2-transact-sql.md).  
  
> [!NOTE]  
>  Выражение не может иметь тип **text**, **ntext** или **image**, так как эти типы нельзя неявно преобразовать в тип **varchar** или **nvarchar**.  
  
 *time_zone*  
 Выражение, которое представляет смещение часового пояса в минутах (если это целое число), например –120, или в часах и минутах (если это строка), например "+13:00". Диапазон охватывает значения от +14 до -14 (в часах). Выражение приводится к местному времени для указанного часового пояса time_zone.  
  
> [!NOTE]  
>  Если выражение является символьной строкой, оно должно иметь формат {+|-}TZH:THM.  
  
## <a name="return-type"></a>Тип возвращаемых данных  
 **datetimeoffset**. Дробная точность такая же, как у аргумента *datetime*.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. Изменение смещения часового пояса для текущего значения даты и времени  
 В следующем примере смещение пояса для текущего значения даты и времени изменяется на часовой пояс `-07:00`.  
  
```sql  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2019-04-22 16:23:51.7666667 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>Б. Изменение смещения часового пояса в минутах  
 В следующем примере текущий часовой пояс изменяется на `-120` минут.  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), -120)
-- RETURNS: 2019-04-22 11:39:21.6986813 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>В. Добавление 13-часового смещения часового пояса  
 В следующем примере 13-часовое смещение часового пояса добавляется к дате и времени.  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), '+13:00')
-- RETURNS: 2019-04-22 11:39:29.0339301 +13:00
```  
  
## <a name="see-also"></a>См. также:  
 [Функции CAST и CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Типы данных и функции даты и времени (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE (Transact-SQL)](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  

