---
title: SeekEnum | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7135d6582ea6d09c6f1b0ab3842c69d3d60d4fc9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711416"
---
# <a name="seekenum"></a>SeekEnum
Указывает тип [Seek](../../../ado/reference/ado-api/seek-method.md) для выполнения.  
  
|Константа|Значение|Описание|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Выполняет поиск первого ключа, равным *KeyValues*.|  
|**adSeekLastEQ**|2|Выполняет поиск последнего ключа, равным *KeyValues*.|  
|**adSeekAfterEQ**|4|Ищет ключ равен *KeyValues* или после которой должны были произойти, соответствующие.|  
|**adSeekAfter**|8|Ищет ключ сразу после where совпадения *KeyValues* должны были произойти.|  
|**adSeekBeforeEQ**|16|Ищет ключ равен *KeyValues*или непосредственно перед которой должны были произойти, соответствующие.|  
|**adSeekBefore**|32|Ищет ключ непосредственно перед там, где совпадение с *KeyValues* должны были произойти.|  
  
## <a name="adowfc-equivalent"></a>Эквивалент ADO и WFC  
 Пакет: **com.ms.wfc.data**  
  
|Константа|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>Объект применения  
 [Метод Seek](../../../ado/reference/ado-api/seek-method.md)
