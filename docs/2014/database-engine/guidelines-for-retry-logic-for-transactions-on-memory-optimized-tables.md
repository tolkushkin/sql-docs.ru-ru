---
title: Рекомендации по логику повторных попыток для транзакций в таблицах, оптимизированных для памяти | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2a35c37-4449-49ee-8bba-928028f1de66
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01f719470419940b130967b7c1360c4ae0c281eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779218"
---
# <a name="guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables"></a>Рекомендации для логики повторного выполнения транзакций для таблиц, оптимизированных для памяти
  Условия ошибки, возникающие с транзакциями, которые обращаются к оптимизированным для памяти таблицам.  
  
-   41302. Текущая транзакция попыталась обновить запись, которая была изменена после начала этой транзакции.  
  
-   41305. Текущей транзакции не удалось выполнить фиксацию из-за ошибки проверки уровня изоляции REPEATABLE READ.  
  
-   41325. Текущей транзакции не удалось выполнить фиксацию из-за ошибки сериализуемой проверки.  
  
-   41301. Предыдущая транзакция, от которой зависит текущая транзакция, прервана, текущая транзакция не может быть зафиксирована.  
  
 Частая причина этих ошибок — взаимодействие одновременно выполняющихся транзакций. Общее действие для исправления — повторное выполнение транзакции.  
  
 Дополнительные сведения об этих условиях ошибок см. в разделе на обнаружение конфликтов, проверки и проверках зависимости фиксации в [транзакции в таблицах, оптимизированных для памяти](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Взаимоблокировки (код ошибки 1205) не могут возникнуть для оптимизированных для памяти таблиц. Блокировки не используются для оптимизированных для памяти таблиц. Но если приложение уже содержит логику повторных попыток для взаимоблокировок, ее можно расширить для поддержки новых кодов ошибок.  
  
## <a name="considerations-for-retrying"></a>Рекомендации для повторных попыток  
 Обычно в приложениях возникает конфликт между транзакциями и требуется реализовать логику устранения этих конфликтов. Количество обнаруженных конфликтов зависит от нескольких факторов.  
  
-   Конфликты отдельных строк. Возможность появления конфликтов растет с числом транзакций, которые пытаются обновить одну и ту же строку.  
  
-   Количество строк, считываемых транзакциями REPEATABLE READ. Чем больше строк считывается, тем выше вероятность того, что некоторые из них обновляются параллельными транзакциями. Это приводит к ошибкам проверки операций чтения с возможностью повторения.  
  
-   Размер диапазонов сканирования, используемых транзакциями SERIALIZABLE. Чем больше диапазон сканирования, тем выше вероятность того, что параллельные транзакции сформируют фантомные строки и вызовут ошибки проверки сериализации.  
  
     Приложению трудно избежать таких конфликтов, для этого нужна логика повторных попыток.  
  
> [!IMPORTANT]  
>  Транзакциям для чтения и записи, которые обращаются к оптимизированным для памяти таблицам, требуется логика повторов.  
  
### <a name="considerations-for-read-only-transactions-and-natively-compiled-stored-procedures"></a>Рекомендации для транзакций только для чтения и скомпилированные в памяти хранимых процедур  
 Транзакциям в режиме только для чтения, охватывающим выполнение одной скомпилированной в собственном коде хранимой процедуры, не требуется проверка транзакций REPEATABLE READ и SERIALIZABLE. Для транзакций только для чтения конфликты операций записи не возникают.  
  
 Однако по-прежнему могут возникать ошибки зависимости. Они реже, чем ошибки в результате конфликтов. Поэтому во многих случаях не требуется специфическая логика повторов для транзакций только для чтения, охватывающих одно выполнение скомпилированных в собственном коде хранимых процедур.  
  
### <a name="considerations-for-read-only-transactions-and-cross-container-transactions"></a>Рекомендации для транзакций только для чтения и транзакций между контейнерами  
 Транзакции между контейнерами только для чтения, которые запускаются вне контекста хранимой процедуры, скомпилированной в собственном коде, не проверяют, осуществляется ли доступ к оптимизированным для памяти таблицам с уровнем изоляции SNAPSHOT. Однако при доступе к оптимизированным для памяти таблицам в изоляции REPEATABLE READ или SERIALIZABLE проверка выполняется в момент фиксации. В этом случае может потребоваться логика повторов.  
  
 Дополнительные сведения см. в разделе о транзакциях между контейнерами в [уровни изоляции транзакций](../../2014/database-engine/transaction-isolation-levels.md).  
  
## <a name="implementing-retry-logic"></a>Реализация логики повторов  
 Как и в случае с другими транзакциями, которые обращаются к таблицам, оптимизированным для памяти, следует принять во внимание логику повторов для обработки потенциальных неполадок, например записи конфликтов (код ошибки 41302) или ошибок зависимости (код ошибки 41301). В большинстве приложений интенсивность отказов будет низкой, но все же необходимо обрабатывать ошибки, повторно выполняя транзакции. Два возможных метода реализации логики повторного выполнения:  
  
-   Клиентские повторы попыток. В общем случае повторения на стороне клиента — предпочтительный способ реализации логики повторов. Клиентское приложение перехватывает ошибку, сформированную транзакцией, и пытается повторить транзакцию. Если существующее клиентское приложение содержит логику повтора попыток для обработки взаимоблокировок, приложение можно расширить с целью обработки новых ошибок.  
  
-   Использование хранимой процедуры оболочки. Клиент вызывает интерпретированную хранимую процедуру [!INCLUDE[tsql](../includes/tsql-md.md)], которая запускает скомпилированную в собственном коде хранимую процедуру или выполняет транзакцию. Затем в процедуре оболочки используется логика try/catch для обнаружения ошибок и повторения вызова процедуры при необходимости. Возможна ситуация, при которой результаты будут возвращены клиенту до возникновения ошибки и клиент не будет располагать информацией, чтобы отбросить их. Поэтому, чтобы обезопасить себя, лучше всего использовать этот метод только с изначально скомпилированными в собственном коде хранимыми процедурами, которые не возвращают клиенту никаких результирующих наборов.  
  
 Логику повторов можно реализовать в [!INCLUDE[tsql](../includes/tsql-md.md)] или в коде приложения среднего уровня.  
  
 Существуют две возможные причины, чтобы рассматривать возможность реализации логики повторов.  
  
-   Клиентское приложение использует логику повторов для других кодов ошибок, например 1205, которую можно расширить.  
  
-   Конфликты происходят редко, и важно уменьшить сквозную задержку с помощью подготовленного выполнения. Дополнительные сведения о выполнении скомпилированных в собственном коде хранимые процедуры напрямую, см. в разделе [Natively Compiled Stored Procedures](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
 В следующем примере показана логика повторов в интерпретированной хранимой процедуре [!INCLUDE[tsql](../includes/tsql-md.md)], которая содержит вызов хранимой процедуры, скомпилированной в собственном коде, или транзакции между контейнерами.  
  
```sql  
CREATE PROCEDURE usp_my_procedure @param1 type1, @param2 type2, ...  
AS  
BEGIN  
  -- number of retries - tune based on the workload  
  DECLARE @retry INT = 10  
  
  WHILE (@retry > 0)  
  BEGIN  
    BEGIN TRY  
  
      -- exec usp_my_native_proc @param1, @param2, ...  
  
      --       or  
  
      -- BEGIN TRANSACTION  
      --   ...  
      -- COMMIT TRANSACTION  
  
      SET @retry = 0  
    END TRY  
    BEGIN CATCH  
      SET @retry -= 1  
  
      -- the error number for deadlocks (1205) does not need to be included for   
      -- transactions that do not access disk-based tables  
      IF (@retry > 0 AND error_number() in (41302, 41305, 41325, 41301, 1205))  
      BEGIN  
        -- these error conditions are transaction dooming - rollback the transaction  
        -- this is not needed if the transaction spans a single native proc execution  
        --   as the native proc will simply rollback when an error is thrown   
        IF XACT_STATE() = -1  
          ROLLBACK TRANSACTION  
  
        -- use a delay if there is a high rate of write conflicts (41302)  
        --   length of delay should depend on the typical duration of conflicting transactions  
        -- WAITFOR DELAY '00:00:00.001'  
      END  
      ELSE  
      BEGIN  
        -- insert custom error handling for other error conditions here  
  
        -- throw if this is not a qualifying error condition  
        ;THROW  
      END  
    END CATCH  
  END  
END  
```  
  
## <a name="see-also"></a>См. также  
 [Основные сведения о транзакциях в таблицах, оптимизированных для памяти](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Транзакции в таблицах, оптимизированных для памяти](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Рекомендации для уровней изоляции транзакций с таблицами, оптимизированными для памяти](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)  
  
  
