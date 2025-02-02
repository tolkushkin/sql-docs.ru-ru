---
title: Установка распределенного воспроизведения (программа установки) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 64479cdc-661a-4e32-a381-8f8b5a238337
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5b2b43d899041d501039ade4d0493a7fdbf0164
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094628"
---
# <a name="install-distributed-replay-setup"></a>Установка распределенного воспроизведения (программа установки)
  Установите компоненты распределенного воспроизведения [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью мастера установки [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . При планировании расположения установленных компонентов примите во внимание следующее.  
  
-   Средство администрирования можно установить на том же компьютере, что и контроллер распределенного воспроизведения, или на другом компьютере.  
  
-   В каждой среде распределенного воспроизведения можно установить только один контроллер.  
  
-   Службу клиента можно установить не более чем на 16 компьютерах (физических или виртуальных).  
  
-   Только один экземпляр службы клиента может быть установлен на компьютере контроллера распределенного воспроизведения. Если в среде распределенного воспроизведения будет больше одного клиента, не рекомендуется устанавливать службу клиента на том же компьютере, что и контроллер. Это может снизить общую скорость распределенного воспроизведения.  
  
-   Для сценариев тестирования производительности не рекомендуется устанавливать средство администрирования, службу контроллера распределенного воспроизведения или службу клиента на целевом экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Установка компонентов на целевом сервере должна выполняться только для проверки совместимости приложений.  
  
-   После установки контроллер распределенного воспроизведения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должен быть запущен перед запуском службы клиента распределенного воспроизведения на клиентах.  
  
> [!NOTE]  
>  Чтобы удалить или изменить компоненты распределенного воспроизведения, воспользуйтесь окном **Программы и компоненты** Windows на **Панели управления**. Выберите [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] в окне **Удаление или изменение программы** и нажмите кнопку **Удалить** , чтобы открыть мастер установки [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . На странице **Выбор компонентов** укажите компоненты программы распределенного воспроизведения, которые нужно удалить.  
  
 **Предварительные условия.**  
  
-   Убедитесь, что компьютеры, которые предполагается использовать, отвечают требованиям, описанным в разделе [Distributed Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
-   Прежде чем начать эту процедуру, создайте учетные записи домена, под которыми будут запускаться службы контроллера и клиента. Рекомендуется, чтобы эти учетные записи не были членами группы «Администраторы» Windows. Дополнительные сведения см. в подразделе «Учетные записи клиента и служб» раздела [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md) .  
  
    > [!NOTE]  
    >  Локальные пользовательские учетные записи можно использовать, если на одном компьютере используется средство администрирования, службы контроллера и клиента.  
  
 **Расположение установки.**  
  
 Если используются расположения файлов по умолчанию и стандартная установка, базовый каталог находится в каталоге C:\Program Files\Microsoft SQL Server. Ниже показано, где именно в этом каталоге устанавливаются двоичные файлы и сборки.  
  
-   32-разрядные системы:  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Инструменты  
  
     \- OR -  
  
     \<Общий каталог компонента>\Tools\\ (предоставленный пользователем альтернативный общий каталог компонента)  
  
-   64-разрядные системы:  
  
     C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86) \120\Tools  
  
     \- OR -  
  
     \<Общий каталог компонента (х86)>\Tools\\ (предоставленный пользователем альтернативный общий каталог компонента (x86))  
  
### <a name="to-install-distributed-replay-features"></a>Установка компонентов распределенного воспроизведения  
  
1.  Чтобы начать установку компонентов распределенного воспроизведения, запустите мастер установки [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
2.  На странице **Правила поддержки установки** указаны проблемы, которые могут возникнуть в ходе установки файлов поддержки SQL Server. Прежде чем продолжить установку, следует устранить все ошибки поддержки установки.  
  
3.  На странице **Ключ продукта** выберите переключатель установки бесплатного выпуска [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]или рабочей версии продукта, которая имеет ключ PID. Дополнительные сведения см. в разделе [выпуски и компоненты SQL Server 2014](../editions-and-components-of-sql-server-2016.md).  
  
4.  На странице **Условия лицензии** прочтите лицензионное соглашение и установите флажок, подтверждая принятие условий соглашения. Чтобы помочь в улучшении [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], можно также включить параметр наблюдения за использованием компонентов и отправлять отчеты в [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  На странице **Файлы поддержки программы установки** щелкните **Установить** , чтобы установить или обновить файлы поддержки программы установки для [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
6.  На странице **Роль установки** выберите **Установка компонентов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**, а затем нажмите кнопку **Далее**, чтобы перейти на страницу **Выбор компонентов**.  
  
7.  На странице **Выбор компонентов** укажите компоненты, которые необходимо установить.  
  
    -   Чтобы установить средства администрирования, выберите **Основные средства управления**.  
  
    -   Чтобы установить службу контроллера, выберите **Контроллер распределенного воспроизведения**.  
  
    -   Чтобы установить службу клиента, выберите **Клиент распределенного воспроизведения**.  
  
     **Важные**: При настройке контроллера распределенного воспроизведения можно указать один или несколько учетных записей пользователей, которые будут использоваться для запуска служб клиента распределенного воспроизведения. Далее представлен список поддерживаемых учетных записей.  
  
    -   Доменная учетная запись пользователя  
  
    -   Пользователь, который создал учетную запись локального пользователя  
  
    -   Администратор  
  
    -   Виртуальная учетная запись и управляемая учетная запись службы (MSA)  
  
    -   Сетевые службы, локальные службы и система  
  
     Учетные записи групп (локальные или доменные) и другие встроенные учетные записи (например, «Все») не принимаются.  
  
8.  При необходимости нажмите кнопку с многоточием (…), чтобы изменить путь к общей папке компонента.  
  
    1.  На 32-разрядных компьютерах путь установки по умолчанию — **C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
    2.  На 64-разрядных компьютерах путь установки по умолчанию — **C:\Program Files (x86)\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
9. По завершении нажмите кнопку **Далее**.  
  
10. На странице **Правила установки** программа установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] проверяет конфигурацию компьютера. По завершении процесса проверки нажмите кнопку **Далее**.  
  
11. На странице **Требования к свободному месту на диске** вычисляется необходимое место на диске для указанных компонентов. Затем необходимое пространство сравнивается с доступным местом на диске.  
  
12. На странице **Отчеты об ошибках** укажите сведения, которые будут отправлены в корпорацию [!INCLUDE[msCoName](../../includes/msconame-md.md)] и помогут улучшить [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Параметр создания отчетов об ошибках включен по умолчанию.  
  
13. На странице **Правила настройки установки** перед началом операции обновления средство проверки конфигурации еще раз выполнит оценку конфигурации компьютера с выбранными компонентами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
14. На странице **Все готово для установки программы** нажмите кнопку **Установить**.  
  
    > [!IMPORTANT]  
    >  После установки компонентов распределенного воспроизведения необходимо создать правила брандмауэра на компьютерах контроллера и клиента и предоставить каждому из клиентских компьютеров разрешения на целевом сервере. Дополнительные сведения см. в статье [Выполнение действий после установки](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
 Далее приводятся дополнительные разделы, в которых описаны другие способы установки компонентов распределенного воспроизведения.  
  
-   [Установка распределенного воспроизведения из командной строки](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
-   [Установка компонентов распределенного воспроизведения с помощью файла конфигурации](../../../2014/sql-server/install/install-distributed-replay-using-a-configuration-file.md)  
  
## <a name="net-framework-security"></a>Безопасность .NET Framework  
 Для установки компонентов распределенного воспроизведения необходимо обладать разрешениями администратора. Только имя входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с разрешениями sysadmin может добавлять учетные записи службы клиента в роль sysadmin тестового сервера. Дополнительные сведения о вопросах безопасности распределенного воспроизведения см. в разделе [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>См. также  
 [Функции, поддерживаемые различными выпусками SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Распределенное воспроизведение SQL Server](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Distributed Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)   
 [Параметры командной строки средства администрирования (программа распределенного воспроизведения)](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [Настройка распределенного воспроизведения](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
