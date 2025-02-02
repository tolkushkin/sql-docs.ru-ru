---
title: Общие сведения о расширенных событиях в SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: overview
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 01ec6f0f6a48fd0d19b6bda98b42afe57abd0a07
ms.sourcegitcommit: 982a1dad0b58315cff7b54445f998499ef80e68d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66175665"
---
# <a name="extended-events-overview"></a>Общие сведения о расширенных событиях

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Расширенная подсистема событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имеет чрезвычайно масштабируемую и легко настраиваемую архитектуру, которая позволяет пользователям собирать именно такое количество информации, которое необходимо для устранения нарушения в работе или выявления проблемы производительности.  

Дополнительные сведения о расширенных событиях см. в следующих источниках: [Быстрое начало. Расширенные события в SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md).


## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>Преимущества системы расширенных событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Расширенные события — это упрощенная система мониторинга производительности, в которой применяется очень небольшой объем ресурсов. Система расширенных событий имеет два графических пользовательских интерфейса (**Мастер новых сеансов** или **Создание сеанса**), которые позволяют создавать, изменять, выводить и анализировать данные сеанса.  
  
## <a name="extended-events-concepts"></a>Общие сведения о расширенных событиях  
 Подсистема расширенных событий (Extended Events) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] основана на таких основных понятиях, как событие и объект-получатель событий, а также использует понятия трассировки событий для Windows (ETW) и вводит несколько новых понятий.  
  
 В следующей таблице даны определения понятий, применяемых в расширенной подсистеме событий.  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Пакеты обработки расширенных событий SQL Server](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|Описывает пакеты расширенных событий, содержащих объекты, которые используются для получения и обработки данных при работе сеанса расширенных событий.|  
|[Цели расширенных событий SQL Server](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)|Описывает объекты-получатели событий, получающие данные во время сеанса событий.|  
|[Подсистема расширенных событий SQL Server](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|Описывает подсистему, которая реализует сеанс расширенных событий, а также управляет им.|  
|[Сеансы расширенных событий SQL Server](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|Описывает сеанс расширенных событий.|  
  
## <a name="extended-events-architecture"></a>Архитектура расширенной подсистемы событий  
 Расширенные события (Extended Events) представляют собой общую систему обработки событий для серверных систем. Инфраструктура расширенных событий поддерживает корреляцию данных из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а при определенных условиях — корреляцию данных из операционной системы и приложений баз данных. В последнем случае выходные данные расширенных событий должны быть направлены в средство отслеживания событий для Windows (ETW) для корреляции данных событий с данными операционной системы или приложений баз данных.  
  
 Все приложения имеют точки выполнения, которые с успехом используются как внутри приложения, так и вне его. Внутри приложения можно поставить асинхронную обработку в очередь, используя сведения, собранные во время начального выполнения задачи. Вне приложения точки выполнения обеспечивают программы наблюдения сведениями о характеристиках поведения и производительности отслеживаемого приложения.  
  
 Расширенные события поддерживают использование данных событий вне процесса. Эти данные используются, как правило, следующими средствами.  
  
-   Средствами трассировки, например приложением SQL Trace и системным монитором.  
  
-   Инструментами ведения журналов, например журналом событий Windows или журналом ошибок [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Пользователями, выполняющими администрирование продукта или разрабатывающими приложения для него.  
  
 Ключевые аспекты расширенных событий:  
  
-   Подсистема расширенных событий не зависит от событий. Подсистема может привязать любое событие к любой цели, так как не ограничена содержимым события. Дополнительные сведения о подсистеме расширенных событий см. в разделе [SQL Server Extended Events Engine](../../relational-databases/extended-events/sql-server-extended-events-engine.md).  
  
-   События отделены от объектов-получателей событий, называемых в расширенных событиях *целями* . Это означает, что любая цель может получать любые события. Кроме того, любое возникающее событие может автоматически потребляться целью, которая регистрирует его и предоставляет дополнительный контекст событий. Дополнительные сведения см. в разделе [SQL Server Extended Events Targets](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).  
  
-   События отделены от действий, предпринимаемых при возникновении события. Следовательно, любое действие можно связать с любым событием.  
  
-   Предикаты могут применять динамические фильтры, когда необходимо получить данные события. Это делает инфраструктуру расширенных событий более гибкой. Дополнительные сведения см. в разделе [SQL Server Extended Events Packages](../../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
 Расширенные события могут синхронно создавать данные событий (и асинхронно обрабатывать эти данные), чем обеспечивается гибкое решение для обработки событий. Кроме того, расширенные события предоставляют следующие возможности.  
  
-   Унифицированный подход к обработке событий во всей серверной системе, одновременно разрешающий пользователям изолировать отдельные события для устранения неполадок.  
  
-   Интеграция и поддержка существующих инструментов приложения трассировки событий Windows.  
  
-   Полностью настраиваемый механизм обработки событий на основе языка [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Возможность динамического мониторинга активных процессов с минимальным влиянием на эти процессы.  
  
-   Сеанс работоспособности системы по умолчанию, который выполняется без каких-либо заметных последствий для производительности. В этом сеансе собираются системные данные, которые можно использовать для решения проблем производительности. Дополнительные сведения см. в статье [Использование сеанса system_health](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## <a name="extended-events-tasks"></a>Задачи расширенной подсистемы событий  

Использование среды [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] или языка [!INCLUDE[tsql](../../includes/tsql-md.md)] для выполнения инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] языка описания данных DDL, динамических административных представлений и функций или представлений каталога дает возможность создавать простые и комплексные решения по диагностике расширенных событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в среде [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|**Обозреватель объектов** позволяет управлять сеансами события.|[Управление сеансами событий в обозревателе объектов](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|Описано, как создать сеанс расширенных событий.|[Создание сеанса расширенных событий](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)|  
|Описывает, как просматривать и обновлять целевые данные.| [Расширенный просмотр целевых данных из расширенных событий в SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|Описывает использование средств расширенной подсистемы событий для создания сеансов и управления сеансами расширенных событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Средства расширенных событий](../../relational-databases/extended-events/extended-events-tools.md)|  
|Описано, как изменить сеанс расширенных событий.|[Изменение сеанса расширенных событий](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|Описывает, как получить информацию о полях, связанных с событиями.|[Получение полей для всех событий](https://msdn.microsoft.com/library/4e4ee03f-5bca-42ed-a37c-db1c82e3aad2)|  
|Описывает, как узнать, какие события доступны в зарегистрированных пакетах.|[Просмотр событий для зарегистрированных пакетов](https://msdn.microsoft.com/library/9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f)|  
|Описывает, как определить, какие цели расширенных событий доступны в зарегистрированных пакетах.|[Просмотр целей расширенных событий для зарегистрированных пакетов](https://msdn.microsoft.com/library/4985aa5f-ac99-49f6-852c-9d25916549e9)|  
|Описывает, как с помощью приведенной ниже процедуры можно просматривать события и действия расширенных событий, аналогичных каждому событию трассировки SQL со связанными столбцами.|[Просмотр эквивалентов расширенных событий для классов событий трассировки SQL](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|Описывает, как выяснить, какие параметры можно задать при использовании аргумента ADD TARGET в инструкции CREATE EVENT SESSION или ALTER EVENT SESSION.|[Получение настраиваемых параметров для аргумента ADD TARGET](https://msdn.microsoft.com/library/08454543-c5c8-4ca3-9af9-f1d82264471c)|  
|Описано, как преобразовать существующий скрипт приложения трассировки SQL в сеанс расширенных событий.|[Преобразование существующего скрипта трассировки SQL в сеанс расширенных событий](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|Описывает, как определить, какие запросы удерживают данную блокировку и каковы план запроса и стек [!INCLUDE[tsql](../../includes/tsql-md.md)] во время получения блокировки.|[Определение запросов, содержащих блокировки](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|Описывает, как определить источник блокировок, приводящих к ухудшению производительности базы данных.|[найти объекты, на которые наложено наибольшее число блокировок](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|Описывает, как использовать расширенные события совместно со средством трассировки событий для Windows (ETW) для наблюдения за активностью системы.|[Мониторинг активности системы с помощью расширенных событий](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
| Использование представлений каталога и динамических административных представлений для расширенных событий | [Использование SELECT и JOIN в системных представлениях для расширенных событий в SQL Server](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |

  
## <a name="see-also"></a>См. также:  
 [Приложения уровня данных](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Поддержка приложений уровня данных для объектов и версий SQL Server](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [Развертывание приложения уровня данных](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Наблюдение за приложениями уровня данных](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)   
 [Динамические административные представления расширенных событий](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Представления каталога расширенных событий (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
 [XELite: кроссплатформенная библиотека для чтения событий XEvent из XEL-файлов или обновляющихся потоков SQL](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/), выпущена в мае 2019 г.  
