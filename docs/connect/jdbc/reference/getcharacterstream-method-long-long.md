---
title: Метод getCharacterStream (long, long) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2881f3a9e0d3a4179334256aa7d2917917cf97f3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781329"
---
# <a name="getcharacterstream-method-long-long"></a>Метод getCharacterStream (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Возвращает данные **Clob** в виде объекта Reader или потока символов с указанной позицией и длиной.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>Параметры  
 *Торговых терминалов*  
  
 Значение **long**, определяющее смещение до первого символа извлекаемого фрагмента значения.  
  
 *length*  
  
 Значение **long**, определяющее длину в символах для извлекаемого фрагмента значения.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Объект Reader, содержащий данные **NCLOB**.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Этот метод getCharacterStream указывается с помощью метода getCharacterStream в интерфейсе java.sql.Clob.  
  
## <a name="see-also"></a>См. также:  
 [Метод getCharacterStream (SQLServerClob)](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [Методы SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Элементы SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  
