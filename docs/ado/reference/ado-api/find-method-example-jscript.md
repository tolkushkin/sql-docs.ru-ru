---
title: Пример метода (JScript) Find | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- Find method [ADO], JScript example
ms.assetid: adb5c37e-7874-41db-b4ee-572c1323deff
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9fa46bba5f4842b277c4b70622165adf95817858
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66694885"
---
# <a name="find-method-example-jscript"></a>Пример метода Find (JScript)
В этом примере используется [записей](../../../ado/reference/ado-api/recordset-object-ado.md) объекта [найти](../../../ado/reference/ado-api/find-method-ado.md) метод для поиска и отображения на компании в ***Northwind*** базы данных, имена которых начинаются с буквы G. вырезания и вставки следующим кодом в блокноте или другом текстовом редакторе и сохраните его как **FindJS.asp**.  
  
```  
<!-- BeginFindJS -->  
<%@  Language=JavaScript %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
  
<head>  
<title>ADO Recordset.Find Example</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body bgcolor="white">  
  
<h1>ADO Recordset.Find Example</h1>  
<%  
    // connection and recordset variables  
    var Cnxn = Server.CreateObject("ADODB.Connection");  
    var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
    var rsCustomers = Server.CreateObject("ADODB.Recordset");  
        // display string  
    var strMessage;      
    var strFind;  
  
    try  
    {  
            // open connection  
        Cnxn.Open(strCnxn);  
  
            //create recordset using object refs  
        SQLCustomers = "select * from Customers;";  
  
        rsCustomers.ActiveConnection = Cnxn;  
        rsCustomers.CursorLocation = adUseClient;  
        rsCustomers.CursorType = adOpenKeyset;  
        rsCustomers.LockType = adLockOptimistic;  
        rsCustomers.Source = SQLCustomers;  
  
        rsCustomers.Open();  
        rsCustomers.MoveFirst();  
  
            //find criteria  
        strFind = "CompanyName like 'g%'"  
        rsCustomers.Find(strFind);  
  
        if (rsCustomers.EOF) {  
            Response.Write("No records matched ");  
            Response.Write(SQLCustomers & "So cannot make table...");  
            Cnxn.Close();  
            Response.End();  
        }   
        else {  
            Response.Write('<table width="100%" border="2">');  
            Response.Write('<tr class="thead2">');  
            // Put Headings On The Table for each Field Name  
            for (thisField = 0; thisField < rsCustomers.Fields.Count; thisField++) {  
                fieldObject = rsCustomers.Fields(thisField);  
                Response.Write('<th width="' + Math.floor(100 / rsCustomers.Fields.Count) + '%">' + fieldObject.Name + "</th>");  
            }  
            Response.Write("</tr>");  
  
            while (!rsCustomers.EOF) {  
                Response.Write('<tr class="tbody">');  
                for(thisField=0; thisField<rsCustomers.Fields.Count; thisField++) {  
                    fieldObject = rsCustomers.Fields(thisField);  
                    strField = fieldObject.Value;  
                    if (strField == null)  
                        strField = "-Null-";  
                    if (strField == "")  
                        strField = "";  
                    Response.Write("<td>" + strField + "</td>");  
                }  
                rsCustomers.Find(strFind, 1, adSearchForward)  
                Response.Write("</tr>");  
            }  
            Response.Write("</table>");  
        }  
    }  
    catch (e)  
    {  
        Response.Write(e.message);  
    }  
    finally  
    {  
        // clean up  
        if (rsCustomers.State == adStateOpen)  
            rsCustomers.Close;  
        if (Cnxn.State == adStateOpen)  
            Cnxn.Close;  
        rsCustomers = null;  
        Cnxn = null;  
    }  
%>  
  
</body>  
  
</html>  
<!-- EndFindJS -->  
```  
  
## <a name="see-also"></a>См. также  
 [Метод Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
