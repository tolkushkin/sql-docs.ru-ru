---
title: 'Группы доступности Always On: взаимодействие'
description: Описываются различные функции, которые могут и не могут работать вместе с группами доступности Always On.
ms.custom: seodec18
ms.date: 04/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 74f459293f0ccf6e6b84a577c685bb0eea9adcb3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66761559"
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>Группы доступности Always On: взаимодействие (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

В этом разделе описывается совместимость [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] с другими функциями [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].

## <a name="Interop"></a> Функции, совместимые с группами доступности Always On

В следующей таблице перечислены функции [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , совместимые с [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Ссылка в столбце **Дополнительные сведения** указывает, что имеются замечания по совместимости данной функции.

|Компонент|Дополнительные сведения|
|:------|:---------------|
|система отслеживания измененных данных|[Репликация, отслеживание изменений, изменение данных и группы доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|
|отслеживание изменений|[Репликация, отслеживание изменений, изменение данных и группы доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|
|Автономные базы данных|[Автономные базы данных с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/contained-databases-with-always-on-availability-groups-sql-server.md)|
|Шифрование базы данных|[Зашифрованные базы данных с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md)|
|Моментальные снимки базы данных|[Моментальные снимки баз данных для групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md)|
|FILESTREAM и FileTable|[FILESTREAM и FileTable с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|
|Полнотекстовый поиск|Примечание. Полнотекстовые индексы синхронизируются с базами данных-получателями Always On.|
|доставка журналов;|[Необходимые условия для выполнения перехода от использования доставки журналов к использованию групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|
|Удаленное хранилище больших двоичных объектов|[Удаленное хранилище больших двоичных объектов (RBS) и группы доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|
|Репликация|[Настройка репликации для групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [Обслуживание базы данных публикации AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [Репликация, отслеживание изменений, изменение данных и группы доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [Подписчики репликации и группы доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)|
|Службы Analysis Services|[Службы Analysis Services с группами доступности AlwaysOn](../../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)|
|Службы Reporting Services|Используйте вторичные реплики, доступные только для чтения, в качестве источника данных для отчетов для снижения нагрузки на первичную реплику, доступную для чтения и записи.<br /><br /> [Службы Reporting Services с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)|
|Компонент Service Broker|[Компонент Service Broker с группами доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)|
|Агент SQL Server|&nbsp;|

## <a name="restrictions"></a> Функции, совместимые с группами доступности AlwaysOn с определенными ограничениями

Следующие функции взаимодействуют с [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] с определенными ограничениями. Дополнительные сведения см. в статьях по ссылкам.

- Межбазовые транзакции и распределенные транзакции ([!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] и Windows Server 2016). Дополнительные сведения см. в статье [Транзакции между базами данных и распределенные транзакции для групп доступности AlwaysOn и зеркального отображения базы данных (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).
- [Сборщик данных системы статистики запроса](../../../relational-databases/data-collection/system-data-collection-set-reports.md#Query) не может надежно работать в среде с недоступными для чтения вторичными базами данных. Чтобы использовать сборщик данных системы статистики запросов, разрешите [доступ на чтение](configure-read-only-access-on-an-availability-replica-sql-server.md) всех вторичных реплик группы доступности. 

## <a name="NoInterop"></a> Функции, несовместимые с группами доступности AlwaysOn

[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] не работает в сочетании со следующими функциями.

- Зеркальное отображение базы данных. Дополнительные сведения см. в статье [Транзакции между базами данных и распределенные транзакции для групп доступности AlwaysOn и зеркального отображения базы данных (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).

## <a name="RelatedContent"></a> См. также

- **Блоги**

  [Руководство по миграции. Миграция на отказоустойчивую кластеризацию и группы доступности SQL Server 2012 с предшествующих кластеров и зеркальных отображений](https://blogs.msdn.microsoft.com/sqlalwayson/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments/)
  [Блоги команды разработчиков SQL Server Always On: официальный блог по SQL Server Always On](https://blogs.msdn.microsoft.com/sqlalwayson/)
  [Блоги инженеров CSS SQL Server](https://blogs.msdn.com/b/psssql/)

- **Технические документы**

  [Руководство по миграции. Переход на группы доступности Always On с предыдущих развертываний, сочетающих зеркальное отображение базы данных и доставку журналов](https://msdn.microsoft.com/library/jj635217)
  [Руководство по решениям режима Always On в Microsoft SQL Server для обеспечения высокой доступности и аварийного восстановления](https://go.microsoft.com/fwlink/?LinkId=227600)
  [Технические документы Майкрософт по SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)
  [Технические документы группы консультантов по SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)

## <a name="see-also"></a>См. также:

[Обзор групп доступности Always On (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
[Предварительные требования, ограничения и рекомендации для групп доступности Always On (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)
