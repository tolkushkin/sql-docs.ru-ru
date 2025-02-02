---
title: Динамические административные представления (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], about dynamic management objects
- server state information [SQL Server]
- dynamic management functions [SQL Server]
- metadata [SQL Server], dynamic management objects
- dynamic management views [SQL Server]
- DMVs [SQL Server]
- functions [SQL Server], dynamic management
- server scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server]
ms.assetid: cf893ecb-0bf6-4cbf-ac00-8a1099e405b1
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1a61d3826cd7a4421eb621d549dfc49155ddadd0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740424"
---
# <a name="system-dynamic-management-views"></a>Системные динамические административные представления
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Динамические административные представления и функции возвращают данные о состоянии сервера, которые могут использоваться для контроля исправности экземпляра сервера, диагностики проблем и настройки производительности.  
  
> [!IMPORTANT]  
>  Динамические административные представления и функции возвращают внутренние данные о состоянии, зависящие от реализации. Возвращаемые ими схемы и данные могут быть изменены в будущих выпусках сервера [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Поэтому в будущих выпусках динамические административные представления и функции могут быть несовместимы с динамическими административными представлениями и функциями сервера в этой версии. Например, в будущих версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] определение любого динамического административного представления может быть расширено путем добавления столбцов в конец списка столбцов. Из-за того что число возвращаемых столбцов может измениться и нарушить работу приложения, использование синтаксиса `SELECT * FROM dynamic_management_view_name` в конечном коде не рекомендуется.  
  
 Есть два типа динамических административных представлений и функций:  
  
-   динамические административные представления и функции области сервера. Для них необходимо разрешение VIEW SERVER STATE на сервере;  
  
-   динамические административные представления и функции области базы данных. Для них необходимо разрешение VIEW DATABASE STATE на базе данных.  
  
## <a name="querying-dynamic-management-views"></a>Запросы к динамическим административным представлениям  
 Ссылки на динамические административные представления в инструкциях языка [!INCLUDE[tsql](../../includes/tsql-md.md)] могут выполняться при помощи имен, состоящих из двух, трех и четырех частей. А ссылки на динамические административные функции в инструкциях языка [!INCLUDE[tsql](../../includes/tsql-md.md)] могут выполняться при помощи двух- или трехкомпонентных имен. Ссылаться на динамические административные представления и функции в инструкциях языка [!INCLUDE[tsql](../../includes/tsql-md.md)] с помощью однокомпонентных имен нельзя.  
  
 Все динамические административные представления и функции существуют в схеме sys и следуют соглашению по именованию следующего вида: dm_*. При использовании динамического административного представления или функции перед именем представления или функции должен стоять префикс схемы sys. Например, для запроса к динамическому административному представлению dm_os_wait_stats выполните следующие инструкции:  
  
 ```sql
SELECT wait_type, wait_time_ms  
FROM sys.dm_os_wait_stats;  
```  
  
### <a name="required-permissions"></a>Необходимые разрешения  
 Для выполнения запроса к динамическому административному представлению и функции необходимо разрешение SELECT на объект, а также разрешения VIEW SERVER STATE или VIEW DATABASE STATE. Тем самым обеспечивается выборочное ограничение доступа пользователя или имени входа к динамическим административным представлениям и функциям. Для этого вначале создайте в базе данных master учетную запись пользователя, а затем запретите для пользователя разрешение SELECT на динамические административные представления и функции, на которые не хотите предоставлять доступ этому пользователю. После этого пользователь не сможет делать выборку из этих представлений и результатов функций независимо от контекста базы данных пользователя.  
  
> [!NOTE]  
>  Так как инструкция DENY имеет более высокий приоритет, если пользователю было предоставлено разрешение VIEW SERVER STATE, но был запрет на разрешение VIEW DATABASE STATE, пользователь сможет получать данные области сервера, но не базы данных.  
  
## <a name="in-this-section"></a>в этом разделе  
 Динамические административные представления и функции организованы в следующие категории:  
  
|||  
|-|-|  
|[Группах доступности AlwaysOn, динамические административные представления и функции (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)|[Оптимизированные для памяти динамические административные представления таблиц &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)|  
|[Динамические административные представления, связанные с системой отслеживания измененных данных (Transact-SQL)](change-data-capture-sys-dm-cdc-errors.md)|[Динамические административные представления и функции, связанные с объектом &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Динамические административные представления, связанные с отслеживания изменений](change-tracking-sys-dm-tran-commit-table.md)|[Запрос уведомления динамические административные представления &#40;Transact-SQL&#41;](query-notifications-sys-dm-qn-subscriptions.md)|  
|[Динамические административные представления, связанные с среда CLR &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)|[Динамические административные представления, связанные с репликацией &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)|  
|[Динамические административные представления зеркального отображения базы данных &#40;Transact-SQL&#41;](database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)|[Динамические административные представления, связанные с регулятора ресурсов &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)|  
|[Динамические административные представления, относящиеся к базе данных &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)|[Динамические представления управления и функции, связанные с безопасностью (Transact-SQL)](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Динамические административные представления и функции, связанные с выполнением (Transact-SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)|[Динамические административные представления и функции, связанные с сервером (Transact-SQL)](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Динамические административные представления расширенных событий](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)|[Динамические административные представления, связанные с компонентом Service Broker (Transact-SQL)](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)|  
|[FileStream и FileTable динамические административные представления &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)|[Динамические административные представления и функции, связанные с пространственными данными &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/c542ac38-451f-43a5-bf8c-4edd38bb738e)|  
|[Компонент Full-Text Search и семантический поиск динамические административные представления и функции &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)|[Хранилище данных SQL и параллельные хранилища данных динамические административные представления &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)|  
|[Георепликация динамические административные представления и функции &#40;база данных Azure SQL&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)|[Динамические административные представления, относящиеся к операционной системе SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)|  
|[Динамические административные представления и функции индекса &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)|[Stretch Database динамические административные представления &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/1193efce-a105-49a9-a8b8-26b063485567)|  
|[Ввод-вывод связанные динамические административные представления и функции &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)|[Динамические административные представления и функции, связанные с транзакциями (Transact-SQL)](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)|  

  
## <a name="see-also"></a>См. также  
 [Предоставление разрешений Server &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)   
 [GRANT, предоставление разрешений на базу данных (Transact-SQL)](../../t-sql/statements/grant-database-permissions-transact-sql.md)   
 [Системные представления &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
