---
title: Общие свойства | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- IdleConnectionTimeout property
- InstanceVisible property
- TempDir property
- AdminTimeout property
- MinIdleSessionTimeout property
- MaxIdleSessionTimeout property
- IdleOrphanSessionTimeout property
- BackupDir property
- CommitTimeout property
- ExternalCommandTimeout property
- Enabled property
- ForceCommitTimeout property
- Port property
- CoordinatorShutdownMode property
- ServerTimeout property
- AllowedBrowsingFolders property
- CoordinatorCancelCount property
- DataDir property
- CoordinatorQueryMaxThreads property
- CoordinatorExecutionMode property
- ExternalConnectionTimeout property
- CollationName property
- EnableFast1033Locale property
- CoordinatorBuildMaxThreads property
- Language property
- StatisticsStoreSize property
- RepositoryConnectionString property
ms.assetid: 88a8117c-396a-469f-a62d-c6f262504021
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b833fe2710ce04cb4a0c8b08fedc9a882c19add
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069030"
---
# <a name="general-properties"></a>Общие свойства
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] поддерживают свойства сервера, перечисленные в следующих таблицах. В этом разделе описываются свойства сервера из файла msmdsrv.ini, которые не отнесены к тому или иному определенному разделу, например Security (безопасность), Network (сеть) или ThreadPool (пул потоков). Дополнительные сведения о дополнительных свойствах сервера и об их настройке см. в разделе [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Применимо к:** Многомерный и Табличный режим сервера, если не указано иное  
  
## <a name="non-specific-category"></a>Общая категория  
 `AdminTimeout`  
 Свойство с 32-разрядным целочисленным значением со знаком, определяющее время ожидания администратора (в секундах). Это дополнительное свойство следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Значение этого свойства по умолчанию равно нулю (0), то есть отсутствует время ожидания.  
  
 `AllowedBrowsingFolders`  
 Строковое свойство, указывающее в списке с разделителями папки, которые можно просматривать при сохранении, открытии и нахождении файлов в диалоговых окнах служб Analysis Services. Учетная запись служб Analysis Services должна иметь разрешения на чтение и запись на все добавленные в список папки.  
  
 `BackupDir`  
 Строковое свойство, определяющее имя каталога для хранения файлов резервных копий по умолчанию в случае путь не указан как часть команды Backup.  
  
 `CollationName`  
 Строковое свойство, определяющее параметры сортировки сервера. Дополнительные сведения см. в разделе [Языки и параметры сортировки (службы Analysis Services)](../languages-and-collations-analysis-services.md).  
  
 `CommitTimeout`  
 Целочисленное свойство, указывающее время в миллисекундах, в течение которого сервер будет ожидать получения блокировки записи для фиксации транзакции. Период ожидания часто бывает необходим из-за того, что серверу приходится дожидаться снятия других блокировок, прежде чем он сможет установить блокировку записи, которая фиксирует транзакцию.  
  
 Значение этого свойства по умолчанию равно нулю (0), то есть сервер ожидает бесконечно. Дополнительные сведения о связанных с блокировкой свойствах см. в [руководстве по использованию служб SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 `CoordinatorBuildMaxThreads`  
 Свойство с 32-разрядным целочисленным значением со знаком, определяющее максимальное количество потоков, назначенных для создания индексов секций. Увеличьте это значение, чтобы ускорить индексацию секций за счет использования памяти. Дополнительные сведения об этом свойстве см. в [Руководстве по использованию служб SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 `CoordinatorCancelCount`  
 Свойство с 32-разрядным целочисленным значением со знаком, определяющее, как часто сервер должен проверять возникновение события Cancel (на основе внутреннего счетчика итераций). Уменьшите это значение, чтобы чаще проверять событие Cancel за счет общей производительности.  
  
 Свойство `CoordinatorCancelCount` не учитывается в табличном режиме сервера.  
  
 `CoordinatorExecutionMode`  
 Свойство с 32-разрядным целочисленным значением со знаком, определяющее максимальное количество параллельных операций, которые сервер пытается выполнить, включая обработку и запросы. Ноль (0) указывает, что сервер принимает решение на основе внутреннего алгоритма. Положительное число указывает общее количество операций. Отрицательное число с обратным знаком указывает максимальное количество операций на процессор.  
  
 Свойство `CoordinatorExecutionMode` не учитывается в табличном режиме сервера.  
  
 Значение этого свойства по умолчанию равно -4, то есть сервер ограничен 4 параллельными операциями на процессор. Дополнительные сведения об этом свойстве см. в [Руководстве по использованию служб SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 `CoordinatorQueryMaxThreads`  
 Свойство с 32-разрядным целочисленным значением со знаком, определяющее максимальное число потоков на сегмент секции во время разрешения запроса. Чем меньше число одновременных пользователей, тем выше может быть это значение за счет использования памяти. И наоборот, это значение следует уменьшить при большом количестве одновременных пользователей.  
  
 `CoordinatorShutdownMode`  
 Логическое свойство, определяющее режим отключения координатора. Это дополнительное свойство следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `DataDir`  
 Строковое свойство, определяющее имя папки, в которой хранятся данные.  
  
 `DeploymentMode`  
 Определяет контекст работы экземпляра сервера служб Analysis Services. Это свойство называется «режим сервера» в диалоговых окон, сообщений и документации. Это свойство настраивается при установке SQL Server в соответствии с режимом сервера, выбранным при установке служб Analysis Services. Это свойство следует рассматривать исключительно как внутреннее и всегда использовать в нем значение, указанное программой установки.  
  
 Ниже приведены допустимые значения для этого свойства.  
  
|Значение|Описание|  
|-----------|-----------------|  
|0|Это значение по умолчанию. Оно задает многомерный режим, используемый для обслуживания многомерных баз данных с хранилищем MOLAP, HOLAP и ROLAP, а также с моделями интеллектуального анализа данных.|  
|1|Указывает экземпляры служб Analysis Service, установленные в составе развертывания PowerPivot для SharePoint. Не следует изменять свойство режима развертывания экземпляра служб Analysis Services, который входит в состав установки PowerPivot для SharePoint. Если изменить режим, данные PowerPivot больше не будут выполняться на сервере.|  
|2|Задает табличный режим, используемый для размещения табличных шаблонов баз данных, использующих хранение в памяти или хранилище DirectQuery.|  
  
 Это монопольные режимы. На сервере, где настроен табличный режим, не могут работать базы данных служб Analysis Services, содержащие кубы и измерения. Если позволяет оборудование компьютера, можно установить на одном компьютере несколько экземпляров служб Analysis Services и настроить для каждого экземпляра свой режим развертывания. Следует помнить, что службы Analysis Services являются ресурсоемким приложением. Развертывание нескольких экземпляров на одном компьютере рекомендуется только для мощных серверов.  
  
 `EnableFast1033Locale`  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `ExternalCommandTimeout`  
 Целочисленное свойство, определяющее время ожидания в секундах для команд, выданных внешним серверам, включая реляционные источники данных и внешние серверы служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Значение данного свойства по умолчанию составляет 3600 (секунд).  
  
 `ExternalConnectionTimeout`  
 Целочисленное свойство, определяющее время ожидания в секундах для создания соединений с внешними серверами, включая реляционные источники данных и внешние серверы служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Это свойство не учитывается, если в строке подключения указано время ожидания соединения.  
  
 Значение данного свойства по умолчанию составляет 60 (секунд).  
  
 `ForceCommitTimeout`  
 Целочисленное свойство, задающее время ожидания в миллисекундах для операции фиксации записи до отмены других команд, предшествующих текущей команде, в том числе выполняемым запросам. Это обеспечивает выполнение фиксации транзакции за счет отмены таких операций с более низким приоритетом, как запросы.  
  
 Значение этого свойства по умолчанию равно 30 секундам (30 000 миллисекундам), то есть другие команды не используют время ожидания, пока время ожидания фиксации транзакции не достигнет 30 секунд.  
  
> [!NOTE]  
>  Запросы и процессы, отмененные этим событием, будут выдавать следующее сообщение об ошибке: "`Server: The operation has been cancelled`".  
  
 Дополнительные сведения об этом свойстве см. в [Руководстве по использованию служб SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
> [!IMPORTANT]  
>  `ForceCommitTimeout` применяется к командам обработки куба и операциям обратной записи.  
  
 `IdleConnectionTimeout`  
 Целочисленное свойство, задающее время ожидания в секундах для неактивных соединений.  
  
 Значение этого свойства по умолчанию равно нулю (0), то есть время ожидания соединения не используется.  
  
 `IdleOrphanSessionTimeout`  
 Целочисленное свойство определяющее время в секундах для хранения потерянных сеансов в памяти. Потерянный сеанс — это сеанс, с которым не связано соединение. Значение по умолчанию — 120 секунд.  
  
 `InstanceVisible`  
 Логическое свойство, указывающее, является ли экземпляр сервера видимым для запросов к экземпляру от службы обозревателя SQL Server. Значение по умолчанию равно True. Если присвоить ему значение false, то экземпляр будет невидим для обозревателя SQL Server.  
  
 `Language`  
 Строковое свойство, определяющее язык, включая сообщения об ошибках и форматирование чисел. Это свойство переопределяет свойство CollationName.  
  
 Значение этого свойства по умолчанию отсутствует, то есть язык определяется свойством CollationName.  
  
 `LogDir`  
 Строковое свойство, определяющее имя папки, в которой хранятся журналы сервера. Данное свойство применяется только тогда, когда для ведения журнала используются дисковые файлы, а не таблицы баз данных (настройка по умолчанию).  
  
 `MaxIdleSessionTimeout`  
 Целочисленное свойство, определяющее максимальное время ожидания в секундах для бездействующего сеанса. Значение по умолчанию — нуль (0). Оно означает, что время ожидания сеансов не истекает никогда. Однако бездействующие сеансы все равно будут удаляться, если для сервера действуют ограничения ресурсов.  
  
 `MinIdleSessionTimeout`  
 Целочисленное свойство, определяющее минимальное время ожидания для бездействующего сеанса (в секундах). Значение по умолчанию — 2700 секунд. После истечения этого времени серверу разрешается закончить сеанс простоя, но только если требуется память.  
  
 `Port`  
 Целочисленное свойство, определяющее номер порта, на котором сервер прослушивает соединения клиентов. Если это свойство не задано, то сервер динамически находит первый неиспользуемый порт.  
  
 Значение этого свойства по умолчанию равно нулю (0), то есть по умолчанию используется порт 2383. Дополнительные сведения о настройке порта см. в разделе [Настройка брандмауэра Windows на разрешение доступа к службам Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 `ServerTimeout`  
 Целое число, определяющее время ожидания в секундах для запросов. Значение по умолчанию равно 3600 секундам (или 60 минутам). Нуль (0) означает, что время ожидания запросов не истекает.  
  
 `TempDir`  
 Строковое свойство, задающее расположение для сохранения временных файлов во время обработки, восстановления и других действий. Значение этого свойства по умолчанию определяется настройкой. Если свойство не задано, то по умолчанию используется папка Data.  
  
## <a name="requestprioritization-category"></a>Категория RequestPrioritization  
 `Enabled`  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `StatisticsStoreSize`  
 Дополнительное свойство, которое следует изменять только под руководством службы поддержки [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>См. также  
 [Настройка свойств сервера в службах Analysis Services](server-properties-in-analysis-services.md)   
 [Определение режима работы сервера экземпляра служб Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
