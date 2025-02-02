---
title: Передача параметров именованной команде | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6863a14a467e1d884d43b982451ec5807820486b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701849"
---
# <a name="passing-parameters-to-a-named-command"></a>Передача параметров именованной команде
Так же, как результат выполнения команды ошибку, передается как *out* переменной именованные команды и параметры для параметризованной команды можно было переданного в качестве *в* переменные в именованную команду.  
  
 В следующем примере, попытка получить все заказы размещенных клиентом, кода **CustomerID** является «ALKFI» из базы данных "Борей". Значение **CustomerID** указывается во время, когда вызывается именованную команду.  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 Обратите внимание на то, что все входные параметры должны указываться до любой выходной переменной, и типы данных параметров должны совпадать, или может быть преобразован в те из соответствующих полей. Инструкция следующее:  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -вызовет ошибку несогласованных типов данных, поскольку требуется входной параметр имеет **строка** типа, отличного от **целое число** типа.  
  
 Вызов следующее:  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 — является допустимым, но вернет пустой результирующий набор, так как записи не существует в базе данных.  
  
## <a name="see-also"></a>См. также  
 [Объект Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
