---
title: sp_help_fulltext_catalogs_cursor (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_cursor
- sp_help_fulltext_catalogs_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs_cursor
ms.assetid: d44478d1-0cc4-415e-9d1a-6dccb64674fa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 29bb5d24681ec159e6663080c7c15c0a67a73fc7
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983074"
---
# <a name="sphelpfulltextcatalogscursor-transact-sql"></a>sp_help_fulltext_catalogs_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Использует курсор для возвращения идентификатора, имени, корневого каталога, состояния и числа полнотекстовых индексированных таблиц для заданного полнотекстового каталога.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Используйте [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) вместо этого представление каталога.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_help_fulltext_catalogs_cursor [ @cursor_return= ] @cursor_variable OUTPUT ,   
     [ @fulltext_catalog_name = ] 'fulltext_catalog_name'   
```  
  
## <a name="arguments"></a>Аргументы  
`[ @cursor_return = ] @cursor_variable OUTPUT` Выходная переменная типа **курсор**. Этот курсор является динамическим, прокручиваемым и доступным только для чтения.  
  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'` — Имя полнотекстового каталога. *fulltext_catalog_name* — **sysname**. Если этот параметр упущен или равен NULL, возвращаются сведения обо всех полнотекстовых каталогах ассоциированных с текущей базой данных.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|Идентификатор полнотекстового каталога.|  
|**ИМЯ**|**sysname**|Имя полнотекстового каталога.|  
|**PATH**|**nvarchar(260)**|Начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], это предложение не оказывает влияние на работу системы.|  
|**СОСТОЯНИЕ**|**int**|Состояние заполнения полнотекстового индекса каталога:<br /><br /> 0 = бездействие<br /><br /> 1 = идет полное заполнение<br /><br /> 2 = пауза<br /><br /> 3 = ограниченный режим<br /><br /> 4 = восстановление<br /><br /> 5 = выключение<br /><br /> 6 = идет добавочное заполнение<br /><br /> 7 = построение индекса<br /><br /> 8 = диск заполнен. Пауза<br /><br /> 9 = отслеживание изменений.|  
|**NUMBER_FULLTEXT_TABLES**|**int**|Число полнотекстовых индексированных таблиц, связанных с каталогом.|  
  
## <a name="permissions"></a>Разрешения  
 Разрешения на выполнение по умолчанию принадлежат роли **public** .  
  
## <a name="examples"></a>Примеры  
 В следующем примере возвращаются сведения о полнотекстовом каталоге `Cat_Desc`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_catalogs_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>См. также  
 [FULLTEXTCATALOGPROPERTY (Transact-SQL)](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
