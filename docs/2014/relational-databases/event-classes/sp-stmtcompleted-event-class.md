---
title: Класс событий SP:StmtCompleted | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:StmtCompleted event class
ms.assetid: 9e8147a4-aeeb-49a6-80f8-df753d0f34cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 056f9adb309f4f65ed1553efa80db597e7598e02
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63050960"
---
# <a name="spstmtcompleted-event-class"></a>SP:StmtCompleted, класс событий
  Класс событий SP:StmtCompleted указывает на то, что выполнение инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] в хранимой процедуре было завершено.  
  
## <a name="spstmtcompleted-event-class-data-columns"></a>Столбцы данных класса событий SP:StmtCompleted  
  
|Имя столбца данных|`Data type`|Описание|Идентификатор столбца|Фильтруемый|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Имя клиентского приложения, установившего соединение с экземпляром [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Этот столбец заполняется значениями, передаваемыми приложением, а не отображаемым именем программы.|10|Да|  
|ClientProcessID|`int`|Идентификатор, присвоенный главным компьютером сервера процессу, в котором работает клиентское приложение. Этот столбец данных заполняется в том случае, если клиент предоставляет идентификатор клиентского процесса.|9|Да|  
|ЦП|`int`|Объем времени ЦП (в миллисекундах), использованного событием.|18|Да|  
|DatabaseID|`int`|Идентификатор базы данных, в которой выполняется хранимая процедура. Определите значение для базы данных, используя функцию DB_ID.|3|Да|  
|DatabaseName|`nvarchar`|Имя базы данных, в которой выполняется хранимая процедура.|35|Да|  
|Duration|`bigint`|Длительность события (в микросекундах).|13|Да|  
|EndTime|`datetime`|Время окончания события. Этот столбец не заполняется для таких классов событий запуска, как SQL:BatchStarting или SP:Starting.|15|Да|  
|EventClass|`int`|Тип события = 45.|27|Нет|  
|EventSequence|`int`|Последовательность данного события в запросе.|51|Нет|  
|GroupID|`int`|Идентификатор группы рабочей нагрузки, в которой запускается событие трассировки SQL.|66|Да|  
|HostName|`nvarchar`|Имя компьютера, на котором выполняется клиентская программа. Этот столбец данных заполняется, если клиент предоставляет имя узла. Чтобы определить имя узла, используйте функцию HOST_NAME.|8|Да|  
|IntegerData|`int`|Целочисленное значение, зависящее от класса событий, перехватываемых при трассировке.|25|Да|  
|IntegerData2|`int`|Смещение конца выполняемой инструкции (в байтах).|55|Да|  
|IsSystem|`int`|Указывает, произошло событие в системном или в пользовательском процессе. 1 = системный, 0 = пользовательский.|60|Да|  
|LineNumber|`int`|Номер строки выполняемой инструкции.|5|Да|  
|LoginName|`nvarchar`|Имя входа пользователя (либо защищенное имя входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , либо учетные данные входа [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows в формате «ДОМЕН\имя_пользователя»).|11|Да|  
|LoginSid|`image`|Идентификатор безопасности вошедшего в систему пользователя. Эти сведения можно найти в представлении каталога sys.server_principals. Значение идентификатора безопасности уникально для каждого имени входа на сервере.|41|Да|  
|NestLevel|`int`|Целочисленное значение, представляющее данные, возвращаемые функцией @@NESTLEVEL.|29|Да|  
|NTDomainName|`nvarchar`|Домен Windows, к которому принадлежит пользователь.|7|Да|  
|NTUserName|`nvarchar`|Имя пользователя Windows.|6|Да|  
|ObjectID|`int`|Идентификатор объекта, назначенный системой.|22|Да|  
|ObjectName|`nvarchar`|Имя объекта, на который указывает ссылка.|34|Да|  
|ObjectType|`int`|Значение, представляющее тип объекта, связанного с событием. Это значение соответствует столбцу типа в представлении каталога sys.objects. Значения см. в разделе [Столбец события трассировки ObjectType](objecttype-trace-event-column.md).|28|Да|  
|Offset|`int`|Начальное смещение инструкции в пределах хранимой процедуры или пакета.|61|Да|  
|Reads|`bigint`|Число логических чтений диска, выполненное сервером для данного события.|16|Да|  
|RequestID|`int`|Идентификатор запроса, содержащего инструкцию.|49|Да|  
|RowCounts|`bigint`|Количество строк, на которые повлияло событие.|48|Да|  
|ServerName|`nvarchar`|Имя экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , для которого производится трассировка.|26|Нет|  
|SessionLoginName|`nvarchar`|Имя входа пользователя, создавшего этот сеанс. Например, при соединении с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] под именем Login1 и при выполнении инструкции под именем Login2 SessionLoginName будет содержать значение Login1, а LoginName — значение Login2. В этом столбце отображаются как имена входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так и имена входа Windows.|64|Да|  
|SourceDatabaseID|`int`|Идентификатор базы данных, в которой находится объект.|62|Да|  
|SPID|`int`|Идентификатор сеанса, в котором произошло событие.|12|Да|  
|StartTime|`datetime`|Время начала события, если оно известно.|14|Да|  
|TextData|`ntext`|Текстовое значение, зависящее от класса событий, фиксируемых при трассировке.|1|Да|  
|TransactionID|`bigint`|Назначенный системой идентификатор транзакции.|4|Да|  
|Writes|`bigint`|Число логических обращений к дискам на запись, выполненное сервером для данного события.|17|Да|  
|XactSequence|`bigint`|Токен, который описывает текущую транзакцию.|50|Да|  
  
## <a name="see-also"></a>См. также  
 [Расширенные события](../extended-events/extended-events.md)   
 [Хранимая процедура sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
