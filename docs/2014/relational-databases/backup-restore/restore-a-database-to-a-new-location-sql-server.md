---
title: Восстановление базы данных в новое место (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], moving
- database restores [SQL Server], creating new databases
- restoring [SQL Server], with move
- restoring databases [SQL Server], creating new databases
- database backups [SQL Server], creating new database from
- backing up databases [SQL Server], creating new database from
- restoring databases [SQL Server], renaming
- database creation [SQL Server], restoring with move
ms.assetid: 4da76d61-5e11-4bee-84f5-b305240d9f42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7a50004cfb39b93ecd0c144fb0d92d37545c83ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62921184"
---
# <a name="restore-a-database-to-a-new-location-sql-server"></a>Восстановление базы данных в новое место (SQL Server)
  В этом разделе описано, как восстановить базу данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в новую папку и при необходимости переименовать ее в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Эта процедура позволяет переместить базу данных по новому пути каталога или создать копию базы данных на том же или другом экземпляре сервера.  
  
 **В этом разделе**  
  
-   **Перед началом работы**  
  
     [Ограничения](#Restrictions)  
  
     [Предварительные требования](#Prerequisites)  
  
     [Рекомендации](#Recommendations)  
  
     [безопасность](#Security)  
  
-   **Чтобы восстановить базу данных в новое расположение и при необходимости ее переименование, с помощью:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [Связанные задачи](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   При восстановлении базы данных из полной резервной копии системный администратор должен быть единственным пользователем, работающим с базой данных.  
  
###  <a name="Prerequisites"></a> Предварительные требования  
  
-   Модель восстановления с полным резервным копированием или с неполным протоколированием регламентирует, что перед восстановлением базы данных необходимо создать резервную копию активного журнала транзакций. Дополнительные сведения см. в статье [Создание резервной копии журнала транзакций (SQL Server)](back-up-a-transaction-log-sql-server.md)).  
  
###  <a name="Recommendations"></a> Рекомендации  
  
-   Чтобы восстановить зашифрованную базу данных, необходимо иметь доступ к сертификату или асимметричному ключу, который использовался для шифрования базы данных. Без сертификата или асимметричного ключа восстановить базу данных нельзя. Поэтому сертификат, используемый для шифрования ключа шифрования базы данных, должен храниться в течение всего времени, пока есть необходимость в резервной копии. Дополнительные сведения см. в статье [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
-   Дополнительные сведения о перемещении базы данных см. в разделе [Копирование баз данных путем создания и восстановления резервных копий](../databases/copy-databases-with-backup-and-restore.md).  
  
-   После восстановления базы данных [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] или более поздней версии в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] база данных автоматически обновляется. Как правило, база данных сразу становится доступной. Но если база данных [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] содержит полнотекстовые индексы, при обновлении будет произведен их импорт, сброс или повторное создание в зависимости от установленного значения свойства сервера  **upgrade_option** . Если при обновлении выбран режим импорта (**upgrade_option** = 2) или перестроения (**upgrade_option** = 0), полнотекстовые индексы во время обновления будут недоступны. В зависимости от объема индексируемых данных процесс импорта может занять несколько часов, а перестроение — в несколько (до десяти) раз больше. Обратите внимание, что если для обновления выбран режим «Импортировать», а полнотекстовый каталог недоступен, то связанные с ним полнотекстовые индексы будут перестроены. Чтобы изменить значение свойства сервера **upgrade_option** , следует использовать процедуру [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql).  
  
###  <a name="Security"></a> безопасность  
 В целях безопасности рекомендуется не присоединять и не восстанавливать базы данных, полученные из неизвестных или ненадежных источников. В этих базах данных может содержаться вредоносный код, вызывающий выполнение непредусмотренных инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] или появление ошибок из-за изменения схемы или физической структуры базы данных. Перед тем как использовать базу данных, полученную из неизвестного или ненадежного источника, выполните на тестовом сервере инструкцию [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) для этой базы данных, а также изучите исходный код в базе данных, например хранимые процедуры и другой пользовательский код.  
  
####  <a name="Permissions"></a> Permissions  
 Если восстанавливаемая база данных не существуют, для выполнения инструкции RESTORE у пользователя должны быть разрешения CREATE DATABASE. Если база данных существует, разрешения на выполнение инструкции RESTORE по умолчанию предоставлены членам предопределенных ролей сервера **sysadmin** и **dbcreator** , а также владельцу базы данных (**dbo**).  
  
 Разрешения на выполнение инструкции RESTORE даются ролям, в которых данные о членстве всегда доступны серверу. Так как членство в предопределенной роли базы данных может быть проверено только тогда, когда база данных доступна и не повреждена, что не всегда имеет место при выполнении инструкции RESTORE, члены предопределенной роли базы данных **db_owner** не имеют разрешений RESTORE.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-restore-a-database-to-a-new-location-and-optionally-rename-the-database"></a>Восстановление базы данных в новую папку и при необходимости ее переименование  
  
1.  После подключения к соответствующему экземпляру компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]в обозревателе объектов разверните дерево сервера, щелкнув имя сервера.  
  
2.  Щелкните правой кнопкой мыши элемент **Базы данных**, а затем выберите пункт **Восстановить базу данных**. Откроется диалоговое окно **Восстановление базы данных** .  
  
3.  Чтобы указать источник и расположение восстанавливаемых резервных наборов данных, используйте страницу **Общие** , раздел **Источник** . Выберите один из следующих вариантов.  
  
    -   **База данных**  
  
         Выберите из раскрывающегося списка базу данных для восстановления. Данный список содержит только базы данных, резервное копирование которых было выполнено в соответствии с журналом резервного копирования **msdb** .  
  
    > [!NOTE]  
    >  Если резервная копия была получена с другого сервера, на целевом сервере не будет журнала резервного копирования для указанной базы данных. В этом случае щелкните пункт **Устройство** , чтобы вручную указать файл или устройство для восстановления.  
  
    1.  **Устройство**  
  
         Нажмите кнопку обзора (**...**), после чего откроется диалоговое окно **Выбор устройств резервного копирования** . В окне **Тип носителя резервной копии** выберите один из перечисленных типов устройств. Чтобы выбрать одно или несколько устройств в окне **Носитель резервной копии** , нажмите кнопку **Добавить**.  
  
         После добавления нужных устройств в списке **Носитель резервной копии** нажмите кнопку **ОК** для возвращения на страницу **Общие** .  
  
         В **источника: Устройство: База данных** выберите имя базы данных, из которой нужно восстановить резервные копии.  
  
         **Примечание.** Этот список доступен, только если выбрано **Устройство** . Будут выбраны только те базы данных, резервные копии которых доступны на выбранном устройстве.  
  
4.  В разделе **Назначение** , в поле **База данных** автоматически появится имя базы данных для восстановления. Для изменения имени базы данных введите новое имя в окно **База данных** .  
  
5.  В поле **Восстановить до** оставьте значение по умолчанию **До последней выбранной резервной копии** или щелкните **Временную шкалу** , чтобы перейти в диалоговое окно **Временная шкала резервной копии** и выбрать вручную конкретное пороговое время восстановления. Дополнительные сведения об указании конкретного момента времени см. в разделе [Backup Timeline](backup-timeline.md) .  
  
6.  В сетке **Резервные наборы данных для восстановления** выберите нужные резервные наборы. В этой сетке отображаются резервные копии, доступные в указанном месте. По умолчанию предлагается план восстановления. Чтобы переопределить предложенный план восстановления, можно изменить выбранные элементы в сетке. Выбор всех резервных копий, которые зависят от восстановления более ранних копий, отменяется автоматически, как только отменяется выбор более ранних копий.  
  
     Дополнительные сведения о столбцах сетки **Восстанавливаемые резервные наборы данных** см. в разделе [Восстановление базы данных (страница "Общие")](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
7.  Чтобы указать новое расположение для файлов баз данных, выберите страницу **Файлы** , а затем нажмите кнопку **Переместить все файлы в папку**. Предоставьте новое расположение для **папки файла данных** и **папки файла журнала**. Дополнительные сведения об этой сетке см. в разделе [Восстановление базы данных (страница "Файлы")](restore-database-files-page.md).  
  
8.  На странице **Параметры** настройте параметры, если в этом есть необходимость. Дополнительные сведения об этих параметрах см. в статье [Восстановление базы данных (страница "Параметры")](restore-database-options-page.md).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-restore-a-database-to-a-new-location-and-optionally-rename-the-database"></a>Восстановление базы данных в новую папку и при необходимости ее переименование  
  
1.  При необходимости определите логическое и физическое имена файлов в резервном наборе, содержащем полную резервную копию базы данных, которую нужно восстановить. Эта инструкция возвращает список файлов базы данных и журнала, содержащихся в резервном наборе данных. Базовый синтаксис:  
  
     RESTORE FILELISTONLY FROM *<устройство_резервного_копирования>* WITH FILE = *номер_файла_резервного_набора*  
  
     В этом случае аргумент *номер_файла_резервного_набора* указывает позицию резервной копии в наборе носителей. Положение резервного набора можно получить с помощью инструкции [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) . Дополнительные сведения см. в подразделе "Указание резервного набора данных" раздела [Аргументы инструкции RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
     Эта инструкция также поддерживает некоторые параметры WITH. Дополнительные сведения см. в разделе [Инструкция RESTORE FILELISTONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql).  
  
2.  Используйте инструкцию [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql) для восстановления полной резервной копии базы данных. По умолчанию файлы данных и журналов восстанавливаются в исходных местоположениях. При перемещении базы данных используйте параметр MOVE, чтобы переместить каждый файл базы данных и избежать конфликтов с существующими файлами.  
  
     Базовый синтаксис [!INCLUDE[tsql](../../includes/tsql-md.md)] для восстановления базы данных в новом месте и с новым именем:  
  
     RESTORE DATABASE *новое_имя_базы_данных*  
  
     FROM *устройство_резервного_копирования* [ ,...*n* ]  
  
     [ WITH  
  
     {  
  
     [ **RECOVERY** | NORECOVERY ]  
  
     [ , ] [ FILE ={ *номер_файла_резервного_набора* | @*номер_файла_резервного_набора* } ]  
  
     [ , ] MOVE '*логическое_имя_файла_в_резервной_копии*' TO '*имя_файла_в_операционной_системе*' [ ,...*n* ]  
  
     }  
  
     ;  
  
    > [!NOTE]  
    >  При подготовке к перемещению базы данных на другой диск необходимо проверить наличие достаточного места и определить потенциальные конфликты с существующими файлами. Это включает использование инструкции [RESTORE VERIFYONLY](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql) , указывающей те же параметры MOVE, которые планируется использовать в инструкции RESTORE DATABASE.  
  
     В следующей таблице аргументы инструкции RESTORE описаны применительно к восстановлению базы данных в новом месте. Дополнительные сведения об этих аргументах см. в разделе [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql).  
  
     *новое_имя_базы_данных*  
     Новое имя базы данных.  
  
    > [!NOTE]  
    >  При восстановлении базы данных на другом экземпляре сервера можно указать исходное имя базы данных вместо нового.  
  
     *устройство_резервного_копирования* [ `,`... *n* ]  
     Указывает список с разделителями-запятыми от 1 до 64 устройств резервного копирования, используемых для восстановления базы данных из резервной копии. Можно указать как физическое устройство резервного копирования, так и соответствующее логическое устройство, если оно определено. Для указания физического устройства резервного копирования используйте параметр DISK или TAPE.  
  
     {ДИСК | ЛЕНТА} `=` *имя_физического_устройства_резервного_копирования*  
  
     Дополнительные сведения см. в разделе [Устройства резервного копирования (SQL Server)](backup-devices-sql-server.md).  
  
     { **RECOVERY** | NORECOVERY }  
     Если в базе данных используется модель полного восстановления, может возникнуть необходимость применить резервные копии журналов транзакций после восстановления базы данных. В этом случае укажите параметр NORECOVERY.  
  
     В противном случае используйте параметр RECOVERY, который применяется по умолчанию.  
  
     FILE ={ *номер_файла_резервного_набора* | @*номер_файла_резервного_набора* }  
     Идентифицирует резервный набор данных для восстановления. Например, аргумент *номер_файла_резервного_набора* , равный **1** , указывает первый резервный набор данных на носителе данных резервных копий, а аргумент *номер_файла_резервного_набора* , равный **2** , указывает второй резервный набор данных. Значение *номер_файла_резервного_набора* резервного набора данных можно получить с помощью инструкции [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) .  
  
     Если этот параметр не указан, по умолчанию используется первый резервный набор на устройстве резервного копирования.  
  
     Дополнительные сведения см. в подразделе "Указание резервного набора данных" раздела [Аргументы инструкции RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
     ПЕРЕМЕСТИТЬ **"*`logical_file_name_in_backup`*"** TO **"*`operating_system_file_name`*"** [ `,`... *n* ]  
     Показывает, что файл данных или журнала, указанный параметром *логическое_имя_файла_в_резервной_копии* , следует восстановить из копии в месте, указанном параметром *имя_файла_в_операционной_системе*. Укажите инструкцию MOVE для каждого логического файла, который надо восстановить из резервного набора данных в новом месте.  
  
    |Параметр|Описание|  
    |------------|-----------------|  
    |*логическое_имя_файла_в_резервной_копии*|Указывает логическое имя файла данных или журнала в резервном наборе данных. Логическое имя файла данных или журнала в резервном наборе данных соответствует его логическому имени в базе данных на момент создания резервного набора данных.<br /><br /> Примечание. Для получения списка логических файлов из набора резервных данных следует использовать инструкцию [RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql).|  
    |*имя_файла_в_операционной_системе*|Задает новое место для файла, указанного параметром *логическое_имя_файла_в_резервной_копии*. Файл будет восстановлен в этом месте.<br /><br /> Параметр *имя_файла_в_операционной_системе* может также указать новое имя для восстановленного файла. Это необходимо, если создается копия существующей базы данных на том же экземпляре сервера.|  
    |*n*|Заполнитель, который показывает, что можно указать дополнительные инструкции MOVE.|  
  
###  <a name="TsqlExample"></a> Примеры (Transact-SQL)  
 В приведенном ниже примере создается база данных `MyAdvWorks` посредством восстановления резервной копии образца базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , в которой содержатся два файла: [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Data и [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Log. В этой базе данных используется простая модель восстановления. База данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] уже существует на экземпляре сервера, поэтому файлы в резервной копии должны быть восстановлены в новом месте. Количество и имена восстанавливаемых файлов базы данных можно определить с помощью инструкции RESTORE FILELISTONLY. Резервная копия базы данных является первым резервным набором данных на устройстве резервного копирования.  
  
> [!NOTE]  
>  В примерах резервного копирования и восстановления журнала транзакций из резервной копии, включая восстановление на момент времени, используется база данных `MyAdvWorks_FullRM`, которая создается из базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], как в следующем примере с базой данных `MyAdvWorks`. Тем не менее полученный в результате `MyAdvWorks_FullRM` базы данных необходимо изменить для использования модели полного восстановления с помощью следующих [!INCLUDE[tsql](../../includes/tsql-md.md)] инструкции: ALTER DATABASE < database_name > SET RECOVERY FULL.  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
-- AdventureWorks2012_Backup is the name of the backup device.  
RESTORE FILELISTONLY  
   FROM AdventureWorks2012_Backup;  
-- Restore the files for MyAdvWorks.  
RESTORE DATABASE MyAdvWorks  
   FROM AdventureWorks2012_Backup  
   WITH RECOVERY,  
   MOVE 'AdventureWorks2012_Data' TO 'D:\MyData\MyAdvWorks_Data.mdf',   
   MOVE 'AdventureWorks2012_Log' TO 'F:\MyLog\MyAdvWorks_Log.ldf';  
GO  
  
```  
  
 Пример создания полной резервной копии базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] см. в разделе [Создание полной резервной копии базы данных (SQL Server)](create-a-full-database-backup-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Создание полной резервной копии базы данных (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [Восстановление резервной копии базы данных &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Создание резервной копии журнала транзакций (SQL Server)](back-up-a-transaction-log-sql-server.md)  
  
-   [Восстановление резервной копии журнала транзакций (SQL Server)](restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>См. также  
 [Управление метаданными при обеспечении доступности базы данных на другом экземпляре сервера (SQL Server)](../databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Копирование баз данных путем создания и восстановления резервных копий](../databases/copy-databases-with-backup-and-restore.md)  
  
  
