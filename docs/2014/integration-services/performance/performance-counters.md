---
title: Счетчики производительности | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], performance counters
- performance counters [Integration Services]
- data flow [Integration Services], performance
- counters [Integration Services]
- data flow engine [Integration Services]
ms.assetid: 11e17f4e-72ed-44d7-a71d-a68937a78e4c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 79c9e433a6b5bcf9babee0060fdf028775e0e8a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62889842"
---
# <a name="performance-counters"></a>Счетчики производительности
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] устанавливают набор счетчиков производительности, предназначенных для наблюдения за производительностью подсистемы обработки потока данных. Например, наблюдая за счетчиком «Выгружено буферов», можно определить, записываются ли временно на диск буфера данных при выполнении пакета. Такая выгрузка снижает производительность и указывает на недостаточный объем памяти компьютера.  
  
> [!NOTE]  
>  Если установить службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] на компьютер, на котором запущена ОС [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], а затем обновить ОС до [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)], то в процессе обновления из компьютера будут удалены счетчики производительности [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Чтобы восстановить счетчики производительности служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] на компьютере, запустите средство установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в режиме исправлений.  
  
 В следующей таблице приводятся описания счетчиков производительности.  
  
|Счетчик производительности|Описание|  
|-------------------------|-----------------|  
|Считано байтов BLOB|Число байт данных BLOB, которое подсистема обработки потока данных считала из всех источников.|  
|Записано байтов BLOB|Число байтов данных BLOB, которые подсистема обработки потока данных записала во все назначения.|  
|Используется файлов BLOB|Количество BLOB-файлов, использованных в текущий момент подсистемой обработки потока данных для буферизации.|  
|Память буферов|Объем используемой памяти. Включает как физическую, так и виртуальную память. Если значение больше, чем объем физической памяти, счетчик **Выгружено буферов** увеличивается как признак увеличения памяти подкачки. Увеличение памяти подкачки замедляет производительность подсистемы обработки потока данных.|  
|Используется буферов|Количество объектов буферов всех типов, используемых в текущий момент подсистемой обработки потока данных и компонентами потока данных.|  
|Выгружено буферов|Количество буферов, записанных на диск в текущий момент. Если подсистеме обработки потока данных не хватает оперативной памяти, буферы, не используемые в данный момент, записываются на диск и повторно загружаются в память при необходимости.|  
|Память плоских буферов|Общий объем памяти в байтах, используемой всеми плоскими буферами. Плоские буфера — это блоки памяти, которые компонент использует для сохранения данных. Плоский буфер — большой блок байтов, к которому обращаются байт за байтом.|  
|Используется плоских буферов|Количество плоских буферов, использованных подсистемой обработки потока данных. Все плоские буферы являются частными буферами.|  
|Память частных буферов|Общий объем памяти, использованной всеми частными буферами. Буфер не является частным, если подсистема обработки потока данных создает его для поддержки потока данных. Частный буфер — это буфер, который используется преобразованием только для временной работы. Например, преобразование «Статистическая обработка» использует частные буферы для выполнения своей работы.|  
|Используется частных буферов|Количество буферов, используемых преобразованиями.|  
|Считано строк|Количество строк, выдаваемых источником. Количество не включает строки, считанные из ссылочных таблиц преобразованием «Уточняющий запрос».|  
|Записано строк|Количество строк, предложенных для назначения. Это число не несет сведений о строках, записанных в целевое хранилище данных.|  
  
 Используйте оснастку консоли управления MMC для быстрого создания журнала, собирающего данные счетчиков производительности.  
  
 Сведения об улучшении производительности см. в разделе [Возможности для повышения производительности потока данных](../data-flow/data-flow-performance-features.md).  
  
## <a name="obtain-performance-counter-statistics"></a>Получение статистики счетчика производительности  
 Для проектов [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], которые развертываются на сервере [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], статистику счетчика производительности вы можете получить с помощью функции [dm_execution_performance_counters (база данных SSISDB)](/sql/integration-services/functions-dm-execution-performance-counters).  
  
 В следующем примере функция возвращает статистику для запущенного выполнения с идентификатором 34.  
  
```  
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
 В следующем примере функция возвращает статистику для всех выполнений, запущенных на сервере [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
```  
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
> [!IMPORTANT]  
>  Для члена роли базы данных `ssis_admin` возвращается статистика производительности всех активных выполнений.  Если пользователь не является членом роли базы данных `ssis_admin`, возвращается статистика производительности активных выполнений, для которых имеются разрешения на чтение.  
  
## <a name="related-content"></a>См. также  
  
-   Средство [Визуализация производительности служб SSIS Performance для Business Intelligence Development Studio (проект CodePlex)](https://go.microsoft.com/fwlink/?LinkId=146626) на узле codeplex.com.  
  
-   Видео [Измерение и основные сведения о показателях пакетов служб SSIS на предприятии (видеоматериал SQL Server)](https://go.microsoft.com/fwlink/?LinkId=150497) на сайте msdn.microsoft.com.  
  
-   Статья поддержки [Счетчик производительности служб SSIS больше недоступен в системном мониторе после обновления до Windows Server 2008](https://go.microsoft.com/fwlink/?LinkId=235319)на узле support.microsoft.com.  
  
## <a name="see-also"></a>См. также  
 [Запуск проектов и пакетов](../packages/run-integration-services-ssis-packages.md)  
  
  
