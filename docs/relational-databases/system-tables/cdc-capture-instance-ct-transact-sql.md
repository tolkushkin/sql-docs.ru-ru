---
title: CDC. &lt;capture_instance&gt;_CT (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc
- cdc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.<capture_instance>_CT
ms.assetid: 979c8110-3c54-4e76-953c-777194bc9751
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 346fea411891f04e4b4742ff50c2dd9cce6f1587
ms.sourcegitcommit: 4c053cd2f15968492a3d9e82f7570dc2781da325
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2018
ms.locfileid: "49336253"
---
# <a name="cdcltcaptureinstancegtct-transact-sql"></a>CDC. &lt;capture_instance&gt;_CT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Таблица изменений, созданная при включении системы отслеживания измененных данных в исходной таблице. Эта таблица содержит по одной строке для каждой операции вставки и удаления в исходной таблице и по две строки для каждой операции обновления в исходной таблице. Если имя таблицы изменений не задано при включении исходной таблицы, создается производное имя. Формат имени — cdc. *capture_instance*_CT где *capture_instance* является именем схемы исходной таблицы и имени исходной таблицы в формате *схема_таблица*. Например если таблицы **Person.Address** в **AdventureWorks** образца базы данных включен для измененных данных, производным именем таблицы изменений будет **cdc. Person_Address_CT**.  
  
 Мы рекомендуем вам **не запрашивать системные таблицы непосредственно**. Вместо этого выполните [cdc.fn_cdc_get_all_changes_ < экземпляр_отслеживания >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) и [cdc.fn_cdc_get_net_changes_ < экземпляр_отслеживания >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) функции.  
  

  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|Регистрационный номер транзакции в журнале (LSN), связанный с фиксацией транзакции изменения.<br /><br /> Все изменения, зафиксированные в одной транзакции, имеют общий номер LSN фиксации. Например, если операции удаления в исходной таблице удаляет две строки, таблица изменений будет содержать две строки, с одинаковым **__ $start_lsn** значение.|  
|**__ $end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> В [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] этот столбец всегда имеет значение NULL.|  
|**__$seqval**|**binary(10)**|Значение последовательности, используемое для упорядочивания изменений строк в пределах транзакции.|  
|**__$operation**|**int**|Определяет операцию языка обработки данных (DML), связанную с изменением. Возможен один из следующих вариантов.<br /><br /> 1 = удаление<br /><br /> 2 = вставка<br /><br /> 3 = обновление (старые значения)<br /><br /> Перед выполнением инструкции обновления в данных столбца содержатся эти значения строк.<br /><br /> 4 = обновление (новые значения)<br /><br /> После выполнения инструкции обновления в данных столбца содержатся эти значения строк.|  
|**__$update_mask**|**varbinary(128)**|Битовая маска, основанная на порядковых номерах измененных столбцов в таблице изменений.|  
|*\<отслеживаемые столбцы исходной таблицы>*|непостоянно|Остальные столбцы в таблице изменений — это столбцы из исходной таблицы, определенные, как отслеживаемые при создании экземпляра отслеживания. Если в списке отслеживаемых столбцов не указано ни одного столбца, в эту таблицу включаются все столбцы из исходной таблицы.|  
|**__ $command_id** |**int** |Отслеживает порядок операций в рамках транзакции. |  
  
## <a name="remarks"></a>Примечания  

`__$command_id` Столбец был столбец был введен в накопительный пакет обновления в версии 2012 по 2016. Для получения сведений о версии и загрузки см. в статье базы Знаний 3030352 в [исправление: таблицы изменений упорядочен неправильно для обновления записи строк после включения измененных данных для базы данных Microsoft SQL Server](https://support.microsoft.com/help/3030352/fix-the-change-table-is-ordered-incorrectly-for-updated-rows-after-you).  Дополнительные сведения см. в разделе [CDC функциональные возможности могут работать неправильно после обновления до новейший пакет CU для SQL Server 2012, 2014 и 2016](https://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/).

## <a name="captured-column-data-types"></a>Типы данных отслеживаемых столбцов  
 Отслеживаемые столбцы, включенные в эту таблицу, имеют те же типы данных и значения, что и соответствующие им столбцы в исходной таблице, за следующими исключениями.  
  
-   **Метка времени** столбцы определяются как **binary(8)**.  
  
-   **Удостоверение** столбцы определяются как **int** или **bigint**.  
  
 Однако значения этих столбцов совпадают со значениями столбцов в исходной таблице.  
  
### <a name="large-object-data-types"></a>Типы данных больших объектов  
 Столбцы типа данных **изображение**, **текст**, и **ntext** всегда назначаются **NULL** значение, если __ $operation = 1 или \_ \_$operation = 3. Столбцы типа данных **varbinary(max)**, **varchar(max)**, или **nvarchar(max)** назначаются **NULL** значения при \_ \_$operation = 3, если столбец изменен во время обновления. Когда \_ \_$operation = 1, этим столбцам присваиваются их значения во время удаления. Вычисляемые столбцы, которые включены в экземпляре отслеживания, всегда имеют значение **NULL**.  
  
 По умолчанию максимальный объем данных, которые можно добавить в столбец, отслеженный с помощью одной инструкции INSERT, UPDATE, WRITETEXT или UPDATETEXT, не должен превышать 65 536 байт или 64 КБ. Чтобы увеличить этот объем для поддержки большего размера данных LOB, используйте [Настройка параметра конфигурации сервера max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md) для указания больший максимальный размер. Дополнительные сведения см. в статье [Настройка параметра конфигурации сервера max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md).  
  
## <a name="data-definition-language-modifications"></a>Изменения, внесенные с помощью языка DDL  
 Изменения DDL в исходной таблице, например добавление или удаление столбцов, записываются в [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) таблицы. Эти изменения не применяются к таблице изменений. То есть определение таблицы изменений остается постоянным. При вставке строк в таблицу изменений процесс отслеживания не учитывает столбцы, которые не появляются в списке отслеживаемых столбцов, связанных с исходной таблицей. Если в списке отслеживаемых столбцов появляется столбец, больше не присутствующий в исходной таблице, этому столбцу присваивается значение NULL.  
  
 Изменение типа данных столбца в исходной таблице, также сохраняется в [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md) таблицы. Тем не менее, это изменение не затрагивает определение таблицы изменений. Тип данных отслеживаемого столбца в таблице изменений меняется, если процесс отслеживания найдет запись журнала, относящуюся к изменению на языке DDL, внесенному в исходную таблицу.  
  
 Если нужно изменить тип данных отслеживаемого столбца в исходной таблице способом, который сократил бы размер этого типа данных, используется следующая процедура, которая обеспечивает успешное изменение соответствующего столбца в таблице изменений.  
  
1.  В исходной таблице обновите значения изменяемого столбца, чтобы они соответствовали нужному размеру типа данных. Например, если вы измените тип данных с **int** для **smallint**, обновите значения до размера, который помещается в **smallint** диапазон "," – 32 768 до 32 767.  
  
2.  В таблице изменений выполните такую же операцию обновления в эквивалентном столбце.  
  
3.  Измените исходную таблицу, задав новый тип данных. Изменение типа данных распространяется на таблицу изменений.  
  
## <a name="data-manipulation-language-modifications"></a>Изменения, внесенные с помощью языка обработки данных  
 При выполнении операций вставки, обновления и удаления в исходной таблице с включенной системой отслеживания измененных данных записи об этих операциях DML фиксируются в журнале транзакций базы данных. Процесс системы отслеживания измененных данных получает сведения об этих изменениях из журнала транзакций и добавляет одна или две строки в таблицу изменений для регистрации изменения. Записи добавляются в таблицу изменений в том же порядке, в каком они были зафиксированы в исходной таблице, однако фиксация записей таблицы изменений, как правило, выполняется для группы изменений, а не для отдельной записи.  
  
 В записи таблицы изменений **__ $start_lsn** столбец используется для записи зафиксированный номер LSN, связанный с изменением в исходной таблице и **столбец __ $seqval** используется для определения порядка изменения в свою транзакцию. С помощью этих столбцов метаданных в совокупности можно обеспечить сохранность порядка фиксации исходных изменений. Поскольку сведения об изменениях в процессе отслеживания извлекаются из журнала транзакций, важно отметить, что записи таблицы изменений не отображаются синхронно с соответствующими изменениями в исходной таблице. Вместо этого, такие изменения отображаются асинхронно после того, как процессом отслеживания обработаны соответствующие записи об изменениях из журнала транзакций.  
  
 Для операций вставки и удаления устанавливаются все биты в маске обновления. Для операций обновления маска обновления как в старой строке обновления, так и в новой меняется, чтобы отразить столбцы, изменившиеся во время обновления.  
  
## <a name="see-also"></a>См. также  
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)  
  
  
