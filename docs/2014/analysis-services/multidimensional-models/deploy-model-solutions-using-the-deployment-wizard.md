---
title: Развертывание решений модели с помощью мастера развертывания | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e18b1786201be9ba671bc08fe7b24ba2207469e9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075380"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Развертывание решений модели с использованием мастера развертывания
  Мастер развертывания служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] использует выходные XML-файлы, создаваемые в проекте служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , в качестве входных. Эти входные файлы можно легко изменить для настройки развертывания проекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Сформированный скрипт развертывания можно затем либо сразу запустить, либо сохранить и запустить позднее.  
  
 Развертывание можно выполнить при помощи мастера. Также можно автоматизировать развертывание или использовать функцию синхронизации. При больших размерах развернутой базы данных на целевых системах рекомендуется использовать секции. Также создание и заполнение секций можно автоматизировать при помощи объектов AMO.  
  
> [!IMPORTANT]  
>  Ни выходные XML-файлы, ни скрипт развертывания не будут содержать идентификаторов пользователя или паролей, если они вводились в строке соединения для источника данных или для олицетворения. Поскольку в данном сценарии они необходимы для обработки, добавьте их вручную. Если в ходе развертывания не выполнится обработка, то эти сведения для соединения и олицетворения при необходимости можно добавить после развертывания. Если в ходе развертывания выполнится обработка, то можно добавить эти сведения с помощью мастера или добавить их в скрипт развертывания после его сохранения.  
  
## <a name="in-this-section"></a>в этом разделе  
 В следующих подразделах рассматривается работа с мастером развертывания служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , входными файлами и скриптом развертывания:  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Запуск мастера развертывания служб Analysis Services](running-the-analysis-services-deployment-wizard.md)|Содержит описание различных способов запуска мастера развертывания служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Основные сведения о входных файлах, применяемых для создания скрипта развертывания](deployment-script-files-input-used-to-create-deployment-script.md)|Содержит описание файлов, используемых мастером развертывания служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] в качестве входных значений, содержимого каждого из таких файлов, а также содержит ссылки на подразделы, в которых описывается, как изменять значения в каждом из входных файлов.|  
|[Основные сведения о скрипте развертывания служб Analysis Services](understanding-the-analysis-services-deployment-script.md)|Содержит описание скрипта развертывания и его выполнения.|  
  
## <a name="see-also"></a>См. также  
 [Развертывание решений модели с помощью XMLA](deploy-model-solutions-using-xmla.md)   
 [Синхронизация баз данных служб Analysis Services](synchronize-analysis-services-databases.md)   
 [Основные сведения о входных файлах, применяемых для создания скрипта развертывания](deployment-script-files-input-used-to-create-deployment-script.md)   
 [Развертывание решений моделей с использованием программы развертывания](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
