---
title: Диалоговое окно «Добавление издателя»
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.addpublisher.f1
helpviewer_keywords:
- Add Publisher dialog box
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 735162edb8e7eda06e99d69ed74d4752b7f0d950
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62676920"
---
# <a name="sql-server-replication-add-publisher-dialog-box"></a>Диалоговое окно «Добавление издателя репликации SQL Server» 
  Диалоговое окно **Добавление издателя** позволяет добавить одного или несколько издателей в левую панель монитора репликации. После добавления издателя в правой панели отображаются сведения об издателе, выбранном в левой панели.  
  
## <a name="options"></a>Параметры  
 **Добавить**  
 Нажмите, чтобы выбрать тип добавляемого издателя, после чего откроется диалоговое окно **Соединение с сервером** . Доступны следующие возможности:  
  
-   **Добавить издатель SQL Server…**  
  
     Подключить к издателю с помощью диалогового окна **Соединение с сервером** .  
  
-   **Добавить издатель Oracle...**  
  
     Подключить к распространителю [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , связанному с издателем Oracle, с помощью диалогового окна **Соединение с сервером** .  
  
-   **Указать распространителя и добавить его издателей...**  
  
     Подключить к распространителю [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , связанному с одним или несколькими издателями, с помощью диалогового окна **Соединение с сервером** .  
  
 После успешного подключения к издателю или распространителю в сетке, расположенной в верхней части диалогового окна, отображаются имена всех издателей и их распространителей.  
  
> [!NOTE]  
>  Зачастую распространитель и издатель работают на одном экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], но распространитель может работать и на другом экземпляре (такую конфигурацию называют удаленным распространителем).  
  
 **Удалить**  
 Чтобы удалить издатель из списка добавляемых издателей, выберите издателя в сетке, расположенной в верхней части диалогового окна, и нажмите кнопку **Удалить** .  
  
> [!NOTE]  
>  Эту кнопку нельзя использовать для удаления издателя, если он отображается в мониторе репликации. Чтобы удалить такого издателя, щелкните правой кнопкой мыши издателя в левой панели монитора репликации и выберите в контекстном меню пункт **Удалить**.  
  
 **Соединяться автоматически, когда запускается монитор репликации**  
 Выберите этот параметр, чтобы разрешить монитору репликации автоматически соединяться с распространителем и извлекать сведения о состоянии издателя, выбранного в сетке в верхней части диалогового окна. Если этот флажок снят, то после запуска монитора репликации необходимо установить соединение вручную: щелкните правой кнопкой мыши значок издателя на левой панели монитора репликации и выберите пункт меню **Подключить**.  
  
 **Автоматически обновлять состояние этого издателя и его публикаций**  
 Выберите этот параметр, чтобы разрешить монитору репликации автоматически обновлять состояние издателя, выбранного в сетке в верхней части диалогового окна. Если выбран этот параметр, то монитор репликации опрашивает распространитель для получения сведений о состоянии издателя и его публикаций. Интервал опроса задается параметром **Частота обновления** . Дополнительные сведения об обновлении в мониторе репликации см. в статье [Кэширование, обновление и производительность монитора репликации](monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Частота обновления**  
 Введите значение (в секундах), указывающее, как часто монитор репликации должен опрашивать распространитель для получения сведений о состоянии. Чем ниже значения, тем чаще производится опрос, что может снизить производительность распространителя, если производится наблюдение за большим числом издателей. Рекомендуется проверить систему для определения подходящего значения. Параметр **Частота обновления** используется также и при включении режима **Автоматическое обновление** в любом окне сведений монитора репликации.  
  
 **Показывать этот издатель в следующей группе**  
 Выберите группу издателей из списка. Издатель отображается в свой группе в левой панели. Группы предоставляют способ упорядочить издателей и не оказывают влияние на работу репликации. Если группы не определены, для создания новой группы нажмите кнопку **Создать группу**.  
  
 **Создать группу**  
 Нажмите эту кнопку для создания новой группы издателей. Группа издателей предоставляет удобный способ упорядочить издателей в мониторе репликации. Группы не оказывают влияние на данные или связи между серверами в топологии репликации.  
  
## <a name="see-also"></a>См. также:  
 [Запуск монитора репликации](monitor/start-the-replication-monitor.md)   
 [Наблюдение за репликацией](monitoring-replication.md)  
  
  
