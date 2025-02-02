---
title: Режимы кворума WSFC и участвующая в голосовании конфигурация (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: ca0d59ef-25f0-4047-9130-e2282d058283
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7febab9f8ecf6cae4df08f110a16c0bdc512a948
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62711439"
---
# <a name="wsfc-quorum-modes-and-voting-configuration-sql-server"></a>Режимы кворума WSFC и участвующая в голосовании конфигурация (SQL Server)
  И [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], и экземпляры отказоустойчивого кластера (FCI) в режиме AlwaysOn используют платформу отказоустойчивых кластеров Windows Server (WSFC).  В WSFC для мониторинга общей исправности кластера и обеспечения максимальной отказоустойчивости на уровне узлов используется подход, основанный на кворуме. Для проектирования, эксплуатации и устранения неполадок решений высокого уровня доступности режима AlwaysOn и решений аварийного восстановления требуется отличное знание режимов кворума WSFC и конфигурации голосования узлов.  
  
 **В этом разделе:**  
  
-   [Определение исправности кластера по кворуму](#ClusterHealthDetectionbyQuorum)  
  
-   [Режимы кворума](#QuorumModes)  
  
-   [Узлы с правом и без права голоса](#VotingandNonVotingNodes)  
  
-   [Рекомендуемые настройки для голосования с кворумом](#RecommendedAdjustmentstoQuorumVoting)  
  
-   [Связанные задачи](#RelatedTasks)  
  
-   [См. также](#RelatedContent)  
  
##  <a name="ClusterHealthDetectionbyQuorum"></a> Определение исправности кластера по кворуму  
 Все узлы в кластере WSFC участвуют в периодической передаче тактового импульса, сообщающего состояние исправности узла другим узлам. Неотвечающие узлы считаются неисправными.  
  
 Набор узлов *кворума* — это большинство узлов с правом голоса и следящих объектов в кластере WSFC. Общая исправность и состояние кластера WSFC определяется периодическим *голосованием с кворумом*.  Наличие кворума означает, что кластер работоспособен и может обеспечивать отказоустойчивость на уровне узла.  
  
 Отсутствие кворума указывает, что кластер неработоспособен.  Необходимо поддерживать общую исправность кластера WSFC, чтобы обеспечить доступность и работоспособность вторичных узлов, на которые смогут переключаться первичные узлы в случае сбоя.  Если голосование с кворумом завершается неудачей, кластер WSFC переводится в режим «вне сети» в качестве меры предосторожности.  При этом также останавливаются все экземпляры [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , зарегистрированные в кластере.  
  
> [!IMPORTANT]  
>  Если кластер WSFC переводится в режим «вне сети» из-за отсутствия кворума, перевести его обратно в оперативный режим потребуется вручную.  
>   
>  Дополнительные сведения см. в разделе: [Аварийное восстановление WSFC через принудительный кворум (SQL Server)](wsfc-disaster-recovery-through-forced-quorum-sql-server.md).  
  
##  <a name="QuorumModes"></a> Режимы кворума  
 *Режим кворума* настраивается на уровне кластера WSFC, который определяет метод проведения голосования с кворумом.  Диспетчер отказоустойчивого кластера рекомендует режим кворума на основании количества узлов в кластере.  
  
 Для определения кворума голосов можно использовать следующие режимы кворума:  
  
-   **Большинство узлов.** Кластер признается работоспособным, если больше половины узлов подтверждают работоспособность кластера.  
  
-   **Большинство узлов и общих папок.** Аналогичен режиму кворума большинства узлов, за исключением того, что удаленная общая папка также настраивается в качестве следящей папки с правом голоса, и подключения от любого узла к этой папке также считаются голосами, подтверждающими работоспособность.  Кластер признается работоспособным, если больше половины возможных голосов подтверждают работоспособность кластера.  
  
     Рекомендуется, чтобы следящая общая папка не размещалась ни на одном узле в кластере и была видима для всех узлов в кластере.  
  
-   **Большинство узлов и дисков.** Аналогичен режиму кворума большинства узлов, за исключением того, что общий дисковый кластерный ресурс также признается следящим объектом с правом голоса, а все подключения от любого узла к этому общему диску считаются голосами, подтверждающими работоспособность.  Кластер признается работоспособным, если больше половины возможных голосов подтверждают работоспособность кластера.  
  
-   **только диск.** Общий дисковый кластерный ресурс признается следящим, а подключение от любого узла к этому общему диску считается голосом, подтверждающим работоспособность.  
  
> [!TIP]  
>  При использовании асимметричной системы хранения для [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]в общем случае следует использовать режим кворума «Большинство узлов» при нечетном числе узлов с правом голоса и режим кворума «Большинство узлов и общих папок» при четном числе узлов с правом голоса.  
  
##  <a name="VotingandNonVotingNodes"></a> Узлы с правом и без права голоса  
 По умолчанию каждый узел в кластере WSFC включается в качестве члена кворума кластера. Каждый узел имеет один голос, который учитывается при определении общей исправности кластера, и каждый узел постоянно пытается образовать кворум.  На данный момент были четко определены узлы кластера WSFC, принимающие участие в голосовании по исправности кластера, которые называются *узлами с правом голоса*.  
  
 Ни один отдельный узел в кластере WSFC не может окончательно определить, является ли кластер в целом работоспособным.  В любой момент времени с точки зрения любого узла может казаться, что некоторые другие узлы не работают, находятся в процессе отработки отказа или не отвечают из-за сбоя сетевого подключения.  Главная задача голосования с кворумом — определить, является ли видимое состояние каждого узла в кластере WSFC фактическим состоянием этих узлов.  
  
 Для всех режимов кворума, кроме "только диски", эффективность голосования кворума зависит от надежности соединений между всеми узлами с правом голоса в кластере. Сетевые соединения между узлами в одной физической подсети следует считать надежными, и голосование кворума следует считать надежным.  
  
 Однако если в голосовании кворума кажется, что узел или другая подсеть не отвечают, но на самом деле они находятся в рабочем состоянии, то, скорее всего, это происходит из-за сбоя соединения между подсетями.  В зависимости от топологии кластера, режима кворума и конфигурации политики отработки отказа, сбой сетевого соединения может приводить к созданию более одного набора узлов с правом голоса.  
  
 Если свой собственный кворум могут организовать несколько наборов узлов с правом голоса, это называется *сценарием с дроблением*.  В этом случае узлы в отдельных кворумах могут вести себя по-разному и находиться в конфликте друг с другом.  
  
> [!NOTE]  
>  Сценарий с дроблением возможен только в случаях, когда системный администратор вручную организует принудительную работу кворума или в очень редких случаях принудительной отработки отказа при явном разделении набора узлов кворума.  
  
 Чтобы упростить настройку кворума и увеличить время безотказной работы, можно задать параметр *NodeWeight* каждого узла, который указывает, учитывается ли голос этого узла при определении кворума.  
  
> [!IMPORTANT]  
>  Для использования параметров NodeWeight необходимо применить следующее исправление ко всем серверам в кластере WSFC:  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): Доступно исправление, позволяющее настраивать узел кластера, не имеющий голосов кворума в [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] и в [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
##  <a name="RecommendedAdjustmentstoQuorumVoting"></a> Рекомендуемые настройки для голосования с кворумом  
 При включении или отключении голоса конкретного узла WSFC соблюдайте следующие правила.  
  
-   **Отсутствие голосования по умолчанию.** Предполагается, что каждый узел не должен голосовать без явного выравнивания.  
  
-   **Охватите все основные реплики.** Каждый узел WSFC, на котором размещена первичная реплика группы доступности или предпочитаемый владелец FCI, должен иметь голос.  
  
-   **Включайте возможных владельцев автоматического перехода на другой ресурс.** Каждый узел, на котором в результате автоматического перехода группы доступности или экземпляра отказоустойчивого кластера на другой ресурс может размещаться первичная реплика доступности, должен иметь голос. Если имеется только одна группа доступности в кластере WSFC, а реплики доступности размещаются только на автономных экземплярах, то это правило охватывает только вторичную реплику, которая является целью автоматического перехода на другой ресурс.  
  
-   **Исключайте узлы вторичного сайта.** В общем случае не давайте голоса узлам WSFC, которые находятся на вторичном сайте аварийного восстановления.  Не следует, чтобы узлы на вторичном сайте могли принимать участие в решение о переводе кластера в режим «вне сети», когда на первичном сайте нет никаких проблем.  
  
-   **Нечетное число голосов.** Если необходимо, добавьте в кластер следящую общую папку, следящий узел или следящий диск и измените режим кворума, чтобы избежать возможного разделения голосов пополам при голосовании с кворумом.  
  
-   **Перераспределяйте назначение голосов после отработки отказа.** Не следует допускать отработку отказа с переходом на конфигурацию кластера, которая не поддерживает работоспособность кворума.  
  
> [!IMPORTANT]
>  При проверке конфигурации кворума голосования WSFC мастер создания групп доступности в режиме AlwaysOn отображает предупреждение, если выполняется любое из следующих условий.  
> 
>  -   Узел кластера, на котором размещена первичная реплика, не имеет голоса.  
> -   Вторичная реплика настроена для автоматического перехода на другой ресурс, а ее узел кластера не имеет голоса.  
> -   [KB2494036](https://support.microsoft.com/kb/2494036) не установлено на всех узлах кластера, на которых размещены реплики доступности. Это обновление необходимо для добавления или удаления голосов для узлов кластера в многосайтовых развертываниях. Однако в односайтовых развертываниях это обычно не требуется, поэтому можно безопасно пропустить предупреждение.  
> 
> [!TIP]
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] предлагает несколько системных динамических административных представлений, которые могут помочь в управлении параметрами конфигурации кластера WSFC и голосовании с кворумом узлов.  
> 
>  Дополнительные сведения можно найти в разделах:  [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql), [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql), [sys.dm_os_cluster_nodes](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql), [sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Просмотр параметров NodeWeight кворума кластера](view-cluster-quorum-nodeweight-settings.md)  
  
-   [Настройка параметров NodeWeight для кворума кластера](configure-cluster-quorum-nodeweight-settings.md)  
  
##  <a name="RelatedContent"></a> См. также  
  
-   [Microsoft SQL Server AlwaysOn Solutions Guide for высокий уровень доступности и аварийного восстановления](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Проверка конфигурации голосов кворума в мастерах групп доступности AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/archive/2012/03/13/quorum-vote-configuration-check-in-alwayson-availability-group-wizards-andy-jing.aspx)  
  
-   [Технологии Windows Server.  Отказоустойчивые кластеры](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [Пошаговое руководство по отказоустойчивым кластерам. Настройка кворума в отказоустойчивом кластере](https://technet.microsoft.com/library/cc770620\(WS.10\).aspx)  
  
## <a name="see-also"></a>См. также  
 [Аварийное восстановление WSFC через принудительный кворум (SQL Server)](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)   
 [Отказоустойчивая кластеризация Windows Server (WSFC) с SQL Server](windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
