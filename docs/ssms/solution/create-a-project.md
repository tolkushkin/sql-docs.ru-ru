---
title: Создание проекта | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], creating
ms.assetid: 7897be19-365b-4b06-bcf0-8a669f67a673
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a2bae29b9292ecd36950c131389a8eb9ecc7253d
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65104883"
---
# <a name="create-a-project"></a>Создание проекта
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
В существующем решении можно создать один или несколько проектов.  
  
## <a name="create-a-new-project-and-add-it-to-a-solution"></a>Создание нового проекта и добавление его к решению  
  
1.  Выберите решение в обозревателе решений.  
  
2.  В меню **Файл** выберите пункт **Добавить**, затем щелкните **Создание проекта**.  
  
3.  В диалоговом окне  **Создание проекта** выберите тип проекта.  
  
    **Шаблоны**  
    В поле **Шаблоны** выберите шаблон. Краткое описание выбранного шаблона проекта появляется под полем **Шаблоны** .  
  
    **Название**  
    Введите имя создаваемого проекта скрипта. Папка с именем проекта создается в месте, указанном в поле **Расположение** . Для некоторых проектов в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] создаются исходные и прочие вспомогательные файлы, которые добавляются в папку нового проекта.  
  
    > [!NOTE]  
    > Для некоторых типов проектов текстовое поле **Имя** недоступно, поскольку при указании расположения задается имя проекта. Например, веб-приложения и веб-службы расположены на веб-сервере и получают свое имя от виртуального каталога, указанного на этом сервере.  
  
    Имена не могут содержать следующие символы:  
  
    -   Решетка (#)  
  
    -   Процент (%)  
  
    -   Амперсанд (&)  
  
    -   Звездочка (*)  
  
    -   Вертикальная черта (|)  
  
    -   Обратная косая черта (\\)  
  
    -   Двоеточие (:)  
  
    -   Кавычки («»)  
  
    -   Знак "меньше" (\<)  
  
    -   Знак «больше» >)  
  
    -   Вопросительный знак (?)  
  
    -   Косая черта (/)  
  
    -   Начальные и конечные пробелы (' ')  
  
    -   Имена, зарезервированные для Microsoft Windows или MS-DOS, такие как ("nul", "aux", "con", "com1", "lpt1" и так далее)  
  
    **Расположение**  
    Укажите расположение, где нужно создать проект, либо выберите его из списка.  
  
    **Обзор**  
    Отображает диалоговое окно **Расположение проекта** , позволяющее визуально выбрать каталог, в котором нужно сохранить проект.  
  
    **Решение**  
    Выберите **Создать новое решение** для создания решения в обозревателе решений. Выберите **Добавить к решению** для добавления нового проекта к решению, отрытому в данный момент в обозревателе решений.  
  
    **Создать каталог для решения**  
    Выберите для доступа к текстовому полю **Имя (решения)** . Этот параметр приведет к созданию нового каталога с именем, выбранным для проекта или решения.  
  
    **Имя решения**  
    Введите имя нового решения, в котором нужно создать проект. По умолчанию это поле использует имя, введенное в поле **Имя** .  
  
    **Примечание** . Для доступа к этому параметру нужно установить флажки **Создать новое решение** в области **Решение** и **Создать каталог для решения** . Некоторые шаблоны проекта не поддерживают этот параметр, например веб-приложения.  
  
    **Добавить к системе управления версиями**  
    Если данный флажок установлен, приложение системы управления версиями откроется при нажатии кнопки **ОК**. Для продолжения задайте все сведения, необходимые приложению системы управления версиями. Для использования этого параметра необходимо установить клиентское приложение системы управления версиями.  
  
4.  Нажмите кнопку **ОК**.  
  
Проекту скрипта можно назначить имя, но имена папок задаются средой [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] и не могут быть изменены. Можно определить букву диска и путь для общего набора папок, используя диалоговое окно **Добавить новый проект** . Щелкните правой кнопкой мыши значок решения в **обозревателе решений**, а затем щелкните **Добавить**. По умолчанию папка проекта скриптов размещена по пути: C:\Documents and Settings\\*имя пользователя*\My Documents\SQL Server Management Studio\Projects\\.  
  
## <a name="see-also"></a>См. также:

[обозревателе решений](../../ssms/solution/solution-explorer.md)  
[Добавление к решению существующий проект](../../ssms/solution/add-an-existing-project-to-a-solution.md)  
[Добавление новых элементов в проект](../../ssms/solution/add-new-items-to-a-project.md)  
[Добавление существующих элементов в проект](../../ssms/solution/add-existing-items-to-a-project.md)  
[Изменение местоположения проектов по умолчанию](../../ssms/solution/change-the-default-location-for-projects.md)  
[Перемещение или удаление элемента или проекта](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
[Удаление решения](../../ssms/solution/delete-a-solution.md)  