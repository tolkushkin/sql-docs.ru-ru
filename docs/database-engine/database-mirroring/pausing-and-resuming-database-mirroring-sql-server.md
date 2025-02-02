---
title: Приостановка и возобновление зеркального отображения базы данных (SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- sessions [SQL Server], database mirroring
- resuming database mirroring
- database mirroring [SQL Server], pausing
- database mirroring [SQL Server], resuming
- pausing database mirroring
ms.assetid: c67802c6-ee8c-4cbd-a6d4-f7b80413a4ab
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 3f9506f97af3f1a276efef01f4c77d2b86f6a7de
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795338"
---
# <a name="pausing-and-resuming-database-mirroring-sql-server"></a>Приостановка и возобновление зеркального отображения базы данных (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Владелец базы данных может приостанавливать и возобновлять сеанс зеркального отображения базы данных в любое время. Приостановление сохраняет состояние сеанса, при этом приостанавливается зеркальное отображение. Во время пиковых нагрузок приостановление может способствовать повышению производительности основного сервера.  
  
 Когда сеанс приостанавливается, основная база данных остается доступной. Приостановленный сеанс зеркального отображения переходит в состояние SUSPENDED, зеркальная база данных перестает соответствовать основной, что ставит под угрозу сохранность данных в основной базе.  
  
 Рекомендуется как можно быстрее возобновить приостановленный сеанс, поскольку во время приостановки зеркального отображения базы данных журнал транзакций не может быть усечен. Таким образом, если сеанс зеркального отображения базы данных приостанавливается на долгое время, журнал транзакций может заполниться до конца, и база данных станет недоступной. Объяснение причин этого см. далее в пункте «Как приостановка и возобновление влияют на усечение журнала» данного раздела.  
  
> [!IMPORTANT]  
>  Следуя принудительному обслуживанию, зеркальное отображение приостанавливается, когда исходный основной сервер заново выполняет подключение. Возобновление зеркального отображения в данной ситуации может привести к потере данных исходным основным сервером. Дополнительные сведения о том, как действовать при возможной потере данных, см. в разделе [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 **В этом разделе.**  
  
-   [Влияние приостановки и возобновления на усечение журнала](#EffectOnLogTrunc)  
  
-   [Избежание переполнения журнала транзакций](#AvoidFullLog)  
  
-   [Связанные задачи](#RelatedTasks)  
  
##  <a name="EffectOnLogTrunc"></a> Влияние приостановки и возобновления на усечение журнала  
 Обычно при обработке в базе данных автоматической контрольной точки журнал транзакций этой базы данных усекается до этой контрольной точки после следующего резервного копирования журнала. Пока зеркальное отображение базы данных остается приостановленным, все текущие записи журнала остаются активными, поскольку основной сервер ожидает их отправки на зеркальный сервер. Неотправленные записи журнала накапливаются в журнале транзакций основной базы данных до возобновления сеанса и отправки этих записей основным сервером на зеркальный сервер.  
  
 При возобновлении сеанса основной сервер немедленно начинает отправлять накопленные записи журнала на зеркальный сервер. Когда зеркальный сервер подтверждает, что он поставил в очередь запись журнала, соответствующую самой старой автоматической контрольной точке, основной сервер усекает журнал основной базы данных до этой контрольной точки. Зеркальный сервер усекает очередь повторов до этой же записи журнала. По мере повторения этого процесса для каждой последовательной контрольной точки журнал постепенно усекается от точки к точке.  
  
> [!NOTE]  
>  Дополнительные сведения о контрольных точках и усечении журнала см. в разделе [Контрольные точки базы данных (SQL Server)](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
##  <a name="AvoidFullLog"></a> Избежание переполнения журнала транзакций  
 Если журнал заполняется до конца (достигается максимальный размер или на экземпляре сервера не хватает пространства), база данных не позволяет обновить данные. Этого можно избежать двумя способами.  
  
-   Возобновить сеанс зеркального отображения базы данных до полного заполнения журнала или расширить пространство для журнала. После возобновления сеанса зеркального отображения базы данных основной сервер отправляет накопленный активный журнал зеркальному серверу и переводит зеркальную базу данных в состояние SYNCHRONIZING. После этого зеркальный сервер сбрасывает журнал на диск и начинает его воспроизведение.  
  
-   Остановить зеркальное отображение базы данных, отключив зеркалирование.  
  
     Когда сеанс зеркального отображения не приостанавливается, а отменяется, все сведения о нем удаляются. На каждом экземпляре сервера-участника остается собственная копия базы данных. При восстановлении предыдущей копии зеркала она будет иметь расхождения с бывшей основной базой данных и будет отставать от нее на время приостановки зеркального отображения. Дополнительные сведения см. в разделе [Удаление зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Приостановление или возобновление зеркального отображения базы данных**  
  
-   [Приостановка или возобновление сеанса зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
 **Остановка зеркального отображения базы данных**  
  
-   [Удаление зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
## <a name="see-also"></a>См. также:  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [Зеркальное отображение базы данных (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Удаление зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
  
