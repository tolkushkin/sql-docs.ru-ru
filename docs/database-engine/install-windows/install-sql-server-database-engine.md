---
title: Установка ядра СУБД SQL Server | Документы Майкрософт
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 163b725e61abc4795b1b4bc28ef202766b8ea900
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794905"
---
# <a name="install-sql-server-database-engine"></a>Установка ядра СУБД SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="overview"></a>Обзор
Компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] входит в состав [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и является основной службой, предназначенной для хранения, обработки и обеспечения безопасности данных. Компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] обеспечивает управляемый доступ к ресурсам и быструю обработку транзакций, что позволяет использовать его даже с самыми требовательными приложениями по обработке данных на предприятии.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает до 50 экземпляров компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] на одном компьютере. Инструкции по созданию типовой установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] см. в статье [Установка SQL Server с помощью мастера установки (программа установки)](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
>[!IMPORTANT]
>Для локальных установок необходимо запускать программу установки с правами администратора. При установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из удаленной общей папки необходимо использовать учетную запись домена с разрешениями на чтение и выполнение для удаленной общей папки.  

## <a name="features"></a>Компоненты
Если на странице «Компоненты для установки» мастера установки **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выбран компонент** Database Engine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , то будут установлены следующие компоненты:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [Репликация SQL Server](../../relational-databases/replication/sql-server-replication.md) ― это необязательный компонент  

-   [Службы машинного обучения (в базе данных) с использованием R и Python](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md) — это необязательный компонент

-   Full-Text Search ― это необязательный компонент  
  
-   Службы Data Quality Services являются необязательным компонентом.  
  
    > [!NOTE]  
    >  В этом выпуске установка флажка **Службы Data Quality Services** в программе установки не приводит к установке сервера служб Data Quality Services (DQS). Для установки сервера DQS необходимо выполнить дополнительные шаги после завершения установки. Дополнительные сведения см. в разделе [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
    
- [Служба запросов Polybase для внешних данных](../../relational-databases/polybase/polybase-guide.md) — это необязательный компонент. Начиная с SQL Server 2019 также доступен соединитель Java для источников данных HDFS.

  
 Следующие дополнительные возможности могут применяться во многих типичных пользовательских сценариях.  
  
-   Клиент Data Quality
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]
-   Компоненты соединения
-   Модели программирования
-   Средства управления
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]
-   Компоненты документации  
  

> [!NOTE]  
>  По умолчанию при установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] образцы баз данных и образцы кода не устанавливаются. Дополнительные сведения об установке примеров баз данных и примеров кода см. в разделе [Образцы Microsoft SQL Server](../../sample/microsoft-sql-server-samples.md). Более старые примеры см. на [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  

  
## <a name="see-also"></a>См. также раздел  
 [Выпуски и поддерживаемые функции SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [Планирование установки SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Решения высокого уровня доступности (SQL Server)](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Обновление SQL Server с помощью мастера установки (программа установки)](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
