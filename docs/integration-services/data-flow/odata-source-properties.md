---
title: Свойства источника OData | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6a7bc11692944f5da349760e3b1e12f473fb15b3
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726680"
---
# <a name="odata-source-properties"></a>Свойства источника OData

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Если щелкнуть правой кнопкой **Источник OData** в потоке данных и выбрать **Свойства**, то свойства компонента **Источник OData** отображаются в окне **Свойства**.  

## <a name="properties"></a>Свойства 

|Свойство|Описание|  
|-|-|  
|CollectionName|Имя коллекции, которую нужно получить из службы OData. Свойство **CollectionName** используется в том случае, когда значение **UseResourcePath** равно False.<br /><br /> Это свойство поддерживает выражения, что позволяет задать значение во время выполнения. Но если метаданные коллекции не соответствуют метаданным, которые использовались во время разработки, то происходит ошибка проверки, из-за чего выполнение потока данных приводит к ошибке.|  
|DefaultStringLength|Это значение указывает длину по умолчанию для строковых столбцов без максимальной длины.<br /><br /> **По умолчанию:** 4000|  
|Запрос|Параметры запроса OData. Это свойство поддерживает выражения и может быть задано во время выполнения.|  
|ResourcePath|Это свойство используется в том случае, когда необходимо указать полный путь к ресурсу, а не просто выбрать имя коллекции. Это свойство используется в том случае, если значение **UseResourcePath** равно True.|  
|UseResourcePath|Если задано значение True, то значение **ResourcePath** добавляется к базовому URL-адресу для определения расположения канала OData. Если значение равно False, то используется значение **CollectionName** .<br /><br /> **По умолчанию:** False|  
  
## <a name="see-also"></a>См. также:
[Источник «OData»](odata-source.md)
