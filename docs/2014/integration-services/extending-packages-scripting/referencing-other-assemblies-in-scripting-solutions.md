---
title: Ссылки на другие сборки в решениях со скриптами | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6f942e1afe40467e331519f276b360f87f9a6da
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62894738"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Ссылки на другие сборки в решениях со сценариями
  Библиотека классов платформы [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] предоставляет разработчику скриптов набор эффективных средств для реализации пользовательской функциональности в пакетах служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Задача «Скрипт» и компонент скрипта также могут использовать пользовательские управляемые сборки.  
  
> [!NOTE]  
>  Чтобы разрешить пакетам использование объектов и методов из веб-службы, используйте команду **Добавить веб-ссылку**, доступную в средствах [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] для приложений (VSTA). В более ранних версиях служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], чтобы использовать веб-службу, приходилось формировать класс-посредник.  
  
## <a name="using-a-managed-assembly"></a>Использование управляемой сборки  
 Чтобы во время разработки службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] могли найти управляемую сборку, нужно сделать следующее:  
  
1.  Сохранить управляемую сборку в любой папке на компьютере.  
  
    > [!NOTE]  
    >  В более ранних версиях служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] можно было добавлять ссылки только на управляемые сборки, хранящиеся в папке %windir%\Microsoft.NET\Framework\vx.x.xxxxx или %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies.  
  
2.  Добавить ссылку на управляемую сборку.  
  
     Чтобы добавить ссылку, в средствах VSTA в диалоговом окне **Добавление ссылки** на вкладке **Обзор** найдите и добавьте управляемую сборку.  
  
 Чтобы службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] могли найти управляемую сборку во время выполнения, необходимо выполнить следующие шаги.  
  
1.  Подписать управляемую сборку строгим именем.  
  
2.  Установить сборку в глобальный кэш сборок на компьютере, где выполняется пакет.  
  
     Дополнительные сведения см. в разделе [Сборка, развертывание и отладка пользовательских объектов](../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Использование библиотеки классов платформы Microsoft .NET Framework  
 Задача «Скрипт» и компонент Script могут использовать преимущества всех остальных объектов и функциональность, которую обеспечивает библиотека классов платформы [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Например, с помощью платформы [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] можно извлекать сведения о среде и взаимодействовать с компьютером, на котором работает пакет.  
  
 В следующем списке описываются некоторые из наиболее часто используемых классов платформы [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
-   `System.Data` Содержит архитектуру ADO.NET.  
  
-   `System.IO` Предоставляет интерфейс для файловой системы и файловых потоков.  
  
-   `System.Windows.Forms` Обеспечивает создание форм.  
  
-   `System.Text.RegularExpressions` Предоставляет классы для работы с регулярными выражениями.  
  
-   `System.Environment` Возвращает сведения о локальном компьютере, текущий пользователь и параметрами компьютеров и пользователей.  
  
-   `System.Net` Обеспечивает сетевые соединения.  
  
-   `System.DirectoryServices` Обеспечивает доступ к Active Directory.  
  
-   `System.Drawing` Предоставляет обширные манипуляции библиотеки изображениями.  
  
-   `System.Threading` Обеспечивает возможность многопоточного программирования.  
  
 Дополнительные сведения о платформе [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] см. в библиотеке MSDN.  
  
![Значок служб Integration Services (маленький)](../media/dts-16.gif "значок служб Integration Services (маленький)")**оставаться до даты со службами Integration Services**<br /> Чтобы загрузить новейшую документацию, статьи, образцы и видеоматериалы корпорации Майкрософт, а также лучшие решения участников сообщества, посетите страницу служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] на сайте MSDN:<br /><br /> [Посетите страницу служб Integration Services на сайте MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Чтобы получать автоматические уведомления об этих обновлениях, подпишитесь на RSS-каналы, предлагаемые на этой странице.  
  
## <a name="see-also"></a>См. также  
 [Расширение пакетов с помощью сценариев](extending-packages-with-scripting.md)  
  
  
