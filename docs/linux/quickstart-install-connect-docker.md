---
title: Начало работы с контейнерами SQL Server Linux в Docker
titleSuffix: SQL Server
description: В этом кратком руководстве показано, как использовать Docker для запуска SQL Server 2017 и образы контейнеров 2019 г. Затем мы создадим базу данных и выполним запрос с помощью sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/14/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.custom: sqlfreshmay19
ms.prod_service: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
zone_pivot_groups: cs1-command-shell
ms.openlocfilehash: 55061de57903d33c5f31c532f680fcf0c66684f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506565"
---
# <a name="quickstart-run-sql-server-container-images-with-docker"></a>Краткое руководство. Запускать образы контейнера SQL Server с помощью Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Это краткое руководство описывает использование Docker для извлечения и запуска образа контейнера SQL Server 2017, [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server). Затем мы подключимся при помощи **sqlcmd** для создания первой базы данных и выполнения запросов.

> [!TIP]
> Если вы хотите попробовать SQL Server 2019 изображение для предварительного просмотра, см. в разделе [предварительной версии SQL Server 2019 в этой статье](quickstart-install-connect-docker.md?view=sql-server-linux-ver15).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

В этом кратком руководстве, использовать Docker для извлечения и запуска образа контейнера SQL Server 2019 предварительной версии, [mssql-server](https://hub.docker.com/r/microsoft/mssql-server). Затем мы подключимся при помощи **sqlcmd** для создания первой базы данных и выполнения запросов.

> [!TIP]
> В этом кратком руководстве создает контейнеры предварительной версии SQL Server 2019. Если вы хотите создавать контейнеры SQL Server 2017, см. в разделе [версию этой статьи в SQL Server 2017](quickstart-install-connect-docker.md?view=sql-server-linux-2017).
::: moniker-end

Этот образ содержит SQL Server, работающий в системе Linux, основанной на Ubuntu 16.04. Он может использоваться с Dосker Engine 1.8+ на Linux или Docker для Mac или Windows. В этом кратком руководстве особое внимание уделяется с помощью SQL Server на **linux** изображения. Образ с Windows не рассматривается, но сведения о нем вы можете найти на странице [mssql-server-windows-developer](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/) центра Docker.

## <a id="requirements"></a> Предварительные требования

- Docker Engine 1.8+ на любом поддерживаемом дистрибутиве Linux или Docker для Mac или Windows. Дополнительные сведения см. в разделе [Установка Docker](https://docs.docker.com/engine/installation/).
- Docker **overlay2** драйвера запоминающего устройства. Это значение по умолчанию для большинства пользователей. Если обнаружится, что вы не используете этот поставщик хранилища и необходимо изменить, см. инструкции и предупреждений в [документации docker overlay2](https://docs.docker.com/storage/storagedriver/overlayfs-driver/#configure-docker-with-the-overlay-or-overlay2-storage-driver).
- Минимум 2 ГБ места на диске.
- Не менее 2 ГБ ОЗУ.
- [Требования к системе для SQL Server на Linux](sql-server-linux-setup.md#system).

<!--The following H2 is versioned for 2017 and 2019. Much of the content is duplicated, so
any changes to one section should be duplicated in the other-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="pullandrun2017"></a> Извлечение и запуск образа контейнера

Прежде чем выполнять следующие действия, убедитесь, что выбран основной оболочке (bash, PowerShell или cmd) в верхней части этой статьи.

1. Получите образ контейнера SQL Server 2017 Linux из реестра контейнеров Microsoft.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   > [!TIP]
   > Если вы хотите попробовать SQL Server 2019 изображение для предварительного просмотра, см. в разделе [предварительной версии SQL Server 2019 в этой статье](quickstart-install-connect-docker.md?view=sql-server-linux-ver15#pullandrun2019).

   Предыдущая команда извлекает последнюю версию образа контейнера с SQL Server 2017. Если вы хотите извлечь конкретный образ, добавьте метку после двоеточия (например, `mcr.microsoft.com/mssql/server:2017-GA-ubuntu`). Для просмотра всех доступных образов, см. в разделе [странице mssql-server, Docker hub](https://hub.docker.com/r/microsoft/mssql-server).

   ::: zone pivot="cs1-bash"
   Для команд bash в этой статье `sudo` используется. В Mac OS `sudo` может не потребоваться. В Linux, если вы не хотите использовать `sudo` для запуска Docker, можно настроить **docker** группы и добавление пользователей в эту группу. Дополнительные сведения см. в разделе [действия после установки для Linux](https://docs.docker.com/install/linux/linux-postinstall/).
   ::: zone-end

2. Чтобы запустить образ контейнера с помощью Docker, выполните следующую команду в оболочке bash (Linux или macOS) или в командной строке PowerShell с повышенными привилегиями.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```
   ::: zone-end

   > [!NOTE]
   > Пароль должен удовлетворять политике паролей SQL Server по умолчанию; в противном случае контейнер не сможет настроить SQL Server и прекратит работу. По умолчанию пароль должен содержать по крайней мере 8 символов и содержать символы трех из следующих четырех категорий: Прописные буквы, строчные буквы, десятичные цифры и символы. Проверить журнал ошибок можно, выполнив команду [docker logs](https://docs.docker.com/engine/reference/commandline/logs/).

   > [!NOTE]
   > По умолчанию она создаст контейнер с выпуском SQL Server 2017 Developer. Процесс запуска контейнера с производственными выпусками немного отличается. Дополнительные сведения см. в разделе [Запуск образов контейнеров с производственными выпусками](sql-server-linux-configure-docker.md#production).

   Следующая таблица содержит описание параметров запуска команды `docker run` из предыдущего примера.

   | Параметр | Описание |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  Присвойте переменной **ACCEPT_EULA** любое значение, чтобы подтвердить свое согласие с [лицензионным соглашением](https://go.microsoft.com/fwlink/?LinkId=746388). Обязательный параметр для образа SQL Server. |
   | **-e 'SA_PASSWORD=\<YourStrong!Passw0rd\>'** | Укажите свой надежный пароль длиной не меньше восьми символов, соответствующий [требованиям к паролям в SQL Server](../relational-databases/security/password-policy.md). Обязательный параметр для образа SQL Server. |
   | **-p 1433:1433** | Сопоставление TCP-порта среды узла (первое значение) с TCP-портом в контейнере (второе значение). В этом примере SQL Server прослушивает TCP 1433 в контейнере, и он предоставляется к порту 1433 на узле. |
   | **--name sql1** | Укажите свое имя для контейнера вместо сгенерированного случайным образом. При запуске нескольких контейнеров использовать одинаковые имена запрещено. |
   | **mcr.Microsoft.com/MSSQL/Server:2017-Latest** | Контейнер образа Linux с SQL Server 2017. |

3. Для просмотра ваших контейнеров Docker используйте команду `docker ps`.


   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker ps -a
   ```
   ::: zone-end

   На следующем рисунке изображен примерный вывод команды.

   ![Вывод команды docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. Если в столбце **STATUS** (состояние) отображается состояние **Up** (запущен), то SQL Server выполняется в контейнере и прослушивает порт, указанный в столбце **PORTS** (порты). Если в столбце **STATUS** контейнера с SQL Server отображается **Exited** (завершен), см.руководство [Устранение неполадок конфигурации](sql-server-linux-configure-docker.md#troubleshooting).

Параметр `-h` (имя узла) может оказаться полезен, но для простоты в этом учебнике он не описывается. Он изменяет внутреннее имя контейнера на пользовательское значение. Это имя отображается при выполнении следующего запроса Transact-SQL.

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Установка параметров `-h` и `--name` равными позволяет легко идентифицировать целевой контейнер.

::: moniker-end
<!--End of 2017 "Pull and run" section-->

<!--This is the 2019 version of the "Pull and run" section-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="pullandrun2019"></a> Извлечение и запуск образа контейнера

Прежде чем выполнять следующие действия, убедитесь, что выбран основной оболочке (bash, PowerShell или cmd) в верхней части этой статьи.

1. Извлечь предварительной версии SQL Server 2019 образа контейнера Linux из Docker Hub.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker pull mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   > [!TIP]
   > В этом кратком руководстве используется Предварительная версия SQL Server 2019 образа Docker. Если вы хотите запустить образ SQL Server 2017, см. в разделе [версию этой статьи в SQL Server 2017](quickstart-install-connect-docker.md?view=sql-server-linux-2017#pullandrun2017).

   Предыдущая команда извлекает контейнер изображения предварительного просмотра SQL Server 2019, используя в Ubuntu. Вместо этого использовать образы контейнеров, в зависимости от RedHat, см. в разделе [образы контейнеров на основе запуска RHEL](sql-server-linux-configure-docker.md#rhel). Список всех доступных образов см. на странице [mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) центра Docker.

   ::: zone pivot="cs1-bash"
   Для команд bash в этой статье `sudo` используется. В Mac OS `sudo` может не потребоваться. В Linux, если вы не хотите использовать `sudo` для запуска Docker, можно настроить **docker** группы и добавление пользователей в эту группу. Дополнительные сведения см. в разделе [действия после установки для Linux](https://docs.docker.com/install/linux/linux-postinstall/).
   ::: zone-end

2. Чтобы запустить образ контейнера с помощью Docker, выполните следующую команду в оболочке bash (Linux или macOS) или в командной строке PowerShell с повышенными привилегиями.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu
   ```
   ::: zone-end

   > [!NOTE]
   > Пароль должен удовлетворять политике паролей SQL Server по умолчанию; в противном случае контейнер не сможет настроить SQL Server и прекратит работу. По умолчанию пароль должен содержать по крайней мере 8 символов и содержать символы трех из следующих четырех категорий: Прописные буквы, строчные буквы, десятичные цифры и символы. Проверить журнал ошибок можно, выполнив команду [docker logs](https://docs.docker.com/engine/reference/commandline/logs/).

   > [!NOTE]
   > По умолчанию она создаст контейнер с Developer edition, SQL Server 2019 предварительной версии.

   Следующая таблица содержит описание параметров запуска команды `docker run` из предыдущего примера.

   | Параметр | Описание |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  Присвойте переменной **ACCEPT_EULA** любое значение, чтобы подтвердить свое согласие с [лицензионным соглашением](https://go.microsoft.com/fwlink/?LinkId=746388). Обязательный параметр для образа SQL Server. |
   | **-e 'SA_PASSWORD=\<YourStrong!Passw0rd\>'** | Укажите свой надежный пароль длиной не меньше восьми символов, соответствующий [требованиям к паролям в SQL Server](../relational-databases/security/password-policy.md). Обязательный параметр для образа SQL Server. |
   | **-p 1433:1433** | Сопоставление TCP-порта среды узла (первое значение) с TCP-портом в контейнере (второе значение). В этом примере SQL Server прослушивает TCP 1433 в контейнере, и он предоставляется к порту 1433 на узле. |
   | **--name sql1** | Укажите свое имя для контейнера вместо сгенерированного случайным образом. При запуске нескольких контейнеров использовать одинаковые имена запрещено. |
   | **mcr.microsoft.com/mssql/server:2019-CTP3.0-ubuntu** | Образ контейнера SQL Server 2019 CTP 3.0 Linux. |

3. Для просмотра ваших контейнеров Docker используйте команду `docker ps`.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker ps -a
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker ps -a
   ```
   ::: zone-end

   На следующем рисунке изображен примерный вывод команды.

   ![Вывод команды docker ps](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. Если в столбце **STATUS** (состояние) отображается состояние **Up** (запущен), то SQL Server выполняется в контейнере и прослушивает порт, указанный в столбце **PORTS** (порты). Если в столбце **STATUS** контейнера с SQL Server отображается **Exited** (завершен), см.руководство [Устранение неполадок конфигурации](sql-server-linux-configure-docker.md#troubleshooting).

Параметр `-h` (имя узла) может оказаться полезен, но для простоты в этом учебнике он не описывается. Он изменяет внутреннее имя контейнера на пользовательское значение. Это имя отображается при выполнении следующего запроса Transact-SQL.

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

Установка параметров `-h` и `--name` равными позволяет легко идентифицировать целевой контейнер.

::: moniker-end
<!--End of 2019 "Pull and run" section-->

## <a id="sapassword"></a> Смена пароля Администратора

<!-- This section was pasted in from includes/sql-server-linux-change-docker-password.md, to better support zone pivots. 2019/02/11 -->

Учетная запись **SA** обладает правами администратора на экземпляре SQL Server, создаваемом во время установки. После создания контейнера SQL Server указанную вами переменную среды `MSSQL_SA_PASSWORD` можно обнаружить, запустив `echo $MSSQL_SA_PASSWORD` в контейнере. В целях безопасности смените пароль SA.

1. Назначьте для пользователя SA надежный пароль.

1. Используйте `docker exec` для запуска **sqlcmd**, чтобы изменить пароль с помощью Transact-SQL. В следующем примере Замените старый пароль, `<YourStrong!Passw0rd>`и задайте новый пароль `<YourNewStrong!Passw0rd>`, собственными значениями пароля.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
   ::: zone-end

## <a name="connect-to-sql-server"></a>Подключение к SQL Server

На следующем шаге воспользуемся средством командной строки SQL Server **sqlcmd** внутри контейнера для подключения к SQL Server.

1. Выполните команду `docker exec -it`, чтобы запустить интерактивную оболочку bash внутри запущенного контейнера. В следующем примере `sql1` — это имя, заданное в параметре `--name` при создании контейнера.

   ::: zone pivot="cs1-bash"
   ```bash
   sudo docker exec -it sql1 "bash"
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   docker exec -it sql1 "bash"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   docker exec -it sql1 "bash"
   ```
   ::: zone-end

2. После входа в контейнер подключитесь локально с помощью sqlcmd. Средство sqlcmd не включено в путь по умолчанию, поэтому необходимо указать полный путь.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   > [!TIP]
   > Вы можете опустить пароль в командной строке. В этом случае вы получите приглашение для его ввода.

3. Если все сработает должным образом, вы перейдете к приглашению команды **sqlcmd**: `1>`.

## <a name="create-and-query-data"></a>Создание и запрос данных

В следующих разделах приведено пошаговое руководство по созданию базы данных, добавлению данных и запуску простого запроса с использованием **sqlcmd** и Transact-SQL.

### <a name="create-a-new-database"></a>Создание базы данных

Выполните следующие шаги, чтобы создать базу данных `TestDB`.

1. В приглашении команды **sqlcmd** вставьте следующую команду Transact-SQL, чтобы создать тестовую базу данных:

   ```sql
   CREATE DATABASE TestDB
   ```

2. В следующей строке напишите запрос, который должен вернуть имена всех баз данных на сервере:

   ```sql
   SELECT Name from sys.Databases
   ```

3. Две предыдущие команды были выполнены не сразу. Необходимо ввести `GO` на новой строке, чтобы выполнить предыдущие команды:

   ```sql
   GO
   ```

### <a name="insert-data"></a>Вставка данных

Теперь создайте таблицу `Inventory` и вставьте две новых строки.

1. В приглашении команды **sqlcmd** переключите контекст на новую базу данных `TestDB`:

   ```sql
   USE TestDB
   ```

2. Создайте таблицу `Inventory`:

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

3. Вставьте данные в новую таблицу:

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

4. Введите `GO`, чтобы выполнить предыдущие команды:

   ```sql
   GO
   ```

### <a name="select-data"></a>Выбор данных

Теперь выполните запрос, чтобы вернуть данные из таблицы `Inventory`.

1. В приглашении команды **sqlcmd** введите запрос, который должен вернуть из таблицы `Inventory` строки, где количество превышает 152:

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

2. Выполните команду:

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>Выход из приглашения команды sqlcmd

1. Чтобы завершить сеанс **sqlcmd**, введите `QUIT`:

   ```sql
   QUIT
   ```

2. Чтобы выйти из интерактивной командной строки в контейнере, введите команду `exit`. Контейнер продолжит работать после выхода из интерактивной оболочки bash.

## <a id="connectexternal"></a> Подключение из-за пределов контейнера

Подключиться к экземпляру SQL Server на компьютере Docker можно также с помощью любого внешнего инструмента в macOS, Windows или Linux, поддерживающего подключения SQL.

В следующем примере используется **sqlcmd** вне контейнера для подключения к SQL Server, запущенному в контейнере. В этом примере предполагается, что в среде вне контейнера, из которой происходит подключение, уже установлены средства командной строки SQL Server. Те же принципы применяются при использовании других средств, но процесс подключения является уникальным для каждого средства.

1. Определите IP-адрес компьютера, на котором размещен контейнер. В Linux используйте команды **ifconfig** или **IP-адрес**. В Windows используйте команду **ipconfig**.

1. Например, установка **sqlcmd** средство на клиентском компьютере. Дополнительные сведения см. в разделе [Установка sqlcmd на Windows](../tools/sqlcmd-utility.md) или [Установка sqlcmd в Linux](sql-server-linux-setup-tools.md).

1. Запустите sqlcmd, указав IP-адрес и порт, сопоставленный с портом 1433 в контейнере. В этом примере это тот же порт 1433, на хост-компьютере. Если вы не указали другой порт сопоставленные на хост-компьютере, использовать его здесь.

   ::: zone pivot="cs1-bash"
   ```bash
   sqlcmd -S <ip_address>,1433 -U SA -P '<YourNewStrong!Passw0rd>'
   ```
   ::: zone-end

   ::: zone pivot="cs1-powershell"
   ```PowerShell
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong!Passw0rd>"
   ```
   ::: zone-end

   ::: zone pivot="cs1-cmd"
   ```cmd
   sqlcmd -S <ip_address>,1433 -U SA -P "<YourNewStrong!Passw0rd>"
   ```
   ::: zone-end

1. Выполните команды языка Transact-SQL. По завершении введите `QUIT`.

Другие распространенные средства для подключения к SQL Server:

- [Visual Studio Code](sql-server-linux-develop-use-vscode.md);
- [SQL Server Management Studio (SSMS) в Windows](sql-server-linux-manage-ssms.md);
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [mssql-cli (предварительная версия)](https://github.com/dbcli/mssql-cli/blob/master/doc/usage_guide.md).
- [PowerShell Core](sql-server-linux-manage-powershell-core.md)

## <a name="remove-your-container"></a>Удаление контейнера

Чтобы удалить контейнер SQL Server, используемый в этом руководстве, выполните следующие команды.

::: zone pivot="cs1-bash"
```bash
sudo docker stop sql1
sudo docker rm sql1
```
::: zone-end

::: zone pivot="cs1-powershell"
```PowerShell
docker stop sql1
docker rm sql1
```
::: zone-end

::: zone pivot="cs1-cmd"
```cmd
docker stop sql1
docker rm sql1
```
::: zone-end

> [!WARNING]
> Остановка и удаление контейнера безвозвратно удаляет все данные SQL Server в контейнере. Чтобы сохранить данные, [создайте и скопируйте файл резервной копии за пределы контейнера](tutorial-restore-backup-in-sql-server-container.md) или используйте [метод постоянного хранения данных контейнера](sql-server-linux-configure-docker.md#persist).

## <a name="docker-demo"></a>Демонстрация возможностей Docker

После того как вы научились использовать образ контейнера SQL Server для Docker, возможно, вы захотите узнать, как использовать Docker для упрощения разработки и тестирования. Следующий видеоролик рассказывает о том, как можно использовать Docker в сценарии непрерывной интеграции и развертывания.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>Следующие шаги

Сведения о восстановлении файлов резервной копии базы данных в контейнере см. в руководстве [Восстановление базы данных SQL Server в контейнере Docker в Linux](tutorial-restore-backup-in-sql-server-container.md). Чтобы изучить другие сценарии, такие как запуск нескольких контейнеров, сохраняемость данных и устранение неполадок, см. в разделе [SQL Server можно настроить образы контейнеров в Docker](sql-server-linux-configure-docker.md).

Кроме того, в репозитории GitHub [mssql docker](https://github.com/Microsoft/mssql-docker) вы найдете ресурсы, отзывы и известные проблемы.
