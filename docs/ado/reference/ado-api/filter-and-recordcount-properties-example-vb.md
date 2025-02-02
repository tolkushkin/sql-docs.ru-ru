---
title: Filter и RecordCount свойства (Visual Basic) | Документация Майкрософт
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
- RecordCount property [ADO], Visual Basic example
- Filter property [ADO], Visual Basic example
ms.assetid: e8bc63c7-8967-438a-9a49-512478a87a15
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0fbb20e623c37528285b8c1dd248ad24217cb2bc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697812"
---
# <a name="filter-and-recordcount-properties-example-vb"></a>Примеры свойств Filter и RecordCount (Visual Basic)
В этом примере откройте [записей](../../../ado/reference/ado-api/recordset-object-ado.md) в таблице издателей в ***Pubs*** базы данных. Затем он использует [фильтра](../../../ado/reference/ado-api/filter-property.md) свойство, чтобы ограничить количество видимых записей на этих издателях, в определенной страны или региона. **RecordCount** свойство используется для отображения разницу между отфильтрованные и неотфильтрованные наборы записей.  
  
```  
'BeginFilterVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    ' recordset variables  
    Dim rstPublishers As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim SQLPublishers As String  
  
     ' criteria variables  
    Dim intPublisherCount As Integer  
    Dim strCountry As String  
    Dim strMessage As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset with data from Publishers table  
    Set rstPublishers = New ADODB.Recordset  
    SQLPublishers = "publishers"  
    rstPublishers.Open SQLPublishers, strCnxn, adOpenStatic, , adCmdTable  
  
    intPublisherCount = rstPublishers.RecordCount  
  
    ' get user input  
    strCountry = Trim(InputBox("Enter a country to filter on (e.g. USA):"))  
  
    If strCountry <> "" Then  
        ' open a filtered Recordset object  
        rstPublishers.Filter = "Country ='" & strCountry & "'"  
  
        If rstPublishers.RecordCount = 0 Then  
            MsgBox "No publishers from that country."  
        Else  
           ' print number of records for the original recordset  
           ' and the filtered recordset  
            strMessage = "Orders in original recordset: " & _  
                vbCr & intPublisherCount & vbCr & _  
                "Orders in filtered recordset (Country = '" & _  
                strCountry & "'): " & vbCr & _  
                rstPublishers.RecordCount  
            MsgBox strMessage  
        End If  
    End If  
  
    ' clean up  
    rstPublishers.Close  
    Cnxn.Close  
    Set rstPublishers = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstPublishers Is Nothing Then  
        If rstPublishers.State = adStateOpen Then rstPublishers.Close  
    End If  
    Set rstPublishers = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndFilterVB  
```  
  
> [!NOTE]
>  Когда вы знаете, вы хотите выбрать данные, это обычно более эффективно, чтобы открыть **записей** с помощью инструкции SQL. В этом примере показано, как можно создать только один **записей** и получение записей из определенной страны.  
  
```  
Attribute VB_Name = "Filter"  
```  
  
## <a name="see-also"></a>См. также  
 [Свойство фильтра](../../../ado/reference/ado-api/filter-property.md)   
 [Свойство RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)   
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
