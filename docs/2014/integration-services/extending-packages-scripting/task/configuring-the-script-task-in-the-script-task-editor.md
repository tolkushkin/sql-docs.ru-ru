---
title: Настройка задачи "Скрипт" в редакторе задачи "Скрипт" | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8e9e1ebbf8a6ba8186d30063bd377f95b8e286d9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62894748"
---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>Настройка задачи «Скрипт» в редакторе задачи «Скрипт»
  Прежде чем писать пользовательский код задачи "Скрипт", настройте ее основные свойства на трех страницах окна **Редактор задачи "Скрипт"**. Дополнительные свойства задачи, не уникальные для задачи «Скрипт», можно настроить в окне «Свойства».  
  
> [!NOTE]  
>  В отличие от предыдущих версий, где можно было указать, являются ли скрипты предварительно скомпилированными, начиная с версии [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] все скрипты компилируются заранее.  
  
## <a name="general-page-of-the-script-task-editor"></a>Страница «Общие свойства» окна «Редактор задачи "Скрипт"»  
 На странице **Общие** окна **Редактор задачи "Скрипт"** назначается уникальное имя и вводится описание задачи "Скрипт".  
  
## <a name="script-page-of-the-script-task-editor"></a>Страница «Скрипт» окна «Редактор задачи "Скрипт"»  
 Страница **Скрипт** окна **Редактор задачи "Скрипт"** отображает пользовательские свойства задачи "Скрипт".  
  
### <a name="scriptlanguage-property"></a>Свойство ScriptLanguage  
 Среда набора средств [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools для работы с приложениями (VSTA) поддерживает языки программирования [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic и [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual С#. После создания скрипта в задаче "Скрипт" изменить значение свойства **ScriptLanguage** нельзя.  
  
 Чтобы задать язык скриптов по умолчанию для компонентов скрипта и задач "Скрипт", воспользуйтесь свойством **ScriptLanguage** на странице **Общие** диалогового окна **Параметры**. Дополнительные сведения см. в разделе [General Page](../../general-page-of-integration-services-designers-options.md).  
  
### <a name="entrypoint-property"></a>Свойство EntryPoint  
 Свойство `EntryPoint` определяет метод класса `ScriptMain` в проекте VSTA, который вызывается средой выполнения служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] в качестве точки входа в код задачи «Скрипт». `ScriptMain` Класс является классом по умолчанию, создаваемым шаблонами скриптов.  
  
 При изменении имени метода в проекте VSTA следует поменять значение свойства `EntryPoint`.  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>Свойства ReadOnlyVariables и ReadWriteVariables  
 В качестве значений этих свойств можно ввести разделенные запятыми списки существующих переменных, чтобы обеспечить доступ к ним в коде задачи «Скрипт» в режиме только для чтения или чтения и записи. Переменные обоих типов доступны в коде через свойство <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> объекта `Dts`. Дополнительные сведения см. в статье [Using Variables in the Script Task](../../extending-packages-scripting/task/using-variables-in-the-script-task.md).  
  
> [!NOTE]  
>  В именах переменных учитывается регистр букв.  
  
 Для выбора переменных нажмите кнопку с многоточием (**…**) рядом с полем свойства. Дополнительные сведения см. в статье [Страница "Выбор переменных"](../../control-flow/select-variables-page.md).  
  
### <a name="edit-script-button"></a>Кнопка «Изменить скрипт»  
 Кнопка **Изменить скрипт** запускает среду разработки VSTA, в которой и создается пользовательский скрипт. Дополнительные сведения см. в разделе [Написание кода и отладка задачи "Скрипт"](coding-and-debugging-the-script-task.md).  
  
## <a name="expressions-page-of-the-script-task-editor"></a>Страница «Выражения» окна «Редактор задачи "Скрипт"»  
 На странице **Выражения** окна **Редактор задачи "Скрипт"** можно с помощью выражений указать значения свойств задачи "Скрипт", перечисленных выше, а также многих других свойств задач. Дополнительные сведения см. в разделе [Выражения служб Integration Services (SSIS)](../../expressions/integration-services-ssis-expressions.md).  
  
![Значок служб Integration Services (маленький)](../../media/dts-16.gif "значок служб Integration Services (маленький)")**оставаться до даты со службами Integration Services**<br /> Чтобы загрузить новейшую документацию, статьи, образцы и видеоматериалы [!INCLUDE[msCoName](../../../includes/msconame-md.md)], а также лучшие решения участников сообщества, посетите страницу служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] на сайте MSDN:<br /><br /> [Посетите страницу служб Integration Services на сайте MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Чтобы получать автоматические уведомления об этих обновлениях, подпишитесь на RSS-каналы, предлагаемые на этой странице.  
  
## <a name="see-also"></a>См. также  
 [Написание кода и отладка задачи «Скрипт»](coding-and-debugging-the-script-task.md)  
  
  
