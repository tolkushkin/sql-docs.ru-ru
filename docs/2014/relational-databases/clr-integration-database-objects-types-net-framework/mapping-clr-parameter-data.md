---
title: Сопоставление данных параметров CLR | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b297d329f11e05ed1b1995004150644e4b76ec9b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874840"
---
# <a name="mapping-clr-parameter-data"></a>Сопоставление данных о параметрах CLR
  В следующей таблице перечислены [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] типы данных, их эквиваленты в системе common language runtime (CLR) для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в `System.Data.SqlTypes` пространства имен и их собственные эквиваленты CLR в [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
||||  
|-|-|-|  
|**Тип данных SQL Server**|Тип (в System.Data.SqlTypes or Microsoft.SqlServer.Types)|**Тип данных CLR (.NET Framework)**|  
|`bigint`|`SqlInt64`|**Int64, допускающее значение NULL\<Int64 >**|  
|`binary`|`SqlBytes, SqlBinary`|`Byte[]`|  
|`bit`|`SqlBoolean`|**Логический, допускающие значения NULL\<логическое >**|  
|`char`|None|None|  
|`cursor`|None|None|  
|`date`|`SqlDateTime`|**DateTime, допускающий значение NULL\<DateTime >**|  
|`datetime`|`SqlDateTime`|**DateTime, допускающий значение NULL\<DateTime >**|  
|`datetime2`|None|**DateTime, допускающий значение NULL\<DateTime >**|  
|`DATETIMEOFFSET`|`None`|**DateTimeOffset, допускающие значения NULL\<DateTimeOffset >**|  
|`decimal`|`SqlDecimal`|**Decimal, допускающий значение NULL\<десятичное >**|  
|`float`|`SqlDouble`|**Double, допускающее значение NULL\<Double >**|  
|`geography`|`SqlGeography`<br /><br /> `SqlGeography` определяется в библиотеке Microsoft.SqlServer.Types.dll, которая устанавливается вместе с SQL Server и могут быть загружены из в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [пакет дополнительных компонентов](https://www.microsoft.com/en-us/download/details.aspx?id=53164).|None|  
|`geometry`|`SqlGeometry`<br /><br /> `SqlGeometry` определяется в библиотеке Microsoft.SqlServer.Types.dll, которая устанавливается вместе с SQL Server и могут быть загружены из в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [пакет дополнительных компонентов](https://www.microsoft.com/en-us/download/details.aspx?id=53164).|None|  
|`hierarchyid`|`SqlHierarchyId`<br /><br /> `SqlHierarchyId` определяется в библиотеке Microsoft.SqlServer.Types.dll, которая устанавливается вместе с SQL Server и могут быть загружены из в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [пакет дополнительных компонентов](https://www.microsoft.com/en-us/download/details.aspx?id=53164).|None|  
|`image`|None|None|  
|`int`|`SqlInt32`|**Int32, допускающий значение NULL\<Int32 >**|  
|`money`|`SqlMoney`|**Decimal, допускающий значение NULL\<десятичное >**|  
|`nchar`|`SqlChars, SqlString`|`String, Char[]`|  
|`ntext`|None|None|  
|`numeric`|`SqlDecimal`|**Decimal, допускающий значение NULL\<десятичное >**|  
|`nvarchar`|`SqlChars, SqlString`<br /><br /> `SQLChars` лучше подходит для передачи данных и доступа, тогда как `SQLString` более подходит для выполнения строковых операций.|`String, Char[]`|  
|`nvarchar(1), nchar(1)`|`SqlChars, SqlString`|**Char, строка, Char [], Nullable\<char >**|  
|`real`|`SqlSingle` (но `SqlSingle` поддерживает больший диапазон значений, чем `real`)|**Единый, допускающие значения NULL\<единый >**|  
|`rowversion`|None|`Byte[]`|  
|`smallint`|`SqlInt16`|**Int16, допускающее значение NULL\<Int16 >**|  
|`smallmoney`|`SqlMoney`|**Decimal, допускающий значение NULL\<десятичное >**|  
|`sql_variant`|None|`Object`|  
|`table`|None|None|  
|`text`|None|None|  
|`time`|None|**Интервал времени, допускающие значения NULL\<TimeSpan >**|  
|`timestamp`|None|None|  
|`tinyint`|`SqlByte`|**Байт, допускающий значение NULL\<байтов >**|  
|`uniqueidentifier`|`SqlGuid`|**Идентификатор GUID, допускающий значение NULL\<Guid >**|  
|`User-defined type(UDT)`|None|Тот же класс связывается с определяемым пользователем типом данных в той же сборке или в зависимой сборке.|  
|**varbinary**|`SqlBytes, SqlBinary`|`Byte[]`|  
|`varbinary(1), binary(1)`|`SqlBytes, SqlBinary`|**байт, Byte [], Nullable\<байтов >**|  
|`varchar`|None|None|  
|`xml`|`SqlXml`|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Автоматическое преобразование типов данных для выходных параметров  
 Метод CLR может возвращать данные вызывающему коду или программе, сопровождая входной параметр модификатором `out` (Microsoft Visual C#) или `<Out()> ByRef` (Microsoft Visual Basic). Если входной параметр принадлежит типу данных CLR в пространстве имен `System.Data.SqlTypes`, и вызывающая программа указывает свой соответствующий тип данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] как входной параметр, преобразование типов осуществляется автоматически, когда метод CLR возвращает тип данных.  
  
 Так, следующая хранимая процедура CLR имеет входной параметр с типом данных CLR `SqlInt32`, помеченный модификатором `out` (C#) или `<Out()> ByRef` (Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 После формирования сборки в базе данных хранимая процедура создается в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] со следующим кодом Transact-SQL, который указывает тип данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `int` для параметра OUTPUT:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 При вызове хранимой процедуры CLR тип данных `SqlInt32` автоматически преобразуется в тип данных `int` и возвращается вызывающей программе.  
  
 Однако не все типы данных CLR могут автоматически преобразовываться в эквивалентные им типы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью выходного параметра. В следующей таблице перечислены эти исключения.  
  
|||  
|-|-|  
|**Тип данных CLR (SQL Server)**|**Тип данных SQL Server**|  
|`Decimal`|smallmoney|  
|`SqlMoney`|smallmoney|  
|`Decimal`|money|  
|`DateTime`|smalldatetime|  
|`SQLDateTime`|smalldatetime|  
  
## <a name="change-history"></a>Журнал изменений  
  
|Обновленное содержимое|  
|---------------------|  
|В таблицу сопоставления добавлены типы `SqlGeography`, `SqlGeometry` и `SqlHierarchyId`.|  
  
## <a name="see-also"></a>См. также  
 [Типы данных SQL Server в платформе .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
