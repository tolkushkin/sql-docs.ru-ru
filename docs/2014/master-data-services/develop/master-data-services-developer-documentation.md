---
title: Разработчик&#39;руководство (Master Data Services) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 067b1f69-84eb-4a13-b220-120cd63704b4
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f87f812ad9f4f12f5f78828e88c220e3dcf494d
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483028"
---
# <a name="developer39s-guide-master-data-services"></a>Разработчик&#39;руководство (Master Data Services)
  Сведения о том, как писать код, для того чтобы настроить взаимодействие пользователей с [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Узнайте, как:  
  
-   Написать программу, которая обращается к веб-службе [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Веб-служба [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] реализована в виде веб-службы Windows Communication Foundation (WCF), с помощью которой разработчики управляют функциями [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] посредством кода.  
  
-   Включить функции веб-службы [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] в существующие приложения.  
  
-   Писать код для выполнения повторяющихся или сложных действий, которые трудно или невозможно совершать с помощью пользовательского интерфейса [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
-   Создавать пользовательский рабочий процесс, который выполняется в ответ на заданное бизнес-правило. Пользовательский рабочий процесс вызывает написанный вами код, который может выполнить любое требуемое действие для обработки рабочего процесса.  
  
## <a name="master-data-manager-web-service"></a>Веб-служба «Диспетчер основных данных»  
 Веб-служба [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] позволяет программно использовать функции [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] с любого компьютера, имеющего доступ к веб-сайту [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Перед написанием кода для доступа к веб-службе необходимо создать классы-посредники, которые содержатся в указанном пространстве имен. В этой документации используется пространство имен посредников <xref:Microsoft.MasterDataServices>. Основным классом-посредником, который используется для выполнения операций веб-службы, является класс <xref:Microsoft.MasterDataServices.ServiceClient>, реализующий интерфейс <xref:Microsoft.MasterDataServices.IService>. Для доступа к веб-службе [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] необходимо из своего кода вызвать методы класса <xref:Microsoft.MasterDataServices.ServiceClient>. Остальные классы из этого пространства имен используются в операциях веб-служб.  
  
### <a name="web-service-content"></a>Содержимое веб-службы  
 [Создание классов-посредников веб-службы диспетчера основных данных](create-master-data-manager-web-service-proxy-classes.md)  
 Описывает процесс включения публикации метаданных с веб-сайта [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , а также создания классов-посредников, которые могут быть использованы для программного доступа к операциям веб-службы.  
  
 [Операции веб-службы по категориям (службы Master Data Services)](categorized-web-service-operations-master-data-services.md)  
 Разбитый на категории перечень операций веб-службы класса <xref:Microsoft.MasterDataServices.ServiceClient>.  
  
## <a name="custom-workflows"></a>Пользовательские рабочие процессы  
 Веб-служба [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] использует бизнес-правила для создания базовых решений рабочих процессов. Можно автоматически обновлять или проверять данные, а также отправлять уведомления по электронной почте на основе заданных условий. Бизнес-правила в [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] предназначены для управления наиболее распространенными сценариями рабочих процессов. Если рабочему процессу требуется более сложная обработка событий, например многоуровневые утверждения или сложные деревья принятия решений, можно настроить [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] на отправку данных созданной вами пользовательской сборке. Для обработки пользовательских рабочих процессов необходимо настроить и запустить службу SQL Server MDS Workflow Integration Service на компьютере с веб-приложением, а также создать сборку, которая реализует интерфейс <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>.  
  
### <a name="custom-workflow-content"></a>Содержимое пользовательского рабочего процесса  
 [Создание настраиваемого рабочего процесса (службы Master Data Services)](create-a-custom-workflow-master-data-services.md)  
 Описание создания сборки обработчика рабочего процесса, настройки и запуска службы SQL Server MDS Workflow Integration Service, а также создания бизнес-правила в веб-приложении [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , которое запускает пользовательский рабочий процесс.  
  
## <a name="web-server-namespaces"></a>Пространства имен веб-сервера  
 Вместе с [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] на компьютер с веб-сервером устанавливается набор сборок. Эти сборки содержат пространства имен, которые можно использовать в расширенных сценариях, где изменяется режим работы веб-сервера. Эти пространства имен описываются в следующей таблице.  
  
|Пространство имен|Описание|  
|---------------|-----------------|  
|<xref:Microsoft.MasterDataServices.Deployment>|Содержит классы, которые можно использовать для создания пакета развертывания из модели и для развертывания пакета в базе данных [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|  
|<xref:Microsoft.MasterDataServices.Services>|Содержит класс, который принимает и обрабатывает операции веб-служб, выполняемые на веб-сервере, посредством приложения [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .|  
|<xref:Microsoft.MasterDataServices.Services.DataContracts>|Содержит классы, которые определяют, каким образом данные передаются с клиентского компьютера через веб-приложение [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] на веб-сервер.|  
|<xref:Microsoft.MasterDataServices.Services.MessageContracts>|Содержит классы, которые определяют, каким образом запросы и ответы передаются с клиентского компьютера через веб-приложение [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] на веб-сервер.|  
|<xref:Microsoft.MasterDataServices.Services.ServiceContracts>|Содержит интерфейс, определяющий операции, которые можно вызывать посредством веб-службы [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .|  
  
  
