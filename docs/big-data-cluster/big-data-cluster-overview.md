---
title: Что такое кластеры больших данных?
titleSuffix: SQL Server big data clusters
description: Дополнительные сведения о кластерах SQL Server 2019 больших данных (Предварительная версия), которые работают на платформе Kubernetes и обеспечивают масштабирование для реляционных и данные из HDFS.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/07/2018
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: fed82f9bda8f72d92157de726eb6ae3c6ed1c0c0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801891"
---
# <a name="what-are-sql-server-big-data-clusters"></a>Что такое кластеры больших данных SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Начиная с [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], кластеры SQL Server больших данных позволяют развертывать масштабируемые кластеры SQL Server, Spark и HDFS контейнеров, работающих на платформе Kubernetes. Эти компоненты работают рядом друг с другом, чтобы можно было чтение, запись и обработки больших данных из Transact-SQL или Spark, позволяя легко объединить и анализа реляционных данных высокой ценности с большими данными большого объема.

Дополнительные сведения о новых функциях и известных проблем для последнего выпуска см. в разделе [заметки о выпуске](release-notes-big-data-cluster.md).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>Сценарии

Кластерами больших данных SQL Server обеспечивают гибкость во взаимодействии с большими данными. Можно запрашивать внешние источники данных, хранение больших данных в HDFS, под управлением SQL Server, или запросы к данным из нескольких внешних источников данных через кластер. Затем можно использовать данные для искусственного Интеллекта, машинного обучения и другие задачи анализа. Дополнительные сведения об этих сценариях в следующих разделах.

### <a name="data-virtualization"></a>Виртуализация данных

За счет использования [SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md), больших данных кластеров SQL Server можно запросить внешних источников данных без перемещения или копирования данных. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] вводит новые соединители с источниками данных.

![Виртуализация данных](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Озера данных

Большие данные кластера SQL Server включает в себя масштабируемые HDFS *пула носителей*. Это можно использовать для хранения больших данных, потенциально поступают из нескольких внешних источников. После того как больших данных сохраняется в файловой системе HDFS в кластере большие данные, можно анализировать и запрашивать данные и использовать ее в сочетании с реляционными данными.

![Озера данных](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Киоск данных горизонтального масштабирования

Кластеры больших данных SQL Server предоставляют горизонтального масштабирования вычислений и хранения для повышения производительности, анализ всех данных. Данные из различных источников могут приниматься и распределяются по *пула данных* узлы как кэш для дальнейшего анализа.

![Киоск данных](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>Встроенная искусственного Интеллекта и машинного обучения

Кластерами больших данных SQL Server включите искусственного Интеллекта и машинного обучения задач на данные, хранящиеся в HDFS пулы носителей и пулы данных. Можно использовать Spark, а также встроенные средства искусственного Интеллекта в SQL Server, с помощью R, Python, Scala и Java.

![ИИ и машинного Обучения](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Управление и мониторинг

Управление и мониторинг предоставляются через сочетание средств командной строки, интерфейсы API, на портал администратора и динамические административные представления.

[Портал администратора кластера](cluster-admin-portal.md) — веб-интерфейс, который отображает состояние и работоспособность модулей POD в кластере. Он также предоставляет ссылки на другие панели мониторинга для log analytics и панели мониторинга.

Azure Data Studio можно использовать для выполнения различных задач в кластере больших данных. Эта функция включена по новому **расширение 2019 г. (Предварительная версия) для SQL Server**. Это расширение предоставляет:

- Встроенные фрагменты кода для общих задач управления.
- Возможность просмотра HDFS, передача файлов, предварительный просмотр файлов и создания каталогов.
- Возможность создания, открыть и запустить записные книжки Jupyter совместимой.
- Мастер виртуализации данных позволяет упростить создание внешних источников данных.

## <a id="architecture"></a> Архитектура

Кластер SQL Server больших данных — это кластер контейнеров Linux, оркестрация с [Kubernetes](https://kubernetes.io/docs/concepts/).

### <a name="kubernetes-concepts"></a>Основные понятия Kubernetes

Kubernetes — это оркестратор контейнеров открытым исходным кодом, которую можно масштабировать развертывание контейнеров в соответствии с потребностями. В следующей таблице приведены некоторые важные термины Kubernetes:

|||
|:--|:--|
| **Cluster** | Кластер Kubernetes — это набор компьютеров, называемых узлами. Один из узлов контролирует кластера и назначенный главный узел; остальные узлы являются рабочими. Главный Kubernetes отвечает для распределения работы между рабочие роли, а также для наблюдения за работоспособностью кластера. |
| **Node** | Узел выполняет контейнерных приложений. Он может быть физический компьютер или виртуальную машину. Кластер Kubernetes может содержать смесь физические узлы компьютера и виртуальной машины. |
| **POD** | Группа контейнеров pod является единицей atomic развертывания Kubernetes. Группа контейнеров pod представляет собой логическую группу, один или несколько контейнеров — и связанные ресурсы необходимые для запуска приложения. Каждый модуль выполняется на узле; узел можно запустить один или несколько модулей POD. Главный Kubernetes автоматически назначает модулей узлов в кластере. |
| &nbsp; ||

В кластерах больших данных в SQL Server Kubernetes отвечает за состояние кластеров больших данных SQL Server; Kubernetes сборок и настроит узлы кластера, назначает узлам модулей и отслеживает работоспособность кластера.

### <a name="big-data-clusters-architecture"></a>Архитектура кластерами больших данных

Узлы в кластере будут расположены в трех логических плоскостей: плоскости управления, плоскость вычислений и плоскости данных. Каждой плоскости имеет разные обязанности в кластере. Каждый узел Kubernetes в кластере SQL Server больших данных заключается в размещении модулей POD для компонентов, по крайней мере одной плоскости.

![Обзор архитектуры](media/big-data-cluster-overview/architecture-diagram-planes.png)

### <a id="controlplane"></a> Плоскость управления

Плоскость управления обеспечивает управление и безопасность для кластера. Он содержит хозяину Kubernetes *главного экземпляра SQL Server*и другие службы кластера уровня, такие как хранилище метаданных Hive и драйвера Spark.

### <a id="computeplane"></a> Вычисления плоскости

Плоскость вычислений предоставляет вычислительные ресурсы в кластер. В нем узлов экземпляров SQL Server на Linux модулей. Можно разделить на POD, содержащихся в плоскости вычислений *вычислительные пулы* для конкретных задач обработки. Пул вычислительных может выступать в качестве [PolyBase](../relational-databases/polybase/polybase-guide.md) группы горизонтального масштабирования для распределенных запросов через разные данные в источники, такие как HDFS, Oracle, MongoDB или Teradata.

### <a id="dataplane"></a> Плоскость данных

Плоскости данных используется для постоянного хранения и кэширования. Он содержит пул данных SQL и пул носителей.  Пул данных SQL содержит один или несколько модулей SQL Server на платформе Linux. Он используется для приема данных из SQL-запросы или заданий Spark. Большие данные SQL Server кластер киосков сохраняются в пуле данных. Пул носителей состоит из модулей пула хранения, состоящая из SQL Server в Linux, Spark и HDFS. Все узлы хранилища в кластере SQL Server больших данных являются членами кластера HDFS.

> [!TIP]
> Дополнительные сведения об архитектуре кластера больших данных и установки, см. в разделе [семинар: Архитектура кластерами больших данных Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters).

## <a name="next-steps"></a>Следующие шаги

Во-первых, больших данных кластеров SQL Server доступен в виде ограниченной общедоступной предварительной версии до SQL Server 2019 программе раннего освоения. Чтобы запросить доступ, зарегистрируйте [здесь](https://aka.ms/eapsignup)и укажите ваш интерес к попробуйте кластеры больших данных. Майкрософт будет рассматривать все запросы и отвечать как можно скорее.
