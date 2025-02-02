---
title: Загрузка модуля PowerShell (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
keywords:
- установка компонентов SQL Server PowerShell, загрузка компонентов SQL Server PowerShell
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0f14a3cee050fff07c7fe5bc2467bcb8209a53c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62672575"
---
# <a name="install-sql-server-powershell-module"></a>Установка модуля SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Эта статья содержит инструкции по установке модуля **SqlServer** PowerShell.
> [!NOTE]
> Существует два модуля PowerShell SQL Server. 
> * **SQLPS**. Этот модуль входит в состав установки SQL Server (для обеспечения обратной совместимости), но больше не обновляется. Самым актуальным модулем PowerShell является модуль **SqlServer**.
> * **SqlServer**. Этот модуль содержит новые командлеты для поддержки новейших функций SQL. Этот модуль также содержит обновленные версии командлетов в **SQLPS**. 

Предыдущие версии модуля **SqlServer** *входили* в состав среды SQL Server Management Studio (SSMS), но только с SSMS версий 16.x. Для работы PowerShell с SSMS 17.0 и более поздних версий необходимо установить модуль **SqlServer** из [коллекции PowerShell](https://www.powershellgallery.com/packages/Sqlserver).
Текущая версия модуля **SqlServer** — 21.1.18080. Она основана на Microsoft.SQLServer.SMO версии v150 и поддерживает следующую версию SQL Server. Последней версией модуля, основанной на Microsoft.SQLServer.SMO версии v140, является 21.0.17279.

Предварительные версии модуля могут выходить чаще. О том, как получить их, см. в разделе внизу этой страницы.

Чтобы установить модуль **SqlServer** из коллекции PowerShell, запустите сеанс [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) и выполните следующие команды. Если при установке возникли проблемы, см. [документацию по Install-Module](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module) и [справочник по Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module).

Чтобы установить модуль **SqlServer**, выполните следующую команду.

```Install-Module -Name SqlServer```

Если на компьютере установлены предыдущие версии модуля **SqlServer**, воспользуйтесь командой `Update-Module` (далее в этой статье) или укажите параметр `-AllowClobber`.  

```Install-Module -Name SqlServer -AllowClobber```

Если не удается запустить сеанс PowerShell от имени администратора, можно выполнить установку для текущего пользователя.

```Install-Module -Name SqlServer -Scope CurrentUser```

Если доступны обновленные версии модуля **SqlServer**, можно обновить версию с помощью команды `Update-Module`.

```Update-Module -Name SqlServer```

Чтобы просмотреть установленные версии модуля.

```Get-Module SqlServer -ListAvailable```

Чтобы использовать конкретную версию модуля, ее можно импортировать с определенным номером версии, как показано далее.

```Import-Module SqlServer -Version 21.1.18080```

> [!NOTE]
> Предварительные (или "preview") версии модуля могут быть доступны в коллекции PowerShell. Их можно найти и установить с помощью обновленных командлетов *Find-Module* и *Install-Module*, которые входят в модуль [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet), передав параметр *-AllowPrerelease*.
>
> Чтобы найти предварительный выпуск или предварительную версию модуля, выполните следующую команду:
>
> ```Find-Module SqlServer -AllowPrerelease```
>
> Чтобы установить конкретную предварительную версию или предварительный выпуск модуля, укажите при установке конкретный номер версии, как показано далее.
>
> ```Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease```
> 

Версии модуля **SqlServer** PowerShell в коллекции PowerShell поддерживают управление версиями и требуют PowerShell 5.0 или более поздней версии. 

* [Модуль SqlServer в коллекции PowerShell](https://www.powershellgallery.com/packages/Sqlserver) 
* [Командлеты SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
* [Командлеты SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
