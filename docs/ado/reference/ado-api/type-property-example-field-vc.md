---
title: Введите пример свойства (объект Field) (Visual C++) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Type property [field] [ADO], VC++ example
ms.assetid: 440dbdb1-16fc-4cfe-9451-59a153852537
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3185f7666d628b6461c3ae3a432393a6965be89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62910446"
---
# <a name="type-property-example-field-vc"></a>Пример свойства Type (объект Field) (Visual C++)
В этом примере показано [тип](../../../ado/reference/ado-api/type-property-ado.md) свойство, отображая имя константы, которая соответствует значению **тип** всех [поле](../../../ado/reference/ado-api/field-object.md) объектов в ***Сотрудников*** таблицы. Функция FieldType является обязательным для выполнения этой процедуры.  
  
## <a name="example"></a>Пример  
  
```  
// BeginTypeFieldCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
  
void TypeX();  
_bstr_t FieldType(int intType);   
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   TypeX();  
   ::CoUninitialize();  
}  
  
void TypeX() {  
   // Define string variables.  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='(local)'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers, initialize pointers.  These are in the ADODB:: namespace.  
   _RecordsetPtr pRstEmployees = NULL;  
   FieldsPtr pFldLoop = NULL;  
  
   try {    
      // Open recordset with data from Employee table.  
      TESTHR(pRstEmployees.CreateInstance(__uuidof(Recordset)));  
      pRstEmployees->Open ("employee", strCnn, adOpenForwardOnly, adLockReadOnly, adCmdTable);  
  
      printf("Fields in Employee Table:\n\n");  
  
      // Enumerate the Fields collection of the Employees table.  
      pFldLoop = pRstEmployees->GetFields();  
      for (short int intFields = 0 ; intFields < (int)pFldLoop->GetCount() ; intFields++) {  
         _variant_t Index;  
         Index.vt = VT_I2;  
         Index.iVal = intFields;  
         printf("  Name: %s\n" , (LPCSTR) pFldLoop->GetItem(Index)->GetName());  
         printf("  Type: %s\n\n", (LPCTSTR)FieldType(pFldLoop->GetItem(Index)->Type));  
      }  
   }  
   catch (_com_error &e) {  
      // Display errors, if any.  Pass connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstEmployees->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         PrintComError(e);  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
  
   // Clean up objects before exit.  
   if (pRstEmployees)  
      if (pRstEmployees->State == adStateOpen)  
         pRstEmployees->Close();  
}  
  
_bstr_t FieldType(int intType) {  
   _bstr_t strType;   
   switch(intType) {  
   case adChar:  
      strType = "adChar";  
      break;  
   case adVarChar:  
      strType = "adVarChar";  
      break;  
   case adSmallInt:  
      strType = "adSmallInt";  
      break;  
   case adUnsignedTinyInt:  
      strType = "adUnsignedTinyInt";  
      break;  
   case adDBTimeStamp:  
      strType = "adDBTimeStamp";  
      break;  
   default:  
      break;  
   }  
   return strType;  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("Error number: %x\t%s\n", pErr->Number, (LPCSTR) pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.    
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
 **Поля в таблице сотрудников.**  
 **Имя: emp_id**  
 **Тип: adChar**  
 **Имя: fname**  
 **Type: adVarChar**  
 **Имя: minit**  
 **Тип: adChar**  
 **Имя: lname**  
 **Type: adVarChar**  
 **Имя: job_id**  
 **Тип: adSmallInt**  
 **Имя: job_lvl**  
 **Type: adUnsignedTinyInt**  
 **Имя: pub_id**  
 **Тип: adChar**  
 **Имя: hire_date**  
 **Тип: adDBTimeStamp**   
## <a name="see-also"></a>См. также  
 [Объект field](../../../ado/reference/ado-api/field-object.md)   
 [Свойство Type (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
