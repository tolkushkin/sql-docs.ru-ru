---
title: Метод getObject (java.lang.String) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a1e955ce-13db-4828-ad59-d9b6a8b2c6cc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 56fc766c22751ea0a1465f9d1a447653b096b8f8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66787464"
---
# <a name="getobject-method-javalangstring"></a>Метод getObject (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Получает значение заданного параметра в виде объекта на языке программирования Java по заданному имени параметра.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Параметры  
 *sCol*  
  
 Значение типа **String**, содержащее имя параметра.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Значение **Object**.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Этот метод getObject определен с помощью метода getObject в интерфейсе java.sql.CallableStatement.  
  
 Этот метод вернет значение данного столбца в виде объекта Java. Объект Java будет иметь заданный по умолчанию тип, соответствующий типу SQL Server столбца и сопоставленный встроенным типам, указанным в спецификации JDBC. Если значение SQL NULL, то драйвер вернет значение Java NULL.  
  
 Этот метод также может быть использован для чтения абстрактных типов данных, относящихся к базе данных. В API JDBC 2.0 возможности метода getObject расширены и поддерживают материализацию данных определяемых пользователем типов SQL. Если в столбце содержится структурированное или уникальное значение, то выполнение этого метода будет аналогично вызову `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`.  
  
 Начиная с версии 3.0 драйвера [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC действуют следующие правила:  
  
-   Значение типа **date** будет возвращаться в виде объекта java.sql.Date.  
  
-   Значение типа **time** будет возвращаться в виде объекта java.sql.Time.  
  
-   Значение типа **datetime2** будет возвращаться в виде объекта java.sql.Timestamp.  
  
-   Значение типа **datetimeoffset** будет возвращаться в виде объекта microsoft.sql.DateTimeOffset.  
  
## <a name="see-also"></a>См. также:  
 [Метод getObject (SQLServerCallableStatement)](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [Элементы SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Класс SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
