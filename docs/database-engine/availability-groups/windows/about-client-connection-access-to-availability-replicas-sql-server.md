---
title: Типы клиентских подключений к репликам в группе доступности
description: Сведения о различных типах подключений, которые клиенты могут устанавливать к первичной или вторичной реплике группы доступности Always On в SQL Server.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 29027e46-43e4-4b45-b650-c4cdeacdf552
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 977d29b873a247bcd50b14546957364725ab10be
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801367"
---
# <a name="types-of-client-connections-to-replicas-within-an-always-on-availability-group"></a>Типы клиентских подключений к репликам в группе доступности Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В группе доступности AlwaysOn можно настроить одну или несколько реплик доступности, подключения к которой могут выполняться в режиме только для чтения, когда они являются вторичными (то есть при работе в качестве вторичной реплики). Каждую реплику доступности можно также настроить так, чтобы она разрешала или исключала соединения только для чтения во время работы под первичной ролью (т. е. во время работы в качестве первичной реплики).  
  
 Чтобы упростить клиентский доступ к базе данных-источнику или получателю в данной группе доступности, необходимо определить прослушиватель группы доступности. По умолчанию новые соединения с прослушивателем группы доступности будут перенаправляться к первичной реплике. Однако можно настроить группу доступности для поддержки маршрутизации только для чтения, которая позволяет своему прослушивателю переадресовывать запросы на соединения только для чтения на вторичную реплику только для чтения. Дополнительные сведения см. в статье [Настройка маршрутизации только для чтения в группе доступности (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md).  
  
 Во время отработки отказа вторичная реплика принимает первичную роль, а прежняя первичная реплика — вторичную роль. Во время процесса отработки отказа завершаются все клиентские соединения с первичной и вторичной репликами. После отработки отказа, когда клиент выполняет повторное соединение с прослушивателем группы доступности, прослушиватель соединяет клиента с новой первичной репликой, кроме тех случаев, когда выполняется запрос на соединение только для чтения. Если маршрутизация только для чтения настроена для клиента и для экземпляров сервера, на которых размещена первичная реплика и хотя бы одна вторичная реплика доступна только для чтения, то запросы на соединение только для чтения перенаправляются на вторичную реплику, которая поддерживает необходимый клиенту тип соединения и доступа. Чтобы обеспечить непрерывность работы клиента после отработки отказа, важно настроить доступ соединения как для вторичной, так и для первичной ролей каждой реплики доступности.  
  
> [!NOTE]  
>  Сведения о прослушивателе групп доступности, обрабатывающем запросы на клиентские подключения, см. в разделе [Прослушиватели групп доступности, возможность подключения клиентов и отработка отказа приложений (SQL Server)](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).  
  
##  <a name="ConnectAccessForSecondary"></a> Типы доступа соединений, поддерживаемые вторичной ролью  
 Вторичная роль поддерживает три альтернативных варианта клиентского соединения, а именно:  
  
 Нет соединений  
 Пользовательские соединения не разрешены. Базы данных-получатели недоступны для доступа в режиме чтения. Это поведение по умолчанию во вторичной роли.  
  
 Соединение с намерением только чтения  
 Базы данных-получатели доступны только для соединений, для которых свойство соединения **Назначение приложения** имеет значение **ReadOnly** (*соединения с намерением чтения*).  
  
 Дополнительные сведения об этом свойстве соединения см. в разделе [Поддержка высокого уровня доступности и аварийного восстановления собственного клиента SQL Server](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
 Разрешить любые соединения только для чтения  
 Для всех баз данных-получателей разрешены соединения доступа только для чтения. Этот вариант разрешает соединения клиентам с более ранними версиями ПО.  
  
 Дополнительные сведения см. в разделе [Настройка доступа только для чтения в реплике доступности (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
##  <a name="ConnectAccessForPrimary"></a> Типы доступа соединений, поддерживаемые первичной ролью  
 Первичная роль поддерживает два альтернативных варианта клиентского соединения, а именно:  
  
 Разрешены все соединения  
 К базам данных-источникам разрешено как соединение в режиме «чтение-запись», так и соединение в режиме «только чтение». Это поведение по умолчанию для первичной роли.  
  
 Разрешены только соединения в режиме «чтение-запись»  
 Если свойство соединения **Назначение приложения** имеет значение **ReadWrite** либо не задано, соединение разрешено. Соединения, для которых ключевое слово строки подключения **Application Intent** имеет значение **только чтение** , не разрешены. Разрешая соединения только в режиме «чтение-запись», можно предотвратить случаи, когда клиенты по ошибке подключают к первичной реплике рабочую нагрузку с намерением чтения.  
  
 Дополнительные сведения об этом свойстве соединения см. в разделе [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Дополнительные сведения см. в статье [Настройка доступа только для чтения в реплике доступности (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
##  <a name="HowConnectionAccessAffectsConnectivity"></a> Влияние конфигурации доступа соединения на клиентское соединение  
 Параметры доступа соединения реплики определяют, проходит или не проходит попытка соединения. В следующей таблице приведены сводные сведения о том, проходит или не проходит попытка соединения по каждому параметру доступа соединения.  
  
|Роль реплики|Поддержка доступа к соединению в реплике|Назначение соединения|Результат попытки подключения|  
|------------------|--------------------------------------------|-----------------------|--------------------------------|  
|Вторичная|All|С намерением только чтения, чтения-записи или назначение соединения не указано|Успешно|  
|Вторичная|Нет (поведение по умолчанию вторичной реплики).|С намерением только чтения, чтения-записи или назначение соединения не указано|Failure|  
|Вторичная|Назначение — только чтение|С намерением чтения|Успешно|  
|Вторичная|Назначение — только чтение|С намерением чтения-записи или назначение соединения не указано|Failure|  
|Первичная|Все (поведение по умолчанию первичной реплики).|С намерением только чтения, чтения-записи или назначение соединения не указано|Успешно|  
|Первичная|Чтение и запись|Назначение — только чтение|Failure|  
|Первичная|Чтение и запись|С намерением чтения-записи или назначение соединения не указано|Успешно|  
  
 Сведения о настройке группы доступности для приема клиентских подключений к ее репликам см. в разделе [Прослушиватели групп доступности, возможность подключения клиентов и отработка отказа приложений (SQL Server)](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).  
  
### <a name="example-connection-access-configuration"></a>Пример конфигурации доступа соединения  
 В зависимости от различных конфигураций реплик доступности для доступа соединения, поддержка клиентских соединений может измениться после отработки отказа группой доступности. Рассмотрим группу доступности, для которой отправка отчетов выполняется на удаленных вторичных репликах с асинхронной фиксацией. Все приложения, работающие в режиме только для чтения, для базы данных в этой группе доступности устанавливают для своего свойства соединения **Назначение приложения** значение **ReadOnly**, после чего все соединения в режиме только для чтения становятся соединениями с намерением чтения.  
  
 В примере этой группы доступности рассматриваются две реплики синхронной фиксации в главном вычислительном центре и две реплики асинхронной фиксации на дополнительном сайте. Для первичной роли все реплики настраиваются на режим доступа «чтение-запись», что предотвращает соединения с намерением только чтения к первичной реплике во всех ситуациях. Вторичная реплика с синхронной фиксацией использует конфигурацию доступа соединения по умолчанию (вариант «нет»), что приводит к отказу во всех клиентских соединениях под вторичной ролью.  И наоборот, реплики асинхронной фиксации настраиваются на разрешение соединений с намерением чтения под вторичной ролью. В следующей таблице приведена сводка по конфигурации в этом примере.  
  
|Реплика|Режим фиксации|Первоначальная роль|Доступ соединения для вторичной роли|Доступ соединения для первичной роли|  
|-------------|-----------------|------------------|------------------------------------------|----------------------------------------|  
|Реплика1|Синхронная|Первичная|None|Чтение и запись|  
|Реплика2|Синхронная|Вторичная|None|Чтение и запись|  
|Реплика3|Асинхронная|Вторичная|С намерением только чтения|Чтение и запись|  
|Реплика4|Асинхронная|Вторичная|Назначение — только чтение|Чтение и запись|  
  
 Как правило, в этом сценарии отработка отказа происходит только между репликами синхронной фиксации, а приложения, работающие в режиме с намерением только чтения, сразу после отработки отказа могут установить повторное соединение с одной из вторичных реплик асинхронной фиксации. Однако, когда авария происходит в главном вычислительном центре, будут потеряны обе реплики синхронной фиксации. Администратор баз данных на дополнительном сайте должен выполнить принудительный переход на другой ресурс вручную на вторичную реплику асинхронной фиксации. При принудительной отработке отказа базы данных-получатели на оставшейся вторичной реплике приостанавливаются и в результате становятся недоступными для рабочих нагрузок в режиме только чтения. Новая первичная реплика, настроенная для соединений в режиме «чтение-запись», предотвращает обращения в режиме с намерением только чтения от конкурирующей рабочей нагрузки в режиме «чтение-запись». Это означает, что пока администратор баз данных не возобновит базы данных-получатели на оставшейся вторичной реплике асинхронной фиксации, клиенты, работающие в режиме с намерением только чтения, не могут подключиться ни к одной реплике доступности.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Настройка доступа только для чтения в реплике доступности (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Настройка маршрутизации только для чтения в группе доступности (SQL Server)](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Отслеживание групп доступности (Transact-SQL)](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
-   [Просмотр свойств реплики доступности (SQL Server)](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [Использование диалогового окна "Создание группы доступности" (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="RelatedContent"></a> См. также  
  
-   [Руководство по решениям режима AlwaysOn в Microsoft SQL Server для обеспечения высокой доступности и аварийного восстановления](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Блог команды разработчиков SQL Server Always On: официальный блог по SQL Server Always On](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Прослушиватели групп доступности, возможность подключения клиентов и отработка отказа приложений (SQL Server)](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Статистика](../../../relational-databases/statistics/statistics.md)  
  
  
