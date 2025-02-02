---
title: Настройка отладчика Transact-SQL | Документация Майкрософт
ms.custom: ''
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.debug.error.sqlde_register_failed
- vs.debug.error.sqlde_accessdenied
- vs.debug.error.sqlde_firewall.remotemachines
helpviewer_keywords:
- Transact-SQL debugger, remote connections
- Windows Firewall [Database Engine], Transact-SQL debugger
- Transact-SQL debugger, Windows Firewall
- Transact-SQL debugger, configuring
- ports [SQL Server], Transact-SQL debugger
- TCP/IP [SQL Server], port numbers
ms.assetid: f50e0b0d-eaf0-4f4a-be83-96f5be63e7ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ec17b61d0ea5d3f44967b517ea3e60c6b6785c6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064192"
---
# <a name="configure-the-transact-sql-debugger"></a>Настройка отладчика Transact-SQL
  Необходимо настроить правила брандмауэра Windows, включив отладку [!INCLUDE[tsql](../../includes/tsql-md.md)] при подключении к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] , который работает на компьютере, отличном от того, на котором работает редактор запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="configuring-the-transact-sql-debugger"></a>Настройка отладчика Transact-SQL  
 Отладчик [!INCLUDE[tsql](../../includes/tsql-md.md)] имеет как серверные, так и клиентские компоненты. Серверные компоненты отладчика устанавливаются с каждым экземпляром ядра СУБД из [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] с пакетом обновления 2 (SP2) или более поздней версии. Клиентские компоненты отладчика устанавливаются в следующих случаях:  
  
-   При установке клиентских средств из [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] или более поздней версии.  
  
-   При установке среды Microsoft Visual Studio 2010 или более поздней версии.  
  
-   При установке среды [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] из веб-загрузки.  
  
 Нет требований по конфигурации для запуска отладчика [!INCLUDE[tsql](../../includes/tsql-md.md)] , если среда [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] работает на том же компьютере, что и экземпляр компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Однако для запуска отладчика [!INCLUDE[tsql](../../includes/tsql-md.md)] при соединении с удаленным экземпляром компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)]для брандмауэра Windows на обоих компьютерах должны быть включены правила программы и порта. Эти правила можно создать в программе установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Если при попытке открыть сеанс отладки на удаленном компьютере возникают ошибки, убедитесь, что на брандмауэре вашего компьютера определены следующие правила.  
  
 Правила можно задать с помощью приложения **Брандмауэр Windows в режиме повышенной безопасности** . В [!INCLUDE[win7](../../includes/win7-md.md)] и [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]откройте **Панель управления**и **Брандмауэр Windows**и выберите **Дополнительные параметры**. В [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] можно также открыть **Диспетчер служб**, развернуть узел **Конфигурация** на панели слева и развернуть **Брандмауэр Windows в режиме повышенной безопасности**.  
  
> [!CAUTION]  
>  Добавление правил в брандмауэр Windows может подвергнуть компьютер угрозам безопасности, которые брандмауэр должен блокировать. Включение правил для удаленной отладки заключается в разблокировании портов и программ, перечисленных в данном разделе.  
  
## <a name="firewall-rules-on-the-server"></a>Правила брандмауэра на сервере  
 На компьютере, где установлен экземпляр компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)], через пункт **Брандмауэр Windows в режиме повышенной безопасности** задайте следующие параметры.  
  
-   Добавьте правило входящего соединения для программы sqlservr.exe. Необходимо иметь правила для каждого экземпляра, к которому должны поддерживаться сеансы удаленной отладки.  
  
    1.  На левой панели окна **Брандмауэр Windows в режиме повышенной безопасности**щелкните правой кнопкой мыши раздел **Правила для входящих подключений**и выберите на панели действий пункт **Создать правило** .  
  
    2.  В диалоговом окне **Тип правила** выберите **Программа**и нажмите кнопку **Далее**.  
  
    3.  В диалоговом окне **Программа** выберите элемент **Путь к этой программе** и введите полный путь к файлу sqlservr.exe для данного экземпляра. По умолчанию sqlservr.exe устанавливается в C:\Program Files\Microsoft SQL Server\MSSQL12. *InstanceName*\MSSQL\Binn, где *InstanceName* — это MSSQLSERVER для экземпляра по умолчанию или имя любого именованного экземпляра.  
  
    4.  В диалоговом окне **Действие** выберите **Разрешить соединение**и нажмите кнопку **Далее**.  
  
    5.  В диалоговом окне **Профиль** выберите профили, описывающие среду соединения для компьютера, с которым необходимо установить сеанс отладки для экземпляра, и нажмите кнопку **Далее**.  
  
    6.  В диалоговом окне **Имя** введите имя и описание для этого правила, затем нажмите кнопку **Готово**.  
  
    7.  В списке **Правила для входящих подключений** щелкните правой кнопкой мыши созданное правило и выберите пункт **Свойства** на панели действий.  
  
    8.  Откройте вкладку **Протоколы и порты** .  
  
    9. В поле **Тип протокола** выберите **TCP** , в поле **Локальный порт** выберите **Динамические порты RPC** , нажмите кнопку **Применить**, а затем — кнопку **ОК**.  
  
-   Добавьте правило входящего подключения для программы svchost.exe, чтобы обеспечить обмен данными DCOM из сеансов удаленного отладчика.  
  
    1.  На левой панели окна **Брандмауэр Windows в режиме повышенной безопасности**щелкните правой кнопкой мыши раздел **Правила для входящих подключений**и выберите на панели действий пункт **Создать правило** .  
  
    2.  В диалоговом окне **Тип правила** выберите **Программа**и нажмите кнопку **Далее**.  
  
    3.  В диалоговом окне **Программа** щелкните **Путь к этой программе** и введите полный путь к файлу svchost.exe. По умолчанию в svchost.exe устанавливается по пути %systemroot%\System32\svchost.exe.  
  
    4.  В диалоговом окне **Действие** выберите **Разрешить соединение**и нажмите кнопку **Далее**.  
  
    5.  В диалоговом окне **Профиль** выберите профили, описывающие среду соединения для компьютера, с которым необходимо установить сеанс отладки для экземпляра, и нажмите кнопку **Далее**.  
  
    6.  В диалоговом окне **Имя** введите имя и описание для этого правила, затем нажмите кнопку **Готово**.  
  
    7.  В списке **Правила для входящих подключений** щелкните правой кнопкой мыши созданное правило и выберите пункт **Свойства** на панели действий.  
  
    8.  Откройте вкладку **Протоколы и порты** .  
  
    9. В поле **Тип протокола** выберите **TCP** , в поле **Локальный порт** выберите **Сопоставитель конечных точек RPC** , нажмите кнопку **Применить**, а затем — кнопку **ОК**.  
  
-   Если согласно политике домена требуется, чтобы сетевые соединения осуществлялись через протокол IPsec, то необходимо также добавить правила входящих подключений для открытия портов 4500 и 500 по протоколу UDP.  
  
## <a name="firewall-rules-on-the-client"></a>Правила брандмауэра на клиенте  
 На компьютере, где запущен редактор запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] , программа установки SQL Server или среды [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] могла уже настроить брандмауэр Windows, разрешив удаленную отладку.  
  
 Если возникают ошибки при попытке открытия сеанса удаленной отладки, то вы можете вручную настроить исключения для программ и портов, настроив правила брандмауэра в окне **Брандмауэр Windows в режиме повышенной безопасности** .  
  
-   Добавление записи для программы svchost  
  
    1.  На левой панели окна **Брандмауэр Windows в режиме повышенной безопасности**щелкните правой кнопкой мыши раздел **Правила для входящих подключений**и выберите на панели действий пункт **Создать правило** .  
  
    2.  В диалоговом окне **Тип правила** выберите **Программа**и нажмите кнопку **Далее**.  
  
    3.  В диалоговом окне **Программа** щелкните **Путь к этой программе** и введите полный путь к файлу svchost.exe. По умолчанию в svchost.exe устанавливается по пути %systemroot%\System32\svchost.exe.  
  
    4.  В диалоговом окне **Действие** выберите **Разрешить соединение**и нажмите кнопку **Далее**.  
  
    5.  В диалоговом окне **Профиль** выберите профили, описывающие среду соединения для компьютера, с которым необходимо установить сеанс отладки для экземпляра, и нажмите кнопку **Далее**.  
  
    6.  В диалоговом окне **Имя** введите имя и описание для этого правила, затем нажмите кнопку **Готово**.  
  
    7.  В списке **Правила для входящих подключений** щелкните правой кнопкой мыши созданное правило и выберите пункт **Свойства** на панели действий.  
  
    8.  Откройте вкладку **Протоколы и порты** .  
  
    9. В поле **Тип протокола** выберите **TCP** , в поле **Локальный порт** выберите **Сопоставитель конечных точек RPC** , нажмите кнопку **Применить**, а затем — кнопку **ОК**.  
  
-   Добавление записи для размещения приложения, в котором размещается редактор запросов [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Если необходимо открывать сеансы удаленной отладки как из среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , так и из среды [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] на том же компьютере, то необходимо добавить оба правила.  
  
    1.  На левой панели окна **Брандмауэр Windows в режиме повышенной безопасности**щелкните правой кнопкой мыши раздел **Правила для входящих подключений**и выберите на панели действий пункт **Создать правило** .  
  
    2.  В диалоговом окне **Тип правила** выберите **Программа**и нажмите кнопку **Далее**.  
  
    3.  В диалоговом окне **Программа** щелкните **Путь к этой программе** и введите одно из следующих трех значений.  
  
        -   Для среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]введите полный путь к ssms.exe. По умолчанию программа ssms.exe устанавливается в папку «C:\Program Files (x86)\Microsoft SQL Server\120\Tools\Binn\Management Studio».  
  
        -   Для среды [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] введите полный путь к devenv.exe.  
  
            1.  По умолчанию devenv.exe для Visual Studio 2010 устанавливается в папку «C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE».  
  
            2.  По умолчанию devenv.exe для Visual Studio 2012 устанавливается в папку «C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE».  
  
            3.  Путь к ssms.exe вы можете получить из ярлыка, который используется для запуска среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Путь к devenv.exe вы можете получить из ярлыка, который используется для запуска среды [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Щелкните ярлык правой кнопкой мыши и выберите пункт **Свойства**. Исполняемый файл и пути указаны в поле **Цель** .  
  
    4.  В диалоговом окне **Действие** выберите **Разрешить соединение**и нажмите кнопку **Далее**.  
  
    5.  В диалоговом окне **Профиль** выберите профили, описывающие среду соединения для компьютера, с которым необходимо установить сеанс отладки для экземпляра, и нажмите кнопку **Далее**.  
  
    6.  В диалоговом окне **Имя** введите имя и описание для этого правила, затем нажмите кнопку **Готово**.  
  
    7.  В списке **Правила для входящих подключений** щелкните правой кнопкой мыши созданное правило и выберите пункт **Свойства** на панели действий.  
  
    8.  Откройте вкладку **Протоколы и порты** .  
  
    9. В поле **Тип протокола** выберите **TCP** , в поле **Локальный порт** выберите **Динамические порты RPC** , нажмите кнопку **Применить**, а затем — кнопку **ОК**.  
  
## <a name="requirements-for-starting-the-debugger"></a>Требования к запуску отладчика  
 Все попытки запустить отладчик [!INCLUDE[tsql](../../includes/tsql-md.md)] должны также отвечать следующим требованиям.  
  
* [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] должна быть запущена под учетной записью, которая является членом предопределенной роли сервера sysadmin.  
  
* Окно редактора запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] должно быть подключено с помощью имени входа для проверки подлинности Windows или [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которое является членом предопределенной роли сервера sysadmin.  
  
* Окно редактора запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] должно быть подключено к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] из [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] с пакетом обновления 2 (SP2) или более поздней версии. Когда окно редактора запросов подключено к экземпляру, работающему в однопользовательском режиме, отладчик запустить невозможно.

* Сервер должен обмениваться данными с клиентом через RPC. Учетная запись, под которой запущена служба SQL Server должен иметь разрешения для клиента на проверку подлинности.  
  
## <a name="see-also"></a>См. также  
 [Отладчик Transact-SQL](transact-sql-debugger.md)   
 [Запуск отладчика Transact-SQL](run-the-transact-sql-debugger.md)   
 [Пошаговая отладка кода Transact-SQL](step-through-transact-sql-code.md)   
 [Сведения отладчика Transact-SQL](transact-sql-debugger-information.md)   
 [Редактор запросов компонента Database Engine (среда SQL Server Management Studio)](database-engine-query-editor-sql-server-management-studio.md)  
  
  
