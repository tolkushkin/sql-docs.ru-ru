---
title: Пример метода (VBScript) Refresh | Документация Майкрософт
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADO], VBScript example
ms.assetid: f2926578-bc60-464b-916e-ddfdb8014253
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 610c0630576719a40d9ba2ab4434fe4538dfc896
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66694457"
---
# <a name="refresh-method-example-vbscript"></a>Пример метода Refresh (VBScript)
> [!IMPORTANT]
>  Начиная с Windows 8 и Windows Server 2012, серверные компоненты служб удаленных рабочих СТОЛОВ, больше не включаются в операционной системе Windows (см. в разделе Windows 8 и [настольная книга по совместимости Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) для получения дополнительных сведений). Клиентские компоненты служб удаленных рабочих СТОЛОВ будет поддерживаться в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Приложения, использующие служб удаленных рабочих СТОЛОВ, следует перевести [WCF-сервиса данных](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Приведенный ниже показано, как задать необходимые параметры [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) во время выполнения. Способ [записей](../../../ado/reference/ado-api/recordset-object-ado.md) извлекается с использованием [обновить](../../../ado/reference/ado-api/refresh-method-ado.md) метод определяется параметрами [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) и [FetchOptions ](../../../ado/reference/rds-api/fetchoptions-property-rds.md) свойства. Чтобы протестировать этот пример, вырезать и вставить следующий код в обычном документ ASP и назовите его **RefreshVBS.asp**. Используйте **найти** найдите файл Adovbs.inc и поместите его в каталог, который вы планируете использовать. Сценарий ASP будет идентификации сервера.  
  
```  
<!-- BeginRefreshVBS -->  
<%@ Language=VBScript %>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Refresh Method Example (VBScript)</title>  
<style>  
<!--  
body {  
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
  
<body>  
<h1>Refresh Method Example (VBScript)</h1>  
  
<H2>RDS API Code Examples </H2>  
<HR>  
<TABLE DATASRC=#RDC>  
   <TR>  
      <TD> <INPUT DATAFLD="FirstName" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="LastName" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="Title" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="HireDate" SIZE=15> </TD>  
   </TR>  
</TABLE>  
  
<!-- RDS.DataControl with no parameters set at design time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDC HEIGHT=1 WIDTH=1>  
</OBJECT>  
<HR>  
Server: <Input Size=70 Name="txtServer" Value="https://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
Connect: <Input Size=70 Name="txtConnect" Value="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'"><BR>  
SQL: <Input Size=70 Name="txtSQL" Value="Select * from Employees">  
<HR>  
<TABLE BORDER=1 WIDTH="60%">  
<TR>  
   <TD COLSPAN=3 BGCOLOR=silver>  
   Choose if you want the Recordset brought back Synchronously on the   
   current calling thread or Asynchronously on another thread.   
   </TD>  
</TR>  
<TR>  
   <TD>Synchronously: <BR>  
      <Input Type="Radio" Name="optExecuteOptions" Checked OnClick="SetExO('adcExecSync')">  
   </TD>  
   <TD>Asynchronously: <BR>  
      <Input Type="Radio" Name="optExecuteOptions"  OnClick="SetExO('adcExecAsync')">  
   </TD>  
   <TD> </TD>  
</TR>  
<TR>  
   <TD COLSPAN=3 BGCOLOR=silver>  
   Fetch Up Front, Background Fetch with Blocking or Background Fetch   
   without Blocking   
   </TD>  
<TR>  
   <TD>Up Front:<BR>  
       <Input Type="Radio" Name="optFetchOptions"  OnClick="SetFO('adcFetchUpFront')">  
   </TD>  
   <TD>Background w/ Blocking:<BR>  
       <Input Type="Radio" Name="optFetchOptions" Checked OnClick="SetFO('adcFetchBackground')">  
   </TD>  
   <TD>Background w/o Blocking:<BR>  
      <Input Type="Radio" Name="optFetchOptions"  OnClick="SetFO('adcFetchAsync')">  
   </TD>  
</TR>  
</TABLE>  
  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run"><BR>  
  
<Script Language="VBScript">  
<!--  
Dim EO         'ExecuteOptions  
Dim FO         'FetchOptions  
EO = "adcExecSync"   'Default value  
FO = "adcFetchBackground"   'Default value  
  
Sub SetExO(NewEO)  
   EO = NewEO  
End Sub  
  
Sub SetFO(NewFO)  
   FO = NewFO  
End Sub  
  
' Set parameters of RDS.DataControl at Run Time  
Sub Run_OnClick  
   RDC.Server = txtServer.Value  
   RDC.SQL = txtSQL.Value  
   RDC.Connect = txtConnect.Value  
   If EO = "adcExecSync" Then   'Determine which ExecuteOption chosen  
      RDC.ExecuteOptions = adcExecSync  
      MsgBox "Recordset brought in on current calling thread Syncronously"  
   Else  
      RDC.ExecuteOptions = adcExecAsync  
      MsgBox "Recordset brought in on another thread Asyncronously"  
   End If  
  
   If FO = "adcFetchBackground" Then      'Determine                 which FetchOption chosen  
      RDC.FetchOptions = adcFetchBackground  
      MsgBox "Control goes back to user after first batch of records returned"  
   ElseIf FO = " adcFetchUpFront" Then  
      RDC.FetchOptions = adcFetchUpFront  
      MsgBox "All records returned before control goes back to user"  
   Else  
      RDC.FetchOptions = adcFetchAsync  
      MsgBox "Control goes back to user immediately"  
   End If  
  
   RDC.Refresh  
End Sub  
-->  
</Script>  
  
</body>  
</html>  
<!-- EndRefreshVBS -->  
```  
  
## <a name="see-also"></a>См. также  
 [Объект DataControl (служба удаленных рабочих СТОЛОВ)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Свойство ExecuteOptions (служба удаленных рабочих СТОЛОВ)](../../../ado/reference/rds-api/executeoptions-property-rds.md)   
 [Свойство FetchOptions (служба удаленных рабочих СТОЛОВ)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)   
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Метод Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)


