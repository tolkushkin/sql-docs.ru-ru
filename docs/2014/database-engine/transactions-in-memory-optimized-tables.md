---
title: Транзакции в таблицах, оптимизированных для памяти | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2cd07d26-a1f1-4034-8d6f-f196eed1b763
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc72eeeb154749b0e889b495fab79bb8bf86db10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843110"
---
# <a name="transactions-in-memory-optimized-tables"></a>Транзакции в таблицах, оптимизированных для памяти
  Управление версиями строк в дисковых таблицах (с использованием уровня изоляции моментальных снимков или параметра READ_COMMITTED_SNAPSHOT) предоставляет форму управления оптимистичным параллелизмом. Модули чтения и записи не блокируют друг друга. При использовании оптимизированных для памяти таблиц модули записи не блокируют модули записи. При управлении версиями строк в дисковых таблицах одна транзакция блокирует строку и попытки обновления строки параллельными транзакциями блокируются. При использовании оптимизированных для памяти таблиц блокировки не применяются. Вместо этого, если две транзакции пытаются обновить одну строку, возникает конфликт «запись-запись» (ошибка 41302).  
  
 В отличие от дисковых таблиц оптимизированные для памяти таблицы обеспечивают управление оптимистичным параллелизмом с более высоким уровнем изоляции — REPEATABLE READ и SERIALIZABLE. Для обеспечения уровней изоляции блокировки не применяются. Вместо этого в конце транзакции выполняется проверка, чтобы убедиться, что не нарушены допущения операций чтения с возможностью повторения или сериализации. Если допущения нарушены, транзакция прерывается. Дополнительные сведения см. в разделе [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md).  
  
 Важная семантика транзакций для оптимизированных для памяти таблиц:  
  
-   Управление версиями  
  
-   Изоляции транзакции на основе моментального снимка  
  
-   Optimistic  
  
-   Обнаружение конфликтов  
  
 Каждая из этих семантик описана в следующих разделах.  
  
## <a name="multi-versioning-in-memory-optimized-tables"></a>Управление версиями в оптимизированных для памяти таблицах  
 Строки оптимизированных для памяти таблиц могут иметь различные версии. Потенциально параллельные транзакции могут получать разные версии одной и той же строки.  
  
 Данные в оптимизированных для памяти таблицах основаны на использовании версий. Для любой строки могут существовать различные версии строк, действительные в разные моменты времени. Дисковые таблицы поддерживают различные версии строк, если параметры READ_COMMITTED_SNAPSHOT или ALLOW_SNAPSHOT_ISOLATION установлены в значение ON. В оптимизированных для памяти таблицах всегда поддерживаются различные версии строк, даже если параметры READ_COMMITTED_SNAPSHOT и ALLOW_SNAPSHOT_ISOLATION имеют значение OFF. Версии строк оптимизированных для памяти таблиц не содержатся в базе данных tempdb. Вместо этого, версии строк хранятся встроенными в составе оптимизированных для памяти структур данных для хранения строк в памяти.  
  
## <a name="snapshot-based-transaction-isolation-for-memory-optimized-tables"></a>Изоляция транзакций на основе моментального снимка у оптимизированных для памяти таблиц  
 Все операции в одной транзакции используют один и тот же транзакционно согласованный моментальный снимок оптимизированных для памяти таблиц. Изоляция всех транзакций у оптимизированных для памяти таблиц выполняется на основе моментальных снимков. Например, транзакция, использующая уровень изоляции SERIALIZABLE для доступа к оптимизированным для памяти таблицам, выполняет все операции на том же транзакционно согласованном моментальном снимке.  
  
 Транзакции, которые обращаются к оптимизированным для памяти таблицам, используют управление версиями строк для получения транзакционно согласованного моментального снимка строк в таблицах. Данные, считанные любой инструкцией транзакции, будут согласованы на уровне транзакции с версией данных, существовавших во время запуска транзакции. Поэтому все изменения, сделанные параллельно выполняемыми транзакциями, невидимы для инструкций в текущей транзакции.  
  
## <a name="optimistic-concurrency-control-for-memory-optimized-tables"></a>Управление оптимистичным параллелизмом у оптимизированных для памяти таблиц  
 Конфликты и ошибки происходят редко и транзакции для оптимизированных для памяти таблиц предполагают, что конфликты с параллельными транзакциями отсутствуют и операции выполняются успешно. Транзакции не принимают блокировки или кратковременные блокировки для оптимизированных для памяти таблиц, чтобы гарантировать уровень изоляции транзакции. Модули записи не блокируют модули чтения. Модули записи не блокируют модули записи. Вместо этого транзакции продолжается с допущением (оптимистическим), что конфликтов с другими транзакциями не существует. Отказ от использования блокировок и кратковременных блокировок и от ожидания завершения обработки тех же строк другими транзакциями улучшает производительность.  
  
 Кроме того, если транзакция (TxA) считывает строки, которые были вставлены или изменены другой транзакцией (TxB), которая находится в процессе фиксации, первая транзакция будет предполагать, что другая транзакция будет зафиксирована вместо ожидания завершения этой операции. В этом случае транзакция TxA примет зависимость от фиксации транзакции TxB.  
  
## <a name="conflict-detection-validation-and-commit-dependency-checks"></a>Обнаружение и проверка конфликтов и проверки зависимости фиксации  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] обнаруживает конфликты между параллельными транзакциями, а также нарушения уровня изоляции и отменяет одну из конфликтующих транзакций. Эту транзакцию необходимо будет повторить. (Дополнительные сведения см. в разделе [Guidelines for Retry Logic для транзакции на оптимизированных для памяти таблицах](../relational-databases/in-memory-oltp/memory-optimized-tables.md).)  
  
 Система оптимистически предполагает отсутствие конфликтов и нарушений изоляции транзакции. При возникновении любых конфликтов, которые могут стать причиной несоответствия в базе данных или нарушить изоляцию транзакции, они обнаруживаются, а транзакция прерывается.  
  
 При обнаружении конфликта транзакция завершается и клиенту необходимо повторить попытку.  
  
 В следующей таблице перечислены условия ошибки, относящиеся к транзакциям, которые обращаются к оптимизированным для памяти таблицам.  
  
### <a name="error-conditions-for-transactions-accessing-memory-optimized-tables"></a>Условия возникновения ошибок для транзакций при доступе к оптимизированным для памяти таблицам.  
  
|Ошибка|Сценарий|  
|-----------|--------------|  
|Конфликт записи. Попытка обновить запись, которая была обновлена со времени запуска транзакции.|UPDATE или DELETE строку, которая была обновлена или удалена параллельной транзакцией.|  
|Ошибка проверки операций чтения с возможностью повторения.|Строка, которая была прочтена транзакцией, изменилась (обновлена или удалена) с момента запуска транзакции. Проверка повторяющихся операций чтения обычно производится при работе с уровнями изоляции транзакции REPEATABLE READ и SERIALIZABLE.|  
|Ошибка сериализуемой проверки.|Новая строка (фантом) была вставлена в один из диапазонов просмотра в транзакции со времени начала транзакции. Строка была бы видимой для транзакции, если бы она была зафиксирована в базе данных до запуска транзакции. Проверка SERIALIZABLE обычно используется при работе с изоляцией SERIALIZABLE и при проверке ограничений PRIMARY KEY.|  
|Ошибка зависимости фиксации.|Транзакция приняла зависимость от другой транзакции, которой не удалось выполнить фиксацию, по причине одной из ошибок, перечисленных в этой таблице, состояния нехватки памяти или из-за ошибки фиксации в журнале транзакций. Эта ошибка может произойти как с транзакциями для чтения и записи, так и только для чтения.|  
  
### <a name="transaction-lifetime"></a>Время существования транзакций  
 Ошибки, упомянутые в предыдущей таблице, могут возникнуть в различные моменты существования транзакции. На следующем рисунке показаны этапы транзакции, которая обращается к оптимизированным для памяти таблицам.  
  
 ![Время существования транзакции. ](../../2014/database-engine/media/hekaton-transactions.gif "Временем существования транзакции.")  
Время существования транзакций, которые обращаются к оптимизированным для памяти таблицам.  
  
#### <a name="regular-processing"></a>Обычная обработка  
 Во время этого этапа выполняются инструкции [!INCLUDE[tsql](../includes/tsql-md.md)], выданные пользователем. Строки считываются из таблиц, а новые версии строк записываются в базу данных. Транзакция изолирована от всех других параллельных транзакций. Транзакция использует моментальный снимок оптимизированных для памяти таблиц, существующий на момент начала транзакции.  
  
 Операции записи в таблицы на этом этапе транзакции еще невидимы другим транзакциям, за одним исключением: обновления и удаления строк являются видимыми для обновления, а операции удаления в других транзакциях, чтобы обнаруживать конфликты записи.  
  
 Если операция обновления или удаления обнаруживает, что была обновлена или удалена строка с момента логического начала транзакции, операция завершается с ошибкой 41302. Сообщение для ошибки 41302: «Текущая транзакция пыталась обновить запись в таблице X, которая была обновлена с момента начала этой транзакции. Транзакция была прервана».  
  
 Данная ошибка приводит к прерыванию транзакции (даже если XACT_ABORT имеет значение OFF). Это значит, что должен быть выполнен откат транзакции при завершении сеанса пользователя. Поврежденные транзакции нельзя зафиксировать, они поддерживают только операции чтения, которые не записываются в журнал и не обращаются к таблицам, оптимизированным для памяти.  
  
#####  <a name="cd"></a> Зависимости фиксации  
 Во время обычной обработки транзакция может считывать строки, созданные другими транзакциями, которые находятся на этапе проверки или фиксации, но еще не зафиксированы. Строки являются видимыми, потому что время логического завершения транзакций назначено в начале этапа проверки.  
  
 Если транзакция считывает такие незафиксированные строки, то она принимает зависимость фиксации от этой транзакции. Это имеет два основных следствия.  
  
-   Транзакция не может быть зафиксирована до того, как будет зафиксирована транзакция, от которой она зависит. Другими словами, она не может перейти на этап фиксации до тех пор, пока все зависимости не будут устранены.  
  
-   Кроме того, результирующие наборы не возвращаются клиенту, пока все зависимости не будут устранены. Это не позволяет клиенту наблюдать незафиксированные данные.  
  
 Если любые зависимые транзакции не удается зафиксировать, то возникает ошибка зависимости фиксации. Это означает, что транзакция не будет зафиксирована с ошибкой 41301 («Предыдущая транзакция, от которой зависит текущая транзакция, прервана, и текущая транзакция не может быть зафиксирована»).  
  
#### <a name="validation-phase"></a>Стадия проверки  
 На этапе проверки система проверяет, что допущения, необходимые для запрошенного уровня изоляции транзакций, были истинны в период от логического начала до логического завершения транзакции.  
  
 В начале этапа проверки транзакции назначается время логического завершения. Версии строк, созданные в базе данных, становятся видимыми другим транзакциям во время логического завершения. Дополнительные сведения см. в разделе [зависимости фиксации](#cd).  
  
##### <a name="repeatable-read-validation"></a>Проверка операций чтения с возможностью повторения  
 Если уровень изоляции транзакции — REPEATABLE READ или SERIALIZABLE или таблицы доступны в режиме изоляции REPEATABLE READ или SERIALIZABLE (Дополнительные сведения см. в разделе «изоляция отдельных операций» в [транзакции Уровни изоляции](../../2014/database-engine/transaction-isolation-levels.md)), система проверяет, что операции чтения можно повторить. Это означает проверку, что версии строк, считываемых транзакцией, по-прежнему представляют собой действительные версии строк во время логического конца транзакции.  
  
 Если были обновлены или изменены какие-либо строки, транзакции не удается выполнить фиксацию с ошибкой 41305 («Текущей транзакции не удалось выполнить фиксацию из-за ошибки проверки уровня изоляции REPEATABLE READ»).  
  
 Это ошибка может также возникать при удалении таблицы после операции вставки, обновления или удаления и перед фиксацией транзакций. Это применимо только для операций вставки, обновления или удаления в хранимых процедурах, скомпилированных в собственном коде. Такие операции записи выполняются, когда интерпретация [!INCLUDE[tsql](../includes/tsql-md.md)] заставляет инструкцию DROP TABLE выполнить блокировку и ждать фиксации транзакции.  
  
##### <a name="serializable-validation"></a>Сериализуемая проверка  
 Сериализуемая проверка выполняется в двух случаях.  
  
-   Если уровень изоляции транзакции — SERIALIZABLE или доступ к таблицам выполняется в режиме изоляции SERIALIZABLE.  
  
-   Если строки вставлены в уникальный индекс, например индекс, созданный для ограничения PRIMARY KEY. Система проверяет, что не были одновременно вставлены строки с одинаковым значением ключа.  
  
 Система проверяет, что фантомные строки не были записаны в базу данных. Операции считывания, выполняемые транзакцией, оцениваются, чтобы определить, что новые строки не были вставлены в диапазоны просмотра этих операций чтения.  
  
 Вставка ключа в уникальный индекс включает неявную операцию считывания, чтобы проверить, что ключ не является дубликатом. Сериализуемая проверка для уникальных индексов гарантирует, что эти индексы не могут иметь дубликаты в случае, если две транзакции одновременно вставляют один и тот же ключ.  
  
 Если обнаружены фантомные строки, то не удалось выполнить фиксацию транзакции с ошибкой 41325 («Текущей транзакции не удалось выполнить фиксацию из-за ошибки сериализуемой проверки»).  
  
#### <a name="commit-processing"></a>Обработка фиксации  
 Если проверка завершается успешно и все зависимости транзакций разрешены, то транзакция переходит на этап обработки фиксации. Во время этого этапа записываются изменения в надежных таблицах в журнал, а журнал сохраняется на диске, чтобы обеспечить надежность. После того как запись журнала для транзакции записана на диск, управление возвращается клиенту.  
  
 Все зависимости фиксации для этой транзакции удаляются, и все транзакции, ожидавшие фиксации этой транзакции, могут быть продолжены.  
  
## <a name="limitations"></a>Ограничения  
  
-   Транзакции между базами данных не поддерживаются с таблицами, оптимизированными для памяти. Каждая транзакция, которая выполняет доступ к оптимизированным для памяти таблицам, не может обращаться более чем к одной базе данных, за исключением доступа на чтение и запись базы данных tempdb и доступа только для чтения к системной базе данных master.  
  
-   Распределенные транзакции не поддерживаются с таблицам, оптимизированными для памяти. Распределенные транзакции, запускаемые с помощью инструкции BEGIN DISTRIBUTED TRANSACTION, не могут получить доступ к оптимизированным для памяти таблицам.  
  
-   Оптимизированные для памяти таблицы не поддерживают ни один из видов блокировки. Явные блокировки через подсказки блокировки (например, TABLOCK, XLOCK, ROWLOCK) не поддерживаются с таблицами, оптимизированными для памяти.  
  
## <a name="see-also"></a>См. также  
 [Основные сведения о транзакциях с таблицами, оптимизированными для памяти](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
  
