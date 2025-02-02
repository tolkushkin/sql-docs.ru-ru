---
title: Отправка в удаленную закрытую очередь сообщений в задаче "Скрипт" | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13d62d72764060ef924d02ef735ff277d14ca4ed
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724283"
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>Отправка в удаленную закрытую очередь сообщений в задаче «Скрипт»

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Служба очередей сообщений (называемая также MSMQ) облегчает разработчикам обеспечение быстрой и надежной связи с прикладными программами при помощи отправки и получения сообщений. Очередь сообщений может находиться в локальном или в удаленном компьютере и может быть открытой или закрытой. В службах [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] диспетчер соединений MSMQ и задача «Очередь сообщений» не поддерживают отправку в закрытую очередь на удаленном компьютере. Но при использовании задачи «Скрипт» можно легко отправить сообщение в удаленную закрытую очередь.  
  
> [!NOTE]  
>  Если нужно создать задачу, которую будет удобно использовать в нескольких пакетах, рекомендуется начать разработку пользовательской задачи с этого образца задачи «Скрипт». Дополнительные сведения см. в разделе [Разработка пользовательской задачи](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Описание  
 В следующем примере для отправки текста (содержащегося в переменной пакета) в удаленную закрытую очередь сообщений используется существующий диспетчер соединений MSMQ вместе с объектами и методами из пространства имен System.Messaging. Вызов метода M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) диспетчера подключений MSMQ возвращает объект **MessageQueue**, метод **Send** которого выполняет эту задачу.  
  
#### <a name="to-configure-this-script-task-example"></a>Настройка этого образца задачи «Скрипт»  
  
1.  Создайте диспетчер соединений MSMQ с именем по умолчанию. Установите путь к допустимой удаленной закрытой очереди в следующем формате:  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  Создайте переменную служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] с именем **MessageText** типа **String**, чтобы передать текст сообщения в скрипт. Введите сообщение по умолчанию как значение переменной.  
  
3.  Добавьте задачу «Скрипт» в область конструктора и измените ее. На вкладке **Скрипт** **редактора задачи "Скрипт"** добавьте переменную `MessageText` к свойству **ReadOnlyVariables**, чтобы сделать переменную доступной в скрипте.  
  
4.  Нажмите кнопку **Изменить скрипт**, чтобы открыть редактор скриптов средств [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] для приложений (VSTA).  
  
5.  В проект скрипта добавьте ссылку на пространство имен **System.Messaging**.  
  
6.  Замените содержимое окна скрипта кодом из следующего раздела.  
  
## <a name="code"></a>Код  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Messaging  
  
Public Class ScriptMain  
  
    Public Sub Main()  
  
        Dim remotePrivateQueue As MessageQueue  
        Dim messageText As String  
  
        remotePrivateQueue = _  
            DirectCast(Dts.Connections("Message Queue Connection Manager").AcquireConnection(Dts.Transaction), _  
            MessageQueue)  
        messageText = DirectCast(Dts.Variables("MessageText").Value, String)  
        remotePrivateQueue.Send(messageText)  
  
        Dts.TaskResult = ScriptResults.Success  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Messaging;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
  
            MessageQueue remotePrivateQueue = new MessageQueue();  
            string messageText;  
  
            remotePrivateQueue = (MessageQueue)(Dts.Connections["Message Queue Connection Manager"].AcquireConnection(Dts.Transaction) as MessageQueue);  
            messageText = (string)(Dts.Variables["MessageText"].Value);  
            remotePrivateQueue.Send(messageText);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
```  
  
## <a name="see-also"></a>См. также:  
 [Задача «Очередь сообщений»](../../integration-services/control-flow/message-queue-task.md)  
  
  
