---
title: Чтение, ReadText, Write и примеры методов WriteText (Visual Basic) | Документация Майкрософт
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
- ReadText method [ADO], Visual Basic example
- Write method [ADO], Visual Basic example
- Read method [ADO], Visual Basic example
- WriteText method [ADO], Visual Basic example
ms.assetid: 699b73f7-04f9-4d46-94b2-6cb12be6de56
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e9fb54ab264b6f1a247407d5bfdecdbdf6c4dc16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712053"
---
# <a name="read-readtext-write-and-writetext-methods-example-vb"></a>Чтение, ReadText, Write и примеры методов WriteText (Visual Basic)
В этом примере показано, как для считывания содержимого текстового поля в обоих текст [Stream](../../../ado/reference/ado-api/stream-object-ado.md) и двоичный файл **Stream**. Другие свойства и методы, представленные включают [позиции](../../../ado/reference/ado-api/position-property-ado.md), [размер](../../../ado/reference/ado-api/size-property-ado-parameter.md), [Charset](../../../ado/reference/ado-api/charset-property-ado.md), и [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
```  
'BeginReadVB  
Private Sub cmdRead_Click()  
    On Error GoTo ErrorHandler  
  
    'Declare variables  
    Dim objStream As Stream  
    Dim varA As Variant  
    Dim bytA() As Byte  
    Dim i As Integer  
    Dim strBytes As String  
  
    'Instantiate and Open Stream  
    Set objStream = New Stream  
    objStream.Open  
  
    'Write the text content of a textbox to the stream  
    If Text1.Text = "" Then  
        Err.Raise 1, , "The text field is blank."  
    End If  
    objStream.WriteText Text1.Text  
  
    'Display the text contents and size of the stream  
    objStream.Position = 0  
    Debug.Print "Default text:"  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    'Switch character set and display  
    objStream.Position = 0  
    objStream.Charset = "Windows-1252"  
    Debug.Print "New Charset text:"  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    'Switch to a binary stream and display  
    objStream.Position = 0  
    objStream.Type = adTypeBinary  
    Debug.Print "Binary:"  
    Debug.Print objStream.Read  
    Debug.Print objStream.Size  
  
    'Load an array of bytes with the text box text  
    ReDim bytA(Len(Text1.Text))  
    For i = 1 To Len(Text1.Text)  
        bytA(i - 1) = CByte(Asc(Mid(Text1.Text, i, 1)))  
    Next  
  
    'Write the buffer to the binary stream and display  
    objStream.Position = 0  
    objStream.Write bytA()  
    objStream.SetEOS  
    objStream.Position = 0  
    Debug.Print "Binary after Write:"  
    Debug.Print objStream.Read  
    Debug.Print objStream.Size  
  
    'Switch back to a text stream and display  
    Debug.Print "Translated back:"  
    objStream.Position = 0  
    objStream.Type = adTypeText  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    ' clean up  
    objStream.Close  
    Set objStream = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not objStream Is Nothing Then  
        If objStream.State = adStateOpen Then objStream.Close  
    End If  
    Set objStream = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndReadVB  
```  
  
## <a name="see-also"></a>См. также  
 [Свойство CharSet (ADO)](../../../ado/reference/ado-api/charset-property-ado.md)   
 [Свойство position (ADO)](../../../ado/reference/ado-api/position-property-ado.md)   
 [Метод Read](../../../ado/reference/ado-api/read-method.md)   
 [Метод ReadText](../../../ado/reference/ado-api/readtext-method.md)   
 [Метод SetEOS](../../../ado/reference/ado-api/seteos-method.md)   
 [Свойство Size (ADO Stream)](../../../ado/reference/ado-api/size-property-ado-stream.md)   
 [Объект Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Создать метод](../../../ado/reference/ado-api/write-method.md)   
 [Метод WriteText](../../../ado/reference/ado-api/writetext-method.md)
