---
title: Параметр конфигурации сервера "server trigger recursion" | Документы Майкрософт
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- recursive triggers [SQL Server]
- triggers [SQL Server], recursive
- server trigger recursion option
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 115d9dde071579c196b115cbe93779145c20a43e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794120"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>Параметр конфигурации сервера «server trigger recursion»
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Параметр **server trigger recursion** предназначен для указания того, допускается ли рекурсивное срабатывание триггеров уровня сервера. Если этот параметр установлен в значение 1 (включено), рекурсивное срабатывание триггеров уровня сервера разрешено. Если он установлен в значение 0 (выключено), рекурсивное срабатывание триггеров уровня сервера не допускается. Установка этого параметра в 0 (выключено) предотвращает только прямую рекурсию при срабатывании триггеров (Чтобы отключить косвенную рекурсию, установите в значение 0 параметр **nested triggers**.) Значение по умолчанию для данного параметра равно 1 (включено). Параметр вступает в силу немедленно, без перезапуска сервера.  
  
 Дополнительные сведения см. в разделе [Создание вложенных триггеров](../../relational-databases/triggers/create-nested-triggers.md).  
  
## <a name="see-also"></a>См. также:  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
