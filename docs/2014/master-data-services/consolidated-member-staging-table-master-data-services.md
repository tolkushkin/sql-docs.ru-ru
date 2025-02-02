---
title: Промежуточная таблица консолидированных элементов (службы Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], attributes staging table
- attributes staging table [Master Data Services]
ms.assetid: 070681ed-be99-49ae-93bd-6402f2134ace
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b0ade33df500a35f8319a2eb0bc412e16b2d1cf8
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65480042"
---
# <a name="consolidated-member-staging-table-master-data-services"></a>Промежуточная таблица консолидированных элементов (службы Master Data Services)
  Промежуточная таблица консолидированных элементов (stg.name_Consolidated) используется в базе данных [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] для создания, обновления, деактивации и удаления консолидированных элементов. Ее также можно использовать для обновления значений атрибутов консолидированных элементов.  
  
##  <a name="TableColumns"></a> Столбцы таблицы  
 В приведенной таблице объясняется, для чего используется каждое поле в консолидированной промежуточной таблице.  
  
|Имя столбца|Описание|  
|-----------------|-----------------|  
|**Идентификатор**|Автоматически назначенный идентификатор. Не вводите значение в этом поле. Если пакет не обработан, это поле пустое.|  
|**ImportType**<br /><br /> Обязательно|Определяет действия в случае, если промежуточные данные совпадают с уже существующими данными в базе данных [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> **0**: Создание новых элементов. Замена существующих данных MDS на промежуточные данные, но только в том случае, если промежуточные данные не имеют значения NULL. Значения NULL не учитываются. Чтобы изменить значение атрибута на значение NULL, используйте **~NULL~**.<br /><br /> **1**: Создание только новых элементов. Любые обновления существующих данных MDS завершаются неудачей.<br /><br /> **2**: Создание новых элементов. Замена существующих данных MDS на промежуточные данные. При импорте значений NULL они будут перезаписывать существующие значения MDS.<br /><br /> **3**: Отключение элемента, основанного на значении кода. Все членства атрибутов, иерархий, коллекций и транзакций обслуживаются, но более недоступны в пользовательском интерфейсе. Если элемент используется как значение атрибута другого элемента на основе домена, отключение элемента завершится неудачей.<br /><br /> **4**: Окончательное удаление элемента, основанного на значении кода. Все членства атрибутов, иерархий, коллекций и транзакций окончательно удалены. Если элемент используется как значение атрибута другого элемента на основе домена, удаление элемента завершится неудачей.|  
|**ImportStatus_ID**<br /><br /> Обязательно|Состояние процесса импорта. Возможны следующие значения:<br /><br /> **0**задается для указания готовности записи к промежуточному хранению;<br /><br /> **1**задается автоматически и указывает на успешное завершение промежуточного процесса записи;<br /><br /> **2**задается автоматически и указывает на ошибку промежуточного процесса записи.|  
|**Batch_ID**<br /><br /> Требуется только для веб-службы|Автоматически назначаемый идентификатор, группирующий записи для промежуточного хранения. Всем элементам в пакете назначен этот идентификатор, который отображается в пользовательском интерфейсе [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] в столбце **ID** .<br /><br /> Если пакет не обработан, это поле пустое.|  
|**BatchTag**<br /><br /> Требуется, за исключением веб-службы|Уникальное имя для данного пакета, до 50 символов.|  
|**HierarchyName**<br /><br /> Обязательно|Имя явной иерархии. Каждый объединенный элемент может принадлежать только одной явной иерархии.|  
|**ErrorCode**|Отображает код ошибки. Для всех записей со значением **ImportStatus_ID** , равным **2**, см. раздел [Ошибки промежуточного процесса (службы Master Data Services)](staging-process-errors-master-data-services.md).|  
|**Code**<br /><br /> Требуется, за исключением случаев, когда коды формируются автоматически для **ImportType1** или **2**. Дополнительные сведения см. в разделе [Автоматическое создание кодов (службы Master Data Services)](../../2014/master-data-services/automatic-code-creation-master-data-services.md).|Уникальный код элемента.|  
|**Название**<br /><br /> Необязательно|Имя элемента.|  
|**NewCode**|Используйте только при изменении кода элемента.|  
|\<Имя атрибута>|Столбец существует для каждого атрибута в сущности. Используется с параметром **ImportType** , который равен **0** или **2**. Для атрибутов в свободной форме укажите новое текстовое или строковое значение атрибута. Для основанных на домене атрибутов необходимо указать код элемента, который будет атрибутом. Для атрибутов ссылок URL-адрес должен начинаться с **http://**.<br /><br /> Примечание. Атрибуты файла. нельзя размещать.|  
  
## <a name="see-also"></a>См. также  
 [Загрузка или обновление членов в службы Master Data Services с помощью промежуточного процесса](add-update-and-delete-data-master-data-services.md)   
 [Перемещение элементов явной иерархии с помощью промежуточного процесса &#40;службы Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Импорт данных &#40;службы Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Просмотр ошибок, возникающих в ходе промежуточного процесса &#40;службы Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [Ошибки промежуточного процесса (службы Master Data Services)](staging-process-errors-master-data-services.md)  
  
  
