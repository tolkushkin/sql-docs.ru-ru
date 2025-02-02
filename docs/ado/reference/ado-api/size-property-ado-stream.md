---
title: Свойство (ADO Stream) Size | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 42a4725efde507112d51b4f9c41af4ba83f63da4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719085"
---
# <a name="size-property-ado-stream"></a>Свойство Size (объект Stream ADO)
Указывает размер потока в байтах.  
  
## <a name="return-values"></a>Возвращаемые значения  
 Возвращает **Long** значение, указывающее размер потока в байтах. Значение по умолчанию — размер потока, или значение -1, если известен размер потока.  
  
## <a name="remarks"></a>Примечания  
 **Размер** может использоваться только с открытым [Stream](../../../ado/reference/ado-api/stream-object-ado.md) объектов.  
  
> [!NOTE]
>  Любое количество битов, которые могут храниться в **Stream** объекта, ограничивается только системные ресурсы. Если **Stream** содержит дополнительные биты не может быть представлена **Long** значение, **размер** усекается и поэтому неточно представлять длину **Stream**.  
  
## <a name="applies-to"></a>Объект применения  
 [Объект Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>См. также  
 [Свойство Size (объект Parameter ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
