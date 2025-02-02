---
title: Страница "Выбор начальной синхронизации данных" (мастер группы доступности AlwaysOn) | Документы Майкрософт
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.adddatabasewizard.selectinitialdatasync.f1
- sql13.swb.newagwizard.selectinitialdatasync.f1
- sql13.swb.addreplicawizard.selectinitialdatasync.f1
ms.assetid: 457b1140-4819-4def-8f7c-54a406e6db12
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: dbfa8c5acd998fed28546baf8b16af09d3abae07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66787706"
---
# <a name="select-initial-data-synchronization-page-always-on-availability-group-wizards"></a>Выбор страницы начальной синхронизации данных (мастера группы доступности AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Используйте страницу AlwaysOn **Выбор начальной синхронизации данных** , чтобы указать требуемые параметры начальной синхронизации данных в новых базах данных-получателях. Эта страница используется тремя мастерами — [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)], [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] и [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)].  
  
 Возможные варианты: **Автоматическое заполнение**, **Полная архивация базы данных и журналов**, **Только присоединение** или **Пропустить начальную синхронизацию данных**. Прежде чем выбрать значение **Автоматическое заполнение**, **Полная** или **Только присоединение**, удостоверьтесь в том, что среда соответствует обязательным условиям.  
    
##  <a name="Recommendations"></a> Рекомендации  
  
-   Во время синхронизации начальных данных следует приостановить задачи баз данных-источников по резервному копированию журналов.  
  
-   На выполнение операций полного резервного копирования и восстановления больших баз данных может требоваться значительное время и ресурсы. В таких случаях рекомендуется готовить базы данных-получатели самостоятельно. Дополнительные сведения см. далее в этом разделе [Подготовка баз данных-получателей вручную](#PrepareSecondaryDbs).  
  
-   Для проведения полной начальной синхронизации данных требуется указать общую сетевую папку. Перед использованием мастера для выполнения полной начальной синхронизации данных рекомендуется реализовать план обеспечения безопасности для разрешений на доступ к общей сетевой папке. Эта мера предосторожности важна, поскольку доступ к потенциально конфиденциальным данным из файла резервной копии может получить любой пользователь с разрешением READ на эту папку. Кроме того, для обеспечения безопасности операций резервного копирования и восстановления рекомендуется защитить сетевые каналы между всеми экземплярами сервера, на которых размещены реплики доступности, и общей сетевой папкой.  
  
     Если требуется обеспечить высокий уровень безопасности операций резервного копирования и восстановления, рекомендуется выбрать параметр **Только присоединение** или **Пропустить начальную синхронизацию данных** .  
  
## <a name="Auto"></a> Автоматическое заполнение
 
 SQL Server автоматически создает вторичные реплики для каждой базы данных в группе. Для работы автоматического заполнения путь к файлу данных и файлу журнала должен быть одинаковым на каждом экземпляре SQL Server, входящем в группу. Доступно в [!INCLUDE[sssql15-md.md](../../../includes/sssql15-md.md)] и более поздних версиях. См. раздел [Автоматическая инициализация группы доступности AlwaysOn](automatically-initialize-always-on-availability-group.md).

##  <a name="Full"></a> Полная архивация базы данных и журналов 
 При выборе параметра **Полная архивация базы данных и журналов** в отношении каждой базы данных-источника в одном рабочем процессе будет выполнено несколько операций: создание полной резервной копии базы данных-источника и резервной копии ее журнала, создание соответствующих баз данных-получателей путем восстановления этих резервных копий на каждом экземпляре сервера, где размещается вторичная реплика, а также присоединение каждой базы данных-получателя к группе доступности.  
  
 Этот параметр следует выбирать, если среда соответствует обязательным условиям использования полной начальной синхронизации данных, и требуется, чтобы мастер запустил синхронизацию данных автоматически.  
  
 **Предварительные условия для использования начальной синхронизации данных для полной архивации базы данных и журналов**  
  
-   Все пути к файлам базы данных должны быть одинаковыми на всех экземплярах сервера, на которых размещены реплики группы доступности.  
  
    > [!NOTE]  
    >  Если на экземпляре сервера, на котором запускается мастер, пути файлов для резервного копирования и восстановления отличаются от путей на любом экземпляре сервера, где размещается вторичная реплика. Операции резервного копирования и восстановления должны выполняться вручную с помощью параметра WITH MOVE. Дополнительные сведения см. далее в этом разделе [Подготовка баз данных-получателей вручную](#PrepareSecondaryDbs).  
  
-   На экземпляре сервера, содержащем вторичную реплику, не может существовать имя базы данных-источника. Это означает, что еще не может существовать ни одна из новых баз данных-получателей.  
  
-   Чтобы при помощи мастера можно было создавать резервные копии и обращаться к ним, необходимо будет указать общую сетевую папку. Для каждой первичной реплики учетная запись, используемая для запуска [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , должна иметь разрешения в файловой системе на чтение и запись в общей сетевой папке. Для вторичных реплик учетная запись должна иметь разрешение на чтение в сетевой папке.  
  
    > [!IMPORTANT]  
    >  Резервные копии журналов будут входить в цепочку резервных копий журналов. Храните файлы резервных копий журналов надлежащим образом.  
  
 **Если условия не выполняются**  
  
 Мастер не может создать базы данных-получатели для этой группы доступности. Дополнительные сведения о их подготовке см. далее в этом разделе [Подготовка баз данных-получателей вручную](#PrepareSecondaryDbs)  
  
 **Если условия соблюдены**  
  
 Если все эти условия выполнены и нужно, чтобы мастер выполнил полную начальную синхронизацию данных, выберите параметр **Полная архивация базы данных и журналов** и укажите сетевую папку. В этом случае мастер создаст полные резервные копии журнала и базы данных для каждой выбранной базы данных и поместит их в указанную сетевую папку. Затем на каждом экземпляре сервера, на котором расположена одна из новых вторичных реплик, мастер создаст базы данных-получатели путем восстановления резервных копий с помощью инструкции RESTORE WITH NORECOVERY. После создания всех баз данных-получателей мастер присоединит их к группе доступности. Сразу после присоединения базы данных-получателя в ней запускается синхронизация данных.  
  
 **Указание общей сетевой папки, доступ к которой имеют все реплики**  
 Для создания и восстановления резервных копий мастеру необходимо указать общую сетевую папку. Учетная запись, используемая для запуска компонента [!INCLUDE[ssDE](../../../includes/ssde-md.md)] на каждом экземпляре сервера, на котором будет размещаться реплика доступности, должна иметь разрешения на чтение и запись в файловой системе на эту сетевую папку.  
  
> [!IMPORTANT]  
>  Резервные копии журналов будут входить в цепочку резервных копий журналов. Храните файлы их резервных копий надлежащим образом.  
  
##  <a name="Joinonly"></a> Только присоединение  
 Этот параметр следует выбирать только при наличии новых баз данных-получателей на каждом экземпляре сервера, размещающем вторичную реплику для группы доступности. Дополнительные сведения о подготовке баз данных-получателей см. в подразделе [Подготовка баз данных-получателей вручную](#PrepareSecondaryDbs)далее в этом разделе.  
  
 Если выбрать параметр **Только присоединение**, мастер попытается присоединить все существующие базы данных-получатели к группе доступности.  
  
## <a name="Skip"></a> Пропустить начальную синхронизацию данных  
 Выберите этот параметр, если хотите самостоятельно выполнить резервное копирование базы данных и журнала каждой базы данных-источника и восстановить их на каждый экземпляр сервера, на котором размещена вторичная реплика. После завершения работы мастера необходимо будет присоединить каждую базу данных-получатель на каждой вторичной реплике.  
  
> [!NOTE]  
>  Дополнительные сведения см. далее в этом разделе [Запуск перемещения данных для базы данных-получателя AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="PrepareSecondaryDbs"></a> Подготовка базы данных-получателя (вручную)  
 Для подготовки баз данных-получателей без помощи мастера [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] можно использовать любой из следующих подходов.  
  
-   Вручную восстановить последнюю резервную копию базы данных-источника с помощью инструкции RESTORE WITH NORECOVERY, а затем восстановить все последовательные резервные копии журнала с помощью инструкции RESTORE WITH NORECOVERY. Если базы данных-получатель и база данных-источник имеют различные пути к файлам, необходимо использовать параметр WITH MOVE. Выполните эту последовательность восстановления на каждом экземпляре сервера, на котором расположена вторичная реплика этой группы доступности.  Для выполнения этих операций резервного копирования и восстановления можно использовать [!INCLUDE[tsql](../../../includes/tsql-md.md)] или Powershell.  
  
     **Дополнительные сведения см. в следующих разделах:**  
  
     [Подготовка базы данных-получателя для присоединения к группе доступности вручную (SQL Server)](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   При добавлении одной или нескольких баз данных-источников к группе доступности можно будет перевести одну или несколько соответствующих баз данных-получателей из доставки журналов в [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Дополнительные сведения см. далее в этом разделе [Необходимые условия для перехода от использования доставки журналов к использованию групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md).  
  
    > [!NOTE]  
    >  После создания всех баз данных-получателей для группы доступности, при необходимости проведения резервного копирования на вторичных репликах, нужно изменить параметры автоматического резервного копирования для группы доступности.  
  
     **Дополнительные сведения см. в следующих разделах:**  
  
     [Необходимые условия для выполнения перехода от использования доставки журналов к использованию групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
     [Настройка резервного копирования в репликах доступности (SQL Server)](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 После создания базы данных-получателя примените к ней все текущие резервные копии журнала.  
  
 Кроме того, можно лично подготовить все базы данных-получатели до запуска мастера. Затем на странице **Выбор начальной синхронизации данных** выберите параметр **Только присоединение** , в результате чего мастер попытается автоматически присоединить новые базы данных-получатели к группе доступности.  
  
##  <a name="LaunchWiz"></a> Связанные задачи  
  
-   [Использование диалогового окна "Создание группы доступности" (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Использование мастера добавления реплики в группу доступности (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Использование мастера добавления базы данных в группу доступности (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [Использование мастера отработки отказа группы доступности (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Запуск перемещения данных для базы данных-получателя AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [Присоединение базы данных-получателя к группе доступности (SQL Server)](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Использование диалогового окна "Создание группы доступности" (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
