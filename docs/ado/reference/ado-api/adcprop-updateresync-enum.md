---
title: ADCPROP_UPDATERESYNC_ENUM | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6ae4a8adbadc97ad2ea5e3659187481fa71e81b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698869"
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
Указывает ли [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) метод сопровождается неявным [Resync](../../../ado/reference/ado-api/resync-method.md) работы метода и если да, область этой операции.  
  
|Константа|Значение|Описание|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|Вызывает **Resync** с комбинацией всех остальных членов ADCPROP_UPDATERESYNC_ENUM.|  
|**adResyncAutoIncrement**|1|По умолчанию. Пытается получить новое значение идентификатора для столбцов, которые автоматически увеличивается или создаваемых различными источника данных, например Microsoft Jet AutoNumber полей или столбцов Microsoft SQL Server Identity.|  
|**adResyncConflicts**|2|Вызывает **Resync** для всех строк, в которых произошел сбой операции обновления или удаления из-за конфликта параллелизма.|  
|**adResyncInserts**|8|Вызывает **Resync** для всех успешно вставленных строк. Тем не менее значения столбцов AutoIncrement не синхронизируются. Вместо этого содержимое только что вставленных строк выполняется повторная синхронизация на основе существующего значения первичного ключа. Если первичный ключ имеет значение «Автоувеличение», **Resync** не получить содержимое нужные строки. Для с автоматически увеличивающимися значениями AutoIncrement значения первичного ключа, вызовите **UpdateBatch** с комбинацией **adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|Не вызывает **Resync**.|  
|**adResyncUpdates**|4|Вызывает **Resync** для всех строк, успешно обновлены.|  
  
## <a name="applies-to"></a>Объект применения  
 [Свойство Update Resync (динамическое) (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
