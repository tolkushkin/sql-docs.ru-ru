---
title: Установка SQL Server 2016 R Services (в базе данных) — SQL Server машинное обучение
description: Добавление поддержки языков для ядра СУБД в SQL Server 2016 R Services в Windows программирования R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: bc9762470b6e2a836c29f53ebfc3ffeadbcc381f
ms.sourcegitcommit: 944af0f6b31bf07c861ddd4d7960eb7f018be06e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66454693"
---
# <a name="install-sql-server-2016-r-services"></a>Установка служб SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

В этой статье объясняется, как установить и настроить **SQL Server 2016 R Services**. Если у вас есть SQL Server 2016, установите этот компонент позволяет выполнение кода R в SQL Server.

Интеграция R в SQL Server 2017, предлагаемое в [служб машинного обучения](../r/r-server-standalone.md), отражая Добавление Python. Если вы хотите выполнить интеграцию R и наличие установочного носителя SQL Server 2017, см. в разделе [установить SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md) добавить компонент. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Контрольный список перед установкой

+ Экземпляр ядра СУБД является обязательным. Невозможно установить только R, несмотря на то, что постепенно добавить его к существующему экземпляру.

+ Для обеспечения непрерывности бизнеса [доступности группы AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) поддерживается для служб R. Необходимо установить службы R и Настройка пакетов, на каждом узле.

+ Не устанавливайте службы R в отказоустойчивом кластере. Механизм безопасности, используемый для изолирования процессов R несовместим с среде отказоустойчивого кластера Windows Server.

+ Не устанавливайте службы R на контроллере домена. Службы R часть установки завершится ошибкой.

+ Не устанавливайте **общие компоненты** > **R Server (изолированный)** на одном компьютере, где запущен экземпляр в базе данных. 

  Параллельную установку с другими версиями R и Python возможны, так как экземпляр SQL Server использует своими собственными копиями открытым исходным кодом R и Anaconda распределений. Тем не менее код, который использует R и Python на компьютере SQL Server за пределами SQL Server может привести к различным проблемам:
    
  + Используется другая библиотека и другой исполняемый файл и получить разные результаты, чем при выполнении в SQL Server.
  + Скрипты R и Python, выполняющиеся на внешние библиотеки не могут управляться SQL Server, что приводит к конкуренции ресурсов.
  
Если вы использовали все предыдущие версии среды разработки Revolution Analytics или пакетов RevoScaleR или если вы установили все предварительные версии SQL Server 2016, необходимо удалить их. Выполнение нескольких версий RevoScaleR и других частных пакетах не поддерживается. Получить справку об удалении предыдущих версий, см. в разделе [обновления и часто задаваемые вопросы установки служб машинного обучения SQL Server](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> После завершения установки необходимо выполнить дополнительные шаги настройки, описанные в этой статье. Эти шаги включают Включение SQL Server для использования внешних скриптов и добавление учетных записей, требуемых для SQL Server для выполнения заданий R от вашего имени. Изменения конфигурации обычно требуют перезапуска данного экземпляра или перезапуск службы панели запуска.

## <a name="get-the-installation-media"></a>Получение установочного носителя

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Требование для установки исправления 

Корпорация Майкрософт выявила проблему с определенной версией двоичных файлов среды выполнения Microsoft VC++ 2013, которые SQL Server устанавливает в качестве необходимого компонента. Если это обновление двоичных файлов среды выполнения VC не установлено, в SQL Server могут возникать проблемы с надежностью в определенных сценариях. Перед установкой SQL Server выполните инструкции, приведенные в [заметках о выпуске SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch), чтобы узнать, требуется ли на вашем компьютере исправление для двоичных файлов среды выполнения VC.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Запуск программы установки

Для локальных установок необходимо запускать программу установки с правами администратора. При установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из удаленной общей папки необходимо использовать учетную запись домена с разрешениями на чтение и выполнение для удаленной общей папки.

1. Запустите мастер установки для SQL Server 2016.

2. На **установки** выберите **автономная установка нового SQL Server или добавление компонентов к существующей установке**.
    
   ![Установка служб R (в базе данных)](media/2016-setup-installation-rsvcs.png "запуск установки компонента database engine с помощью служб R")
   
3. На **Выбор компонентов** выберите следующие параметры:

   - Выберите **службы компонента Database Engine**. Ядро базы данных требуется в каждом экземпляре, который использует машинное обучение.
   - Выберите **службы R (в базе данных)** . Устанавливает поддержку для использования в базе данных R.
    
     ![Выбор компонентов служб R](media/2016setup-rsvcs-features.png "выберите эти компоненты для R Services в базе данных")

    > [!IMPORTANT]
    > Не следует устанавливать R Server и R Services в то же время. Обычно бы установить R Server (изолированный), чтобы создать среду, специалист по обработке данных или разработчик использует для подключения к SQL Server и развертывания решений R. Поэтому вы можете установить только R Server.

4.  На **согласие на установку Microsoft R Open** щелкните **Accept**.
  
    Для скачивания Microsoft R Open, который включает в себя дистрибутив базовых пакетов R открытым исходным кодом и средства, а также улучшенные пакеты R и поставщиков услуг подключения от команды разработчиков Microsoft R требуется лицензионное соглашение для ознакомления.
  
5. После принятия лицензионного соглашения есть небольшой паузы, во время подготовки установщик. Нажмите кнопку **Далее** когда кнопка становится доступной.

6. На **все готово для установки** странице, убедитесь, что включены следующие элементы, а затем выберите **установить**.

   + Службы ядра СУБД
   + Службы R (в базе данных)

    Запишите расположение папки по пути `..\Setup Bootstrap\Log` где хранятся файлы конфигурации. По завершении установки можно просмотреть в файле сводки установленных компонентов.

7. После установки, если будет предложено перезагрузить компьютер, сделайте это сейчас. После завершения установки важно прочитать сообщение мастера установки. Дополнительные сведения см. в разделе [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Настройка переменных среды

Для R интеграции функций только, следует задать **MKL_CBWR** переменную среды, чтобы [гарантировать согласованный результат](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) из вычислений Intel Math Kernel Library (MKL).

1. На панели управления выберите **система и безопасность** > **системы** > **Дополнительные параметры системы**  >   **Переменные среды**.

2. Создайте новую переменную пользователем или системой. 

  + Набор имя переменной `MKL_CBWR`
  + Задать значения переменной `AUTO`

Этот шаг требует перезапуска сервера. Если вы собираетесь включить выполнение сценариев, вы можете воздержаться от перезапуска до завершения всей работы конфигурации.

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>Включение сценариев

1. Откройте [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Можно загрузить и установить соответствующую версию на этой странице: [Скачайте SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Можно также попробовать предварительную версию [Azure Data Studio](../../azure-data-studio/what-is.md), который поддерживает административных задач и запросов к SQL Server.
  
2. Подключитесь к экземпляру, где установлены службы машинного обучения, щелкните **новый запрос** откройте окно запроса и выполните следующую команду:

   ```sql
   sp_configure
   ```
    На данном этапе значение для свойства `external scripts enabled` должно быть **0**. Том, что эта функция отключена по умолчанию. Эту функцию необходимо явно включить администратор, перед запуском сценариев R или Python.
     
3. Чтобы включить внешние средства написания сценариев, выполните следующую инструкцию:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Перезапустите службу.

По завершении установки перезапустите компонент database engine, прежде чем переходить к следующему, Включение выполнения скрипта.

Перезапуск службы также автоматически перезапускает связанный [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] службы.

Вы можете перезапустить службу, используя пункт контекстного меню **перезапустите** команду для экземпляра в среде SSMS или с помощью **служб** панели на панели управления или с помощью [диспетчер конфигурации SQL Server ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Проверка установки

Проверьте состояние установки экземпляра, используя [пользовательские отчеты](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Следуйте инструкциям ниже, чтобы убедиться, что запущены все компоненты, используемые для запуска внешнего скрипта.

1. В SQL Server Management Studio откройте новое окно запроса и выполните следующую команду:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    Задайте для **run_value** значение 1.

2. Откройте **служб** панели или диспетчер конфигурации SQL Server и проверьте **службы панели запуска SQL Server** выполняется. Вы должны иметь одну службу для каждого экземпляра ядра базы данных с R или Python устанавливается. Дополнительные сведения о службе см. в разделе [Extensibility framework](../concepts/extensibility-framework.md).

7. Если панель запуска работает, можно выполнить простые R, чтобы убедиться, что внешних сред выполнения сценариев может взаимодействовать с SQL Server. 

    Откройте новую **запроса** окно в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], а затем запустите следующий сценарий:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    Скрипта может занять немного, пока для запуска в первый раз загружена среда выполнения внешнего скрипта. Результаты должны выглядеть следующим образом:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Применение обновлений

Мы рекомендуем применить последний накопительный пакет обновления для компонентов в машинном обучении и компонент database engine.

На устройствах, подключенных к Интернету накопительные пакеты обновления обычно применяются через Центр обновления Windows, но можно также использовать описанные ниже шаги для управляемой обновлений. При установке обновления для компонента database engine, программа установки запрашивает накопительные пакеты обновления для библиотек R, установленный на тот же экземпляр. 

На серверах с отключенной дополнительные действия не требуются. Дополнительные сведения см. в разделе [установить на компьютерах без доступа к Интернету > Применить накопительные обновления](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Начать с экземпляром базовых показателей уже установлен: Первоначальный выпуск SQL Server 2016, SQL Server 2016 с пакетом обновления 1 или 2 (SP2) для SQL Server 2016.

2. Перейти к списку накопительного пакета обновления: [Обновления SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Выберите последний накопительный пакет обновления. Исполняемый файл загружается и извлекаются автоматически.

4. Запустите программу установки. Примите условия лицензионного соглашения и на странице выбора компонентов, просмотрите список компонентов, для которых применяются накопительные пакеты обновления. Вы должны увидеть установлен для текущего экземпляра, включая службы R каждый компонент. Программа установки скачивает CAB-файлы, необходимые для обновления всех компонентов.

5. Следуйте указаниям мастера, приняв условия лицензирования для распространения R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Дополнительная настройка

При успешном выполнении шага проверки внешнего скрипта Python команды запускаются из SQL Server Management Studio, Visual Studio Code или любой другой клиент, который может отправлять инструкции T-SQL server.

Если вы получили ошибку при выполнении команды, просмотрите дополнительные шаги настройки в этом разделе. Может потребоваться внести дополнительные соответствующие конфигурации службы или базы данных.

На уровне экземпляра может включать дополнительные конфигурации:

* [Настройка брандмауэра для службы машинного обучения SQL Server](../../advanced-analytics/security/firewall-configuration.md)
* [Включить дополнительные сетевые протоколы](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Включение удаленных подключений](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Управление дисковыми квотами](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) во избежание внешних скриптов выполняемые задачи, которые исчерпания дискового пространства

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

В базе данных могут потребоваться следующие обновления конфигурации.

* [Предоставление пользователям разрешения на службы машинного обучения SQL Server](../../advanced-analytics/security/user-permission.md)
* [Добавление SQLRUserGroup в качестве пользователя базы данных](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> Требуются не все перечисленные изменения и не могут быть необходимы. Требования зависят от схемы безопасности, где установлен SQL Server, а также как ожидается, что пользователи для подключения к базе данных и выполнения внешних скриптов. Дополнительные советы по устранению неполадок можно найти здесь: [Часто задаваемые вопросы по обновлению и установке](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Предлагаемые оптимизации

Теперь, когда у вас есть все, что работа, может также потребоваться оптимизация сервера для поддержки машинного обучения или установки обученная моделей.

### <a name="add-more-worker-accounts"></a>Добавить дополнительные рабочие учетные записи

Если вы считаете, что можно активно использовать R, или если ожидается, что многие пользователи будут одновременно выполнять скрипты, можно увеличить количество рабочих учетных записей, назначенных службе панели запуска. Дополнительные сведения см. в разделе [изменение пула учетных записей пользователей для службы машинного обучения SQL Server](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Оптимизация сервера для выполнения внешних скриптов

Параметры по умолчанию для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] установки предназначены для оптимизации баланса сервера для различных служб, которые поддерживаются компонентом database engine, которая может включать извлечения, преобразования и загрузки (ETL) процессов, отчетов, аудита, и приложения, использующие [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] данных. Таким образом параметры по умолчанию, может оказаться, что ресурсы для машинного обучения быть ограничены или регулироваться, особенно в случае операции с интенсивным использованием памяти.

Чтобы убедиться, что заданий машинного обучения приоритеты и выделялись необходимые ресурсы в соответствующим образом, мы рекомендуем использовать для настройки внешнего пула ресурсов регулятора ресурсов SQL Server. Можно также изменить объем памяти, выделяемый для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] компонент database engine, либо увеличить количество учетных записей, которые работают под [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] службы.

- Чтобы настроить пул ресурсов для управления внешними ресурсами, см. в разделе [создания пула внешних ресурсов](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Чтобы изменить объем памяти, зарезервированной для базы данных, см. в разделе [параметры конфигурации памяти сервера](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Чтобы изменить количество учетных записей R, которые можно запустить, [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], см. в разделе [изменение пула учетных записей пользователей для машинного обучения](../administration/modify-user-account-pool.md).

Если вы используете Standard Edition и нет регулятора ресурсов, можно использовать динамические административные представления (DMV) и расширенных событий, а также события Windows, мониторинг, чтобы обеспечить управление ресурсами сервера, которые используются R. Дополнительные сведения см. в разделе [мониторинг и управление службами R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Установка дополнительных пакетов R

Решения R, созданные для SQL Server можно вызвать базовых функций R, функции из частных пакетах, установленная с SQL Server и сторонние пакеты R, несовместима с версией R с открытым кодом устанавливается SQL Server.

Пакеты, которыми вы хотите пользоваться из SQL Server, должны быть установлены в библиотеке по умолчанию, используемой экземпляром. Если у вас есть отдельная Установка R на компьютере, или если вы установили пакеты в библиотеки пользователей, нельзя будет использовать эти пакеты с T-SQL.

Процесс установки и управления пакетами R отличается в SQL Server 2016 и SQL Server 2017. В SQL Server 2016 администратор базы данных необходимо установить пакеты R, необходимые пользователям. В SQL Server 2017 можно настроить группы пользователей для совместного использования пакетов на уровне базы данных, или настроить роли базы данных, чтобы пользователи могли устанавливать собственные пакеты. Дополнительные сведения см. в разделе [Установка новых пакетов R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Следующие шаги

Разработчики R можно приступить к работе с простыми примерами и ознакомиться с основами как R работает с SQL Server. Следующий шаг см. следующие ссылки:

+ [Учебник. Запуск R в T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Учебник. Аналитика в базе данных для разработчиков R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Чтобы просмотреть примеры машинного обучения, которые основаны на реальных сценариев, см. в разделе [машинного обучения учебники](../tutorials/machine-learning-services-tutorials.md).