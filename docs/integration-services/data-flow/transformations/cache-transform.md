---
title: Преобразование кэша | Документы Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.cachetrans.f1
- sql13.dts.designer.cachetranscon.f1
- sql13.dts.designer.cachetransmap.f1
helpviewer_keywords:
- Cache transform
ms.assetid: a5683fc8-9c32-4634-819e-e9815627e4f1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a33198113b770aff85a52a153272f019d4ffdca7
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726266"
---
# <a name="cache-transform"></a>преобразование кэша

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Преобразование «Преобразование кэша» создает ссылочный набор данных для преобразования «Уточняющий запрос», выполняя запись из подключенного источника данных в потоке данных в диспетчер соединений с кэшем. Преобразование «Подстановка» выполняет подстановки, соединяя данные из входных столбцов подключенного источника данных и данные из столбцов в связанной базе данных.  
  
 Диспетчер соединений с кэшем можно использовать, если нужно, чтобы преобразование «Подстановка» работало в режиме полного кэширования. В этом режиме ссылочный набор данных загружается в кэш еще до запуска преобразования «Уточняющий запрос».  
  
 Инструкции по настройке преобразования "Подстановка" в режиме полного кэширования с помощью диспетчера соединений с кэшем и преобразования "Преобразование кэша" см. в разделе [Реализация преобразования "Уточняющий запрос" в режиме полного кэширования с помощью диспетчера соединений с кэшем](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md).  
  
 Дополнительные сведения о кэшировании ссылочного набора данных см. в разделе [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
> [!NOTE]  
>  «Преобразование кэша» записывает только уникальные строки в диспетчер соединений с кэшем.  
  
 В пределах одного пакета только одно преобразование «Преобразование кэша» может производить запись в один диспетчер соединений с кэшем. Если в пакете содержится несколько преобразований «Преобразование кэша», запись в диспетчер соединений будет производить первое преобразование, вызванное при запуске пакета. Операции записи последующих преобразований «Преобразование кэша» завершатся ошибкой.  
  
 Дополнительные сведения см. в разделе [Редактор диспетчера соединений с кэшем](../../../integration-services/data-flow/transformations/cache-connection-manager.md).  
  
## <a name="configuration-of-the-cache-transform"></a>Настройка преобразования кэша  
 Диспетчер соединений с кэшем можно настроить на сохранение данных в файлы кэша (CAW).  
  
 Можно настроить преобразование «Преобразование кэша» следующими способами.  
  
-   Указать диспетчер соединений с кэшем.  
  
-   Сопоставить входные столбцы в преобразовании «Преобразование кэша» с целевыми столбцами в диспетчере соединений с кэшем.  
  
    > [!NOTE]  
    >  Каждый входной столбец должен быть сопоставлен с целевым, имеющим тот же тип данных. В противном случае конструктор служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] отобразит сообщение об ошибке.  
  
     **Редактор диспетчера соединений с кэшем** можно использовать для изменения типов данных, имен и других свойств столбцов.  
  
 Свойства задаются с помощью конструктора служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Дополнительные сведения о свойствах, которые можно установить в диалоговом окне **Расширенный редактор** , см. в разделе [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Дополнительные сведения о настройке свойств см. в разделе [Установление свойств компонента потока данных](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="cache-transformation-editor-connection-manager-page"></a>Редактор преобразования «Кэш» (страница «Диспетчер соединений»)
  Используйте страницу **Диспетчер соединений** диалогового окна **Редактор преобразования «Кэш»** , чтобы выбрать существующий диспетчер соединений с кэшем или создать новый.  
  
 Дополнительные сведения о диспетчере соединений с кэшем см. в разделе [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md).  
  
### <a name="options"></a>Параметры  
 **Cache connection manager**  
 Выберите в списке существующий диспетчер соединений с кэшем или создайте новое соединение с помощью кнопки **Создать** .  
  
 **Создать**  
 Создайте новое соединение с помощью диалогового окна «Редактор диспетчера соединений с кэшем».  
  
 **Изменить**  
 Измените существующее соединение.  
  
## <a name="see-also"></a>См. также:  
 [Преобразования служб Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Поток данных](../../../integration-services/data-flow/data-flow.md)  
  
  
