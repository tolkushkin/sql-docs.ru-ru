---
title: Выборка данных BLOB-объектов с помощью метода IRow::GetColumns и интерфейса ISequentialStream | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching BLOB data
- ISequentialStream interface
- GetColumns method
- BLOBs, fetching
ms.assetid: b57decda-b0c1-4ef6-8c81-491956de2890
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04eb0e01b1c98552c0364c5b60d918608ae23faa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62511379"
---
# <a name="fetching-blob-data-using-irowgetcolumns-and-isequentialstream"></a>Выборка данных BLOB при помощи метода IRow::GetColumns и интерфейса ISequentialStream
  Следующая функция использует методы **IRow::GetColumns** и **ISequentialStream** для выборки больших данных:  
  
```  
void InitializeAndExecuteCommand()  
{  
    ULONG iidx;  
    WCHAR* wCmdString=OLESTR("SELECT * FROM MyTable");  
    // Do the initialization, create the session, and set command text.  
    hr = pICommandText->Execute(NULL, IID_IRow, NULL,   
                         &cNumRows,(IUnknown **)&pIRow)))  
    //Get 1 column at a time.  
    for(ULONG i=0; i < NoOfColumns; i++)  
      GetSequentialColumn(pIRow, iidx);  
    // Do the clean up.  
}  
HRESULT GetSequentialColumn(IRow* pUnkRow, ULONG iCol)  
{  
    HRESULT hr = NOERROR;  
    ULONG cbRead = 0;  
    ULONG cbTotal = 0;  
    ULONG cColumns = 0;  
    ULONG cReads = 0;  
    ISequentialStream* pIStream = NULL;  
    WCHAR* pBuffer[kMaxBuff]; //50 chars read by ISequentialStream::Read()  
    DBCOLUMNINFO* prgInfo;  
    OLECHAR* pColNames;  
    IColumnsInfo* pIColumnsInfo;  
    DBID columnid;  
    DBCOLUMNACCESS column;  
    hr = pUnkRow->QueryInterface(IID_IColumnsInfo,   
                            (void**) &pIColumnsInfo);  
    if(FAILED(hr))  
        goto CLEANUP;  
    hr = pIColumnsInfo->GetColumnInfo(&cColumns, &prgInfo, &pColNames);  
    // Get Column ID.  
    columnid = (prgInfo + (iCol))->columnid;  
    IUnknown* pUnkStream = NULL;  
    ZeroMemory(&column, sizeof(column));  
    column.columnid = prgInfo[iCol].columnid;  
    // Ask for Iunknown interface pointer.  
    column.wType = DBTYPE_IUNKNOWN;  
    column.pData = (LPVOID*) &pUnkStream;  
  
    hr = pUnkRow->GetColumns(1, &column);  
    // Get ISequentialStream from Iunknown pointer retrieved from  
    // GetColumns().  
    hr = pUnkStream->QueryInterface(IID_ISequentialStream,   
                                   (LPVOID*) &pIStream);  
    ZeroMemory(pBuffer, kMaxBuff * sizeof(WCHAR));  
    // Read 50 chars at a time until no more data.  
    do  
    {  
        hr = pIStream->Read(pBuffer, kMaxBuff, &cbRead);  
        cbTotal = cbTotal + cbRead;  
        // Process the data.  
    } while(cbRead > 0);  
  // Do the cleanup.  
    return hr;  
}  
```  
  
## <a name="see-also"></a>См. также  
 [Выборка данных большого двоичного объекта при помощи интерфейса IRow](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
  
