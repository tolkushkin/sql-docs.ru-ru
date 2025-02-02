---
title: Класс событий Broker:Forwarded Message Dropped | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Forwarded Message Dropped event class
ms.assetid: ec242d0b-77b0-45f5-8b12-186a14b173a8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf6e9bb278417d69be0ec0a99cb1c47d88ffddff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664030"
---
# <a name="brokerforwarded-message-dropped-event-class"></a>Broker:Forwarded Message Dropped, класс событий
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] создает событие Broker:Forwarded Message Dropped при удалении компонентом Service Broker сообщения, предназначенного для переадресации.  
  
## <a name="brokerforwarded-message-dropped-event-class-data-columns"></a>Столбцы данных класса событий Broker:Forwarded Message Dropped  
  
|Столбец данных|Тип|Описание|Номер столбца|Фильтруемый|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|Имя клиентского приложения, установившего соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Этот столбец заполняется значениями, передаваемыми приложением, а не отображаемым именем программы.|10|Да|  
|BigintData1|`bigint`|Порядковый номер сообщения.|52|Нет|  
|ClientProcessID|`int`|Идентификатор, присвоенный компьютером сервера процессу, в котором работает клиентское приложение. Этот столбец данных заполняется в том случае, если клиент вводит идентификатор клиентского процесса.|9|Да|  
|DatabaseID|`int`|Идентификатор базы данных, указанной в инструкции USE *database* , или базы данных по умолчанию, если для данного экземпляра инструкция USE *database*не выполнялась. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] отображает имя базы данных, если столбец данных «Имя сервера» захвачен при трассировке и сервер доступен. Определите значение для базы данных, используя функцию DB_ID.|3|Да|  
|DatabaseName|`nvarchar`|Имя базы данных, в которой выполняется инструкция пользователя.|35|Да|  
|DBUserName|`nvarchar`|Идентификатор экземпляра брокера, отправившего это сообщение.|40|Нет|  
|Ошибка|`int`|Идентификатор сообщения в sys.messages для текста в событии.|31|Нет|  
|EventClass|`int`|Тип захваченного класса событий. Всегда равен 191 для Broker:Forwarded Message Dropped.|27|Нет|  
|EventSequence|`int`|Порядковый номер этого события.|51|Нет|  
|FileName|`nvarchar`|Имя службы, для которой предназначено сообщение.|36|Нет|  
|GUID|`uniqueidentifier`|Идентификатор диалога. Этот идентификатор передается в составе сообщения и является общим для обоих участников диалога.|54|Нет|  
|HostName|`nvarchar`|Имя компьютера, на котором выполняется клиентская программа. Заполнение этого столбца данных производится в том случае, если клиент предоставляет имя узла. Чтобы определить имя узла, используйте функцию HOST_NAME.|8|Да|  
|IndexID|`int`|Число прыжков, оставшихся у перенаправленного сообщения.|24|Нет|  
|IntegerData|`int`|Номер фрагмента перенаправленного сообщения.|25|Нет|  
|LoginSid|`image`|Идентификатор безопасности вошедшего в систему пользователя. Значение идентификатора безопасности уникально для каждого имени входа на сервере.|41|Да|  
|NTDomainName|`nvarchar`|Домен Windows, к которому принадлежит пользователь.|7|Да|  
|NTUserName|`nvarchar`|Имя пользователя, которому принадлежит соединение, создавшее это событие.|6|Да|  
|ObjectId|`int`|Оставшееся время существования перенаправленного сообщения.|22|Нет|  
|ObjectName|`nvarchar`|Идентификатор перенаправленного сообщения.|34|Нет|  
|OwnerName|`nvarchar`|Идентификатор экземпляра брокера, которому направлено сообщение.|37|Нет|  
|RoleName|`nvarchar`|Роль дескриптора диалога. Может принимать одно из следующих значений.<br /><br /> Инициатор. Данный брокер начал диалог.<br /><br /> Цель. Данный брокер является назначением диалога.|38|Нет|  
|ServerName|`nvarchar`|Имя экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , подвергаемого трассировке.|26|Нет|  
|Severity|`int`|Уровень серьезности для текста в событии.|29|Нет|  
|SPID|`int`|Идентификатор процесса сервера, который [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] присвоил процессу, связанному с клиентом.|12|Да|  
|StartTime|`datetime`|Время начала события, если доступно.|14|Да|  
|State|`int`|Указывает место в исходном коде [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которое вызвало это событие. Каждое место, которое может вызвать это событие, обозначается отдельным кодом состояния. Сотрудник службы технической поддержки Microsoft может использовать этот код состояния для обнаружения участка, выполнение которого привело к событию.|30|Нет|  
|Success|`int`|Текущее время существования сообщения. Если это значение больше или равно времени жизни сообщения, то сообщение удаляется.|23|Нет|  
|TargetLoginName|`nvarchar`|Сетевой адрес, на который переадресовано данное сообщение.|42|Нет|  
|TargetUserName|`nvarchar`|Имя вызывающей службы для сообщения.|39|Нет|  
|TextData|`ntext`|Описание причины удаления сообщения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|1|Да|  
|Transaction ID|`bigint`|Назначенный системой идентификатор транзакции.|4|Нет|  
  
 Столбец TextData данного события содержит описание причины удаления сообщения, выполненного [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>См. также  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
