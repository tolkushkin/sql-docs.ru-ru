---
title: sys.database_event_session_actions (база данных SQL Azure) | Документация Майкрософт
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 32494df1-7ab7-4b88-a858-6b1021d67433
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da64525978a5655df1832d70959929d6221c9a7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936324"
---
# <a name="sysdatabaseeventsessionactions-azure-sql-database"></a>sys.database_event_session_actions (база данных SQL Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Возвращает строку для каждого действия над каждым событием из сеанса событий.  
  
||  
|-|  
|**Область применения**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] До версии 12 и любые более поздние версии.|  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Идентификатор сеанса событий. Не допускает значение NULL.|  
|event_id|**int**|Идентификатор события. Этот идентификатор уникален внутри объекта сеанса событий. Не допускает значение NULL.|  
|name|**sysname**|Имя действия. Допускает значение NULL.|  
|пакет|**sysname**|Имя пакета событий, который содержит событие. Допускает значение NULL.|  
|module|**sysname**|Имя модуля, который содержит событие. Допускает значение NULL.|  
  
## <a name="permissions"></a>Разрешения  
 Необходимо разрешение VIEW DATABASE STATE на сервере.  
  
## <a name="remarks"></a>Примечания  
 Это представление имеет следующее количество элементов связей.  
  
||||  
|-|-|-|  
|От|Чтобы|Связь|  
|sys.database_event_session_actions.event_session_id|sys.sys.database_event_sessions.event_session_id|Многие к одному|  
|sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions.event_session_id|sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events.event_id|Многие к одному|  
  
  
