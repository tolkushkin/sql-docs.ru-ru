---
title: Метод Close (SQLServerConnection) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f0f26585-bdf7-4737-b434-8c7e115c8e94
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f1dc9a524e9993ad31e6c89ab27e481dd8266d8c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803587"
---
# <a name="close-method-sqlserverconnection"></a>Метод close (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Моментально освобождает для данного объекта [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) базу данных и ресурсы JDBC, не дожидаясь их автоматического освобождения.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Этот метод close определен с помощью метода close в интерфейсе java.sql.Connection.  
  
 Вызов метода close в середине транзакции приводит к откату этой транзакции.  
  
## <a name="see-also"></a>См. также:  
 [Элементы SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Класс SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
