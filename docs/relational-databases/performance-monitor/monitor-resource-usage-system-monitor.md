---
title: Наблюдение за использованием ресурсов (системный монитор) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], resource usage
- System Monitor [SQL Server], about Windows System Monitor
- resource usage monitoring [SQL Server]
- System Monitor [SQL Server]
- counters [SQL Server], resource usage subjects
- performance counters [SQL Server], resource usage subjects
- Windows System Monitor [SQL Server], about Windows System Monitor
- monitoring [SQL Server], server resource usage
- monitoring resource usage [SQL Server]
- Windows System Monitor [SQL Server]
- database monitoring [SQL Server], resource usage
- database performance [SQL Server], resource usage
- tuning databases [SQL Server], resource usage
- server performance [SQL Server], resource usage
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 8de6f5ade289780d5f0929af2f5a62e7facfe39b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62649560"
---
# <a name="monitor-resource-usage-system-monitor"></a>Наблюдение за использованием ресурсов (системный монитор)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В состав серверной операционной системы Microsoft Windows входит графическое средство для измерения производительности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]— системный монитор. Он позволяет просматривать объекты [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , счетчики производительности, а также поведения других объектов, таких как процессоры, память, кэш, потоки и процессы. С каждым из этих объектов связан набор счетчиков, измеряющих степень использования устройства, длину очередей, задержки и другие показатели производительности и внутренней перегрузки.  
  
> [!NOTE]  
>  Этот системный монитор заменяет системный монитор Windows NT 4.0.  
  
## <a name="benefits-of-system-monitor"></a>Преимущества системного монитора  
 Системный монитор может быть полезным для одновременного контроля счетчиков операционной системы Windows и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для определения корреляции между производительностью [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и Windows. Например, контроль счетчиков Windows для операций ввода-вывода на диске и одновременно счетчиков диспетчера буферов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может выявить закономерности всей системы.  
  
 Системный монитор позволяет получить статистические данные о текущей активности и производительности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Применение системного монитора предоставляет следующие возможности.  
  
-   Просматривать данные одновременно на любом числе компьютеров.  
  
-   Просматривать и изменять диаграммы, отражающие текущую активность, отображать значения счетчиков, обновляемых с частотой, которую определяет пользователь.  
  
-   Экспортировать данные из диаграмм, журналов, журналов предупреждений и отчетов в электронные таблицы или приложения баз данных для дальнейшей обработки и печати.  
  
-   Добавлять системные предупреждения, которые вносят событие в журнал предупреждений и уведомляют пользователей, формируя сетевые предупреждения.  
  
-   Запускать предопределенные приложения в первый раз или каждый раз, когда значение счетчика становится выше или ниже заданного значения.  
  
-   Создавать файлы журналов, содержащие данные о различных объектах в разных компьютерах.  
  
-   Присоединять к одному файлу выбранные разделы из других файлов журналов для формирования долговременного архива.  
  
-   Просматривать отчеты о текущей активности или создавать отчеты на основе данных существующих файлов журналов.  
  
-   Сохранять отдельные диаграммы, предупреждения, журналы, параметры отчетов или данные для запуска всего рабочего пространства для повторного использования.  
  
    > [!NOTE]  
    >  В системах позднее Windows NT 4.0 системный монитор заменил монитор производительности. Для выполнения указанных задач можно использовать системный монитор или монитор производительности.  
  
## <a name="system-monitor-performance"></a>Производительность системного монитора  
 При мониторинге [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и операционной системы Microsoft Windows для исследования вопросов, связанных с производительностью, первоначальные усилия должны быть сосредоточены на трех основных областях.  
  
-   Активность работы с диском  
  
-   Использование процессора  
  
-   Использование памяти  
  
 Контроль компьютера, в котором выполняется системный монитор, может слегка влиять на производительность компьютера. Поэтому или регистрируйте данные системного монитора на другом диске (или компьютере), чтобы уменьшить воздействие процедуры контроля на контролируемый компьютер, или выполняйте системный монитор с удаленного компьютера. Контролируйте только те счетчики, которые необходимы. При мониторинге слишком большого числа счетчиков в процессе мониторинга возникают дополнительные затраты ресурсов, что влияет на производительность того компьютера, за которым производится наблюдение.  
  
## <a name="system-monitor-tasks"></a>Задачи системного монитора  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Описываются случаи применения системного монитора и обсуждается снижение производительности при использовании системного монитора.|[Запуск системного монитора](../../relational-databases/performance-monitor/run-system-monitor.md)|  
|Описаны способы отслеживания счетчиков дискового пространства для определения активности диска и количества операций ввода-вывода, создаваемых компонентами SQL Server.|[Наблюдение за использованием диска](../../relational-databases/performance-monitor/monitor-disk-usage.md)|  
|Описаны способы отслеживания экземпляра Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , чтобы определить, находятся ли уровни загрузки ЦП в стандартных диапазонах.|[Мониторинг использования ЦП](../../relational-databases/performance-monitor/monitor-cpu-usage.md)|  
|Описаны способы мониторинга экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для подтверждения того, что память используется в допустимых пределах.|[Наблюдение за использованием памяти](../../relational-databases/performance-monitor/monitor-memory-usage.md)|  
|Описаны способы создания предупреждения, которое будет выводиться, когда счетчик системного монитора достигает порогового значения.|[Создание предупреждения для базы данных SQL Server](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)|  
|Описаны способы создания диаграмм, предупреждений, журналов и отчетов для отслеживания экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Создание диаграмм, предупреждений, журналов и отчетов](../../relational-databases/performance-monitor/create-charts-alerts-logs-and-reports.md)|  
|Приводится список объектов и счетчиков, используемых системным монитором для отслеживания деятельности на компьютерах, где установлены экземпляры [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Использование объектов SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md)|  
|Приводится список объектов и счетчиков, используемых системным монитором для отслеживания действий OLTP в памяти.|[Счетчики производительности XTP (In-Memory OLTP) для SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)|  
  
  
