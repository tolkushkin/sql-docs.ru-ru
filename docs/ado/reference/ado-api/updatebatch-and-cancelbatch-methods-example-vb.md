---
title: Примеры методов UpdateBatch и Cancelbatch по методы (Visual Basic) | Документация Майкрософт
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
- UpdateBatch method [ADO]
- CancelBatch method [ADO]
ms.assetid: 41625f6f-e12d-4d8d-9f60-0729ce64c31e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 653045da77e9639979a4e70a8e5d7991e7361225
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710427"
---
# <a name="updatebatch-and-cancelbatch-methods-example-vb"></a>Примеры методов UpdateBatch и Cancelbatch по методы (Visual Basic)
В этом примере показано [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) в сочетании с [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) метод.  
  
```  
'BeginUpdateBatchVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    'connection and recordset variables  
    Dim rstTitles As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
     'record variables  
    Dim strTitle As String  
    Dim strMessage As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' open recordset for batch uodate  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenKeyset, adLockBatchOptimistic, adCmdTable  
  
    rstTitles.MoveFirst  
    ' Loop through recordset and ask user if she wants  
    ' to change the type for a specified title.  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "psychology" Then  
            strTitle = rstTitles!Title  
            strMessage = "Title: " & strTitle & vbCr & _  
               "Change type to self help?"  
  
            If MsgBox(strMessage, vbYesNo) = vbYes Then  
                rstTitles!Type = "self_help"  
            End If  
        End If  
  
        rstTitles.MoveNext  
    Loop  
  
    ' Ask the user if she wants to commit to all the  
    ' changes made above.  
    If MsgBox("Save all changes?", vbYesNo) = vbYes Then  
        rstTitles.UpdateBatch  
    Else  
        rstTitles.CancelBatch  
    End If  
  
    ' Print current data in recordset.  
    rstTitles.Requery  
    rstTitles.MoveFirst  
    Do While Not rstTitles.EOF  
        Debug.Print rstTitles!Title & " - " & rstTitles!Type  
        rstTitles.MoveNext  
    Loop  
  
    ' Restore original values because this is a demonstration.  
    rstTitles.MoveFirst  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "self_help" Then  
            rstTitles!Type = "psychology"  
        End If  
        rstTitles.MoveNext  
    Loop  
    rstTitles.UpdateBatch  
  
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
'EndUpdateBatchVB  
```  
  
## <a name="see-also"></a>См. также  
 [Метод CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Метод UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
