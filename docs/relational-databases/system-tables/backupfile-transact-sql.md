---
title: backupfile (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupfile
- backupfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- file backups [SQL Server], backupfile system table
- backupfile system table
ms.assetid: f1a7fc0a-f4b4-47eb-9138-eebf930dc9ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed2f40b2ea4f711c36a3c17031047fef555ab12a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62645509"
---
# <a name="backupfile-transact-sql"></a>backupfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Содержит по одной строке для всех данных или файла журнала базы данных. Столбцы описывают конфигурацию файла, существовавшую во время создания резервной копии. Определяется ли файл включен в резервную копию **is_present** столбца. Эта таблица хранится в **msdb** базы данных.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|Уникальный идентификационный номер файла, содержащего набор данных с резервной копией. Ссылки на **backupset(backup_set_id)**.|  
|**first_family_number**|**tinyint**|Семейный номер первого носителя, содержащего данный файл резервной копии. Может иметь значение NULL.|  
|**first_media_number**|**smallint**|Номер носителя для первого носителя, содержащего данный файл резервной копии. Может иметь значение NULL.|  
|**filegroup_name**|**nvarchar(128)**|Имя файловой группы, содержащей резервную копию файла базы данных. Может иметь значение NULL.|  
|**page_size**|**int**|Размер страницы в байтах.|  
|**file_number**|**numeric(10,0)**|Идентификационный номер файла уникален в пределах базы данных (соответствует **sys.database_files**. **file_id**).|  
|**backed_up_page_count**|**numeric(10,0)**|Количество страниц, для которых были созданы резервные копии. Может иметь значение NULL.|  
|**file_type**|**char(1)**|Была создана резервная копия одного из файлов:<br /><br /> D = файл данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)];<br /><br /> L = журнал [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)];<br /><br /> F = полнотекстовый каталог.<br /><br /> Может иметь значение NULL.|  
|**source_file_block_size**|**numeric(10,0)**|Устройство, на котором во время создания резервной копии хранились первоначальные данные или журнальный файл. Может иметь значение NULL.|  
|**file_size**|**numeric(20,0)**|Длина скопированного файла в байтах. Может иметь значение NULL.|  
|**logical_name**|**nvarchar(128)**|Логическое имя файла, резервная копия которого создана. Может иметь значение NULL.|  
|**physical_drive**|**nvarchar(260)**|Имя физического диска или секции. Может иметь значение NULL.|  
|**physical_name**|**nvarchar(260)**|Остаток имени физического файла (операционная система). Может иметь значение NULL.|  
|**state**|**tinyint**|Одно из следующих состояний файла.<br /><br /> 0 = ONLINE<br /><br /> 1 = RESTORING<br /><br /> 2 = RECOVERING<br /><br /> 3 = RECOVERY PENDING <br /><br /> 4 = SUSPECT<br /><br /> 6 = OFFLINE<br /><br /> 7 = DEFUNCT<br /><br /> 8 = УДАЛЕНЫ<br /><br /> Примечание. Значение 5 пропущено в том случае, так что эти значения соответствуют значениям для состояний базы данных.|  
|**state_desc**|**nvarchar(64)**|Одно из следующих описаний состояния файла.<br /><br /> ONLINE RESTORING <br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT OFFLINE DEFUNCT|  
|**create_lsn**|**numeric(25,0)**|Регистрационный номер в журнале, под которым был создан файл.|  
|**drop_lsn**|**numeric(25,0)**|Регистрационный номер в журнале, под которым файл был удален. Может иметь значение NULL.<br /><br /> Если файл не удален, установлено значение NULL.|  
|**file_guid**|**uniqueidentifier**|Уникальный идентификатор файла.|  
|**read_only_lsn**|**numeric(25,0)**|Регистрационный номер в журнале, под которым файловая группа, содержащая файл, изменила тип доступа с «для чтения и записи» на «только для чтения» (самое последнее изменение). Может иметь значение NULL.|  
|**read_write_lsn**|**numeric(25,0)**|Регистрационный номер транзакции в журнале, под которым файловая группа, содержащая файл, изменила тип с «только для чтения» на «для чтения и записи» (самое последнее изменение). Может иметь значение NULL.|  
|**differential_base_lsn**|**numeric(25,0)**|Основной регистрационный номер транзакции в журнале для разностного резервного копирования. Разностная резервная копия содержит только те экстенты данных, наличие последовательности журнала номер равным или больше, чем **differential_base_lsn**.<br /><br /> Для других типов резервных копий установлено значение NULL.|  
|**differential_base_guid**|**uniqueidentifier**|Для разностных резервных копий уникальный идентификатор самой последней резервной копии формирует базовую копию файлов для разностного копирования; если установлено значение NULL, то файл был включен в разностные резервные копии, но добавлен после создания базы.<br /><br /> Для других типов резервных копий установлено значение NULL.|  
|**backup_size**|**numeric(20,0)**|Размер резервной копии этого файла в байтах.|  
|**filegroup_guid**|**uniqueidentifier**|Идентификатор файловой группы. Чтобы найти информацию о файловой группе в таблице backupfilegroup, используйте **filegroup_guid** с **backup_set_id**.|  
|**is_readonly**|**bit**|1 = файл только для чтения.|  
|**is_present**|**bit**|1 = файл содержится в резервном наборе данных.|  
  
## <a name="remarks"></a>Примечания  
 Инструкция RESTORE VERIFYONLY FROM *устройство_резервного_копирования* WITH LOADHISTORY заполняет столбцы **backupmediaset** таблицу с соответствующими значениями из заголовка набора носителей.  
  
 Чтобы уменьшить число строк в данной таблице, а также в других резервных и таблицах журнала, выполните [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) хранимой процедуры.  
  
## <a name="see-also"></a>См. также  
 [Резервное копирование и восстановление таблиц &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfilegroup (Transact-SQL)](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily (Transact-SQL)](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset (Transact-SQL)](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Системные таблицы (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
