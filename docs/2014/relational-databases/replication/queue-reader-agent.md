---
title: Агент чтения очереди | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.queuereaderagent.f1
helpviewer_keywords:
- Queue Reader Agent dialog box
ms.assetid: f02d24b6-dcb5-4126-b56e-fab41cfe4337
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f07c9be82be63d01d563499a80e049e572a4150
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262063"
---
# <a name="queue-reader-agent"></a>Агент чтения очереди.
  В диалоговом окне **Агент чтения очереди** предоставляются подробные данные об агенте чтения очереди, в том числе состояние, данные журнала, информационные сообщения и любые сообщения об ошибках.  
  
## <a name="options"></a>Параметры  
 Выберите для просмотра в меню **Просмотр** сеансы агента чтения очереди, а затем конкретный сеанс в сетке, обозначенный как **Сеансы агента чтения очереди**. Подробные сведения об этом сеансе отображаются в сетке, помеченной как **Действия в выбранном сеансе**. Если выбранный сеанс закончен с ошибкой, также выводится на экран текстовое поле, помеченное как **Описание ошибки или сообщение выбранного сеанса** .  
  
 **Просмотр**  
 Выбрать сеансы описываются, как агента чтения очереди для просмотра. Как правило, агент чтения очереди работает постоянно, поэтому просмотреть можно только один сеанс.  
  
 **Состояние**  
 Состояние агента чтения очереди. Возможные значения состояния показаны в следующем списке:  
  
-   Ошибка  
  
-   Попытка повторно выполнить неудачно завершившиеся команды  
  
-   Не выполняется  
  
-   Запущен  
  
 **Start Time**  
 Время начала сеанса.  
  
 **Время окончания**  
 Время окончания сеанса. Если агент не остановлен, это поле остается пустым.  
  
 **Длительность**  
 Продолжительность последнего сеанса агента чтения очереди. Если в данный момент агент работает, отображается время его работы, после завершения сеанса агента отображается общая длительность сеанса.  
  
 **Сообщение об ошибке**  
 Если сеанс завершился ошибкой, в этом поле выводится последнее сообщение об ошибке, записанное агентом чтения очереди. Если сеанс завершился без ошибки, это поле остается пустым.  
  
 **Сообщение действия**  
 Все информационные сообщения и сообщения об ошибках, которые агент чтения очереди записал во время выбранного сеанса.  
  
 **Время действия**  
 Время, когда было выполнено действие, описанное в столбце **Сообщение действия** .  
  
 **Описание ошибки или сообщение выбранного сеанса**  
 Выводится, только если выбранный сеанс отображает значение **Ошибка** в столбце **Состояние** . Это текстовое поле отображает подробные данные об ошибке и о выполняемой во время возникновения ошибки команде. Также содержит ссылки на дополнительные данные, имеющие отношение к ошибке.  
  
## <a name="see-also"></a>См. также  
 [Запуск монитора репликации](monitor/start-the-replication-monitor.md)   
 [Просмотр сведений и выполнение задач с помощью монитора репликации](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Наблюдение за репликацией](monitoring-replication.md)   
 [Replication Agents Overview](agents/replication-agents-overview.md)  
  
  
