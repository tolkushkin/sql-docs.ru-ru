---
title: Создайте пример метода (Visual Basic) | Документация Майкрософт
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
- Create method [ADOX], Visual Basic example
ms.assetid: d7ea0244-596a-404e-8f30-71cadab8d8fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9fb207d7ba30c12b1d694bbef5337c51e1062440
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703322"
---
# <a name="create-method-example-vb"></a>Пример метода Create (Visual Basic)
Ниже показано, как создать новую базу данных Microsoft Jet с [создать](../../../ado/reference/adox-api/create-method-adox.md) метод.  
  
```  
Attribute VB_Name = "Create"  
Option Explicit  
  
' BeginCreateDatabaseVB  
Sub CreateDatabase()  
    On Error GoTo CreateDatabaseError  
  
    Dim cat As New ADOX.Catalog  
    cat.Create "Provider='Microsoft.Jet.OLEDB.4.0';Data Source='new.mdb'"  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
CreateDatabaseError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateDatabaseVB  
```  
  
## <a name="see-also"></a>См. также  
 [Объект Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Метод Create (ADOX)](../../../ado/reference/adox-api/create-method-adox.md)
