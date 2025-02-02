---
title: Сжатие базы данных | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.shrinkdatabase.f1
helpviewer_keywords:
- shrinking databases
- databases [SQL Server], shrinking
- decreasing database size
- database shrinking [SQL Server]
- reducing database size
ms.assetid: 83afbf74-fd50-4c39-831c-b1f473a50620
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21f58cd6991b760edeefb81c37e02c617f8e09cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917011"
---
# <a name="shrink-a-database"></a>Сжатие базы данных
  В этом подразделе содержатся инструкции по сжатию базы данных при помощи обозревателя объектов [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Сжатие файлов данных позволяет освободить неиспользуемое пространство путем перемещения страниц данных с конца файла в незанятое пространство ближе к началу файла. Когда в конце файла образуется достаточно свободного места, страницы данных в конце файла могут быть освобождены и возвращены в файловую систему.  
  

  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Размер базы данных нельзя сделать меньше минимального размера базы данных. Минимальный размер — это первоначальный размер, заданный при создании базы данных, или последний размер, явно установленный операцией изменения размера файла (например, DBCC SHRINKFILE). Если, допустим, база данных была создана с размером 10 МБ и затем увеличилась до 100 МБ, ее можно сжать только до 10 МБ, даже если удалить из нее все данные.  
  
-   Невозможно сжать базу данных во время создания ее резервной копии. И наоборот, нельзя создать резервную копию базы данных во время операции сжатия.  
  
-   Инструкция DBCC SHRINKDATABASE завершится с ошибкой при обнаружении оптимизированного для памяти xVelocity индекса columnstore. Работа, выполненная до встречи с индексом columnstore, будет выполнена успешно, поэтому база данных может иметь меньший размер. Чтобы выполнить инструкцию DBCC SHRINKDATABASE, отключите все индексы columnstore до ее запуска, а затем перестройте индексы columnstore.  
  
###  <a name="Recommendations"></a> Рекомендации  
  
-   Просмотр количества свободного (нераспределенного) пространства в базе данных. Дополнительные сведения см. в разделе [Отображение данных и сведений о пространстве журнала для базы данных](display-data-and-log-space-information-for-a-database.md).  
  
-   Обратите внимание на следующие сведения при планировании сжатия базы данных.  
  
    -   Наибольший эффект от операции сжатия достигается при ее применении после операции, создающей много неиспользуемого пространства, например после усечения таблицы или удаления таблицы.  
  
    -   Большинству баз данных требуется некоторое свободное пространство для выполнения обычных ежедневных операций. Если сжатие базы данных производится регулярно, но она снова увеличивается в размерах, это означает, что место, освобожденное при сжатии, необходимо для нормальной работы. В таких случаях повторное сжатие базы данных бессмысленно.  
  
    -   Операция сжатия не избавляет от фрагментации индексов в базе данных и обычно приводит к еще более сильной фрагментации. Это еще одна причина, по которой не стоит выполнять регулярное сжатие базы данных.  
  
    -   Не следует устанавливать параметр базы данных AUTO_SHRINK в значение ON без достаточных на то оснований.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Необходимо быть членом предопределенной роли сервера **sysadmin** или предопределенной роли базы данных **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-shrink-a-database"></a>Сжатие базы данных  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]и разверните его.  
  
2.  Разверните узел **Базы данных**и щелкните правой кнопкой мыши базу данных, которую нужно сжать.  
  
3.  В меню наведите указатель на пункт **Задачи**, **Сжать**и выберите команду **База данных**.  
  
     **База данных**  
     Отображает имя выбранной базы данных.  
  
     **Выделенное в данный момент место**  
     Отображает суммарное используемое и неиспользуемое пространство для выбранной базы данных.  
  
     **Доступное свободное место**  
     Отображает суммарное свободное место для файлов журналов и данных в выбранной базе данных.  
  
     **Реорганизовать файлы перед освобождением неиспользованного места**  
     Установка данного флажка эквивалентна выполнению инструкции DBCC SHRINKDATABASE с заданием целевого процентного параметра. Снятие этого флажка равнозначно выполнению процедуры DBCC SHRINKDATABASE с параметром TRUNCATEONLY. По умолчанию при открытии диалогового окна этот флажок не установлен. Если этот флажок установлен, то пользователь должен задать целевое процентное значение.  
  
     **Максимальное свободное пространство в файлах после сжатия**  
     Введите максимальный процент свободного пространства, которое должно остаться в базе данных после ее сжатия. Допустимы значения от 0 до 99.  
  
4.  Нажмите кнопку **ОК**.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-shrink-a-database"></a>Сжатие базы данных  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере инструкция [DBCC SHRINKDATABASE](/sql/t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql) используется для уменьшения размера данных и файлов журнала в базе данных `UserDB` и для выделения `10` процентов свободного пространства в этой базе данных.  
  
 [!code-sql[DBCC#DBCC_SHRINKDB1](../../snippets/tsql/SQL14/tsql/dbcc/transact-sql/dbcc_other.sql#dbcc_shrinkdb1)]  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После сжатия базы данных  
 Данные, перемещаемые в процессе сжатия файла, могут быть разбросаны по любым доступным местам в файле. Это вызывает фрагментацию индекса и может увеличить время выполнения запросов, выполняющих поиск в диапазоне индекса. Чтобы устранить фрагментацию, предусмотрите возможность перестроения индексов файла после сжатия.  
  
## <a name="see-also"></a>См. также  
 [Сжатие файла](shrink-a-file.md)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.database_files (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [DBCC (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-transact-sql)   
 [DBCC SHRINKFILE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)   
 [Файлы и файловые группы базы данных](database-files-and-filegroups.md)  
  
  
