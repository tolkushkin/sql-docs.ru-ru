---
title: MoveRecordOptionsEnum | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8119b553ba7d85b9a3e1cabc49975967a0a751af
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719184"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
Задает поведение [записи](../../../ado/reference/ado-api/record-object-ado.md) объект [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) метод.  
  
|Константа|Значение|Описание|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|По умолчанию. Выполняет операцию перемещения по умолчанию: Операция завершается ошибкой, если целевой файл или каталог уже существует, и операция обновляет гипертекстовых ссылок.|  
|**adMoveOverWrite**|1|Перезаписывает конечный файл или каталог, даже если он уже существует.|  
|**adMoveDontUpdateLinks**|2|Изменяет поведение по умолчанию **MoveRecord** метод, не обновляя гипертекстовых ссылок источника **записи**. Поведение по умолчанию зависит от возможностей поставщика. Операции перемещения обновляет ссылки, если поставщик может быть перенесен. Если поставщик не может исправить ссылки или если это значение не указано, перемещение успешно, даже если ссылки не были исправлены.|  
|**adMoveAllowEmulation**|4|Запросы, что поставщик попытка моделировать перемещения (с помощью загрузки, отправка и операции удаления). Если попытка переместить **записи** завершается сбоем, так как URL-адрес назначения находится на другом сервере или обслуживаемых другого поставщика, чем исходный, это может привести к повышенной задержки и потери данных, из-за возможности другого поставщика при Перемещение ресурсов между поставщиками.|  
  
## <a name="adowfc-equivalent"></a>Эквивалент ADO и WFC  
 Эти константы не имеют эквивалентов ADO и WFC.  
  
## <a name="applies-to"></a>Объект применения  
 [Метод MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
