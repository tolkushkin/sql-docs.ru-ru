---
title: EXECUTE, Requery и Clear (JScript) также пример метода | Документация Майкрософт
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
- Requery method [ADO], JScript example
- Clear method [ADO], JScript example
- Execute method [ADO], JScript example
ms.assetid: 51a87e91-c9d9-4e49-af47-79cce2c4cfe0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: abcc619a47994684edce33b2e5b19f7786f517d4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697915"
---
# <a name="execute-requery-and-clear-methods-example-jscript"></a>EXECUTE, Requery и Clear методы (JScript)
В этом примере показано **Execute** метод, при запуске из обоих [команда](../../../ado/reference/ado-api/command-object-ado.md) объекта и [подключения](../../../ado/reference/ado-api/connection-object-ado.md) объекта. Он также использует [Requery](../../../ado/reference/ado-api/requery-method.md) метод для извлечения текущих данных в [записей](../../../ado/reference/ado-api/recordset-object-ado.md)и [снимите](../../../ado/reference/ado-api/clear-method-ado.md) метод, чтобы удалить содержимое [ошибки](../../../ado/reference/ado-api/errors-collection-ado.md)коллекции. ( **Ошибки** коллекции осуществляется через **подключения** объект [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) свойство [записей](../../../ado/reference/ado-api/recordset-object-ado.md).) Назовите файл **ExecuteJS.asp**.  
  
```  
<!-- BeginExecuteJS -->  
<%@LANGUAGE="JScript"%>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<%  
    strLastName = new String(Request.Form("AuthorLName"));  
  
    if (strLastName.indexOf("undefined") > -1)  
        strLastName = "";  
%>  
  
<html>  
  
<head>  
<title>Execute, Requery and Clear Methods Example (JScript)</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
-->  
</style>  
</head>  
  
<body bgcolor="White">  
<h1>Execute, Requery and Clear Methods Example (JScript)</h1>  
<%  
    if (strLastName.length > 0)  
    {  
        // command and recordset variables  
        var Connect = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='pubs';Integrated Security='SSPI';";  
        var Cnxn = Server.CreateObject("ADODB.Connection");  
        var cmdAuthor = Server.CreateObject("ADODB.Command");  
        var rsAuthor = Server.CreateObject("ADODB.Recordset");  
        var rsAuthor2 = Server.CreateObject("ADODB.Recordset");  
        var SQLAuthor2, strMessage, strMessage2;  
        var Err, ErrCount;  
  
        try  
        {  
            // open connection  
            Cnxn.Open(Connect);  
  
            // command object parameters  
            cmdAuthor.CommandText = "SELECT * FROM Authors WHERE au_lname = ?";  
            cmdAuthor.Parameters.Append(cmdAuthor.CreateParameter("Last Name", adChar, adParamInput, 20, strLastName));  
            cmdAuthor.ActiveConnection = Cnxn;  
  
            // recordset from command.execute  
            rsAuthor = cmdAuthor.Execute();  
  
            // recordset from connection.execute  
            SQLAuthor2 = "SELECT * FROM Authors";  
            rsAuthor2 = Cnxn.Execute(SQLAuthor2);  
  
                // check for errors  
                ErrCount = Cnxn.errors.count;  
                if(ErrCount !== 0) //write the errors  
                {  
                    for(Err = 0; Err = ErrCount; Err++){  
                        Err = Cnxn.errors.item;  
                        Response.Write(Err);  
                    }  
                    // clean out any existing errors  
                    Cnxn.Errors.Clear;  
                }  
  
                // show the data      
            Response.Write("<HR><HR>");  
  
                // first recordset  
            Response.Write("<b>Command.Execute results</b>")  
            while (!rsAuthor.EOF)  
            {  
                // build output string by starting a new line  
                strMessage = "<P>";  
                strMessage += "<br>";  
  
                // recordset data   
                strMessage += rsAuthor("au_fname") + " ";   
                strMessage += rsAuthor("au_lname") + " ";  
  
                // end the line  
                strMessage += "</P>";  
  
                // show the results  
                Response.Write(strMessage);  
  
                // get next record  
                rsAuthor.MoveNext;  
            }  
  
            Response.Write("<HR><HR>");  
  
            // second recordset  
            Response.Write("<b>Connection.Execute results</b>")  
            while (!rsAuthor2.EOF)  
            {  
                // start a new line  
                strMessage2 = "<P>";  
  
                // first and last name are in first column  
                strMessage2 += rsAuthor2("au_fname") + " "   
                strMessage2 += rsAuthor2("au_lname") + " ";  
  
                // end the line  
                strMessage2 += "</P>";  
  
                // show results  
                Response.Write(strMessage2);  
  
                // get next record  
                rsAuthor2.MoveNext;  
            }  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // clean up  
            if (rsAuthor.State == adStateOpen)  
                rsAuthor.Close;  
            if (rsAuthor2.State == adStateOpen)  
                rsAuthor2.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsAuthor1 = null;  
            rsAuthor2 = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<hr>  
  
<form method="POST" action="ExecuteJS.asp" id=form1 name=form1>  
  <p align="left">Enter last name of author to find (e.g., Ringer): <input type="text" name="AuthorLName" size="40"></p>  
  <p align="left"><input type="submit" value="Submit" name="B1"><input type="reset" value="Reset" name="B2"></p>  
</form>  
</body>  
  
</html>  
<!-- EndExecuteJS -->  
```  
  
## <a name="see-also"></a>См. также  
 [Метод Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Объект Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Объект Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Объект ошибки](../../../ado/reference/ado-api/error-object.md)   
 [Выполнение метода (объект Command ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Выполнение метода (объект Connection ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Метод Requery](../../../ado/reference/ado-api/requery-method.md)
