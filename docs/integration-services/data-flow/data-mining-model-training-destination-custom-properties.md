---
title: Пользовательские свойства назначения "Обучение модели интеллектуального анализа данных" | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f0a70216-fdac-44ae-af29-35f65626217c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1dfad3ec6e575529026aa7aa93468be97cd7955e
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727023"
---
# <a name="data-mining-model-training-destination-custom-properties"></a>Пользовательские свойства назначения «Обучение модели интеллектуального анализа данных»

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Назначение «Обучение модели интеллектуального анализа данных» обладает как пользовательскими свойствами, так и свойствами, общими для всех компонентов потока данных.  
  
 В следующей таблице описаны пользовательские свойства назначения «Обучение модели интеллектуального анализа данных». Все свойства доступны для чтения и записи.  
  
|Свойство|Тип данных|Описание|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|Уникальный идентификатор диспетчера соединений.|  
|ASConnectionString|String|Строка соединения с экземпляром служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] или с проектом служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|ObjectRef|String|XML-тег, определяющий структуру интеллектуального анализа данных, которую использует преобразование.|  
  
 Ввод и входные столбцы назначения «Обучение модели интеллектуального анализа данных» не обладают пользовательскими свойствами.  
  
 Дополнительные сведения см. в разделе [Data Mining Model Training Destination](../../integration-services/data-flow/data-mining-model-training-destination.md).  
  
## <a name="see-also"></a>См. также:  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
