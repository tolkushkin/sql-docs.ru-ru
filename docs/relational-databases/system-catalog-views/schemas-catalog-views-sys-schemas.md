---
title: sys.schemas (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- schemas_TSQL
- sys.schemas_TSQL
- schemas
- sys.schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.schemas catalog view
ms.assetid: 29af5ce5-2af7-4103-8f08-3ec92603ba05
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8519dc4846f148b1b4d1bc83589baf0cc6a81e12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65983147"
---
# <a name="schemas-catalog-views---sysschemas"></a>Схемы каталога представления — sys.schemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Содержит по одной строке для каждой схемы базы данных.  
  
> [!NOTE]  
>  Схемы базы данных отличаются от XML-схем, которые используются для определения модели содержимого XML-документов.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Имя схемы. Уникален в пределах базы данных.|  
|**schema_id**|**int**|Идентификатор схемы. Уникален в пределах базы данных.|  
|**principal_id**|**int**|Идентификатор участника, владеющего этой схемой.|  
  
## <a name="remarks"></a>Примечания  
Схемы базы данных действуют как пространства имен или контейнеры для объектов, таких как таблицы, представления, процедуры и функции, которые могут находиться в **sys.objects** представления каталога.  

Каждая схема имеет владельца. Владельцем является безопасности [участника](../../relational-databases/security/authentication-access/principals-database-engine.md).
  
## <a name="permissions"></a>Разрешения  
 Необходимо быть членом роли **public**. Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>См. также  
[Субъекты](../../relational-databases/security/authentication-access/principals-database-engine.md)

[Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[Представления каталога схем &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   

[sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
