---
title: Доступ к диагностическим сведениям в журнале расширенных событий | Документы Майкрософт
description: Трассировка драйвера OLE DB для SQL Server и доступ к диагностическим сведениям в журнале расширенных событий
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: dd9db627fcf79114c010cc33c2552886fb7a6dc2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777932"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Доступ к диагностическим сведениям в журнале расширенных событий
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Начиная с версии [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] драйвер OLE DB для SQL Server и отслеживание доступа к данным ([Трассировка доступа к данным](https://go.microsoft.com/fwlink/?LinkId=125805)) обновлены. Упрощено получение диагностических сведений об ошибках подключения из кольцевого буфера соединений и сведений о производительности приложений из журнала расширенных событий.  
  
 Дополнительные сведения о чтении журнала расширенных событий см. в разделе [View Event Session Data](../../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md). 

  
> [!NOTE]  
>  Эта функция предназначена только для диагностики и устранения неполадок; она может оказаться неприменимой для целей аудита или обеспечения безопасности.  
  
## <a name="remarks"></a>Remarks  
 Для операций соединения драйвер OLE DB для SQL Server будет отправлять клиенту идентификатор соединения. Если подключение завершилось ошибкой, то можно в кольцевом буфере подключений ([Устранение связанных с подключением неполадок в SQL Server 2008 с использованием кольцевого буфера подключений](https://go.microsoft.com/fwlink/?LinkId=207752)) найти поле **ClientConnectionID** и получить диагностические данные по ошибке подключения. Идентификаторы подключений клиентов регистрируются в кольцевом буфере только при возникновении ошибки. (Если подключение завершилось сбоем до отправки предварительного пакета входа, то идентификатор подключения клиента не формируется.) Идентификатор клиентского соединения — это 16-байтовый идентификатор GUID. Идентификатор подключения клиента также можно найти в расположении вывода расширенных событий, если действие **client_connection_id** добавляется к событиям в сеансе расширенных событий. Если необходима дополнительная помощь в диагностике, то можно включить отслеживание доступа к данным и повторно выполнить команду соединения, а затем отследить в поле **ClientConnectionID** в трассировке доступа к данным операцию, завершившуюся ошибкой.  
   
  
 Драйвер OLE DB для SQL Server также отправляет идентификатор активности конкретного потока. Идентификатор активности регистрируется в сеансах расширенных событий, если сеанс запущен со включенным параметром TRACK_CAUSAILITY. Если возникли проблемы производительности, связанные с активным соединением, то можно получить идентификатор активности из трассировки доступа клиента к данным (поле**ActivityID** ) и найти идентификатор активности в выходных данных расширенных событий. Идентификатор активности в расширенном событии — это 16-байтовый идентификатор GUID (не совпадающий с идентификатором GUID подключения клиента), к которому добавлен четырехбайтовый номер последовательности. Номер последовательности представляет порядок запроса в потоке и указывает относительный порядок пакетных инструкций и инструкций RPC для данного потока. Идентификатор **ActivityID** также может отправляться для пакетных инструкций SQL и запросов RPC, если отслеживание доступа к данным включено, а 18-й бит слова конфигурации отслеживания доступа к данным установлен.  
  
 В следующем образце код [!INCLUDE[tsql](../../../includes/tsql-md.md)] служит для запуска сеанса расширенных событий, который будет сохраняться в кольцевом буфере и регистрировать идентификаторы активности, отправляемые с клиента при выполнении операций RPC и пакетных операций.  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
  
```  
  
## <a name="control-file"></a>Управляющий файл  
 — Содержимое драйвера OLE DB для SQL Server-файл элемента управления (ctrl.guid):  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x630ff  0   MSDADIAG.ETW
{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}  0x630ff  0   MSOLEDBSQL.1  
```  
  
## <a name="mof-file"></a>MOF-файл  
 — Содержимое драйвера OLE DB для SQL Server MOF-файл:  
  
```  
#pragma classflags("forceupdate")  
#pragma namespace ("\\\\.\\Root\\WMI")  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSDADIAG.ETW  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F3-3CC6-0B9C-6651-9649CCE5C752}"),  
 DisplayName("msdadiag"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace : Bid2Etw_MSDADIAG_ETW  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextA : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextW : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSOLEDBSQL.1  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59D-D3E8-9684-AEAC-B214EFD91B31}"),  
 DisplayName("MSOLEDBSQL.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace : Bid2Etw_MSOLEDBSQL_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextA : Bid2Etw_MSOLEDBSQL_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextW : Bid2Etw_MSOLEDBSQL_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
```  
  
## <a name="see-also"></a>См. также:  
 [Обработка ошибок](../../oledb/ole-db-errors/errors.md)  
  
  
