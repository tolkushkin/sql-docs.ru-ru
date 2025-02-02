---
title: Настройка распределенной группы доступности
description: 'В этом разделе описано создание и настройка распределенной группы доступности Always On. '
ms.custom: seodec18
ms.date: 08/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 2963dd3f867b4080d383f51dc9f41baf0a1733ec
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793740"
---
# <a name="configure-a-distributed-always-on-availability-group"></a>Настройка распределенной группы доступности Always On  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Для создания распределенной группы доступности необходимо создать две группы доступности, каждая из которых имеет собственный прослушиватель. После этого можно объединить эти группы доступности в распределенную группу доступности. Ниже представлен простой пример c Transact-SQL. В этом примере представлены не все детали создания групп доступности и прослушивателей; основное внимание уделяется ключевым требованиям.

Технические сведения о распределенных группах доступности см. в статье [Распределенные группы доступности](distributed-availability-groups.md).

## <a name="prerequisites"></a>предварительные требования

### <a name="set-the-endpoint-listeners-to-listen-to-all-ip-addresses"></a>Настройка прослушивателей конечных точек на прослушивание всех IP-адресов

Убедитесь, что конечные точки могут взаимодействовать между различными группами доступности в распределенной группе доступности. Если в одной группе доступности задана определенная сеть в конечной точке, распределенная группа доступности будет работать неправильно. На каждом сервере, на котором будет размещаться реплика распределенной группы доступности, настройте прослушиватель так, чтобы он ожидал передачи данных со всех IP-адресов (`LISTENER_IP = ALL`).

#### <a name="create-a-listener-to-listen-to-all-ip-addresses"></a>Создание прослушивателя для прослушивания всех IP-адресов

Например, следующий скрипт создает в TCP-порте 5022 конечную точку прослушивателя, которая прослушивает все IP-адреса.  

```sql
CREATE ENDPOINT [aodns-hadr] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
FOR DATA_MIRRORING (
   ROLE = ALL, 
   AUTHENTICATION = WINDOWS NEGOTIATE,
   ENCRYPTION = REQUIRED ALGORITHM AES
)
GO
```

#### <a name="alter-a-listener-to-listen-to-all-ip-addresses"></a>Изменение прослушивателя для прослушивания всех IP-адресов

Например, следующий скрипт изменяет конечную точку прослушивателя таким образом, чтобы прослушивались все IP-адреса.  

```sql
ALTER ENDPOINT [aodns-hadr] 
    AS TCP (LISTENER_IP = ALL)
GO
```

## <a name="create-first-availability-group"></a>Создание первой группы доступности

### <a name="create-the-primary-availability-group-on-the-first-cluster"></a>Создание первичной группы доступности в первом кластере  
Создайте группу доступности в первом отказоустойчивом кластере Windows Server (WSFC).   В этом примере это группа доступности с именем `ag1` для базы данных `db1`. Первичная реплика первичной группы доступности называется **глобальной первичной** в распределенной группе доступности. Server1 — это глобальная первичная реплика в нашем примере.        
  
```sql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
>[!NOTE]
>В предыдущем примере используется прямое присвоение начальных значений, где **SEEDING_MODE** получает значение **AUTOMATIC** как для реплик, так и для распределенной группы доступности. С такой конфигурацией вторичные реплики и вторичная группа доступности заполняются автоматически и не требуют резервного копирования и восстановления первичной базы данных вручную.  
  
### <a name="join-the-secondary-replicas-to-the-primary-availability-group"></a>Присоединение вторичной реплики к первичной группе доступности  
Все вторичные реплики должны быть присоединены к группе доступности **ALTER AVAILABILITY GROUP** с параметром **JOIN** . Поскольку в этом примере используется прямое присвоение начальных значений, необходимо, помимо прочего, вызвать метод  **ALTER AVAILABILITY GROUP** с параметром **GRANT CREATE ANY DATABASE** . Это позволяет группе доступности создать базу данных и начать ее автоматическое заполнение из первичной реплики.  
  
В этом примере во вторичной реплике `server2`выполняются указанные ниже команды, предназначенные для присоединения группы доступности `ag1` . После этого группа доступности получает возможность создавать базы данных во вторичной реплике.  
  
```sql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  

>[!NOTE]
>Когда группа доступности создает базу данных во вторичной реплике, она устанавливает в качестве владельца базы данных учетную запись, от имени которой была выполнена инструкция `ALTER AVAILABILITY GROUP`, предоставляя этой учетной записи разрешение на создание любых баз данных. Дополнительные сведения см. в разделе [Предоставление группе доступности разрешения на создание базы данных во вторичной реплике](automatic-seeding-secondary-replicas.md#grantCreate).
  
### <a name="create-a-listener-for-the-primary-availability-group"></a>Создание прослушивателя для первичной группы доступности  

После этого добавьте прослушиватель для первичной группы доступности в первый кластер WSFC. В этом примере прослушиватель имеет имя `ag1-listener`. Подробные инструкции по созданию прослушивателя см. в разделе [Создание или настройка прослушивателя группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```sql
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( 
        WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , 
        PORT = 60173);    
GO  
```  
  

## <a name="create-second-availability-group"></a>Создание второй группы доступности  
 Создайте вторую группу доступности, `ag2`, во втором кластере WSFC. В этом случае база данных не указана, так как она автоматически заполняется данными из первичной группы доступности.  Первичная реплика вторичной группы доступности называется **сервером пересылки** в распределенной группе доступности. Server3 — это сервер пересылки в нашем примере. 
  
```sql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
> Во вторичной группе доступности необходимо использовать ту же конечную точку зеркального отображения базы данных (в этом примере — порт 5022). В противном случае после локальной отработки отказа репликация будет остановлена.  
  
### <a name="join-the-secondary-replicas-to-the-secondary-availability-group"></a>Присоединение вторичных реплик к вторичной группе доступности  
 В этом примере во вторичной реплике `server4`выполняются указанные ниже команды, предназначенные для присоединения группы доступности `ag2` . После этого группа доступности получает возможность создавать базы данных во вторичной реплике для прямого присвоения начальных значений.  
  
```sql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### <a name="create-a-listener-for--the-secondary-availability-group"></a>Создание прослушивателя для вторичной группы доступности  
 После этого добавьте прослушиватель для вторичной группы доступности во второй кластер WSFC. В этом примере прослушиватель имеет имя `ag2-listener`. Подробные инструкции по созданию прослушивателя см. в разделе [Создание или настройка прослушивателя группы доступности (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
## <a name="create-distributed-availability-group-on-first-cluster"></a>Создание распределенной группы доступности в первом кластере  
 В первом WSFC создайте распределенную группу доступности (в этом примере она называется `distributedag` ). Используйте команду **CREATE AVAILABILITY GROUP** с параметром **DISTRIBUTED** . Параметр **AVAILABILITY GROUP ON** указывает группы доступности, входящие в состав распределенной группы доступности: `ag1` и `ag2`.  
  
```sql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL** указывает прослушиватель для каждой группы доступности, а также конечную точку зеркального отображения базы данных для группы доступности. В этом примере это порт `5022` (а не порт `60173` , который использовался для создания прослушивателя). Если вы используете подсистему балансировки нагрузки, например в Azure, [добавьте правило балансировки нагрузки для порта распределенной группы доступности](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#add-load-balancing-rule-for-distributed-availability-group). Добавьте правило для порта прослушивателя в дополнение к порту экземпляра SQL Server. 
  
## <a name="join-distributed-availability-group-on-second-cluster"></a>Присоединение распределенной группы доступности во втором кластере  
 Присоедините распределенную группу доступности во втором кластере WSFC.  
  
```sql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

## <a name="failover"></a>Присоединение базы данных во вторичной реплике второй группы доступности
Когда база данных во вторичной реплике второй группы доступности перейдет в состояние восстановления, вам нужно вручную присоединить ее к группе доступности.

```sql  
ALTER DATABASE [db1] SET HADR AVAILABILITY GROUP = [ag2];   
```
  
## <a name="failover"></a> Отработка отказа во вторичную группу доступности  

В настоящее время поддерживается только отработка отказа вручную. Чтобы произвести отработку отказа распределенной группы доступности вручную, выполните указанные ниже действия.

1. Чтобы избежать потерь данных, настройте для распределенной группы доступности синхронную фиксацию.
1. Подождите, пока распределенная группа доступности синхронизируется.
1. В глобальной первичной реплике задайте для роли распределенной группы доступности значение `SECONDARY`.
1. Проверьте готовность к отработке отказа.
1. Выполните отработку отказа первичной группы доступности.

В следующем примере Transact-SQL пошагово демонстрируется отработка отказа распределенной группы доступности с именем `distributedag`:

1. Настройте для распределенной группы доступности синхронную фиксацию, выполнив следующий код на *обеих* репликах (глобальной основной и пересылки).   
    
      ```sql  
      -- sets the distributed availability group to synchronous commit 
       ALTER AVAILABILITY GROUP [distributedag] 
       MODIFY 
       AVAILABILITY GROUP ON
       'ag1' WITH 
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        ), 
        'ag2' WITH  
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        );
       
       -- verifies the commit state of the distributed availability group
       select ag.name, ag.is_distributed, ar.replica_server_name, ar.availability_mode_desc, ars.connected_state_desc, ars.role_desc, 
       ars.operational_state_desc, ars.synchronization_health_desc from sys.availability_groups ag  
       join sys.availability_replicas ar on ag.group_id=ar.group_id
       left join sys.dm_hadr_availability_replica_states ars
       on ars.replica_id=ar.replica_id
       where ag.is_distributed=1
       GO

      ```  
   >[!NOTE]
   >В распределенной группе доступности состояние синхронизации между двумя группами доступности зависит от режима доступности обеих реплик. В режиме синхронной фиксации текущие первичная и вторичная группы доступности должны быть настроены с использованием режима доступности `SYNCHRONOUS_COMMIT`. По этой причине приведенный выше скрипт необходимо выполнить как в глобальной первичной реплике, так и в реплике пересылки.

1. Подождите, пока состояние распределенной группы доступности изменится на `SYNCHRONIZED`. Выполните следующий запрос в глобальной первичной реплике (первичная реплика в первичной группе доступности). 
    
      ```sql  
      SELECT ag.name
             , drs.database_id
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.end_of_log_lsn 
        FROM sys.dm_hadr_database_replica_states drs,
        sys.availability_groups ag
          WHERE drs.group_id = ag.group_id;      
      ```  

    Продолжите работу, когда параметр **synchronization_state_desc** группы доступности примет значение `SYNCHRONIZED`. Если параметр **synchronization_state_desc** не равен `SYNCHRONIZED`, запускайте команду каждые пять секунд, пока он не изменится. Не продолжайте работу до установки состояния **synchronization_state_desc** = `SYNCHRONIZED`. 

1. В глобальной первичной реплике задайте для роли группы доступности значение `SECONDARY`. 

    ```sql
    ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
    ```  

    На этом этапе распределенная группа доступности недоступна.

1. Проверьте готовность к отработке отказа. Выполните следующий запрос:

    ```sql
    SELECT ag.name, 
        drs.database_id, 
        drs.group_id, 
        drs.replica_id, 
        drs.synchronization_state_desc, 
        drs.end_of_log_lsn 
    FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
    WHERE drs.group_id = ag.group_id; 
    ```  
    Группа доступности готова к отработке отказа, если **synchronization_state_desc** имеет значение `SYNCHRONIZED`, а **end_of_log_lsn** совпадает для обеих групп доступности. 

1. Проведите отработку отказа из первичной группы доступности во вторичную. Запустите следующую команду в SQL Server, где размещена первичная реплика дополнительной группы доступности. 

    ```sql
    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```  

    После этого этапа распределенная группа доступности будет доступна.
      
После выполнения описанных выше шагов, распределенная группа доступности выполняет отработку отказа без потери данных. Если группы доступности находятся на удаленном расстоянии друг от друга, что приводит к задержке, измените режим доступности обратно на ASYNCHRONOUS_COMMIT. 
  
## <a name="remove-a-distributed-availability-group"></a>Удаление распределенной группы доступности  
 Следующая инструкция Transact-SQL удаляет распределенную группу доступности с именем `distributedag`:  
  
```sql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## <a name="create-distributed-availability-group-on-failover-cluster-instances"></a>Создание распределенной группы доступности в экземплярах отказоустойчивого кластера

Вы можете создать распределенную группу доступности, используя группу доступности на экземпляре отказоустойчивого кластера (FCI). В этом случае прослушиватель группы доступности не требуется. Используйте имя виртуальной сети (VNN) для первичной реплики экземпляра отказоустойчивого кластера. В следующем примере показана распределенная группа доступности с именем SQLFCIDAG. Группа доступности SQLFCIAG SQLFCIAG содержит две реплики FCI. Имя виртуальной сети для первичной реплики FCI имеет значение SQLFCIAG-1, а для вторичной — SQLFCIAG-2. Распределенная группа доступности также включает в себя SQLAG-DR для аварийного восстановления.

![Распределенная группа доступности AlwaysOn](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 Следующая инструкция DDL создает эту распределенную группу доступности. 

```sql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

URL-адрес прослушивателя соответствует имени виртуальной сети первичного экземпляра FCI.

## <a name="manually-fail-over-fci-in-distributed-availability-group"></a>Ручная отработка отказа отказоустойчивого кластера в распределенной группе доступности

Для выполнения ручной отработки отказа в группе доступности отказоустойчивого кластера обновите распределенную группу доступности в соответствии с измененным URL-адресом прослушивателя. Например, выполните следующую инструкцию DDL как в основной, так и в дополнительной группах доступности SQLFCIAG:

```sql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2.contoso.com:5022'
    )
```  
  
## <a name="next-steps"></a>Следующие шаги

 [CREATE AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
