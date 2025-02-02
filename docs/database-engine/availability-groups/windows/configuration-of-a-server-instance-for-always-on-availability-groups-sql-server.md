---
title: Включение функции группы доступности для экземпляра SQL Server
description: В этой статье описывается включение функции группы доступности Always On для экземпляра SQL Server.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 65feba8f50d4f293e97f9443c0ff006bf40b5029
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772619"
---
# <a name="enable-the-always-on-availability-group-feature-for-a-sql-server-instance"></a>Включение функции группы доступности Always On для экземпляра SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Этот раздел содержит сведения о требованиях к настройке экземпляра [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] для поддержки [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  Важные сведения о предварительных требованиях и ограничениях [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] для узлов с отказоустойчивой кластеризацией Windows Server (WSFC) и экземпляров [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]см. в статье [Предварительные требования, ограничения и рекомендации для групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
   
##  <a name="TermsAndDefinitions"></a> Термины и определения  
 [Группы доступности AlwaysOn](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
 Решение по обеспечению высокой доступности и аварийного восстановления, заменяющее зеркальное отображение базы данных на уровне предприятия. *Группа доступности* поддерживает среду отработки отказа для дискретного набора пользовательских баз данных, известных как *базы данных доступности*, которые совместно выполняют переход на другой ресурс.  
  
 реплика доступности  
 Создание экземпляра группы доступности, которая размещена на определенном экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и поддерживает локальную копию каждой базы данных доступности, входящей в группу доступности. Существует два типа реплик доступности: одна *первичная* и от одной до четырех *вторичных реплик*. Экземпляры сервера, на которых размещаются реплики доступности для данной группы доступности, должны размещаться на разных узлах одной кластеризации WSFC.  
  
 [конечная точка зеркального отображения базы данных](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 Конечная точка — это объект SQL Server, позволяющий SQL Server обмениваться данными по сети. Для участия в зеркальном отображении базы данных и/или [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , экземпляр сервера требует наличия специальной, выделенной конечной точки. Все подключения зеркального отображения и групп доступности на экземпляре сервера используют одну конечную точку зеркального отображения базы данных. Эта точка является конечной точкой специального назначения. Она используется исключительно для приема подключений от других экземпляров сервера.  
  
##  <a name="ConfigSI"></a> Настройка экземпляра сервера для поддержки групп доступности AlwaysOn  
 Для поддержки [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]экземпляр сервера должен находиться на узле в отказоустойчивом кластере WSFC, в котором размещается группа доступности; для него должна быть включена поддержка [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] и должна иметься конечная точка зеркального отображения базы данных.  
  
1.  Включите функцию "Группы доступности AlwaysOn" на всех экземплярах сервера, которые будут использоваться в одной или нескольких группах доступности. На данном экземпляре сервера может быть размещена только одна реплика доступности для данной группы доступности.  
  
2.  Убедитесь, что в экземпляре сервера есть конечная точка зеркального отображения базы данных.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Включение функции "Группы доступности AlwaysOn"**  
  
-   [Включение и отключение групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Определение того, существует ли конечная точка зеркального отображения базы данных**  
  
-   [sys.database_mirroring_endpoints (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
 **Создание конечной точки зеркального отображения базы данных**  
  
-   [Создание конечной точки зеркального отображения базы данных для групп доступности AlwaysOn (SQL Server PowerShell)](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Создание конечной точки зеркального отображения базы данных с проверкой подлинности Windows (Transact-SQL)](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Включение использования сертификатов для исходящих соединений в конечной точке зеркального отображения базы данных (Transact-SQL)](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="RelatedContent"></a> См. также  
  
-   **Блоги**  
  
     [Обучающая серия Always ON — HADRON. Использование рабочего пула для баз данных с HADRON](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Блоги команды разработчиков SQL Server Always On: официальный блог по SQL Server Always On](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Блоги инженеров CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Видеоролики**  
  
     [Microsoft SQL Server с рабочим названием Denali Always On, часть 1: вводные сведения о решении следующего поколения по обеспечению высокого уровня доступности](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server с рабочим названием Denali Always On, часть 2: создание критически важного решения по обеспечению высокого уровня доступности с использованием Always On](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Технические документы**  
  
     [Руководство по решениям режима AlwaysOn в Microsoft SQL Server для обеспечения высокой доступности и аварийного восстановления](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Технические документы Майкрософт Microsoft по SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Технические документы группы консультантов по SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Предварительные требования, ограничения и рекомендации для групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Конечная точка зеркального отображения базы данных (SQL Server)](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Группы доступности Always On: взаимодействие (SQL Server)](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [Отказоустойчивая кластеризация и группы доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Отказоустойчивая кластеризация Windows Server (WSFC) с SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Экземпляры отказоустойчивого кластера (режим AlwaysOn) (SQL Server)](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
