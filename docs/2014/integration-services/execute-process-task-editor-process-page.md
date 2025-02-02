---
title: Редактор задач процесса (страница «процесс») выполнение | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process Task Editor
ms.assetid: 0fc22406-e79b-47a4-a7e4-108d4ce6202f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa799404777f8f0ef0a8a07a81c8c7961c636004
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059032"
---
# <a name="execute-process-task-editor-process-page"></a>Редактор задачи «Выполнение процесса» (страница «Процесс»)
  Страница **Процесс** диалогового окна **Редактор задачи «Выполнение процесса»** позволяет настраивать параметры выполнения процесса. Эти параметры включают исполняемый объект, его расположение, аргументы командной строки и переменные для входных и выходных данных.  
  
 Дополнительные сведения об этой задаче см. в разделе [Execute Process Task](control-flow/execute-process-task.md).  
  
## <a name="options"></a>Параметры  
 **Требуется полное имя файла**  
 Указывает, закончится ли задача ошибкой, если исполняемый объект не найден в указанном месте.  
  
 **Исполняемый объект**  
 Введите имя исполняемого модуля.  
  
 **Аргументы**  
 Введите аргументы командной строки.  
  
 **WorkingDirectory**  
 Введите путь к папке, содержащей исполняемый объект, или нажмите кнопку обзора **(...)** и укажите эту папку.  
  
 **StandardInputVariable**  
 Выберите переменную для ввода данных для этого процесса или нажмите кнопку \<**Создать переменную...**> для создания новой переменной:  
  
 **См. также:**  [Добавить переменную](../../2014/integration-services/add-variable.md)  
  
 **StandardOutputVariable**  
 Выберите переменную для получения выходных данных этого процесса или нажмите кнопку \<**Создать переменную...**> для создания новой переменной.  
  
 **StandardErrorVariable**  
 Выберите переменную для получения выходных данных об ошибке этого процессора или нажмите кнопку \<**Создать переменную...**> для создания новой переменной.  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 Укажите, должна ли задача завершаться с ошибкой, если код завершения отличен от кода, указанного в параметре **SuccessValue**.  
  
 **SuccessValue**  
 Укажите значение, возвращаемое исполняемым объектом при успешном завершении задачи. По умолчанию, устанавливается значение **0**.  
  
 **Время ожидания**  
 Указывает число секунд, в течение которых может выполняться данный процесс. Значение **0** показывает, что значение времени ожидания не используется и процесс выполняется до завершения или сбоя.  
  
 **TerminateProcessAfterTimeOut**  
 Указывает, должен ли процесс быть принудительно остановлен по истечении времени, обозначенного в параметре **TimeOut** . Этот параметр доступен только при значении параметра **Время ожидания** , отличном от **0**.  
  
 **WindowStyle**  
 Указывает стиль окна, в котором выполняется процесс.  
  
## <a name="see-also"></a>См. также  
 [Справочник по сообщениям об ошибках служб Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Страница «Выражения»](expressions/expressions-page.md)  
  
  
