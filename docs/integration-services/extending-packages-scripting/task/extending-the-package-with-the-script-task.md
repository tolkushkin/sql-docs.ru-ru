---
title: Расширение пакета с помощью задачи "Скрипт" | Документы Майкрософт
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
- scripts [Integration Services]
- SSIS Script task
- tasks [Integration Services], scripts
- Script task [Integration Services], about Script task
- scripts [Integration Services], about Script task with packages
- SSIS Script task, about Script task
ms.assetid: 911e6d26-a6fd-4fc3-a111-bf5f048e9bff
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 88dccf4ab545b04267a970e64be64bcbd61cdf45
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724092"
---
# <a name="extending-the-package-with-the-script-task"></a>Расширение пакета с помощью задачи «Скрипт»

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Задача "Скрипт" расширяет возможности времени выполнения для пакетов служб [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] благодаря пользовательскому коду, написанному на языке [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic или [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#, который компилируется и выполняется во время выполнения пакетов. Задача «Скрипт» упрощает разработку пользовательской задачи времени выполнения, если задачи, включенные в службы [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], не полностью удовлетворяют требованиям разработчика. Задача «Скрипт» самостоятельно пишет весь инфраструктурный код, давая разработчику возможность сосредоточиться исключительно на коде, необходимом для пользовательской обработки.  
  
 Задача "Скрипт" взаимодействует с пакетом-контейнером через глобальный объект **Dts**, экземпляр класса <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel>, предоставляемого средой скриптов. В задаче «Скрипт» можно писать код, который изменяет значения, хранящиеся в переменных служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]. Позже пакет использует эти обновленные значения для определения рабочего процесса. Задача «Скрипт» может также использовать пространство имен [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], библиотеку классов платформы [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] и пользовательские сборки для реализации собственной функциональности.  
  
 Задача «Скрипт» и инфраструктурный код, который она создает, значительно упрощают разработку пользовательской задачи. Однако, чтобы понять, как работает задача "Скрипт", будет полезно прочитать раздел [Разработка пользовательской задачи](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md), чтобы ознакомиться с шагами разработки пользовательской задачи.  
  
 Если создается задача, которую планируется повторно использовать в нескольких пакетах, вместо использования задачи «Скрипт» следует разработать собственную задачу. Дополнительные сведения см. в разделе [Сравнение решений со сценариями и пользовательских объектов](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="in-this-section"></a>в этом разделе  
 В следующих разделах представлены дополнительные сведения о задаче «Скрипт».  
  
 [Настройка задачи «Скрипт» в редакторе задачи «Скрипт»](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 Объясняется, как настроенные в окне **Редактор задачи "скрипт"** свойства влияют на возможности и производительность кода в задаче "Скрипт".  
  
 [Написание кода и отладка задачи «Скрипт»](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 Объясняется использование редактора средств [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] для приложений (VSTA) для разработки скриптов, содержащихся в задаче "Скрипт".  
  
 [Использование переменных в задаче «Скрипт»](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 Объясняется использование переменных с помощью свойства <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>.  
  
 [Соединение с источниками данных в задаче «Скрипт»](../../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 Объясняется использование соединений с помощью свойства <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>.  
  
 [Вызов событий в задаче «Скрипт»](../../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 Объясняется инициирование событий с помощью свойства <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>.  
  
 [Ведение журнала в задаче «Скрипт»](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 Объясняется регистрация сведений с помощью метода <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>.  
  
 [Возврат результатов из задачи «Скрипт»](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)  
 Объясняется возвращение результатов через свойства <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> и <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>.  
  
 [Примеры задачи «Скрипт»](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 Содержит примеры, в которых показано несколько возможных использований задачи «Скрипт».  
  
## <a name="see-also"></a>См. также:  
 [Задача "Скрипт"](../../../integration-services/control-flow/script-task.md)   
 [Сравнение задачи «Скрипт» и компонента скрипта](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
