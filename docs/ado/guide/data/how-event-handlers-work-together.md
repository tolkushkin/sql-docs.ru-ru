---
title: Совместная работа обработчиков событий | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cb02a96e6ee3d28c67e21996677c02b58fc97c07
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718391"
---
# <a name="how-event-handlers-work-together"></a>Совместная работа обработчиков событий
Если вы программируете на Visual Basic, все обработчики событий для **подключения** и **записей** события должен быть реализован, независимо от того, ли вы фактически обработать все события. Объем работ по реализации, что необходимо сделать зависит от языка программирования. Дополнительные сведения см. в разделе [создание экземпляра события ADO языком](../../../ado/guide/data/ado-event-instantiation-by-language.md).  
  
## <a name="paired-event-handlers"></a>Обработчики парных событий  
 Каждый обработчик событий будет имеет связанный **завершить** обработчик событий. Например, в том случае, когда приложение изменяет значение поля, **события WillChangeField** вызывается обработчик события. Если изменение приемлем, приложение оставляет **adStatus** параметр без изменений и выполняется операция. По завершении операции **FieldChangeComplete** событие уведомляет приложение о завершении операции. Если она завершится успешно, **adStatus** содержит **adStatusOK**; в противном случае **adStatus** содержит **adStatusErrorsOccurred** и необходимо проверить **ошибка** объекта, чтобы определить причину ошибки.  
  
 Когда **события WillChangeField** является именем, можно предположить, что изменение не следует выполнить. В этом случае задайте **adStatus** для **adStatusCancel.** Операция отменяется и **FieldChangeComplete** получает событие **adStatus** значение **adStatusErrorsOccurred**. **Ошибка** объект содержит **adErrOperationCancelled** таким образом, чтобы ваши **FieldChangeComplete** обработчик знает, что операция была отменена. Тем не менее, необходимо проверить значение **adStatus** параметра перед изменением, поскольку настройка параметра **adStatus** для **adStatusCancel** не действует, если был задан параметр Чтобы **adStatusCantDeny** при входе в процедуру.  
  
 Иногда операция может вызвать несколько событий. Например **записей** объект пару событий для **поле** изменений и **записи** изменения. Когда приложение изменяет значение **поле**, **события WillChangeField** вызывается обработчик события. Если определит, что операция может продолжаться, **события WillChangeRecord** также вызывается обработчик событий. Если этот обработчик также позволяет по-прежнему событие, изменения и **FieldChangeComplete** и **RecordChangeComplete** обработчики событий вызываются. Порядок, в котором вызываются обработчики событий для определенной операции будет не определен, поэтому старайтесь не писать код, зависящий от вызова обработчиков в определенной последовательности.  
  
 В случаях когда несколько событий будет, одно из событий может привести к отмене отложенной операции. Например, в том случае, когда приложение изменяет значение элемента **поле**, оба **события WillChangeField** и **события WillChangeRecord** обработчики событий обычно вызывается. Тем не менее если она будет отменена в первый обработчик событий, связанный с ним **завершить** обработчик немедленно вызывается с **adStatusOperationCancelled**. Второй обработчик никогда не вызывается. Если, однако первый обработчик событий позволяет выполнить событие, будет вызван обработчик событий. Если он затем отменяет операцию, оба **завершить** событий будет вызываться, как показано в предыдущих примерах.  
  
## <a name="unpaired-event-handlers"></a>Обработчики непарных событий  
 До тех пор, пока состояние, передаваемый событие не является **adStatusCantDeny**, можно отключить уведомления о событиях для любых событий, возвращая **adStatusUnwantedEvent** в *состояние*параметра. Например, если ваш **завершить** обработчик событий вызывается в первый раз, можно вернуть **adStatusUnwantedEvent**. Впоследствии вы получите только **будет** события. Тем не менее некоторые события могут запускаться по более чем одной основной причине. В этом случае для этого события соответствует *Причина* параметра. При возврате **adStatusUnwantedEvent**, будет получать уведомления для этого события только в том случае, если они встречаются для этой конкретной причины. Другими словами вы потенциально получите уведомление для каждой из возможных причин событие может быть включено.  
  
 Единый **будет** обработчики событий можно использовать при необходимо просмотреть параметры, которые будут использоваться в операции. Можно изменить эти параметры операции или отменить операцию.  
  
 Кроме того, оставьте **завершить** включено уведомление о событии. При вызове первый обработчик событий будет возвращать **adStatusUnwantedEvent**. Впоследствии вы получите только **завершить** события.  
  
 Единый **завершить** обработчики событий можно использовать для управления асинхронных операций. Каждой асинхронной операции имеет соответствующий **завершить** событий.  
  
 Например, может занять много времени для заполнения большой [записей](../../../ado/reference/ado-api/recordset-object-ado.md) объекта. Если ваше приложение написано правильно, вы можете начать `Recordset.Open(...,adAsyncExecute)` операции и продолжить выполнение других задач обработки. Со временем можно уведомления, если **записей** заполняется **ExecuteComplete** событий.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>Обработчики событий для одного и нескольких объектов  
 Гибкость языка программирования, например Microsoft Visual C++® позволяет иметь один обработчик событий: обработка событий из нескольких объектов. Например, имеется один **Disconnect** обработчик событий: обработка событий из нескольких **подключения** объектов. Если одно из подключений завершился, **Disconnect** обработчик событий будет вызываться. Чтобы сообщить нужное подключение вызвавшее событие, так как обработчик событий объекта будет иметь значение к соответствующему **подключения** объекта.  
  
> [!NOTE]
>  Этот метод не может использоваться в Visual Basic, так как этот язык можно сопоставлять только один объект обработчика событий.  
  
## <a name="see-also"></a>См. также  
 [Общие сведения об обработчике событий ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Создание экземпляра события ADO по языку](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Параметры события](../../../ado/guide/data/event-parameters.md)   
 [Типы событий](../../../ado/guide/data/types-of-events.md)
