---
title: Классы-оболочки Java ADO | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 34a4ab7327edfb6f6f4204fb457ade97be4f5975
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702924"
---
# <a name="ado-java-class-wrappers"></a>Классы-оболочки Java для объектов ADO
Этот код объявляет экземпляр ADO [записей](../../../ado/reference/ado-api/recordset-object-ado.md) оболочки класса и инициализирует его, все в одной строке кода. Кроме того, он объявляет переменные для каждого аргумента в [откройте](../../../ado/reference/ado-api/open-method-ado-recordset.md) метод, особенно для [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) и [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) (так как Java не поддерживает перечисленные типы). Он открывает и закрывает **записей** объекта. Задав Rs1 NULL просто планирует эту переменную, чтобы освободить после ее выпуска систематический и с периодической неиспользуемых объектов выполняет Java.  
  
```java
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>См. также  
 [Использование пакета Microsoft SDK для Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
