---
title: SQL Server распределенного воспроизведения | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Distributed Replay
- SQL Server Distributed Replay
ms.assetid: 58ef7016-b105-42c2-90a0-364f411849a4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 900fdcafe18c2a885ea7191ce8619e46e8f0f963
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026268"
---
# <a name="sql-server-distributed-replay"></a>Распределенное воспроизведение SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Функция распределенного воспроизведения [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] позволяет оценить влияние будущих обновлений [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ее также можно использовать для оценки влияния обновления аппаратной части и операционной системы, а также для настройки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="benefits-of-distributed-replay"></a>Преимущества распределенного воспроизведения  
 Как и приложение [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], распределенное воспроизведение можно использовать для воспроизведения записанной трассировки в обновленной тестовой среде. В отличие от приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], распределенное воспроизведение не ограничено воспроизведением рабочих нагрузок с одного компьютера.  
  
 Распределенное воспроизведение является лучше масштабируемым решением, чем [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Распределенное воспроизведение используется для воспроизведения рабочих нагрузок со многих компьютеров и лучше моделирует важные реальные рабочие нагрузки.  
  
 Функция распределенного воспроизведения [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] позволяет использовать несколько компьютеров для воспроизведения данных трассировки и моделирования важной рабочей нагрузки. Программу распределенного воспроизведения можно использовать для тестирования совместимости приложений, производительности и планирования загрузки.  
  
## <a name="when-to-use-distributed-replay"></a>Применение распределенного воспроизведения  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] и распределенного воспроизведения частично совпадают.  
  
 С помощью приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] можно воспроизводить записанную трассировку в обновленной тестовой среде. Кроме того, результаты воспроизведения можно анализировать с целью поиска потенциальных функциональных несовместимостей и проблем производительности. Однако приложение [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] позволяет воспроизводить рабочую нагрузку только с одного компьютера. При воспроизведении работы загруженного приложения OLTP с большим числом активных параллельных соединений или пропускной способностью на сеть приложению [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] может не хватить ресурсов.  
  
 Распределенное воспроизведение является лучше масштабируемым решением, чем [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Распределенное воспроизведение используется для воспроизведения рабочих нагрузок с нескольких компьютеров и лучше моделирует важные реальные рабочие нагрузки.  
  
 В следующей таблице описывается, когда нужно использовать каждое средство.  
  
|Инструмент|Применение|  
|----------|---------------|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]|Нужно использовать обычный механизм воспроизведения на одном компьютере. В частности, если необходимы возможности построчной отладки, такие как команды **По шагам**, **Выполнить до текущей позиции**и **Точка останова** .<br /><br /> Необходимо воспроизвести трассировку служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Распределенное воспроизведение|Необходимо оценить совместимость приложений. Например, нужно протестировать варианты обновления [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и операционной системы, модернизацию оборудования или настройку индекса.<br /><br /> Уровень параллелизма в записанной трассировке настолько высок, что один клиент воспроизведения не сможет ее смоделировать.|  
  
## <a name="distributed-replay-concepts"></a>Основные понятия распределенного воспроизведения  
 Среда распределенного воспроизведения включает следующие компоненты.  
  
-   **Средство администрирования распределенного воспроизведения**. Консольное приложение **DReplay.exe**используется для взаимодействия с контроллером распределенного воспроизведения. Используйте средство администрирования для управления распределенным воспроизведением.  
  
-   **Контроллер распределенного воспроизведения**. Компьютер, на котором выполняется служба Windows контроллера распределенного воспроизведения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Контроллер распределенного воспроизведения управляет согласованными действиями клиентов распределенного воспроизведения. В каждой среде распределенного воспроизведения можно установить только один экземпляр контроллера.  
  
-   **Клиенты распределенного воспроизведения**. Один или несколько компьютеров (физических или виртуальных), на которых запущена служба Windows клиента распределенного воспроизведения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Клиенты распределенного воспроизведения работают совместно для имитации рабочей нагрузки на экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. В каждой среде распределенного воспроизведения можно установить один или несколько клиентов.  
  
-   **Целевой сервер**. Экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , который клиенты распределенного воспроизведения могут использовать для воспроизведения данных трассировки. Рекомендуется размещать целевой сервер в среде тестирования.  
  
 Средство администрирования, контроллер и клиент распределенного воспроизведения могут быть установлены на одном компьютере или на разных компьютерах. На одном компьютере может выполняться только один экземпляр контроллера распределенного воспроизведения или службы клиента.  
  
 На следующем рисунке показана физическая архитектура распределенного воспроизведения в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 ![Распределенная архитектура воспроизведения](../../tools/distributed-replay/media/distributedreplayarch.gif "распределенная архитектура воспроизведения")  
  
## <a name="distributed-replay-tasks"></a>Задачи распределенного воспроизведения  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Настройка распределенного воспроизведения.|[Настройка распределенного воспроизведения](../../tools/distributed-replay/configure-distributed-replay.md)|  
|Описывает подготовку входных данных трассировки.|[Подготовка входных данных трассировки](../../tools/distributed-replay/prepare-the-input-trace-data.md)|  
|Описывает процесс воспроизведения данных трассировки.|[Воспроизведение данные трассировки](../../tools/distributed-replay/replay-trace-data.md)|  
|Описывает просмотр результатов данных трассировки распределенного воспроизведения.|[просмотреть результаты воспроизведения](../../tools/distributed-replay/review-the-replay-results.md)|  
|Описывает, как при помощи средства администрирования можно инициировать операции на контроллере, наблюдать за ними и отменять их.|[Параметры командной строки средства администрирования (программа распределенного воспроизведения)](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)|  
  
## <a name="see-also"></a>См. также:  
 [Форум о распределенном воспроизведении SQL Server](https://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [Использование распределенного воспроизведения для нагрузочного теста SQL Server. Часть 2](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [Использование распределенного воспроизведения для нагрузочного теста SQL Server. Часть 1](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
