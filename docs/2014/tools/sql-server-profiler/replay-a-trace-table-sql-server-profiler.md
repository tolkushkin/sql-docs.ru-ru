---
title: Воспроизведение таблицы трассировки (SQL Server Profiler) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 6a0ad817-3d8d-4495-889d-c66a7ef9e8bb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e80a18cef595ae3543aba8a656aca9267607e38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240491"
---
# <a name="replay-a-trace-table-sql-server-profiler"></a>воспроизвести таблицу трассировки (приложение SQL Server Profiler)
  Воспроизведением называется возможность открывать сохраненную трассировку и снова ее воспроизводить. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] содержит в себе многопоточный модуль воспроизведения, который имитирует соединения пользователей и проверку подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Воспроизведение хорошо помогает при диагностике ошибок приложений и процессов. Отыскав и исправив ошибку, запустите трассировку, обнаружившую эту ошибку, в отношении исправленной версии приложения или процесса. а затем, после воспроизведения исходной трассировки, сравнить результаты.  
  
 Чтобы воспроизведение было возможным, необходимо помимо классов событий, отобранных для отслеживания, фиксировать и специальные классы событий. Эти события фиксируются по умолчанию при использовании шаблона трассировки **TSQL_Replay** . Дополнительные сведения см. в разделе [Replay Requirements](replay-requirements.md).  
  
### <a name="to-replay-a-trace-table"></a>Воспроизведение таблицы трассировки  
  
1.  Откройте таблицу трассировки, которая содержит классы событий, необходимые для воспроизведения.  
  
2.  В меню **Воспроизведение** выберите **Начать**и установите соединение с экземпляром сервера, на котором требуется воспроизвести трассировку.  
  
3.  В диалоговом окне **Настройка воспроизведения** на вкладке **Основные параметры воспроизведения** укажите **Сервер воспроизведения**. Нажмите кнопку **Изменить** , чтобы изменить сервер, который отображается в диалоговом окне **Сервер воспроизведения** .  
  
4.  По желанию можно выбрать одно из следующих мест назначения, где можно сохранить воспроизведение:  
  
    -   **Сохранить в файл** , что указывает на файл, в котором должно быть сохранено воспроизведение.  
  
    -   **Сохранить в таблицу**позволяет указать таблицу базы данных, в которую будут записаны результаты воспроизведения.  
  
5.  Выберите либо **Воспроизвести события в порядке трассировки**, либо **Воспроизвести события, используя несколько потоков**. В нижеследующей таблице объясняются различия между этими параметрами.  
  
    |Параметр|Описание|  
    |------------|-----------------|  
    |**Воспроизвести события в порядке трассировки**|Воспроизводит события в том порядке, в котором они были записаны. Выбор этого параметра включает возможность отладки.|  
    |**Воспроизвести события, используя несколько потоков**|В этом варианте используются несколько потоков для воспроизведения каждого события независимо от последовательности. Выбор этого параметра способствует оптимальной производительности.|  
  
6.  Чтобы проследить за ходом воспроизведения, выберите **Отобразить результаты воспроизведения** .  
  
7.  При необходимости выберите вкладку **Дополнительные параметры воспроизведения**, чтобы задать следующие параметры:  
  
    -   Чтобы воспроизвести все идентификаторы серверных процессов (SPID), выберите **Воспроизвести системные SPID**.  
  
    -   Чтобы ограничить воспроизведение процессами, принадлежащими конкретному SPID, выберите **Воспроизвести только один SPID**. В поле **SPID для воспроизведения**введите SPID.  
  
    -   чтобы воспроизвести события за определенный период времени, выберите **Предел воспроизведения по дате и времени**. Выберите дату и время для параметров **Время запуска**и **Время окончания**, чтобы указать период для включения в воспроизведение.  
  
    -   чтобы указать, как сервер [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должен управлять процессами во время воспроизведения, настройте **Параметры монитора исправности**.  
  
## <a name="see-also"></a>См. также  
 [Разрешения, необходимые для запуска приложения SQL Server Profiler](sql-server-profiler.md)   
 [Воспроизведение трассировок](replay-traces.md)   
 [Открытие таблицы трассировки (приложение SQL Server Profiler)](open-a-trace-table-sql-server-profiler.md)   
 [Приложение SQL Server Profiler](sql-server-profiler.md)  
  
  
