---
title: Открытие и закрытие примеры методов (Visual C++) | Документация Майкрософт
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
- Close method [ADO], VC++ example
- Open method [ADO], VC++ example
ms.assetid: f74a81fd-cbcc-4143-b9f8-774c88dd4fad
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1f8e397482833c54d9ed58604720e7bbd6321f26
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707416"
---
# <a name="open-and-close-methods-example-vc"></a>Примеры методов Open и Close (Visual C++)
В этом примере используется **откройте** и [закрыть](../../../ado/reference/ado-api/close-method-ado.md) методы на обоих [записей](../../../ado/reference/ado-api/recordset-object-ado.md) и [подключения](../../../ado/reference/ado-api/connection-object-ado.md) объекты, которые были открыты.  
  
```  
// Open_Close_Methods.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <oledb.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// class extracts only fname,lastname and hire_date from employee table  
class CEmployeeRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CEmployeeRs)  
  
      // Column fname is the 2nd field in the table     
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_sze_fname,   
      sizeof(m_sze_fname), le_fnameStatus, FALSE)  
  
      // Column lname is the 4th field in the table.  
      ADO_VARIABLE_LENGTH_ENTRY2(4, adVarChar, m_sze_lname,   
      sizeof(m_sze_lname), le_lnameStatus, FALSE)  
  
      // Column hiredate is the 8th field in the table.  
      ADO_VARIABLE_LENGTH_ENTRY2(8, adDBDate,m_sze_hiredate,   
      sizeof(m_sze_hiredate), le_hiredateStatus, TRUE)  
  
   END_ADO_BINDING()  
  
public:  
   CHAR   m_sze_fname[21];  
   ULONG   le_fnameStatus;  
   CHAR   m_sze_lname[31];  
   ULONG   le_lnameStatus;  
   DBDATE   m_sze_hiredate;  
   ULONG   le_hiredateStatus;  
};  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void OpenX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   OpenX();  
   ::CoUninitialize();  
}  
  
void OpenX() {  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB:: namespace  
   _RecordsetPtr pRstEmployee = NULL;  
   _ConnectionPtr pConnection = NULL;  
  
   // Define string variables.  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   IADORecordBinding *picRs = NULL;   // Interface Pointer declared.  
   CEmployeeRs emprs;   // C++ Class object  
   DBDATE varDate;  
  
   try {  
      // open connection and record set  
      TESTHR(pConnection.CreateInstance(__uuidof(Connection)));  
      pConnection->Open(strCnn, "", "", adConnectUnspecified);  
  
      TESTHR(pRstEmployee.CreateInstance(__uuidof(Recordset)));  
      pRstEmployee->Open("Employee", _variant_t((IDispatch *)pConnection,true),   
         adOpenKeyset, adLockOptimistic, adCmdTable);  
  
      // Open an IADORecordBinding interface pointer for Binding Recordset to a class.  
      TESTHR(pRstEmployee->QueryInterface(__uuidof(IADORecordBinding),(LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ Class here.  
      TESTHR(picRs->BindToRecordset(&emprs));  
  
      // Assign first employee record's hire date to variable, then change hire date.  
      varDate = emprs.m_sze_hiredate;  
      printf("Original data\n");  
      printf("\tName - Hire Date\n");  
      printf("  %s  %s - %d/%d/%d\n\n",  
         emprs.le_fnameStatus == adFldOK ?   
         emprs.m_sze_fname : "<NULL>",  
         emprs.le_lnameStatus == adFldOK ?   
         emprs.m_sze_lname : "<NULL>",  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.month : 0,  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.day : 0,  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.year : 0);   
  
      emprs.m_sze_hiredate.year = 1900;  
      emprs.m_sze_hiredate.month = 1;  
      emprs.m_sze_hiredate.day = 1;  
      picRs->Update(&emprs);  
  
      printf("\nChanged data\n");  
      printf("\tName - Hire Date\n");  
      printf("  %s %s - %d/%d/%d\n\n",  
         emprs.le_fnameStatus == adFldOK ?   
         emprs.m_sze_fname : "<NULL>",  
         emprs.le_lnameStatus == adFldOK ?   
         emprs.m_sze_lname : "<NULL>",  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.month : 0,  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.day : 0,  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.year : 0);   
  
      // Requery Recordset and reset the hire date.  
      pRstEmployee->Requery(adOptionUnspecified);  
  
      // Open IADORecordBinding interface pointer for Binding Recordset to a class.  
      TESTHR(pRstEmployee->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Rebind the Recordset to a C++ Class here.  
      TESTHR(picRs->BindToRecordset(&emprs));  
      emprs.m_sze_hiredate = varDate;  
      picRs->Update(&emprs);  
      printf("\nData after reset\n");  
      printf("\tName - Hire Date\n");  
      printf("  %s %s - %d/%d/%d", emprs.le_fnameStatus == adFldOK ?   
         emprs.m_sze_fname : "<NULL>",  
         emprs.le_lnameStatus == adFldOK ?   
         emprs.m_sze_lname : "<NULL>",  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.month : 0,  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.day : 0,  
         emprs.le_hiredateStatus == adFldOK ?   
         emprs.m_sze_hiredate.year : 0);   
   }  
   catch(_com_error &e) {  
      // Display errors, if any. Pass a connection pointer accessed from the Connection.  
      PrintProviderError(pConnection);  
      PrintComError(e);  
   }  
  
   // Clean up objects before exit.  
   if (pRstEmployee)  
      if (pRstEmployee->State == adStateOpen)  
         pRstEmployee->Close();  
   if (pConnection)  
      if (pConnection->State == adStateOpen)  
         pConnection->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0) {  
      long nCount = pConnection->Errors->Count;  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print COM errors.   
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
## <a name="see-also"></a>См. также  
 [Метод Close (ADO)](../../../ado/reference/ado-api/close-method-ado.md)   
 [Объект Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Метод Open (объект Connection ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Метод Open (объект Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Объект Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
