---
title: sp_syscollector_create_collection_item (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_item
- sp_syscollector_create_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collection_item
- data collector [SQL Server], stored procedures
ms.assetid: 60dacf13-ca12-4844-b417-0bc0a8bf0ddb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1e155fb51bd5f78a3c4a639e9233746131ddf6f5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004145"
---
# <a name="spsyscollectorcreatecollectionitem-transact-sql"></a>sp_syscollector_create_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Создает элемент сбора в определяемом пользователем наборе сбора. Элемент сбора определяет, какие данные должны собираться, а также частоту их сбора.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_syscollector_create_collection_item   
      [ @collection_set_id = ] collection_set_id   
    , [ @collector_type_uid = ] 'collector_type_uid'  
    , [ @name = ] 'name'   
    , [ [ @frequency = ] frequency ]  
    , [ @parameters = ] 'parameters'  
    , [ @collection_item_id = ] collection_item_id OUTPUT  
```  
  
## <a name="arguments"></a>Аргументы  
 [ @collection_set_id = ] *collection_set_id*  
 Уникальный локальный идентификатор набора элементов сбора. *collection_set_id* — **int**.  
  
 [ @collector_type_uid = ] '*collector_type_uid*'  
 Идентификатор GUID, идентифицирующий тип сборщика, используемый для этого элемента *аргумент collector_type_uid* — **uniqueidentifier** без значения по умолчанию... Чтобы получить список типов сборщиков, выполните запрос системного представления syscollector_collector_types.  
  
 [ @name =] '*имя*"  
 Имя элемента сбора. *имя* — **sysname** и не может быть пустой строкой или NULL.  
  
 *имя* должно быть уникальным. Чтобы получить список имен элементов текущего сбора, выполните запрос системного представления syscollector_collection_items.  
  
 [ @frequency =] *частота*  
 Используется для указания времени (в секундах), определяющего, насколько часто этот элемент сбора собирает данные. *частота* — **int**, значение по умолчанию 5. Минимальное значение, которое можно указать, составляет 5 секунд.  
  
 Если набор сбора настроен на режим без кэширования, частота не учитывается, поскольку этот режим предусматривает выполнение сбора данных и передачу по расписанию, указанному для набора сбора. Чтобы просмотреть режим сбора набора элементов сбора, запросите [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) системное представление.  
  
 [ @parameters =] '*параметры*"  
 Входные параметры для типа сборщика. *Параметры* — **xml** значение по умолчанию NULL. *Параметры* схемы должны совпадать со схемой параметров типа сборщика.  
  
 [ @collection_item_id =] *collection_item_id*  
 Уникальный идентификатор, определяющий элемент элементов набора. *collection_item_id* — **int** и у выходные данные.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="remarks"></a>Примечания  
 Функция sp_syscollector_create_collection_item должна выполняться в контексте системной базы данных msdb.  
  
 Набор сбора, в который добавляется элемент сбора, необходимо остановить перед созданием элемента сбора. Добавлять элементы сбора в системные наборы сбора невозможно.  
  
## <a name="permissions"></a>Разрешения  
 Для выполнения этой процедуры требуется членство в предопределенной роли базы данных dc_admin (с разрешением EXECUTE).  
  
## <a name="examples"></a>Примеры  
 В следующем примере элемент сбора создается на основе типа сборщика `Generic T-SQL Query Collector Type` и добавляется в набор сбора `Simple collection set test 2`. Создание коллекции указанного набора, выполните пример Б в [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
```  
USE msdb;  
GO  
DECLARE @collection_item_id int;  
DECLARE @collection_set_id int = (SELECT collection_set_id   
                                  FROM syscollector_collection_sets  
                                  WHERE name = N'Simple collection set test 2');  
DECLARE @collector_type_uid uniqueidentifier =   
    (SELECT collector_type_uid  
     FROM syscollector_collector_types  
     WHERE name = N'Generic T-SQL Query Collector Type');  
DECLARE @params xml =   
    CONVERT(xml, N'\<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
                <Value>SELECT * FROM sys.objects</Value>  
                <OutputTable>MyOutputTable</OutputTable>  
            </Query>  
            <Databases>   
                <Database> UseSystemDatabases = "true"   
                           UseUserDatabases = "true"  
                </Database>  
            </Databases>  
         \</ns:TSQLQueryCollector>');  
  
EXEC sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid,  
    @name = 'My custom TSQL query collector item',  
    @frequency = 6000,  
    @parameters = @params,  
    @collection_item_id = @collection_item_id OUTPUT;  
```  
  
## <a name="see-also"></a>См. также  
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Сбор данных](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)   
 [sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)   
 [syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)   
 [функция sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)   
 [syscollector_collection_items (Transact-SQL)](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
