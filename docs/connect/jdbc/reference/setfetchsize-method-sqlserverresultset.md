---
title: Метод setFetchSize (SQLServerResultSet) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c5d0bd8714714a479f9370ed2c60b626006e1964
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803375"
---
# <a name="setfetchsize-method-sqlserverresultset"></a>Метод setFetchSize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Дает драйверу JDBC подсказку относительно числа строк, которые должны быть извлечены из базы данных, когда этому объекту [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) нужны дополнительные строки.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Параметры  
 *rows*  
  
 Значение **int**, которое указывает число строк, которые нужно перенести.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Этот метод setFetchSize указывается с помощью метода setFetchSize в интерфейсе java.sql.ResultSet.  
  
 Если указан нулевой размер выборки, то драйвер JDBC не учитывает это значение и оценивает предполагаемый размер выборки. Значение по умолчанию задается объектом [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), который создал результирующий набор. Размер выборки можно изменить в любой момент.  
  
 Этот метод изменяет размер выборки блока для серверных курсоров. Изменение вступает в силу при следующем вызове процедуры sp_cursorfetch драйвером JDBC. Если задать нулевой размер выборки, будет восстановлен тип выборки по умолчанию для используемого в данный момент типа курсора.  
  
## <a name="see-also"></a>См. также:  
 [Элементы SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Класс SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
