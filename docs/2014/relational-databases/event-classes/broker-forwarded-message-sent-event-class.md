---
title: Класс событий Broker:Forwarded Message Sent | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Forwarded Message Sent event class
ms.assetid: d0ef74d9-a4ef-4918-aa21-6b267e85569f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 51784663fdfec66f851bed479184ae21170a3681
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664020"
---
# <a name="brokerforwarded-message-sent-event-class"></a>Broker:Forwarded Message Sent, класс событий
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] формирует событие класса Broker:Forwarded Message Sent, когда компонент Service Broker перенаправляет сообщение.  
  
## <a name="brokerforwarded-message-sent-event-class-data-columns"></a>Столбцы данных класса событий Broker:Forwarded Message Sent  
  
|Столбец данных|Тип|Описание|Номер столбца|Фильтруемый|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|Имя клиентского приложения, установившего соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Этот столбец заполняется значениями, передаваемыми приложением, а не отображаемым именем программы.|10|Да|  
|BigintData1|`bigint`|Порядковый номер сообщения.|52|Нет|  
|ClientProcessID|`int`|Идентификатор, присвоенный компьютером сервера процессу, в котором работает клиентское приложение. Этот столбец данных заполняется в том случае, если клиент вводит идентификатор клиентского процесса.|9|Да|  
|DatabaseID|`int`|Идентификатор базы данных, указанной в инструкции USE *database* , или базы данных по умолчанию, если для данного экземпляра инструкция USE *database*не выполнялась. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] отображает имя базы данных, если столбец данных «Имя сервера» захвачен при трассировке и сервер доступен. Определите значение для базы данных, используя функцию DB_ID.|3|Да|  
|DBUserName|`nvarchar`|Идентификатор экземпляра посредника для службы, отправившей сообщение.|40|Нет|  
|EventClass|`int`|Тип захваченного класса событий. Для класса событий Broker:Forwarded Message Sent всегда равен 139.|27|Нет|  
|EventSequence|`int`|Порядковый номер этого события.|51|Нет|  
|FileName|`nvarchar`|Имя службы, для которой предназначено сообщение.|36|Нет|  
|GUID|`uniqueidentifier`|Идентификатор диалога. Этот идентификатор передается в составе сообщения и является общим для обоих участников диалога.|54|Нет|  
|HostName|`nvarchar`|Имя компьютера, на котором выполняется клиентская программа. Заполнение этого столбца данных производится в том случае, если клиент предоставляет имя узла. Чтобы определить имя узла, используйте функцию HOST_NAME.|8|Да|  
|IndexID|`int`|Число прыжков, оставшихся у перенаправленного сообщения.|24|Нет|  
|IntegerData|`int`|Номер фрагмента перенаправленного сообщения.|25|Нет|  
|IsSystem|`int`|Указывает, произошло событие в системном или в пользовательском процессе. 1 = системный, 0 = пользовательский.|60|Нет|  
|LoginSid|`image`|Идентификатор безопасности вошедшего в систему пользователя. Значение идентификатора безопасности уникально для каждого имени входа на сервере.|41|Да|  
|NTDomainName|`nvarchar`|Домен Windows, к которому принадлежит пользователь.|7|Да|  
|NTUserName|`nvarchar`|Имя пользователя, которому принадлежит соединение, создавшее это событие.|6|Да|  
|ObjectId|`int`|Значение оставшегося времени жизни перенаправленного сообщения на момент перенаправления.|22|Нет|  
|ObjectName|`nvarchar`|Идентификатор перенаправленного сообщения.|34|Нет|  
|OwnerName|`nvarchar`|Идентификатор посредника, которому направлено сообщение.|37|Нет|  
|RoleName|`nvarchar`|Роль дескриптора диалога. Может принимать одно из следующих значений.<br /><br /> Инициатор. Данный брокер начал диалог.<br /><br /> Цель. Данный брокер является назначением диалога.|38|Нет|  
|ServerName|`nvarchar`|Имя экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , подвергаемого трассировке.|26|Нет|  
|SPID|`int`|Идентификатор процесса сервера, который [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] присвоил процессу, связанному с клиентом.|12|Да|  
|StartTime|`datetime`|Время начала события, если доступно.|14|Да|  
|Success|`int`|Количество времени, затраченного на процесс перенаправления.|23|Нет|  
|TargetLoginName|`nvarchar`|Сетевой адрес, по которому экземпляр отправляет сообщение. Обратите внимание, что он может отличаться от конечного места назначения сообщения.|42|Нет|  
|TargetUserName|`nvarchar`|Имя вызывающей службы для сообщения.|39|Нет|  
|TransactionID|`bigint`|Назначенный системой идентификатор транзакции.|4|Нет|  
  
  
