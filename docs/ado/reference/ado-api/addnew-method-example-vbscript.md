---
title: Пример метода AddNew (VBScript) | Документация Майкрософт
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
- AddNew method [ADO], VBScript
ms.assetid: dcdcaf0a-b9b0-4d81-8728-43c38c4c853b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d1409dda550c13c296d0b11e7fa5dd1d63d6f09d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698857"
---
# <a name="addnew-method-example-vbscript"></a>Пример метода AddNew (VBScript)
В этом примере используется [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) метод, чтобы создать новую запись с указанным именем.  
  
 Используйте следующий пример в Active Server Page (ASP). Используйте **найти** найдите файл Adovbs.inc и поместите его в каталог, который вы планируете использовать. Вырежьте и вставьте следующий код в блокноте или другом текстовом редакторе и сохраните его в **AddNewVBS.asp**. Результат можно просмотреть в любом браузере клиента.  
  
 Чтобы использовать в примере, добавьте новую запись в формате HTML. Нажмите кнопку **добавить новый**. См. в разделе [удалить пример метода](../../../ado/reference/ado-api/delete-method-example-vbscript.md) для удаления нежелательных записей.  
  
```  
<!-- BeginAddNewVBS -->  
<%@Language = VBScript %>  
<%' use this meta tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
    <TITLE>ADO AddNew Method (VBScript)</TITLE>  
    <STYLE>  
    <!--  
    body {  
       font-family: 'Verdana','Arial','Helvetica',sans-serif;  
       BACKGROUND-COLOR:white;  
       COLOR:black;  
        }  
    TH {  
       background-color: #008080;   
       font-family: 'Arial Narrow','Arial',sans-serif;   
       font-size: xx-small;  
       color: white;  
       }  
    TD {   
       text-align: center;  
       background-color: #f7efde;  
       font-family: 'Arial Narrow','Arial',sans-serif;   
       font-size: xx-small;  
        }  
    -->  
    </STYLE>  
</HEAD>  
<BODY>   
  
<H1>ADO AddNew Method (VBScript)</H1>  
  
<% ' to integrate/test this code replace the   
   ' Data Source value in the Connection string%>  
<%   
    ' connection and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
    Dim fld, Err  
  
    ' open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Cnxn.Open strCnxn  
  
     ' create and open Recordset using object refs  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "Customers"  
  
    rsCustomers.ActiveConnection = Cnxn  
    rsCustomers.CursorLocation = adUseClient  
    rsCustomers.CursorType = adOpenKeyset  
    rsCustomers.LockType = adLockOptimistic  
    rsCustomers.Source = strSQLCustomers  
    rsCustomers.Open  
  
    'If this is first time page is open, Form collection  
    'will be empty when data is entered. run AddNew method  
    If Not IsEmpty(Request.Form) Then  
        If Not Request.Form("CompanyName") = "" Then  
            rsCustomers.AddNew  
                rsCustomers("CustomerID") = Request.Form("CompanyID")  
                rsCustomers("CompanyName") = Request.Form("CompanyName")  
                rsCustomers("ContactName") = Request.Form("FirstName") & _  
                    " " & Request.Form("LastName")  
                rsCustomers("Phone") = Request.Form("PhoneNumber")  
                rsCustomers("City") = Request.Form("City")  
                rsCustomers("Region") = Request.Form("State")  
            rsCustomers.Update  
             ' check for errors  
            If Cnxn.Errors.Count > 0 Then  
                For Each Err In Cnxn.Errors  
                    Response.Write("Error " & Err.SQLState & ": " & _  
                        Err.Description & " | " & Err.NativeError)  
                Next  
            Cnxn.Errors.Clear  
            rsCustomers.CancelUpdate  
            End If  
            'On Error GoTo 0  
        rsCustomers.MoveFirst  
        End If  
    End If  
%>  
  
<TABLE COLSPAN="8" CELLPADDING=5 BORDER=1 ALIGN="center">  
<!-- BEGIN column header row for Customer Table-->  
    <TR>  
        <TH>Customer ID</TH>  
        <TH>Company Name</TH>  
        <TH>Contact Name</TH>  
        <TH>Phone Number</TH>  
        <TH>City</TH>  
        <TH>State/Province</TH>  
        </TR>  
  
    <% ' show the data  
        Do Until rsCustomers.EOF  
            Response.Write("<TR>")  
            Response.Write("<TD>" & rsCustomers("CustomerID") & "</TD>")  
            Response.Write("<TD>" & rsCustomers("CompanyName")& "</TD>")  
            Response.Write("<TD>" & rsCustomers("ContactName") & "</TD>")  
            Response.Write("<TD>" & rsCustomers("Phone") & "</TD>")  
            Response.Write("<TD>" & rsCustomers("City") & "</TD>")  
            Response.Write("<TD>" & rsCustomers("Region") & "</TD>")  
            Response.Write("</TR>")  
        rsCustomers.MoveNext   
        Loop   
    %>  
</TABLE>   
  
<HR>  
  
<!--  
    Form to enter new record posts variables  
    back to this page  
-->  
<FORM Method=post Action="AddNewVbs.asp" Name=Form>  
    <TABLE>  
        <TR>  
            <TD>Company ID:</TD>  
            <TD><INPUT Size="5" Name="CompanyID" maxLength=5  ></TD>  
        </TR>  
        <TR>  
            <TD>Company Name:</TD>  
            <TD><INPUT Size="50" Name="CompanyName" ></TD>  
        </TR>  
        <TR>  
            <TD>Contact First Name:</TD>  
            <TD><INPUT Size="50" Name="FirstName" ></TD>  
        </TR>  
        <TR>  
            <TD>Contact Last Name:</TD>  
            <TD><INPUT Size="50" Name="LastName" ></TD>  
        </TR>  
        <TR>  
            <TD>Contact Phone:</TD>  
            <TD><INPUT Size="50" Name="PhoneNumber" ></TD>  
        </TR>  
        <TR>  
            <TD>City:</TD>  
            <TD><INPUT Size="50" Name="City" ></TD>  
        </TR>  
        <TR>  
            <TD>State / Province:</TD>  
            <TD><INPUT Size="5" Name="State" ></TD>  
        </TR>  
        <TR>  
            <TD Align="right"><INPUT Type="submit" Value="Add New"></TD>  
            <TD Align="left"><INPUT Type="reset" Value="Reset Form"></TD>  
        </TR>  
    </TABLE>  
</FORM>  
  
<%  
    ' Show connection.  
    Response.Write("Following is the connection string: <br><br>")  
    Response.Write(Cnxn)  
  
    ' Clean up.  
    If rsCustomers.State = adStateOpen then  
       rsCustomers.Close  
    End If  
    If Cnxn.State = adStateOpen then  
       Cnxn.Close  
    End If  
    Set rsCustomers=Nothing  
    Set Cnxn=Nothing  
    Set fld=Nothing  
%>  
  
<SCRIPT Language = "VBScript">  
Sub Form_OnSubmit  
   MsgBox "Sending New Record to Server",,"ADO-ASP _Example"  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
<!-- EndAddNewVBS -->  
```  
  
## <a name="see-also"></a>См. также  
 [Метод AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
