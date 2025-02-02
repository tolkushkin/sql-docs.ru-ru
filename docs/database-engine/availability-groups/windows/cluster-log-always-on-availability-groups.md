---
title: Создание и анализ журнала CLUSTER.LOG для группы доступности
description: 'Описывается создание и анализ журнала кластера для группы доступности Always On. '
ms.custom: ag-guide, seodec18
ms.date: 06/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a9e3c1-2a5f-4b98-a424-0ffc15d312cf
author: rothja
ms.author: jroth
manager: jroth
ms.openlocfilehash: 1d025a77cace9d8bbcdd746c2e6a193f23efd34d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66772592"
---
# <a name="generate-and-analyze-the-clusterlog-for-an-always-on-availability-group"></a>Создание и анализ журнала CLUSTER.LOG для группы доступности Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В качестве ресурса отказоустойчивого кластера существуют внешние взаимодействия между SQL Server, службой отказоустойчивого кластера Windows Server (WSFC) и библиотекой SQL Server (hadrres.dll), которые невозможно отслеживать внутри SQL Server. Журнал WSFC — CLUSTER.LOG — позволяет диагностировать проблемы в кластере WSFC или в библиотеке ресурсов SQL Server.  
  
 На приведенной ниже схеме показана связь между приложениями, такими как SQL Server и диспетчер кластеров Windows, инициирующими создание, удаление ресурса группы доступности или изменение его состояния.  
  
## <a name="generate-cluster-log"></a>Создание журнала кластера  
 Вы можете создать журнал кластера одним из двух способов:  
  
1.  Используйте команду `cluster /log /g` в командной строке. Эта команда создает журналы кластера в каталоге \windows\cluster\reports на каждом узле WSFC. Преимуществом этого метода является то, что с помощью параметра `/level` можно указать уровень детализации создаваемых журналов. Недостатком является то, что невозможно задать целевой каталог для создаваемых журналов кластера. Дополнительные сведения см. в статье [Создание cluster.log в рамках отказоустойчивой кластеризации Windows Server 2008](https://blogs.msdn.com/b/clustering/archive/2008/09/24/8962934.aspx).  
  
2.  Используйте командлет [Get-ClusterLog](https://technet.microsoft.com/library/ee461045.aspx) PowerShell. Преимущество этого метода заключается в том, что можно создать журнал кластера со всех узлов в один конечный каталог на узле, где выполняется командлет. Недостатком является то, что невозможно указать уровень детализации создаваемых журналов.  
  
 Приведенные ниже команды PowerShell создают журналы кластера со всех узлов кластера за последние 15 минут и помещают их в текущий каталог. Эти команду нужно выполнять в окне PowerShell с правами администратора.  
  
```powershell  
Import-Module FailoverClusters   
Get-ClusterLog -TimeSpan 15 -Destination .  
```  
  
## <a name="always-on-log-verbosity"></a>Детализация журнала AlwaysOn  
 Вы можете повысить уровень детализации журналов в CLUSTER.LOG для группы доступности. Чтобы изменить уровень детализации, сделайте следующее:  
  
1.  В меню **Пуск** откройте **Диспетчер отказоустойчивости кластеров**.  
  
2.  Разверните кластер и узел **Службы и приложения**, а затем щелкните имя группы доступности.  
  
3.  В области сведений щелкните правой кнопкой мыши ресурс группы доступности и выберите пункт **Свойства**.  
  
4.  Перейдите на вкладку **Свойства** .  
  
5.  Измените свойство **VerboseLogging**. По умолчанию **VerboseLogging** равно `0`, то есть выводятся информационные сообщения, предупреждения и ошибки. **VerboseLogging** может принимать значения от `0` до `2`.  
  
6.  Нажмите кнопку **ОК**.  
  
7.  Еще раз щелкните правой кнопкой мыши ресурс группы доступности и выберите **Take this resource offline** (Перевести этот ресурс в автономный режим).  
  
8.  Еще раз щелкните правой кнопкой мыши ресурс группы доступности и выберите **Bring this resource online** (Перевести этот ресурс в режим "в сети").  
  
## <a name="availability-group-resource-events"></a>События для ресурса группы доступности  
 В приведенной ниже таблице перечислены различные виды событий в CLUSTER.LOG, относящиеся к ресурсу группы доступности. Дополнительные сведения о подсистеме размещения ресурсов (RHS) и мониторе управления ресурсами (RCM) в кластере WSFC см. в разделе [Подсистема размещения ресурсов (RHS) в отказоустойчивых кластерах Windows Server 2008](https://blogs.technet.com/b/askcore/archive/2009/11/23/resource-hosting-subsystem-rhs-in-windows-server-2008-failover-clusters.aspx).  
  
|Идентификатор|Source|Пример из CLUSTER.LOG|  
|----------------|------------|------------------------------|  
|Сообщения с префиксом `[RES]` и `[hadrag]`|hadrres.dll (библиотека ресурсов AlwaysOn)|00002cc4.00001264::2011/08/05-13:47:42.543 INFO  [RES] SQL Server Availability Group \<ag>: `[hadrag]` Offline request.<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.558 ERR   [RES] SQL Server Availability Group \<ag>: `[hadrag]` Lease Thread terminated<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.605 INFO  [RES] SQL Server Availability Group \<ag>: `[hadrag]` Free SQL statement<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.902 INFO  [RES] SQL Server Availability Group \<ag>: `[hadrag]` Disconnect from SQL Server|  
|Сообщения с префиксом `[RHS]`|RHS.EXE (подсистема размещения ресурсов, хост-процесс библиотеки hadrres.dll)|00000c40.00000a34::2011/08/10-18:42:29.498 INFO  [RHS] Resource ag has come offline. RHS is about to report resource status to RCM.|  
|Сообщения с префиксом `[RCM]`|Монитор управления ресурсами (служба кластеров)|000011d0.00000f80::2011/08/05-13:47:42.480 INFO  [RCM] rcm::RcmGroup::Move: Bringing group 'ag' offline first...<br /><br /> 000011d0.00000f80::2011/08/05-13:47:42.496 INFO  [RCM] TransitionToState(ag) Online-->OfflineCallIssued.|  
|RcmApi/ClusAPI|Вызов API, который обычно означает, что SQL Server запрашивает действие|000011d0.00000f80::2011/08/05-13:47:42.465 INFO  [RCM] rcm::RcmApi::MoveGroup: (ag, 2)|  
  
## <a name="debug-always-on-resource-dll-in-isolation"></a>Отладка библиотеки ресурсов AlwaysOn в изоляции  
 Это рекомендации по отладке, позволяющие настроить кластер для выполнения библиотеки ресурсов AlwaysOn (hadrres.dll) в изоляции от других библиотек ресурсов. По умолчанию кластер WSFC выполняет все библиотеки ресурсов в одном экземпляре rhs.exe. При этом все ресурсы в кластере совместно используют один экземпляр rhs.exe. При попытке отладки hadrres.dll с помощью отладчика приостановка в точке останова может привести к тому, что другие ресурсы, совместно использующие экземпляр rhs.exe, также будут приостановлены. Кроме того, при запуске нескольких групп доступности в одном кластере аналогичная конфигурация может привести к приостановке всех групп доступности, когда вы останавливаетесь в точек останова для отладки одной группы доступности.  
  
 Чтобы изолировать группу доступности от других библиотек ресурсов кластера, включая другие группы доступности, сделайте следующее для запуска hadrres.dll внутри отдельного процесса rhs.exe:  
  
1.  Откройте **редактор реестра** и перейдите к следующему разделу: HKEY_LOCAL_MACHINE\Cluster\Resources. Этот раздел содержит ключи для всех ресурсов, каждый из которых имеет собственный GUID.  
  
2.  Найдите ключ ресурса, содержащий значение **Name**, совпадающее с именем группы доступности.  
  
3.  Измените значение **SeparateMonitor** на **1**.  
  
4.  Перезапустите кластерную службу для своей группы доступности в кластере WSFC.  
  
  
