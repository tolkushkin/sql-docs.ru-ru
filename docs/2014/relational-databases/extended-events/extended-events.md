---
title: Расширенные события | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485c748aad8b07a5e8b92a02c03d51a82e5f362a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990705"
---
# <a name="extended-events"></a>Расширенные события
  Расширенная подсистема событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имеет чрезвычайно масштабируемую и легко настраиваемую архитектуру, которая позволяет пользователям собирать именно такое количество информации, которое необходимо для устранения нарушения в работе или выявления проблемы производительности.  
  
 Дополнительные сведения о расширенных событиях можно найти в статье [Расширенные события SQL Server](https://blogs.msdn.com/b/extended_events/).  
  
## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>Преимущества системы расширенных событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Расширенные события — это упрощенная система мониторинга производительности, в которой применяется очень небольшой объем ресурсов. Система расширенных событий имеет два графических пользовательских интерфейса (**Мастер новых сеансов** или **Создание сеанса**), которые позволяют создавать, изменять, выводить и анализировать данные сеанса.  
  
## <a name="extended-events-concepts"></a>Общие сведения о расширенных событиях  
 Подсистема расширенных событий (Extended Events) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] основана на таких основных понятиях, как событие и объект-получатель событий, а также использует понятия трассировки событий для Windows (ETW) и вводит несколько новых понятий.  
  
 В следующей таблице даны определения понятий, применяемых в расширенной подсистеме событий.  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Пакеты обработки расширенных событий SQL Server](sql-server-extended-events-packages.md)|Описывает пакеты расширенных событий, содержащих объекты, которые используются для получения и обработки данных при работе сеанса расширенных событий.|  
|[Цели расширенных событий SQL Server](../../database-engine/sql-server-extended-events-targets.md)|Описывает объекты-получатели событий, получающие данные во время сеанса событий.|  
|[Подсистема расширенных событий SQL Server](sql-server-extended-events-engine.md)|Описывает подсистему, которая реализует сеанс расширенных событий, а также управляет им.|  
|[Сеансы расширенных событий SQL Server](sql-server-extended-events-sessions.md)|Описывает сеанс расширенных событий.|  
  
## <a name="extended-events-architecture"></a>Архитектура расширенной подсистемы событий  
 Расширенные события (Extended Events) представляют собой общую систему обработки событий для серверных систем. Инфраструктура расширенных событий поддерживает корреляцию данных из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а при определенных условиях — корреляцию данных из операционной системы и приложений баз данных. В последнем случае выходные данные расширенных событий должны быть направлены в средство отслеживания событий для Windows (ETW) для корреляции данных событий с данными операционной системы или приложений баз данных.  
  
 Все приложения имеют точки выполнения, которые с успехом используются как внутри приложения, так и вне его. Внутри приложения можно поставить асинхронную обработку в очередь, используя сведения, собранные во время начального выполнения задачи. Вне приложения точки выполнения обеспечивают программы наблюдения сведениями о характеристиках поведения и производительности отслеживаемого приложения.  
  
 Расширенные события поддерживают использование данных событий вне процесса. Эти данные используются, как правило, следующими средствами.  
  
-   Средствами трассировки, например приложением SQL Trace и системным монитором.  
  
-   Инструментами ведения журналов, например журналом событий Windows или журналом ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Пользователями, выполняющими администрирование продукта или разрабатывающими приложения для него.  
  
 Ключевые аспекты расширенных событий:  
  
-   Подсистема расширенных событий не зависит от событий. Подсистема может привязать любое событие к любой цели, так как не ограничена содержимым события. Дополнительные сведения о подсистеме расширенных событий см. в разделе [SQL Server Extended Events Engine](sql-server-extended-events-engine.md).  
  
-   События отделены от объектов-получателей событий, называемых в расширенных событиях *целями* . Это означает, что любая цель может получать любые события. Кроме того, любое возникающее событие может автоматически потребляться целью, которая регистрирует его и предоставляет дополнительный контекст событий. Дополнительные сведения см. в разделе [SQL Server Extended Events Targets](../../database-engine/sql-server-extended-events-targets.md).  
  
-   События отделены от действий, предпринимаемых при возникновении события. Следовательно, любое действие можно связать с любым событием.  
  
-   Предикаты могут применять динамические фильтры, когда необходимо получить данные события. Это делает инфраструктуру расширенных событий более гибкой. Дополнительные сведения см. в разделе [SQL Server Extended Events Packages](sql-server-extended-events-packages.md).  
  
 Расширенные события могут синхронно создавать данные событий (и асинхронно обрабатывать эти данные), чем обеспечивается гибкое решение для обработки событий. Кроме того, расширенные события предоставляют следующие возможности.  
  
-   Унифицированный подход к обработке событий во всей серверной системе, одновременно разрешающий пользователям изолировать отдельные события для устранения неполадок.  
  
-   Интеграция и поддержка существующих инструментов приложения трассировки событий Windows.  
  
-   Полностью настраиваемый механизм обработки событий на основе языка [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Возможность динамического мониторинга активных процессов с минимальным влиянием на эти процессы.  
  
-   Сеанс работоспособности системы по умолчанию, который выполняется без каких-либо заметных последствий для производительности. В этом сеансе собираются системные данные, которые можно использовать для решения проблем производительности. Дополнительные сведения см. в статье [Использование сеанса system_health](use-the-ssms-xe-profiler.md).  
  
## <a name="extended-events-tasks"></a>Задачи расширенной подсистемы событий  
 Использование среды [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] или языка [!INCLUDE[tsql](../../includes/tsql-md.md)] для выполнения инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] языка описания данных DDL, динамических административных представлений и функций или представлений каталога дает возможность создавать простые и комплексные решения по диагностике расширенных событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в среде [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|**Обозреватель объектов** позволяет управлять сеансами события.|[Управление сеансами событий в обозревателе объектов](../../ssms/object/object-explorer.md)|  
|Описано, как создать сеанс расширенных событий.|[Создание сеанса расширенных событий](../../database-engine/create-an-extended-events-session.md)|  
|Описывает, как просматривать и обновлять целевые данные.|[Просмотр данных о сеансе событий](../../database-engine/view-event-session-data.md)|  
|Описывает использование средств расширенной подсистемы событий для создания сеансов и управления сеансами расширенных событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Средства расширенных событий](extended-events-tools.md)|  
|Описано, как изменить сеанс расширенных событий.|[Изменение сеанса расширенных событий](alter-an-extended-events-session.md)|  
|Описано, как копировать или экспортировать целевые данные.|[Копирование или экспорт целевых данных](../../database-engine/copy-or-export-target-data.md)|  
|Описывает, как изменить представление результатов трассировки для настройки параметров анализа данных.|[Изменение представления результатов трассировки](../../database-engine/modify-the-trace-results-view.md)|  
|Описывает, как получить информацию о полях, связанных с событиями.|[Получение полей для всех событий](../../database-engine/get-the-fields-for-all-events.md)|  
|Описывает, как узнать, какие события доступны в зарегистрированных пакетах.|[Просмотр событий для зарегистрированных пакетов](../../database-engine/view-the-events-for-registered-packages.md)|  
|Описывает, как определить, какие цели расширенных событий доступны в зарегистрированных пакетах.|[Просмотр целей расширенных событий для зарегистрированных пакетов](../../database-engine/view-the-extended-events-targets-for-registered-packages.md)|  
|Описывает, как с помощью приведенной ниже процедуры можно просматривать события и действия расширенных событий, аналогичных каждому событию трассировки SQL со связанными столбцами.|[Просмотр эквивалентов расширенных событий для классов событий трассировки SQL](view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Описывает, как выяснить, какие параметры можно задать при использовании аргумента ADD TARGET в инструкции CREATE EVENT SESSION или ALTER EVENT SESSION.|[Получение настраиваемых параметров для аргумента ADD TARGET](../../database-engine/get-the-configurable-parameters-for-the-add-target-argument.md)|  
|Описано, как преобразовать существующий скрипт приложения трассировки SQL в сеанс расширенных событий.|[Преобразование существующего скрипта трассировки SQL в сеанс расширенных событий](convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Описывает, как определить, какие запросы удерживают данную блокировку и каковы план запроса и стек [!INCLUDE[tsql](../../includes/tsql-md.md)] во время получения блокировки.|[Определение запросов, содержащих блокировки](determine-which-queries-are-holding-locks.md)|  
|Описывает, как определить источник блокировок, приводящих к ухудшению производительности базы данных.|[найти объекты, на которые наложено наибольшее число блокировок](find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Описывает, как использовать расширенные события совместно со средством трассировки событий для Windows (ETW) для наблюдения за активностью системы.|[Мониторинг активности системы с помощью расширенных событий](monitor-system-activity-using-extended-events.md)|  
  
## <a name="see-also"></a>См. также  
 [Приложения уровня данных](../data-tier-applications/data-tier-applications.md)   
 [Поддержка приложений уровня данных для объектов и версий SQL Server](../data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [Развертывание приложения уровня данных](../data-tier-applications/deploy-a-data-tier-application.md)   
 [Наблюдение за приложениями уровня данных](../data-tier-applications/monitor-data-tier-applications.md)   
 [Динамические административные представления расширенных событий](../views/views.md)   
 [Представления каталога расширенных событий &#40;Transact-SQL&#41;] (~/relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql  
  
  
