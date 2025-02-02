---
title: Примеры OriginalValue и Underlyingvalue свойства (Visual Basic) | Документация Майкрософт
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
- UnderlyingValue property [ADO], Visual Basic example
- OriginalValue property [ADO]
ms.assetid: 1750804b-d7ef-47d6-8d73-1f51fa1cbe4a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8caf11b72de62c62484f7548a9f73f33b70795bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707124"
---
# <a name="originalvalue-and-underlyingvalue-properties-example-vb"></a>Примеры OriginalValue и Underlyingvalue свойства (Visual Basic)
В этом примере показано [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) и [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) свойства, отображая сообщение, если запись основного данных был изменен в течение [записей](../../../ado/reference/ado-api/recordset-object-ado.md) пакетное обновление.  
  
```  
'BeginOriginalValueVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstTitles As ADODB.Recordset  
    Dim fldType As ADODB.Field  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
    ' Open connection.  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset for batch update  
    ' using object refs to set properties  
    Set rstTitles = New ADODB.Recordset  
    Set rstTitles.ActiveConnection = Cnxn  
    rstTitles.CursorType = adOpenKeyset  
    rstTitles.LockType = adLockBatchOptimistic  
    strSQLTitles = "titles"  
    rstTitles.Open strSQLTitles  
  
    ' Set field object variable for Type field  
    Set fldType = rstTitles!Type  
  
    ' Change the type of psychology titles  
    Do Until rstTitles.EOF  
        If Trim(fldType) = "psychology" Then  
            fldType = "self_help"  
        End If  
        rstTitles.MoveNext  
    Loop  
  
    ' Similate a change by another user by updating  
    ' data using a command string  
    Cnxn.Execute "UPDATE Titles SET type = 'sociology' " & _  
       "WHERE type = 'psychology'"  
  
    'Check for changes  
    rstTitles.MoveFirst  
    Do Until rstTitles.EOF  
        If fldType.OriginalValue <> fldType.UnderlyingValue Then  
            MsgBox "Data has changed!" & vbCr & vbCr & _  
                "  Title ID: " & rstTitles!title_id & vbCr & _  
                "  Current value: " & fldType & vbCr & _  
                "  Original value: " & _  
                fldType.OriginalValue & vbCr & _  
                "  Underlying value: " & _  
                fldType.UnderlyingValue & vbCr  
        End If  
    rstTitles.MoveNext  
    Loop  
  
    ' Cancel the update because this is a demonstration  
    rstTitles.CancelBatch  
  
    ' Restore original values  
    Cnxn.Execute "UPDATE Titles SET type = 'psychology' " & _  
        "WHERE type = 'sociology'"  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndOriginalValueVB  
```  
  
## <a name="see-also"></a>См. также  
 [Свойство OriginalValue (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Свойство UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
