---
title: Диспетчер подключений подписки Azure | Документы Майкрософт
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpsubscrconn.f1
- sql14.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b3dec7a683bcebc28f9bfe90e4b4091a70892f8
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728344"
---
# <a name="azure-subscription-connection-manager"></a>Диспетчер подключений подписки Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Диспетчер подключений подписки Azure** позволяет пакету служб SSIS подключаться к подписке Azure с помощью указываемых вами значений свойств: идентификатора подписки Azure и сертификата управления.  
  
 **Диспетчер подключений подписки Azure** входит в состав [пакета дополнительных компонентов SQL Server Integration Services (SSIS) для Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
1.  В диалоговом окне **Добавление диспетчера соединений со службами SSIS** выберите **Подписка Azure**и щелкните **Добавить**.  Отобразится следующее диалоговое окно **Azure Subscription Connection Manager Editor** (Редактор диспетчера подключений подписки Azure).  
  
    ![SSIS-AzureSubscriptionConnectionManager](../../integration-services/connection-manager/media/ssis-azuresubscriptionconnectionmanager.png)
  
2.  Введите уникальный идентификатор подписки Azure, который идентифицирует подписку Azure, в поле **Идентификатор подписки Azure**.  Значение можно найти на [портале управления Azure](https://manage.windowsazure.com) на странице **Параметры** .  
  
    ![SSIS-AzureSettings-SubscriptionID](../../integration-services/connection-manager/media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")  
  
3.  В раскрывающихся списках выберите значения **Расположение хранилища сертификатов управления** и **Имя хранилища сертификатов управления** .  
  
4.  Введите значение **Отпечаток сертификата управления** или щелкните **Обзор…** и выберите сертификат из выбранного хранилища. Сертификат должен быть передан как сертификат управления для подписки. Чтобы сделать это, нажмите кнопку **Отправить** на следующей странице портала Azure (см. эту [запись MSDN](https://msdn.microsoft.com/library/azure/gg551722.aspx) для получения дополнительных сведений).  
  
     ![SSIS-AzureSettings-ManagementCertificate](../../integration-services/connection-manager/media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")  
  
5.  Нажмите кнопку **Проверить подключение** для проверки подключения.  
  
6.  Чтобы закрыть диалоговое окно, нажмите кнопку **ОК** .  
  
  
