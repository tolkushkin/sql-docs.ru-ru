---
title: Пример свойства ActiveConnection (Visual C++) Catalog | Документация Майкрософт
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
- ActiveConnection property [ADOX], VC++ example
ms.assetid: 518905a9-6044-4194-af6c-84952d95939d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 64388f36f93857c9c6b2b5c036d3c96ddda9152d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707964"
---
# <a name="catalog-activeconnection-property-example-vc"></a>Пример свойства ActiveConnection объекта Catalog (Visual C++)
Установка [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) присвоено допустимое соединение, откройте «открывает» каталог. Из открытых каталога можно получить доступ к схеме объектов, содержащихся в каталоге.  
  
```  
// CatalogActiveConnectionCpp.cpp  
// compile with: /EHsc  
#import "msado15.dll" rename("EOF", "EndOfFile")  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void OpenConnectionX();  
void OpenConnectionWithStringX();  
  
int main() {  
   if ( FAILED( ::CoInitialize(NULL) ) )  
      return -1;  
  
   OpenConnectionX();  
   OpenConnectionWithStringX();  
   ::CoUninitialize();  
}  
  
void OpenConnectionX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Define ADODB object pointers  
   ADODB::_ConnectionPtr m_pCnn = NULL;  
  
   // Define string variables.  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = 'c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCnn.CreateInstance(__uuidof(ADODB::Connection)));  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCnn->Open(strcnn, "", "", NULL);  
      m_pCatalog->PutActiveConnection(_variant_t((IDispatch *) m_pCnn));  
      _variant_t vIndex = (short) 0;  
      cout<<m_pCatalog->Tables->GetItem(vIndex)->Type<<endl;  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in OpenConnectionX...." << endl;  
   }  
  
   if (m_pCnn)  
      if (m_pCnn->State == 1)  
         m_pCnn->Close();  
}  
  
void OpenConnectionWithStringX() {  
   HRESULT hr = S_OK;  
  
   // Define ADOX object pointers, initialize pointers. These are in ADODB namespace.  
   _CatalogPtr m_pCatalog = NULL;  
  
   // Define string variables.  
   _bstr_t strcnn("Provider='Microsoft.JET.OLEDB.4.0';Data source = 'c:\\Northwind.mdb';");  
  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof (Catalog)));  
      m_pCatalog->PutActiveConnection(strcnn);  
      _variant_t vIndex = (short) 0;  
      cout<<m_pCatalog->Tables->GetItem(vIndex)->Type<<endl;  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
   catch(...) {  
      cout << "Error occured in OpenConnectionWithStringX...." << endl;  
   }  
}  
```  
  
## <a name="see-also"></a>См. также  
 [Свойство ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
