---
title: Настройка зашифрованной зеркальной базы данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- cryptography [SQL Server], database mirroring
- encryption [SQL Server], database mirroring
- database master key [SQL Server], database mirroring
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 932564950db75223993567374693cd0549b05172
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795215"
---
# <a name="set-up-an-encrypted-mirror-database"></a>Настройка зашифрованной зеркальной базы данных
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Чтобы включить автоматическое шифрование главного ключа базы данных зеркальной базы данных, необходимо предоставить пароль, используемый для шифрования главного ключа экземпляра зеркального сервера. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздние версии включают в себя механизмы для передачи пароля. Перед началом зеркального отображения базы данных необходимо создать учетные данные для главного ключа базы данных с помощью хранимой процедуры **sp_control_dbmasterkey_password** . Необходимо повторить этот процесс для каждой базы данных, для которой будет создаваться зеркальное отображение. Дополнительные сведения см. в разделе [sp_control_dbmasterkey_password (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md).  
  
> [!CAUTION]  
>  Не включайте дешифрование базы данных отработки отказа, оно не должно быть для **sa** и другим серверам-участникам с обширными правами доступа. База данных может быть настроена таким образом, чтобы иерархия ее ключей не могла быть расшифрована главным ключом службы. Эта возможность поддерживается для максимальной защиты баз данных, содержащих информацию, доступ к которой не может иметь **sa** или другие участники на уровне сервера с обширными правами доступа. Включение расшифровки отработки отказа для такой базы данных сводит на нет эту защиту, позволяя **sa** и другим привилегированным участникам на уровне сервера расшифровывать базу данных.  
  
## <a name="see-also"></a>См. также:  
 [sp_control_dbmasterkey_password (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [Иерархия средств шифрования](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Настройка зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
  
  
