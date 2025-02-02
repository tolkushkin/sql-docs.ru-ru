---
title: Основные понятия программирования репликации | Документация Майкрософт
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- replication [SQL Server], planning
- programming [SQL Server replication], planning
- programming [SQL Server replication]
ms.assetid: 2cd846e7-5bf3-4144-8772-703c4f439a2a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf393a3e0f117098dc4a85bae3e6c68728f43a64
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721812"
---
# <a name="replication-programming-concepts"></a>Основные понятия программирования репликации
  До начала разработки приложения, в котором используются функциональные возможности репликации, необходимо выполнить следующие общие шаги планирования:  
  
1.  Определить топологию репликации.  
  
2.  Определить функциональные возможности приложения.  
  
3.  Учесть в плане требования безопасности.  
  
4.  Выбрать среду разработки.  
  
5.  Выбрать соответствующий программный интерфейс репликации.  
  
 В остальной части данного раздела указанные шаги рассматриваются более подробно. Чтобы можно было наглядно ознакомиться с процессом планирования, приведен также пример.  
  
## <a name="defining-the-replication-topology"></a>Определение топологии репликации  
 Первый шаг программной реализации средств репликации состоит в определении топологии репликации для конкретного приложения. Если ведется разработка приложения, в котором будет использоваться существующая топология репликации, такого как клиентское приложение, получающее доступ к данным на существующем подписчике, необходимо сразу же перейти к следующему шагу.  
  
> [!NOTE]  
>  В некоторых случаях единственным назначением приложения является развертывание топологии репликации.  
  
 Определение топологии репликации зависит от многих факторов, включая следующие:  
  
-   Необходимость обновления реплицированных данных, и кто это должен делать.  
  
-   Требования к распределению данных, касающиеся согласованности, автономности и задержки.  
  
-   Среду репликации, включая бизнес-пользователей, техническую инфраструктуру, сеть и средства обеспечения безопасности, а также характеристики данных.  
  
-   Типы и параметры репликации.  
  
-   Топологии репликации и степень их соответствия типам репликации.  
  
 Если вы еще не имели дела с репликацией [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ознакомьтесь со статьей [Типы репликации](../types-of-replication.md).  
  
## <a name="defining-application-functionality"></a>Определение функциональных возможностей приложения  
 После определения топологии репликации необходимо принять решение по выбору функциональных возможностей, предоставляемых приложением. Эти функциональные возможности могут начинаться со скрипта, с помощью которого синхронизируется подписка, и заканчиваться приложением с пользовательским интерфейсом для настройки репликации. Репликацией поддерживаются следующие общие задачи программирования:  
  
-   Подготовка средств репликации к работе.  
  
-   Синхронизация подписчиков.  
  
-   Сопровождение топологии репликации.  
  
-   Текущее наблюдение за топологией репликации.  
  
-   Устранение неполадок в работе средств репликации.  
  
 Кроме того, широко применяется подход, предусматривающий расширение возможностей приложения путем совместного применения функциональных средств репликации с другими функциями, предоставляемыми в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. В следующей таблице выделяются некоторые расширенные функциональные возможности, которые могут быть предоставлены в конкретном приложении репликации.  
  
|Функция|Пример|  
|-------------------|-------------|  
|Администрирование сервера с использованием управляющих объектов [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (объектов SMO)|Приложение, которое предоставляет возможность администратору подключаться и настраивать базу данных в качестве издателя в топологии репликации.|  
|Доступ к данным с использованием технологии ADO.NET|Приложение, которое позволяет пользователю получать доступ программным путем и вносить изменения в реплицированные данные продаж в локальной базе данных подписчика, работая в режиме «вне сети», а затем подключаться и синхронизировать подписку по запросу нажатием одной кнопки.|  
  
## <a name="planning-for-security"></a>Планирование средств безопасности  
 Обеспечение безопасности является важной задачей в любом приложении, поэтому планирование средств безопасности должно быть завершено до написания любого кода. Задачу обеспечения безопасности приложения можно разделить на три основные части: безопасность базы данных, безопасность репликации и написание безопасного кода.  
  
 Сведения об обеспечении безопасности приведены в следующих разделах:  
  
-   [Безопасность репликации SQL Server](../security/view-and-modify-replication-security-settings.md)  
  
-   [Центр обеспечения безопасности для базы данных Azure SQL и SQL Server Database Engine](../../security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
## <a name="choosing-a-development-environment"></a>Выбор среды разработки  
 Разработка приложения репликации может быть осуществлена на базе одного из трех основных вариантов среды разработки. Каждая среда разработки предоставляет доступ к одним и тем же функциональным возможностям репликации, за некоторыми исключениями. Приложения репликации могут разрабатываться в каждом из следующих вариантов среды.  
  
-   **Управляемый код**  
  
     Объектно-ориентированная среда разработки, которая позволяет воспользоваться преимуществами программирования [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] и среды CLR .NET. Управляемый код является рекомендуемой средой программирования как для разработки .NET, так и для приложений [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Управляемые интерфейсы репликации обеспечивают возможность программирования средств администрирования репликации в объектно-ориентированной форме, не требуя знаний в области [!INCLUDE[tsql](../../../includes/tsql-md.md)], а также предоставляют определенные функциональные средства обратного вызова при эксплуатации агентов репликации, доступ к которым нельзя получить из скриптов. Управляемый код представляет собой наилучшую среду для разработки многократно используемых компонентов и приложений с пользовательским интерфейсом.  
  
-   **Создание скриптов**  
  
     Простые приложения, в которых выполняется ряд команд в качестве системных хранимых процедур репликации в скриптах [!INCLUDE[tsql](../../../includes/tsql-md.md)] или команд в пакетных файлах. Безусловно, обеспечивается возможность выполнять скрипты в управляемой среде с использованием внутрипроцессного управляемого поставщика [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], но те же функциональные возможности можно получить с применением управляемых интерфейсов репликации, которые предоставляют также функциональные средства обратного вызова. Среда скриптовой поддержки является наиболее подходящей для выполнения задач, которые вызываются лишь несколько раз и для которых не требуются функциональные возможности обратного вызова, таких как установка сервера репликации.  
  
-   **Машинный код**  
  
     Объектно-ориентированная среда разработки, в которой используется прямой доступ к системе или к COM-объектам так, что не происходит управление кодом в среде CLR. Интерфейсы репликации с машинным кодом считаются устаревшими или не поддерживаются. Дополнительные сведения см. в статьях [Устаревшие функции репликации SQL Server](../deprecated-features-in-sql-server-replication.md) или [Обратная совместимость репликации](../replication-backward-compatibility.md).  
  
## <a name="choose-the-appropriate-replication-programming-interface"></a>Выбор соответствующего программного интерфейса репликации  
 Конечный шаг планирования предусматривает выбор соответствующего программного интерфейса репликации, который реализует необходимые функциональные возможности репликации для выбранной среды разработки. В следующей таблице показаны доступные программные интерфейсы репликации.  
  
|Интерфейс|Среда|Области применения|  
|---------------|-----------------|----------|  
|[Основные понятия объектов RMO](replication-management-objects-concepts.md)|Управляемый код|Администрирование, текущее наблюдение и синхронизация.|  
|<xref:Microsoft.SqlServer.Replication>|Управляемый код|Синхронизация.|  
|<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|Управляемый код|Создание обработчиков бизнес-логики для интеграции пользовательской логики с процессом синхронизации слиянием.|  
|[Хранимые процедуры репликации (Transact-SQL)](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql)|Написание скриптов|Администрирование и текущее наблюдение.|  
|[Replication Agent Executables Concepts](replication-agent-executables-concepts.md)|Написание скриптов|Синхронизация.|  
  
## <a name="example"></a>Пример  
 В [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] должна обеспечиваться публикация данных для 200 торговых представителей во всем мире. Торговые представители часто находятся в командировках и вынуждены использовать переносные компьютеры или карманные компьютеры для обмена данными с заказчиком и добавления новых заказов. Затем изменения в данных должны быть синхронизированы с издателем, после подключения торговым представителем своего переносного компьютера к сети.  
  
 Для данного приложения шаги планирования могут выглядеть следующим образом:  
  
1.  Топология репликации для этого приложения уже существует. Но в клиенте должна быть создана новая подписка по запросу. В публикации должны использоваться параметризованные фильтры для обеспечения репликации только уникального набора данных для каждого торгового представителя.  
  
2.  Кроме типичного доступа к данным, необходимого для приложения в системе продаж, это приложение должно предоставлять менеджеру по продажам возможность в любое время синхронизировать подписку по запросу путем нажатия одной кнопки. Установкой и эксплуатацией приложения должен заниматься сам торговый представитель, поэтому он должен иметь возможность настроить конфигурацию подписки и применить исходный моментальный снимок на клиенте. В качестве необязательного средства в приложении будет использоваться инфраструктура проверки возможности беспроводного обмена данными, предусмотренная в Windows, для автоматической синхронизации подписки при обнаружении доступного соединения.  
  
3.  Должны соблюдаться все рекомендации по безопасности, касающиеся репликации, в том числе использование проверки подлинности Windows и виртуальной частной сети при соединении с издателем. Если должна быть реализована веб-синхронизация, то следует использовать соединение по протоколу SSL. Дополнительные сведения см. в статье [Настройка веб-синхронизации](../configure-web-synchronization.md).  
  
4.  Чтобы можно было воспользоваться преимуществами средств [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], приложение разрабатывается на основе языка определения управляемого кода.  
  
5.  Изучение этих требований показывает, что все необходимые функциональные возможности репликации для этого приложения может предоставить управляемый интерфейс объектов RMO.  
  
 Сценарий, рассматриваемый в данном примере, был реализован в образце приложения, который поставляется в составе [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  
