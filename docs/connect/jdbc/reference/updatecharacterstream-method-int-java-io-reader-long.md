---
title: Метод updateCharacterStream (java.io.Reader, long) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c426b0e3-2f9d-425a-b7da-1d0325e292d1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7a3747df1ff5f64b0f7ebdfa1ff383eb497a8d0a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784214"
---
# <a name="updatecharacterstream-method-int-javaioreader-long"></a>Метод updateCharacterStream (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Обновляет указанный столбец заданным значением символьного потока, который будет содержать указанное число символов.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x,  
                                  long length)  
```  
  
#### <a name="parameters"></a>Параметры  
 *columnIndex*  
  
 Значение типа **int**, указывающее индекс столбца.  
  
 *x*  
  
 Объект средства чтения.  
  
 *length*  
  
 Длина потока.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Этот метод updateCharacterStream указывается с помощью метода updateCharacterStream в интерфейсе java.sql.ResultSet.  
  
 Этот метод передает символы Юникода от объекта средства чтения выбранным текстовым и двоичным столбцам. Сюда входят все текстовые и двоичные столбцы, а также столбцы varbinary, varbinary(max), image и XML, но не входят столбцы определяемых пользователем типов данных.  
  
 Если длина потока отличается от указанной в параметре *length*, драйвер JDBC выдаст исключение при обновлении или вставке строки.  
  
 Если длина потока неизвестна, параметр *length* может иметь значение "–1", показывающее, что драйвер должен принимать поток любой длины. При использовании sqljdbc4.jar, если приложению нужно обновить столбец из потока, длина которого неизвестна, рекомендуем применять метод JDBC 4.0 [updateCharacterStream &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-int-java-io-reader.md).  
  
## <a name="see-also"></a>См. также:  
 [Метод updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Элементы SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Класс SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
