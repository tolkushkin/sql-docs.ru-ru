---
title: Добавление компонентов к экземпляру SQL Server 2014 (программа установки) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- feature adding [SQL Server]
- SQL Server, features
- adding features to SQL Server
ms.assetid: 97931fdc-d943-48dd-81b9-ae8b8d2c6dad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 147fe717919035c365ef2e3507e46a4323694570
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779375"
---
# <a name="add-features-to-an-instance-of-sql-server-2014-setup"></a>добавить компоненты в экземпляр SQL Server 2014 (программа установки)
  В этом разделе приведена пошаговая процедура добавления компонентов в экземпляр [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Некоторые компоненты и службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] принадлежат определенному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Такие компоненты называются привязанными к экземпляру. Они имеют ту же версию, что и экземпляр, которому они принадлежат, и используются только для этого экземпляра. К экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]можно добавить привязанные к экземпляру компоненты и общие компоненты, если они еще не установлены. Перечень функций, поддерживаемых в разных выпусках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], см. в разделе [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Чтобы добавить компоненты к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из командной строки, см. в разделе [Установка SQL Server 2014 из командной строки](install-sql-server-from-the-command-prompt.md).  
  
## <a name="prerequisites"></a>предварительные требования  
 Перед продолжением изучите разделы [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md).  
  
> [!NOTE]  
>  Для локальных установок необходимо запускать программу установки с правами администратора. Если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] устанавливается с удаленного общего ресурса, необходимо использовать учетную запись домена, у которой есть разрешения на чтение на этом удаленном ресурсе.  
  
> [!NOTE]  
>  При добавлении компонентов к экземпляру [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] к ним добавляются существующие настройки отчета об использовании. Для изменения этих параметров используйте средство **Отчеты об ошибках и использовании [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** из меню [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Средства настройки**.  
  
## <a name="procedures"></a>Процедуры  
  
#### <a name="to-add-features-to-an-instance-of-includesscurrentincludessscurrent-mdmd"></a>Сведения о добавлении компонентов к экземпляру [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Вставьте установочный носитель [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . В корневой папке дважды щелкните файл setup.exe. Для установки из сетевого ресурса перейдите в корневую папку на этом ресурсе и дважды щелкните файл setup.exe. Если открылось диалоговое окно «Установка [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] », то [!INCLUDE[clickOK](../../includes/clickok-md.md)] , чтобы установить обязательные компоненты, а затем кнопку **Отмена** , чтобы выйти из программы установки [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
2.  Мастер установки запускает центр установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Чтобы добавить новый компонент в существующий экземпляр [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], щелкните **Установка** в области навигации слева, а затем выберите **Новая установка изолированного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или добавление компонентов к существующей установке**.  
  
3.  Средство проверки конфигурации системы запустит операцию обнаружения на компьютере. Щелкните **Просмотр подробностей**, чтобы просмотреть подробности проверки. Чтобы продолжить, [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
4.  На странице «Обновление продукта» приведены последние обновления продукта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Если устанавливать обновления не требуется, снимите флажок **Включить обновления продукта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Если обновлений продукта не обнаружено, программа установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не выводит на экран эту страницу и сразу переходит на страницу **Установка файлов** .  
  
5.  На странице «Установка установочных файлов» программа установки отображает индикаторы хода загрузки, извлечения и установки установочных файлов. При обнаружении обновления программы установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] оно также будет установлено, если указано, что его следует использовать. Чтобы установить файлы поддержки программы установки, нажмите кнопку **Установить** .  
  
6.  Прежде чем программа установки продолжит работу, средство проверки конфигурации системы проверит текущее состояние системы компьютера.  
  
7.  На странице "Тип установки" выберите параметр **Добавить компоненты в существующий экземпляр [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** и выберите экземпляр, который требуется обновить.  
  
8.  Выберите компоненты для установки на странице «Выбор компонентов». После выбора компонента описание его группы отображается в правой панели окна. Можно установить любое сочетание компонентов (устанавливаемые компоненты отмечаются флажками). Дополнительные сведения см. в разделе [выпуски и компоненты SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md). Каждый компонент может быть установлен только один раз в данном экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Для установки нескольких компонентов необходимо установить дополнительный экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Требования для выбранных компонентов показаны на правой панели. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] установит обязательный компонент, который еще не был установлен, в шаге установки, описанном ниже в данной процедуре.  
  
     Прежде чем программа установки продолжит работу, средство проверки конфигурации системы проверит текущее состояние системы компьютера. Чтобы продолжить, нажмите кнопку **Далее** .  
  
9. На странице «Необходимое пространство на диске» отображается расчет дискового пространства для выбранных компонентов, а также приводится сравнение требуемого и доступного места на диске, где выполняется программа установки.  
  
10. Набор операций, оставшихся в этом разделе, зависит от того, какие компоненты были выбраны для установки. В зависимости от сделанного выбора, на экране могут отображаться не все страницы.  
  
11. На странице «Конфигурация сервера — Учетные записи служб» укажите учетные записи входа для служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Набор служб, которые можно настроить на этой странице, зависит от компонентов, выбранных при установке.  
  
     Можно назначить одну учетную запись входа всем службам [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или настроить учетные записи служб индивидуально. Можно также указать, будут службы запускаться автоматически или вручную либо будут отключены. [!INCLUDE[msCoName](../../includes/msconame-md.md)] рекомендует настраивать учетные записи служб индивидуально, предоставляя каждой из служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] только минимальные права, необходимые для выполнения ее задач. Дополнительные сведения см. в разделах [Настройка сервера — учетные записи служб](../../sql-server/install/server-configuration-service-accounts.md) и [Настройка учетных записей службы Windows и разрешений](../configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Чтобы задать одну учетную запись входа для всех учетных записей служб этого экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], укажите учетные данные в полях, которые находятся в нижней части страницы.  
  
     **Примечание по безопасности** : [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     После ввода данных входа для служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] нажмите кнопку **Далее**.  
  
12. На вкладке **Настройка сервера — параметры сортировки** можно для компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] и служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]задать параметры сортировки, отличные от параметров по умолчанию. Дополнительные сведения см. в разделе [Настройка сервера — параметры сортировки](../../sql-server/install/server-configuration-collation.md).  
  
13. На странице «Настройка компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] — провизионирование учетных записей» укажите следующие сведения:  
  
    -   Режим безопасности: выберите для экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]режим проверки подлинности, «Проверка подлинности Windows» или «Смешанный режим». Если выбран смешанный режим проверки подлинности, необходимо задать надежный пароль для встроенной учетной записи системного администратора [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
         После удачного соединения устройства с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]в режиме проверки подлинности Windows и смешанном режиме начинает действовать один механизм безопасности. Дополнительные сведения см. в разделе [Database Engine Configuration - Account Provisioning](../../sql-server/install/database-engine-configuration-account-provisioning.md).  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Администраторы: для экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]должен быть задан как минимум один системный администратор. Чтобы добавить учетную запись, с которой выполняется программа установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , нажмите кнопку **Добавить текущего пользователя**. Чтобы добавить или удалить учетные записи из списка системных администраторов, нажмите кнопку **Добавить** или **Удалить**, затем измените список пользователей, групп или компьютеров, которые будут иметь права администраторов на этот экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в разделе [Database Engine Configuration - Account Provisioning](../../sql-server/install/database-engine-configuration-account-provisioning.md).  
  
     После изменения списка нажмите кнопку **ОК**. Проверьте список администраторов в диалоговом окне конфигурации. После завершения работы со списком нажмите кнопку **Далее**.  
  
14. На странице «Конфигурация компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] — каталоги данных» можно указать каталоги установки, отличные от заданных по умолчанию. Чтобы произвести установку в каталог по умолчанию, нажмите кнопку **Далее**.  
  
    > [!IMPORTANT]  
    >  Если при установке были указаны каталоги, отличные от каталогов по умолчанию, проверьте их уникальность для данного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ни один из каталогов, заданных в этом диалоговом окне, не должен совпадать с каталогами, указанными для других экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Дополнительные сведения см. в разделе [Настройка компонента Database Engine — каталоги данных](../../sql-server/install/database-engine-configuration-data-directories.md).  
  
15. Чтобы включить FILESTREAM в экземпляре [!INCLUDE[ssDE](../../includes/ssde-md.md)], используйте страницу «Конфигурация компонента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] — FILESTREAM». Дополнительные сведения о FILESTREAM см. в разделе [Настройка компонента Database Engine — Filestream](../../sql-server/install/database-engine-configuration-filestream.md). Чтобы продолжить, нажмите кнопку Далее.  
  
16. На странице "Настройка служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] — провизионирование учетных записей" задайте режим сервера и пользователей или учетные записи, которые будут обладать разрешениями администратора для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Режим сервера определяет, какие подсистемы памяти и хранения используются на сервере. Решения разных типов работают в разных режимах сервера. Если планируется размещать на сервере базы данных многомерных кубов, выберите параметр по умолчанию, режим сервера «Многомерные данные и интеллектуальный анализ данных». Что касается разрешений администратора, то необходимо указать по меньшей мере одного системного администратора для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Чтобы добавить учетную запись, от имени которой запущена программа установки SQL Server, нажмите кнопку **Добавить текущего пользователя**. Чтобы добавить учетные записи в список системных администраторов или удалить записи из списка, нажмите кнопку **Добавить** или **Удалить**, а затем измените список пользователей, групп или компьютеров, которые будут иметь права администратора для служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Дополнительные сведения о режиме сервера и разрешениях администратора см. в разделе [Настройка служб Analysis Services — провизионирование учетных записей](../../sql-server/install/analysis-services-configuration-account-provisioning.md).  
  
     После изменения списка нажмите кнопку **ОК**. Проверьте список администраторов в диалоговом окне конфигурации. После завершения работы со списком нажмите кнопку **Далее**.  
  
17. На странице «Конфигурация компонента [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] — каталоги данных» можно указать каталоги установки, отличные от заданных по умолчанию. Чтобы произвести установку в каталог по умолчанию, нажмите кнопку **Далее**.  
  
    > [!IMPORTANT]  
    >  Если при установке были указаны каталоги, отличные от каталогов по умолчанию, проверьте их уникальность для данного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ни один из каталогов, заданных в этом диалоговом окне, не должен совпадать с каталогами, указанными для других экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Дополнительные сведения см. в разделе [Настройка служб Analysis Services — каталоги данных](../../sql-server/install/analysis-services-configuration-data-directories.md).  
  
18. На странице «Конфигурация служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]» укажите тип установки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Дополнительные сведения о режимах настройки [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] см. в разделе [Параметры конфигурации служб Reporting Services (SSRS)](../../sql-server/install/reporting-services-configuration-options-ssrs.md).  
  
19. Страница «Конфигурация контроллера распределенного воспроизведения» позволяет указать пользователей, которым нужно предоставить административные разрешения для службы контроллера распределенного воспроизведения. Пользователи, имеющие административные разрешения, будут иметь неограниченный доступ к службе контроллера распределенного воспроизведения.  
  
     Нажмите кнопку **Добавить текущего пользователя** , чтобы добавить пользователей, которым требуется предоставить разрешения на доступ к службе контроллера распределенного воспроизведения. Нажмите кнопку **Добавить** , чтобы добавить разрешения на доступ к службе контроллера распределенного воспроизведения. Нажмите кнопку **Удалить** , чтобы удалить разрешения на доступ к службе контроллера распределенного воспроизведения.  
  
     Чтобы продолжить, нажмите кнопку **Далее**.  
  
20. Страница «Конфигурация клиента распределенного воспроизведения» позволяет указать пользователей, которым нужно предоставить административные разрешения для службы клиента распределенного воспроизведения. Пользователи с административными разрешениями будут иметь неограниченный доступ к службе клиента распределенного воспроизведения.  
  
     **Имя контроллера** — это необязательный параметр со значением по умолчанию \<*blank*>. Введите имя контроллера, с которым будет связываться клиентский компьютер для доступа к службе клиента распределенного воспроизведения. Следует отметить следующее.  
  
    -   Если контроллер уже настроен, введите имя этого контроллера при настройке каждого клиента.  
  
    -   Если контроллер еще не настроен, имя контроллера можно оставить пустым. Однако необходимо вручную ввести имя контроллера в файл **конфигурации клиента** .  
  
     Укажите **рабочий каталог** для службы клиента распределенного воспроизведения. Рабочий каталог по умолчанию — \<*буква диска*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     Укажите **Каталог результатов** для службы клиента распределенного воспроизведения. Каталог результатов по умолчанию — \<*буква диска*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     Чтобы продолжить, нажмите кнопку **Далее**.  
  
21. На странице "Отчеты об ошибках" укажите сведения, которые будут отправлены [!INCLUDE[msCoName](../../includes/msconame-md.md)] и помогут улучшить [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. По умолчанию параметры создания отчетов об ошибках включены.  
  
22. Средство проверки конфигурации выполнится еще раз для оценки конфигурации компьютера с выбранными компонентами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
23. На странице готовности к установке показано представление параметров установки в виде дерева, заданных в программе установки. На этой странице программа установки указывает, включена ли функция обновления продукта, а также последнюю версию обновления. После нажатия кнопки «Установить» программа установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вначале установит обязательные компоненты для выбранных компонентов, а затем и сами компоненты.  
  
24. Во время установки на странице «Выполнение установки» отображается состояние, позволяющее наблюдать за выполнением установки.  
  
25. После установки на странице Завершение будет приведена ссылка на файл сводного журнала установки и даны другие важные примечания. Чтобы завершить процесс установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , нажмите кнопку **Готово**.  
  
26. Если будет предложено перезагрузить компьютер, выполните перезагрузку. После завершения установки важно прочитать сообщение мастера установки. Дополнительные сведения о файлах журналов установки см. в разделе [Просмотр и чтение файлов журналов программы установки SQL Server](view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Next Steps  
 Настройте установку [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Чтобы сократить уязвимую для атак контактную зону системы, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выборочно устанавливает и активирует ключевые службы и функции. Дополнительные сведения см. в разделе [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>См. также:  
 [Просмотр и чтение файлов журналов программы установки SQL Server](view-and-read-sql-server-setup-log-files.md)   
 [Проверка установки SQL Server](validate-a-sql-server-installation.md)   
 [Удаление установки SQL Server 2014](repair-a-failed-sql-server-installation.md)   
 [Обновление до SQL Server 2014 с помощью мастера установки &#40;установки&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Установка SQL Server 2014 из командной строки](install-sql-server-from-the-command-prompt.md)  
  
  
