---
title: Пример свойства SortOrder (Visual Basic) | Документация Майкрософт
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
- SortOrder property [ADOX]
ms.assetid: d9502254-d89b-4bcb-94f1-6418f89e7f30
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f3506070a55b852292067ec89ee24ee11417d6da
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705774"
---
# <a name="sortorder-property-example-vb"></a>Пример свойства SortOrder (Visual Basic)
В этом примере показано [SortOrder](../../../ado/reference/adox-api/sortorder-property-adox.md) свойство [столбец](../../../ado/reference/adox-api/column-object-adox.md) , добавленную в [столбцы](../../../ado/reference/adox-api/columns-collection-adox.md) коллекцию [индекс](../../../ado/reference/adox-api/index-object-adox.md). Код добавляет по возрастанию индекса столбцу страны в **сотрудников** таблицы, затем отображает записи. Затем код добавляет убывания индекса столбцу страны в **сотрудников** таблицы и отображает записи еще раз. Отображается разница между сортировкой по возрастанию и убыванию индексов.  
  
```  
' BeginSortOrderVB  
Sub Main()  
    On Error GoTo SortOrderXError  
  
    Dim cnn As New ADODB.Connection  
    Dim catNorthwind As New ADOX.Catalog  
    Dim idxAscending As New ADOX.Index  
    Dim idxDescending As New ADOX.Index  
    Dim rstEmployees As New ADODB.Recordset  
  
    ' Connect to the catalog.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
    Set catNorthwind.ActiveConnection = cnn  
  
    ' Append Country column to new index.  
    idxAscending.Columns.Append "Country"  
    idxAscending.Columns("Country").SortOrder = adSortAscending  
    idxAscending.Name = "Ascending"  
    idxAscending.IndexNulls = adIndexNullsAllow  
  
    'Append new index to Employees table.  
    catNorthwind.Tables("Employees").Indexes.Append idxAscending  
  
    rstEmployees.Index = idxAscending.Name  
    rstEmployees.Open "Employees", cnn, adOpenKeyset, _  
        adLockOptimistic, adCmdTableDirect  
  
    With rstEmployees  
        .MoveFirst  
        Debug.Print "Index = " & .Index  
        Debug.Print "  Country - Name"  
  
        ' Enumerate the Recordset. The value of the  
        ' IndexNulls property will determine if the newly  
        ' added record appears in the output.  
        Do While Not .EOF  
            Debug.Print "    " & !Country & " - " & _  
                !FirstName & " " & !LastName  
            .MoveNext  
        Loop  
  
        .Close  
    End With  
  
    ' Append Country column to new index.  
    idxDescending.Columns.Append "Country"  
    idxDescending.Columns("Country").SortOrder = adSortDescending  
    idxDescending.Name = "Descending"  
    idxDescending.IndexNulls = adIndexNullsAllow  
  
    'Append descending index to Employees table.  
    catNorthwind.Tables("Employees").Indexes.Append idxDescending  
  
    rstEmployees.Index = idxDescending.Name  
    rstEmployees.Open "Employees", cnn, adOpenKeyset, _  
        adLockOptimistic, adCmdTableDirect  
  
    With rstEmployees  
        .MoveFirst  
        Debug.Print "Index = " & .Index  
        Debug.Print "  Country - Name"  
  
        ' Enumerate the Recordset. The value of the  
        ' IndexNulls property will determine if the newly  
        ' added record appears in the output.  
        Do While Not .EOF  
            Debug.Print "    " & !Country & " - " & _  
                !FirstName & " " & !LastName  
            .MoveNext  
        Loop  
  
        .Close  
    End With  
  
    ' Delete new indexes because this is a demonstration.  
    catNorthwind.Tables("Employees").Indexes.Delete idxAscending.Name  
    catNorthwind.Tables("Employees").Indexes.Delete idxDescending.Name  
  
    'Clean up  
    cnn.Close  
    Set catNorthwind = Nothing  
    Set idxAscending = Nothing  
    Set idxDescending = Nothing  
    Set rstEmployees = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
SortOrderXError:  
  
    Set catNorthwind = Nothing  
    Set idxAscending = Nothing  
    Set idxDescending = Nothing  
  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndSortOrderVB  
```  
  
## <a name="see-also"></a>См. также  
 [Объект Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Коллекция Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Объект INDEX (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Свойство SortOrder (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md)
