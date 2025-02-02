---
title: Подключение к SQL Server в случае, если доступ системных администраторов заблокирован | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 156a8e765812c14da0888148505311d52c267916
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62782387"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>Подключение к SQL Server в случае, если доступ системных администраторов заблокирован
  В этом разделе описывается, как восстановить доступ к компоненту [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] в качестве системного администратора. Системный администратор может утратить доступ к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] по одной из следующих причин:  
  
-   по ошибке удалены все члены предопределенной роли сервера sysadmin;  
  
-   по ошибке удалены все группы Windows, которые являлись членами предопределенной роли сервера sysadmin;  
  
-   имена входа, являющиеся членами предопределенной роли сервера sysadmin, принадлежат лицам, которые покинули компанию или недоступны;  
  
-   учетная запись sa отключена, или никто не знает ее пароля.  
  
 Одним из способов восстановления доступа является повторная установка [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и присоединение всех баз данных к новому экземпляру. Такое решение занимает продолжительное время, а для восстановления имен входа может потребоваться восстановление базы данных master из резервной копии. Если резервная копия базы данных master создана давно, в ней могут отсутствовать некоторые сведения. В более свежей резервной копии базы данных master могут содержаться имена входа, относящиеся к предыдущему экземпляру, и поэтому администраторы по-прежнему будут заблокированы.  
  
## <a name="resolution"></a>Решение  
 Запустите экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в однопользовательском режиме с использованием параметра **-m** или **-f** . Затем любой член локальной группы администраторов на компьютере может подключиться к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в качестве члена предопределенной роли сервера sysadmin.  
  
> [!NOTE]  
>  При запуске экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в однопользовательском режиме сначала нужно остановить службу «Агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ». В противном случае агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может установить соединение первым, что не позволит подключиться второму пользователю.  
  
 При использовании параметра **-m** с **sqlcmd** или [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]вы можете ограничить подключения к определенному клиентскому приложению. Например, **-m"sqlcmd"** разрешает только одно подключение, которое должно идентифицироваться как клиентская программа **sqlcmd** . Этот параметр следует использовать, когда [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] запускается в однопользовательском режиме, а единственное доступное соединение занято неизвестным клиентским приложением. Чтобы подключиться с помощью редактора запросов в [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], используйте **-m"Microsoft SQL Server Management Studio - Query"**.  
  
> [!IMPORTANT]  
>  Не используйте этот параметр как средство безопасности. Клиентское приложение предоставляет имя клиентского приложения и может указать ложное имя в составе строки подключения.  
  
 Пошаговые инструкции по запуску [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в однопользовательском режиме см. в разделе [Настройка параметров запуска сервера (диспетчер конфигурации SQL Server)](scm-services-configure-server-startup-options.md).  
  
## <a name="step-by-step-instructions"></a>Пошаговые инструкции  
 Следующие инструкции описывают процесс соединения с [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , работающим на платформе Windows 8 или более поздней версии. Небольшие изменения для предыдущих версий SQL Server или Windows приведены. Эти инструкции должны выполняться в течение сеанса входа в Windows в качестве члена группы локальных администраторов, и предполагается, что на компьютере установлена [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
1.  Запустите [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]с начальной страницы. В меню **Вид** выберите команду **Зарегистрированные серверы**. (Если сервер еще не зарегистрирован, щелкните правой кнопкой мыши узел **Группы локальных серверов**, наведите указатель на пункт **Задачи**и выберите пункт **Зарегистрировать локальные серверы**.)  
  
2.  В области "Зарегистрированные серверы" щелкните правой кнопкой мыши сервер и выберите пункт **Диспетчер конфигурации SQL Server**. После этого программа должна запросить разрешение на запуск от имени администратора, а затем откроется программа диспетчера конфигурации.  
  
3.  Закройте среду [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  На левой панели диспетчера конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выберите **Службы SQL Server**. На панели справа найдите свой экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. (Экземпляр по умолчанию [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] включает **(MSSQLSERVER)** после имени компьютера. Именованные экземпляры появляются в верхнем регистре с тем же названием, что и в списке «зарегистрированные серверы»). Щелкните правой кнопкой мыши экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а затем выберите пункт **Свойства**.  
  
5.  На **параметры запуска** на вкладке **укажите параметр запуска** введите `-m` и нажмите кнопку `Add`. (Это дефис, затем буква «m» в нижнем регистре.)  
  
    > [!NOTE]  
    >  В некоторых предыдущих версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] нет вкладки **Параметры запуска** . В этом случае на вкладке **Дополнительно** дважды щелкните **Параметры запуска**. Параметры открываются в очень маленьком окне. Не изменяйте существующие параметры. В самом конце добавьте новый параметр `;-m` и нажмите `OK`. (Это точка с запятой, затем дефис, затем буква «m» в нижнем регистре.)  
  
6.  Нажмите кнопку `OK`, а после сообщения о перезагрузке, щелкните правой кнопкой мыши имя сервера и нажмите кнопку **перезапустите**.  
  
7.  После перезагрузки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ваш сервер находится в однопользовательском режиме. Убедитесь, что агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не выполняется. Если он был запущен, то он займет ваше единственное соединение.  
  
8.  На стартовом экране Windows 8 щелкните правой кнопкой мыши пиктограмму для [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. В нижней части экрана выберите **Запуск от имени администратора**. (Это передаст учетные данные администратора в SSMS.)  
  
    > [!NOTE]  
    >  В более ранних версиях Windows параметр **Запуск от имени администратора** появляется в виде подменю.  
  
     В некоторых конфигурациях SSMS попытается установить несколько подключений. Многочисленные соединения приведут к ошибке, поскольку [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] находится в однопользовательском режиме. Можно выбрать одно из следующих действий для выполнения. Выполните одно из следующих действий.  
  
    1.  Подключитесь с помощью обозревателя объектов, используя проверку подлинности Windows (которая включает учетные данные администратора). Разверните **Безопасность**, затем **Имена входа**и дважды щелкните имя входа. На **ролей сервера** выберите `sysadmin`, а затем нажмите кнопку `OK`.  
  
    2.  Вместо соединения с помощью обозревателя объектов подключитесь с помощью окна запросов, используя проверку подлинности Windows (которая включает учетные данные администратора). (Подключиться подобным образом можно только в том случае, если подключение не выполнено с помощью обозревателя объектов.) Выполните следующий код, чтобы добавить новое имя входа, проверка подлинности Windows, которое является членом `sysadmin` предопределенной роли сервера. В следующем примере создается пользователь с именем `CONTOSO\PatK`.  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  Если экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] работает в режиме смешанной проверки подлинности, подключитесь к окну запросов при помощи проверки подлинности Windows (которая включает учетные данные администратора). Выполните следующий код для создания нового [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имя входа проверки подлинности, который является членом `sysadmin` предопределенной роли сервера.  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  Замените ************ надежным паролем.  
  
    4.  Если ваш [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] работает в смешанном режиме проверки подлинности и сбросить пароль `sa` учетной записи, подключитесь к окну запросов с использованием проверки подлинности Windows (которая включает учетные данные администратора). Изменение пароля `sa` учетную запись со следующим синтаксисом.  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  Замените ************ надежным паролем.  
  
9. Следующие действия переведут [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] обратно в многопользовательский режим. Закройте среду SSMS.  
  
10. На левой панели диспетчера конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выберите **Службы SQL Server**. На правой панели щелкните экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]правой кнопкой мыши и выберите пункт **Свойства**.  
  
11. На **параметры запуска** на вкладке **существующие параметры** выберите `-m` и нажмите кнопку `Remove`.  
  
    > [!NOTE]  
    >  В некоторых предыдущих версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] нет вкладки **Параметры запуска** . В этом случае на вкладке **Дополнительно** дважды щелкните **Параметры запуска**. Параметры открываются в очень маленьком окне. Удалить `;-m` , добавленный ранее и нажмите кнопку `OK`.  
  
12. Щелкните правой кнопкой мыши имя сервера и выберите пункт **Перезапустить**.  
  
 Теперь можно подключиться с помощью нескольких учетных записей, которая является членом объекта `sysadmin` предопределенной роли сервера.  
  
## <a name="see-also"></a>См. также  
 [Запуск SQL Server в однопользовательском режиме](start-sql-server-in-single-user-mode.md)   
 [Параметры запуска службы Database Engine](database-engine-service-startup-options.md)  
  
  
