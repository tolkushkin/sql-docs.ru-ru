---
title: sys.conversation_groups (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_groups_TSQL
- conversation_groups
- sys.conversation_groups
- sys.conversation_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_groups catalog view
ms.assetid: 3f35815e-2de4-42a2-a972-8f0141dad0b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01e6e1d47061f445d7aa7d53fb548a2ebfcaefd6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049866"
---
# <a name="sysconversationgroups-transact-sql"></a>sys.conversation_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Это представление каталога содержит по одной строке для каждой группы сообщений.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**conversation_group_id**|**uniqueidentifier**|Идентификатор группы сообщений. Не допускает значения NULL.|  
|**service_id**|**int**|Идентификатор службы для диалогов в этой группе. Не допускает значения NULL.|  
|**is_system**|**bit**|Указывает на принадлежность или отсутствие принадлежности к системному экземпляру. Допускает значение NULL.|  
  
## <a name="permissions"></a>Разрешения  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
