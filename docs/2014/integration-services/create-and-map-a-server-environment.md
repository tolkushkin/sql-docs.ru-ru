---
title: Создание и сопоставление серверной среды | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isenvprop.variables.f1
- sql12.ssis.ssms.iscreateenv.f1
- sql12.ssis.ssms.isenvprop.permissions.f1
- sql12.ssis.ssms.isenvprop.general.f1
ms.assetid: b1cbb697-713f-48e4-b234-b23724d87451
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 15f45af03125ebd797de0e36cb67516b4f01408d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060152"
---
# <a name="create-and-map-a-server-environment"></a>Создание и сопоставление серверной среды
  Вы создаете серверную среду, которая должна указывать значения среды выполнения для пакетов, которые содержатся в проекте, развернутом на сервере [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Можно сопоставить переменные среды с параметрами для определенного пакета, для пакетов точки входа или для всех пакетов в данном проекте. Пакет точки входа — обычно родительский пакет, который выполняет дочерний пакет.  
  
> [!IMPORTANT]  
>  Для данного выполнения пакет может выполняться только со значениями, содержащимися в односерверной среде.  
  
 У представлений можно запрашивать список серверных сред, ссылок на среды и переменных сред. Также можно вызывать хранимые процедуры для добавления, удаления и изменения сред, ссылок на среды и переменных сред. Дополнительные сведения см. в разделе **Серверные среды, переменные сервера и ссылки на серверные среды** в [SSIS Catalog](catalog/ssis-catalog.md).  
  
### <a name="to-create-and-use-a-server-environment"></a>Создание и использование серверной среды  
  
1.  В среде [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] разверните узел Каталоги [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] > **SSISDB** в обозревателе объектов и найдите папку **Среды** для проекта, для которого требуется создать среду.  
  
2.  Щелкните правой кнопкой мыши папку **Среды** и выберите команду **Создать среду**.  
  
3.  Введите имя для среды и, при желании, описание, затем нажмите кнопку **ОК**.  
  
4.  Щелкните правой кнопкой мыши новую среду и выберите команду **Свойства**.  
  
5.  На странице **Переменные** выполните следующие действия, чтобы добавить переменную.  
  
    1.  Выберите **Тип** переменной. Имя переменной **не обязательно** должно совпадать с именем параметра проекта, с которым эта переменная будет сопоставлена.  
  
    2.  Введите необязательное **Описание** для переменной.  
  
    3.  Введите **Значение** переменной среды.  
  
         Сведения о правилах для имен переменных сред см. в разделе **Переменная среды** в [SSIS Catalog](catalog/ssis-catalog.md).  
  
    4.  Укажите, содержит ли переменная конфиденциальное значение, установив или сняв флажок **Конфиденциально** .  
  
         Если флажок **Конфиденциально**установлен, значение переменной не отображается в поле **Значение** .  
  
         Конфиденциальные значения шифруются в каталоге SSISDB. Дополнительные сведения о шифровании см. в разделе [SSIS Catalog](catalog/ssis-catalog.md).  
  
6.  На странице **Разрешения** предоставьте или запретите соответствующие разрешения выбранным пользователям и ролям, выполнив следующие действия.  
  
    1.  Щелкните **Обзор**и выберите одного или нескольких пользователей и ролей в диалоговом окне **Обзор всех участников** .  
  
    2.  В области **Имена входа или роли** выберите пользователя или роль, которой будут предоставлены или запрещены разрешения.  
  
    3.  В области **Явно** щелкните **Предоставить** или **Запретить** рядом с каждым разрешением.  
  
7.  Чтобы создать скрипт среды, щелкните **Скрипт**. По умолчанию скрипт открывает новое окно редактора запросов.  
  
    > [!TIP]  
    >  Кнопку **Скрипт** необходимо нажимать после внесения таких изменений в свойства среды, как добавление переменной, и перед тем как будет нажата кнопка **ОК** в диалоговом окне **Свойства среды**. В противном случае скрипт создан не будет.  
  
8.  Чтобы сохранить изменения в свойствах среды, нажмите кнопку **ОК** .  
  
9. В узле **SSISDB** в обозревателе объектов раскройте папку **Проекты** , щелкните правой кнопкой мыши проект и выберите команду **Настроить**.  
  
10. На странице **Ссылки** нажмите кнопку **Добавить** , чтобы добавить среду, а затем нажмите кнопку **ОК** , чтобы сохранить ссылку на среду.  
  
11. Снова щелкните правой кнопкой мыши проект и выберите пункт **Настроить**.  
  
12. Для сопоставления переменной среды с параметром, добавленным в пакет во время разработки, или с параметром, созданным во время преобразования проекта [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] в модель развертывания проекта, выполните следующие действия.  
  
    1.  На вкладке **Параметры** на странице **Параметры** нажмите кнопку обзора рядом с полем **Значение** .  
  
    2.  Нажмите кнопку **Использовать переменную среды**, а затем выберите созданную переменную среды.  
  
13. Для сопоставления переменной среды со свойством диспетчера соединений выполните следующие действия. Параметры для свойств диспетчера соединений автоматически создаются на сервере служб SSIS.  
  
    1.  На вкладке **Диспетчеры соединений** на странице **Параметры** нажмите кнопку обзора рядом с полем **Значение** .  
  
    2.  Нажмите кнопку **Использовать переменную среды**, а затем выберите созданную переменную среды.  
  
14. Нажмите кнопку **ОК** дважды для сохранения изменений.  
  
  
