---
title: Отсоединение от экземпляра сервера SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7783fa93912c305403cc34ad6e52668123d164ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192075"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Отсоединение от экземпляра SQL Server
  Закрытие и отсоединение объектов SMO [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] вручную не требуется. Соединения открываются и закрываются по мере необходимости.  
  
## <a name="connection-pooling"></a>Организация пулов соединений  
 Соединение не освобождается автоматически при вызове метода <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A>. Чтобы освободить соединение обратно в пул, необходимо явно вызвать метод <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A>. Можно также запросить соединение вне пула. Это делается путем установки свойства <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> свойства <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>, которое ссылается на объект <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Отсоединение от экземпляра SQL Server для объектов RMO  
 При программировании с использованием объектов RMO закрытие серверных соединений немного отличается от закрытия при использовании объектов SMO.  
  
 Так как соединение с сервером для объекта RMO обслуживается <xref:Microsoft.SqlServer.Management.Common.ServerConnection> объекта, этот объект также используется при отсоединении от экземпляра [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] при программировании с помощью объектов RMO. Чтобы закрыть соединение с помощью объекта <xref:Microsoft.SqlServer.Management.Common.ServerConnection>, вызовите метод <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> объекта RMO. После закрытия соединения объекты RMO использовать нельзя.  
  
## <a name="example"></a>Пример  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Закрытие и отсоединение объекта SMO на языке Visual Basic  
 Этот пример кода показывает, как запросить соединение вне пула, задав свойство <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> свойства объекта <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Закрытие и отсоединение объекта SMO на языке Visual C#  
 Этот пример кода показывает, как запросить соединение вне пула, задав свойство <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> свойства объекта <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
```  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
