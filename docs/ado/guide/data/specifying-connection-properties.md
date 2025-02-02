---
title: Указание свойств подключения | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 659701a984a675418b8654e9f747efe5d9e07762
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700327"
---
# <a name="specifying-connection-properties"></a>Указание свойств подключения
Можно указать большое количество информации, определяемое [строку подключения](../../../ado/guide/data/creating-a-connection-string.md) путем задания свойств **подключения** объекта до открытия соединения. Например, вы сможете достигнуть тот же эффект, рассматривался в строке подключения [Создание строки подключения](../../../ado/guide/data/creating-a-connection-string.md) , используя следующий код.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase имеет значение только в том случае, после открытия соединения.  
  
> [!NOTE]
>  В ADO не должны использовать пароль, содержащий точку с запятой («;»), если пароль заключен в одинарные кавычки.
