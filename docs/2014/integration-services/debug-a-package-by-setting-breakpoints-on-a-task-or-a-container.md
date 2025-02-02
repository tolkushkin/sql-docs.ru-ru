---
title: Выполнение отладки пакета путем установки точек останова для задачи или контейнера | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 907caaa37c429dd2f788d0123f7f8ee0bbf8a27a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059657"
---
# <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a>Выполнение отладки пакета путем установки точек останова для задачи или контейнера
  Эта процедура описывает, как установить точки останова в пакете, задаче, контейнерах «цикл по элементам», «цикл по каждому элементу» и контейнере последовательности.  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>Установка точки останова в пакете, задаче или контейнере  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , содержащий необходимый пакет.  
  
2.  Дважды щелкните пакет, для которого следует установить точки останова.  
  
3.  В конструкторе служб SSIS сделайте следующее.  
  
    -   Чтобы установить точки останова в объекте пакета, перейдите на вкладку **Поток управления** , поместите курсор где-либо на заднем плане области конструктора, щелкните правой кнопкой мыши и выберите пункт **Изменить точки останова**.  
  
    -   Чтобы установить точки останова в потоке управления пакета, перейдите на вкладку **Поток управления** , правой кнопкой мыши щелкните задачу, контейнер "цикл по элементам", "цикл по каждому элементу" или контейнер последовательности и выберите пункт **Изменить точки останова**.  
  
    -   Чтобы установить точки останова в обработчике события, перейдите на вкладку **Обработчик события** , щелкните правой кнопкой мыши задачу, контейнер "цикл по элементам", "цикл по каждому элементу" или контейнер последовательности и выберите пункт **Изменить точки останова**.  
  
4.  В диалоговом окне **Задание точек останова \<имя контейнера>** выберите точки останова для включения.  
  
5.  При необходимости измените тип счетчика попаданий и значение числа попаданий для каждой точки останова.  
  
6.  Чтобы сохранить пакеты, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
## <a name="see-also"></a>См. также  
 [Инструменты устранения неполадок при разработке пакета](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Отладка скрипта с помощью точек останова в задаче и компоненте «Скрипт»](data-flow/transformations/script-component.md)   
 [Написание кода и отладка задачи «Скрипт»](control-flow/script-task.md)   
 [Кодирование и отладка компонента скрипта](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
