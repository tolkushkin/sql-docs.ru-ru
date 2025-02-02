---
title: Доступ к хранилищам данных и общим папкам с использованием проверки подлинности Windows | Документация Майкрософт
description: Узнайте, как настроить каталог служб MSSQL Integration Services в Базе данных SQL Azure и Azure-SSIS Integration Runtime в Фабрике данных Azure для запуска пакетов с доступом к хранилищам данных и общим папкам с использованием проверки подлинности Windows.
ms.date: 3/22/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
manager: craigg
ms.openlocfilehash: 218b6930e05319a4e5a1096536cf1dc31a0a94b5
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010518"
---
# <a name="access-data-stores-and-file-shares-with-windows-authentication-from-ssis-packages-in-azure"></a>Доступ к хранилищам данных и общим папкам из пакетов служб Integration Services в Azure с использованием проверки подлинности Windows

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Можно использовать проверку подлинности Windows для доступа к хранилищам данных, таким как серверы SQL Server, общие папки, Файлы Azure и т. д., из пакетов служб Integration Services, запущенных в среде выполнения интеграции Azure-SSIS Integration Runtime в Фабрике данных Azure (ADF). Хранилища данных могут быть локальными, размещаться на виртуальных машинах Azure или выполняться в Azure в качестве управляемых служб. Если используются локальные хранилища, вам нужно присоединить Azure-SSIS Integration Runtime к виртуальной сети, подключенной к вашей локальной сети. Подробнее см. в руководстве по [присоединению Azure-SSIS Integration Runtime к виртуальной сети](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network). Есть четыре способа доступа к хранилищам данных с использованием проверки подлинности Windows из пакетов служб Integration Services, выполняющихся в Azure-SSIS IR.

| Метод подключения | Область действия | Этап настройки | Метод доступа в пакетах | Число наборов учетных данных и подключенных ресурсов | Тип подключенных ресурсов | 
|---|---|---|---|---|---|
| Настройка контекста выполнения на уровне действий | Для каждого выполняемого действия пакета служб Integration Services | Настройте свойство **проверки подлинности Windows** для настройки контекста выполнения или запуска как при выполнении пакетов служб Integration Services в виде действий "Выполнение пакета SSIS" в конвейерах ADF.<br/><br/> Дополнительные сведения см. в руководстве по [настройке действий "Выполнение пакета SSIS"](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity). | Доступ к ресурсам напрямую из пакетов с использованием UNC-пути, например при использовании общих папок или Файлов Azure: `\\YourFileShareServerName\YourFolderName` или `\\YourAzureStorageAccountName.file.core.windows.net\YourFolderName` | Поддержка только одного набора учетных данных для всех подключенных ресурсов: | — общие файловые ресурсы в локальной среде и (или) на виртуальных машинах Azure;<br/><br/> — файлы Azure, как описано в [этой статье](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows); <br/><br/> – серверы SQL Server в локальной среде или на виртуальных машинах Azure с проверкой подлинности Windows;<br/><br/> – другие ресурсы с проверкой подлинности Windows. |
| Настройка контекста выполнения на уровне каталога | Для каждой среды Azure-SSIS IR, но будет переопределяться, если также настроен контекст выполнения на уровне действия (см. выше) | Выполните хранимую процедуру SSISDB `catalog.set_execution_credential`, чтобы настроить контекст выполнения или запуска как.<br/><br/> Дополнительные сведения см. ниже в этой статье. | Доступ к ресурсам напрямую из пакетов с использованием UNC-пути, например при использовании общих папок или Файлов Azure: `\\YourFileShareServerName\YourFolderName` или `\\YourAzureStorageAccountName.file.core.windows.net\YourFolderName` | Поддержка только одного набора учетных данных для всех подключенных ресурсов: | — общие файловые ресурсы в локальной среде и (или) на виртуальных машинах Azure;<br/><br/> — файлы Azure, как описано в [этой статье](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows); <br/><br/> – серверы SQL Server в локальной среде или на виртуальных машинах Azure с проверкой подлинности Windows;<br/><br/> – другие ресурсы с проверкой подлинности Windows. |
| Сохранение учетных данных посредством команды `cmdkey` | Для каждой Azure-SSIS IR, но будет переопределяться, если также настроен контекст выполнения на уровне действия или на уровне каталога (см. выше) | Выполните команду `cmdkey` в пользовательском скрипте установки (`main.cmd`) при подготовке или перенастройке среды Azure-SSIS IR, например, если используются общие папки или Файлы Azure: `cmdkey /add:YourFileShareServerName /user:YourDomainName\YourUsername /pass:YourPassword` или `cmdkey /add:YourAzureStorageAccountName.file.core.windows.net /user:azure\YourAzureStorageAccountName /pass:YourAccessKey`.<br/><br/> Дополнительные сведения см. в статье [Пользовательская установка для среды выполнения интеграции Azure–SSI](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup). | Доступ к ресурсам напрямую из пакетов с использованием UNC-пути, например при использовании общих папок или Файлов Azure: `\\YourFileShareServerName\YourFolderName` или `\\YourAzureStorageAccountName.file.core.windows.net\YourFolderName` | Поддержка нескольких наборов учетных данных для разных подключенных ресурсов: | — общие файловые ресурсы в локальной среде и (или) на виртуальных машинах Azure;<br/><br/> — файлы Azure, как описано в [этой статье](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows); <br/><br/> – серверы SQL Server в локальной среде или на виртуальных машинах Azure с проверкой подлинности Windows;<br/><br/> – другие ресурсы с проверкой подлинности Windows. |
| Подключение дисков во время выполнения пакета (без сохранения состояния) | Для каждого пакета | Выполните команду `net use` в задаче "Выполнение процесса", которая добавляется в начало потока управления в пакетах, например, `net use D: \\YourFileShareServerName\YourFolderName`. | Обращение к общим папкам через подключенные диски. | Поддержка нескольких дисков для разных файловых ресурсов: | — общие файловые ресурсы в локальной среде и (или) на виртуальных машинах Azure;<br/><br/> — файлы Azure, как описано в [этой статье](https://docs.microsoft.com/azure/storage/files/storage-how-to-use-files-windows); |
|||||||

> [!WARNING]
> Если вы не применяете указанные выше способы доступа к хранилищам данных с использованием проверки подлинности Windows, зависящие от проверки подлинности Windows пакеты не смогут получить к ним доступ и будут возвращать ошибки во время выполнения. 

Далее в статье описано, как настроить каталог служб Integration Services (SSISDB), размещенный на сервере Базы данных SQL Azure или в Управляемом экземпляре, для запуска пакетов в среде Azure-SSIS IR, в которой используется проверка подлинности Windows для доступа к хранилищам данных. 

## <a name="you-can-only-use-one-set-of-credentials"></a>Можно использовать только один набор учетных данных
Если в пакете служб Integration Services применяется проверка подлинности Windows, можно использовать только один набор учетных данных. Учетные данные домена, указываемые при выполнении инструкций из этой статьи, применяются ко всем операциям (интерактивным или запланированным) в среде Azure-SSIS IR, пока эти данные не будут изменены или удалены. Если пакет должен подключаться к нескольким хранилищам данных с разными наборами учетных данных, следует рассмотреть другие описанные выше способы.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Указание учетных данных домена для проверки подлинности Windows
Чтобы задать учетные данные домена, с помощью которых пакеты смогут подключаться к локальным хранилищам данных, используя проверку подлинности Windows, сделайте следующее:

1.  С помощью SQL Server Management Studio (SSMS) или другого средства подключитесь к серверу Базы данных SQL Azure или Управляемому экземпляру, где размещается SSISDB. Дополнительные сведения см. в статье [Подключение к каталогу SSIS (SSISDB) в Azure](ssis-azure-connect-to-catalog-database.md).

2.  Откройте окно запроса для текущей базы данных SSISDB.

3.  Выполните следующую хранимую процедуру и укажите соответствующие учетные данные домена:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  Запустите пакеты служб SSIS. Пакеты будут использовать предоставленные учетные данные для доступа к локальным хранилищам данных с помощью проверки подлинности Windows.

### <a name="view-domain-credentials"></a>Просмотр учетных данных домена
Чтобы просмотреть активные учетные данные домена, выполните указанные ниже действия.

1.  С помощью SSMS или другого средства подключитесь к серверу Базы данных SQL Azure или Управляемому экземпляру, где размещается SSISDB. Дополнительные сведения см. в статье [Подключение к каталогу SSIS (SSISDB) в Azure](ssis-azure-connect-to-catalog-database.md).

2.  Откройте окно запроса для текущей базы данных SSISDB.

3.  Выполните следующую хранимую процедуру и просмотрите выходные данные:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>Удаление учетных данных домена
Чтобы удалить учетные данные, заданные согласно инструкциям в этой статье, выполните указанные ниже действия.

1.  С помощью SSMS или другого средства подключитесь к серверу Базы данных SQL Azure или Управляемому экземпляру, где размещается SSISDB. Дополнительные сведения см. в статье [Подключение к каталогу SSIS (SSISDB) в Azure](ssis-azure-connect-to-catalog-database.md).

2.  Откройте окно запроса для текущей базы данных SSISDB.

3.  Выполните следующую хранимую процедуру:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-a-sql-server-on-premises"></a>Подключение к SQL Server в локальной среде 
Чтобы проверить возможность подключения к SQL Server в локальной среде, сделайте следующее:

1.  Чтобы выполнить эту проверку, найдите компьютер, не присоединенный к домену.

2.  На не присоединенном к домену компьютере выполните следующую команду, чтобы запустить SSMS с требуемыми учетными данными домена:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  В среде SSMS проверьте возможность подключения к требуемому серверу SQL Server в локальной среде.

### <a name="prerequisites"></a>предварительные требования
Для доступа к SQL Server в локальной среде из пакетов, выполняющихся в Azure, сделайте следующее:

1.  В диспетчере конфигурации SQL Server включите протокол TCP/IP.
2.  Разрешите доступ в брандмауэре Windows. Дополнительные сведения см. в руководстве по [настройке брандмауэра Windows для включения доступа к SQL Server](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).
3.  Присоедините Azure-SSIS IR к виртуальной сети, подключенной к SQL Server в локальной среде.  Дополнительные сведения см. в руководстве по [присоединению Azure-SSIS Integration Runtime к виртуальной сети](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
4.  Выполните хранимую процедуру SSISDB `catalog.set_execution_credential`, чтобы указать учетные данные, как описано в этой статье.

## <a name="connect-to-a-file-share-on-premises"></a>Подключение к общей папке в локальной среде 
Чтобы проверить возможность подключения к общей папке в локальной среде, сделайте следующее:

1.  Чтобы выполнить эту проверку, найдите компьютер, не присоединенный к домену.

2.  На компьютере, не присоединенном к домену, выполните приведенные ниже команды. Эти команды открывают окно командной строки с требуемыми учетными данными домена, а затем проверяют возможность подключения к общей папке в локальной среде, получая список каталогов.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Проверьте, возвращен ли список каталогов из общей папки в локальной среде.

### <a name="prerequisites"></a>предварительные требования
Для доступа к общей папке в локальной среде из пакетов, выполняющихся в Azure, сделайте следующее:

1.  Разрешите доступ в брандмауэре Windows.
2.  Присоедините Azure-SSIS IR к виртуальной сети, подключенной к общей папке в локальной среде.  Дополнительные сведения см. в руководстве по [присоединению Azure-SSIS Integration Runtime к виртуальной сети](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
3.  Выполните хранимую процедуру SSISDB `catalog.set_execution_credential`, чтобы указать учетные данные, как описано в этой статье.

## <a name="connect-to-a-file-share-on-azure-vm"></a>Подключение к общей папке на виртуальной машине Azure
Для включения доступа к общей папке на виртуальной машине Azure из пакетов, выполняющихся в Azure, сделайте следующее:

1.  С помощью SSMS или другого средства подключитесь к серверу Базы данных SQL Azure или Управляемому экземпляру, где размещается SSISDB. Дополнительные сведения см. в статье [Подключение к каталогу SSIS (SSISDB) в Azure](ssis-azure-connect-to-catalog-database.md).

2.  Откройте окно запроса для текущей базы данных SSISDB.

3.  Выполните следующую хранимую процедуру и укажите соответствующие учетные данные домена:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>Подключение к общей папке в службе файлов Azure
Дополнительные сведения о файлах Azure см. в разделе [Файлы Azure](https://azure.microsoft.com/services/storage/files/).

Для включения доступа к общей папке в Файлах Azure из пакетов, выполняющихся в Azure, сделайте следующее:

1.  С помощью SSMS или другого средства подключитесь к серверу Базы данных SQL Azure или Управляемому экземпляру, где размещается SSISDB. Дополнительные сведения см. в статье [Подключение к каталогу SSIS (SSISDB) в Azure](ssis-azure-connect-to-catalog-database.md).

2.  Откройте окно запроса для текущей базы данных SSISDB.

3.  Выполните следующую хранимую процедуру и укажите соответствующие учетные данные домена:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Следующие шаги
- Развертывание пакетов. Дополнительные сведения см. в статье [Развертывание проекта служб SSIS с помощью SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Запуск пакетов. Дополнительные сведения см. в статье [Выполнение пакета служб SSIS с помощью SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Планирование выполнения пакетов. Дополнительные сведения см. в разделе [Планирование выполнения пакетов служб SSIS в Azure](ssis-azure-schedule-packages.md).
