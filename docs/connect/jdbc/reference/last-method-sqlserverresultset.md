---
title: Последний метод (SQLServerResultSet) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.last
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ac9bef59-8c31-437b-a183-619cc778fe7a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f97a3d27deeb4a51663cb108ab3adc77b75e29e8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790032"
---
# <a name="last-method-sqlserverresultset"></a>Метод last (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Перемещает курсор в последнюю строку этого объекта [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public boolean last()  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 **значение true,** допустимость новой текущей строкой. **false** Если больше нет строк для обработки.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Последний метод определен с помощью последнего метода в интерфейсе java.sql.ResultSet.  
  
## <a name="see-also"></a>См. также:  
 [Элементы SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Класс SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
