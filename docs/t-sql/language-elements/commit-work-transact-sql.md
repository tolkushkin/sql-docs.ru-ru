---
title: COMMIT WORK (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMMIT_WORK_TSQL
- WORK_TSQL
- WORK
- COMMIT WORK
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- COMMIT WORK statement
ms.assetid: 4de76f33-399e-4912-a617-6eb6c560a058
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 342d6a2ca2ea51de4e9f887acd39a829713fe275
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2019
ms.locfileid: "65982675"
---
# <a name="commit-work-transact-sql"></a>COMMIT WORK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Обозначает завершение транзакции.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
COMMIT [ WORK ]  
[ ; ]  
```  
  
## <a name="remarks"></a>Remarks  
 Эта инструкция действует идентично инструкции COMMIT TRANSACTION, но в отличие от COMMIT TRANSACTION не принимает пользовательское имя транзакции. С указанием или без указания дополнительного ключевого слова WORK этот синтаксис COMMIT совместим с SQL-92.  
  
## <a name="see-also"></a>См. также:  
 [BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION (Transact-SQL)](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK (Transact-SQL)](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION (Transact-SQL)](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
