---
title: Интегрированный терминал
titleSuffix: Azure Data Studio
description: Дополнительные сведения о встроенном терминале студии данных Azure.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: d29234810e30efd204f498e2f7c63ba6571cbfe7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797526"
---
# <a name="integrated-terminal"></a>Интегрированный терминал

В [!INCLUDE[name-sos](../includes/name-sos-short.md)], вы можете открыть интегрированный терминал, изначально начиная с корня рабочей области. Это удобно, так как не нужно переключаться windows или изменить состояние существующих терминалов, для выполнения быстрых задач командной строки.

Чтобы открыть терминал:

* Используйте **Ctrl +'** сочетания клавиш с символ обратного апострофа.
* Используйте **представление** | **интегрированный терминал** команды меню.
* Из **палитру команд** (**Ctrl + Shift + P**), используйте **интегрированный терминал просмотреть: переключатель** команды.

![Терминалов](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> Вы можете по-прежнему открыть внешнюю оболочку с помощью обозревателя **откройте командную строку** команды (**открыть в терминале** на Mac или Linux) Если вы предпочитаете работать за пределами [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="managing-multiple-terminals"></a>Управление несколькими терминалы

Можно создать несколько терминалы для разных расположений и беспрепятственно перемещаться между ними. Можно добавлять экземпляры терминала, нажав значок плюса в правом верхнем углу **ТЕРМИНАЛОВ** панели или путем запуска **Ctrl + Shift + "** команды. В раскрывающемся списке, который может использоваться для переключения между ними создается еще одна запись.

![Несколько терминалы](media/integrated-terminal/terminal-multiple-instances.png)

Можно кнопку Remove терминалов экземпляров, нажав клавишу корзину.

> [!TIP]
> Если вы используете несколько терминалы широко, можно добавить настраиваемые сочетания клавиш для `focusNext`, `focusPrevious` и `kill` команды описанные в [раздел привязок ключ](#key-bindings) необходимость разрешения переходов между ними, используя только клавиатуру.

## <a name="configuration"></a>Конфигурация

Оболочки используется значение по умолчанию — `$SHELL` в Linux и macOS, PowerShell в Windows 10 и cmd.exe в более ранних версиях Windows. Их можно переопределить вручную, задав `terminal.integrated.shell.*` в [параметры](settings.md). Аргументы могут передаваться оболочки терминала в Linux и macOS с помощью `terminal.integrated.shellArgs.*` параметры.

### <a name="windows"></a>Windows

Правильной настройке оболочки на Windows сводится к поиска справа исполняемый файл и обновить параметр. Ниже приведен список распространенных исполняемые файлы оболочки и их местоположениях по умолчанию.

```json
// 64-bit cmd if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\cmd.exe"
// 64-bit PowerShell if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
```

> [!NOTE]
> Для использования в качестве интегрированного терминала, оболочки исполняемый файл должен быть консольное приложение, чтобы `stdin/stdout/stderr` может быть перенаправлен.

> [!TIP]
> Интегрированная оболочка терминалов выполняется с разрешениями [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Если необходимо выполнить команду оболочки с повышенным уровнем разрешений (администратора) или разные разрешения, можно использовать служебные программы платформы, такие как `runas.exe` в окне терминала.

### <a name="shell-arguments"></a>Аргументы оболочки

При запуске приложения, можно передать аргументы в оболочку.

Например, чтобы включить выполнение bash как оболочка входа (которой выполняется `.bash_profile`), передайте `-l` аргумента (в двойные кавычки):

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>Параметры отображения терминалов

Вы можете настроить интегрированный терминал шрифта и высота строки со следующими параметрами:

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>Терминалов сочетания клавиш

**Представления: Переключить интегрированный терминал** команда привязана к **Ctrl +'** для быстрого переключения встроенная панель терминалов и.

Ниже приведены сочетания клавиш для быстрого перехода в окне интегрированного терминала.

|Key|Command|  
|---|---|  
|**CTRL +\`**|Показать встроенный терминал|  
|**Ctrl + Shift +\`**|Создать новый терминал|  
|**CTRL + стрелка вверх**|Прокрутите страницу вверх|  
|**CTRL + стрелка вниз**|Прокрутите вниз|  
|**Ctrl + PageUp**|Прокрутка страницы вверх|  
|**Ctrl + PageDown**|Прокрутка страницы вниз|  
|**CTRL + Home**|Прокрутить до верхней границы|  
|**Ctrl + End**|Прокрутите вниз|  
|**CTRL + K**|Очистить терминала|  

Других команд терминала, доступны и могут быть привязаны к вашей основной сочетания клавиш.

Подробные сведения.

* `workbench.action.terminal.focus`. Фокус в окне терминала. Это подобно переключателя, но рассматриваются терминалов вместо спрятать, если она видна.
* `workbench.action.terminal.focusNext`. Основное внимание уделяется терминалов следующего экземпляра.
* `workbench.action.terminal.focusPrevious`. Основное внимание уделяется терминалов предыдущего экземпляра.
* `workbench.action.terminal.kill`. Удаляет текущий экземпляр терминала.
* `workbench.action.terminal.runSelectedText`. Запустите выбранный текст в экземпляре терминала.
* `workbench.action.terminal.runActiveFile`. Запустите файл с активным в экземпляре терминалов.

### <a name="run-selected-text"></a>Выполнение выделенного текста

Чтобы использовать `runSelectedText` команды, выделите текст в редакторе и выполните команду **терминалов: Выполнение выделенного текста в окне терминала Active** через **палитра команд** (**Ctrl + Shift + P**). Терминал предпринимает попытку выполнить выделенный текст:

![Запустите выделенный текст](media/integrated-terminal/terminal_run_selected.png)

Если текст не выбран в активном редакторе, строки, в которой находится курсор, выполняется в окне терминала.

### <a name="copy--paste"></a>Копирование и вставка

Сочетания клавиш для копирования и вставки по соблюдать стандарты платформы:

* Linux: **Ctrl + Shift + C** и **Ctrl + Shift + V**
* Mac: **Cmd + C** и **Cmd + V**
* Windows: **CTRL + C** и **Ctrl + V**

### <a name="find"></a>Найти

Интегрированный терминал имеет функциональные возможности базового поиска, который можно активировать с помощью **Ctrl + F**.

Если вы хотите, чтобы **Ctrl + F** для перехода в оболочку вместо запуска поиска мини-приложения в Linux и Windows, необходимо удалить сочетание клавиш следующим образом:

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>Переименовать сеансов терминала

Интегрированной сеансы терминалов могут теперь переименованы с помощью **терминалов: Переименуйте** (`workbench.action.terminal.rename`) команды. Новое имя отображается в терминалов выбора раскрывающегося списка.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>Форсирование планов сочетания клавиш для передачи через терминал

Когда фокус ввода установлен во встроенном терминале, многие сочетания клавиш не будет работать так, как передаются для нажатия клавиш и использованных в окне терминала, сам. `terminal.integrated.commandsToSkipShell` Параметр позволяет обойти эту проблему. Он содержит массив имен команд, сочетания клавиш оболочкой не будет обработан и обрабатываться с помощью [!INCLUDE[name-sos](../includes/name-sos-short.md)] система привязки ключа. По умолчанию сюда входят все терминалов сочетания клавиш в дополнение к выберите несколько часто используемые сочетания клавиш.

