---
title: Пример метода AddNew (Visual Basic) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- AddNew method [ADO], Visual Basic example
ms.assetid: d439e097-65f3-471d-8799-5a1263beb3c1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8b3e56f2e78b8557785917f8f60b3f837f3079b9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703966"
---
# <a name="addnew-method-example-vb"></a>Пример метода AddNew (Visual Basic)
В этом примере используется [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) метод, чтобы создать новую запись с указанным именем.  
  
```  
'BeginAddNewVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstEmployees As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQL As String  
     'record variables  
    Dim strID As String  
    Dim strFirstName As String  
    Dim strLastName As String  
    Dim blnRecordAdded As Boolean  
  
    ' Open a connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Northwind';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open Employees Table with a cursor that allows updates  
    Set rstEmployees = New ADODB.Recordset  
    strSQL = "Employees"  
    rstEmployees.Open strSQL, strCnxn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
    ' Get data from the user  
    strFirstName = Trim(InputBox("Enter first name:"))  
    strLastName = Trim(InputBox("Enter last name:"))  
  
    ' Proceed only if the user actually entered something  
    ' for both the first and last names  
    If strFirstName <> "" And strLastName <> "" Then  
  
        rstEmployees.AddNew  
        rstEmployees!firstname = strFirstName  
        rstEmployees!LastName = strLastName  
        rstEmployees.Update  
        blnRecordAdded = True  
  
        ' Show the newly added data  
        MsgBox "New record: " & rstEmployees!EmployeeId & " " & _  
        rstEmployees!firstname & " " & rstEmployees!LastName  
  
    Else  
        MsgBox "Please enter a first name and last name."  
    End If  
  
    ' Delete the new record because this is a demonstration  
    Cnxn.Execute "DELETE FROM Employees WHERE EmployeeID = '" & strID & "'"  
  
    ' clean up  
    rstEmployees.Close  
    Cnxn.Close  
    Set rstEmployees = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
   ' clean up  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndAddNewVB  
```  
  
## <a name="see-also"></a>См. также  
 [Метод AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
