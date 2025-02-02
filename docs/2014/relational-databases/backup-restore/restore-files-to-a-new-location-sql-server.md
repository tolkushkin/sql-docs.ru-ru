---
title: Восстановление файлов в новое место (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring files [SQL Server], how-to topics
- restoring databases [SQL Server], moving
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
ms.assetid: b4f4791d-646e-4632-9980-baae9cb1aade
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b30322bb48cfff6e0bca092d72aa9d5ad0990948
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875074"
---
# <a name="restore-files-to-a-new-location-sql-server"></a>Восстановление файлов в новое место (SQL Server)
  В этом разделе описано, как восстановить файлы в новом расположении в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы**  
  
     [Ограничения](#Restrictions)  
  
     [безопасность](#Security)  
  
-   **Восстановление файлов в новом расположении с помощью:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Системный администратор, восстанавливающий файлы, должен быть единственным лицом, использующим восстанавливаемую базу данных в данный момент.  
  
-   Инструкция RESTORE недопустима в явной или неявной транзакции.  
  
-   Перед началом восстановления файлов по модели полного восстановления или модели восстановления с неполным протоколированием необходимо выполнить резервное копирование активного журнала транзакций (который называется заключительным фрагментом журнала). Дополнительные сведения см. в разделе [Создание резервной копии журнала транзакций (SQL Server)](back-up-a-transaction-log-sql-server.md).  
  
-   Чтобы восстановить зашифрованную базу данных, необходимо иметь доступ к сертификату или асимметричному ключу, который использовался для шифрования базы данных. Без сертификата или асимметричного ключа восстановить базу данных нельзя. Поэтому сертификат, используемый для шифрования ключа шифрования базы данных, должен храниться в течение всего времени, пока есть необходимость в резервной копии. Дополнительные сведения см. в статье [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Если восстанавливаемая база данных не существуют, для выполнения инструкции RESTORE у пользователя должны быть разрешения CREATE DATABASE. Если база данных существует, разрешения на выполнение инструкции RESTORE по умолчанию предоставлены членам предопределенных ролей сервера **sysadmin** и **dbcreator** , а также владельцу базы данных (**dbo**) (для параметра FROM DATABASE_SNAPSHOT база данных всегда существует).  
  
 Разрешения на выполнение инструкции RESTORE даются ролям, в которых данные о членстве всегда доступны серверу. Так как членство в предопределенной роли базы данных может быть проверено только тогда, когда база данных доступна и не повреждена, что не всегда имеет место при выполнении инструкции RESTORE, члены предопределенной роли базы данных **db_owner** не имеют разрешений RESTORE.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-restore-files-to-a-new-location"></a>Восстановление файлов и групп файлов в новое место  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], разверните его, а затем разверните узел **Базы данных**.  
  
2.  Щелкните правой кнопкой мыши нужную базу данных, наведите указатель на пункт **Задачи**, а затем выберите пункты **Восстановить**и **Файлы и файловые группы**.  
  
3.  На странице **Общие** в списке **В базу данных** введите имя восстанавливаемой базы данных. Можно ввести новую базу данных или выбрать уже существующую из раскрывающегося списка. Список включает все базы данных на сервере кроме системных баз данных **master** и **tempdb**.  
  
4.  Чтобы указать источник и расположение восстанавливаемых резервных наборов данных, выберите один из следующих вариантов.  
  
    -   **Из базы данных**  
  
         Введите имя базы данных в списке. Данный список содержит только базы данных, резервное копирование которых было выполнено в соответствии с журналом резервного копирования **msdb** .  
  
    -   **С устройства**  
  
         Нажмите кнопку обзора. В диалоговом окне **Указание устройств резервного копирования** выберите один из перечисленных типов устройств в списке **Тип носителя резервной копии** . Чтобы выбрать одно или несколько устройств в списке **Носитель резервной копии** , нажмите кнопку **Добавить**.  
  
         После добавления нужных устройств в списке **Носитель резервной копии** нажмите кнопку **ОК** для возвращения на страницу **Общие** .  
  
5.  В сетке **Выберите резервные наборы данных для восстановления** выберите нужные резервные наборы. В этой сетке отображаются резервные копии, доступные в указанном месте. По умолчанию предлагается план восстановления. Чтобы переопределить предложенный план восстановления, можно изменить выбранные элементы в сетке. Если выбор каких-то резервных копий отменяется, то автоматически отменяется и выбор зависящих от них резервных копий.  
  
    |Заголовок столбца|Значения|  
    |-----------------|------------|  
    |**Восстановить**|Установленные флажки обозначают резервные наборы данных, отмеченные для восстановления.|  
    |**Name**|Имя резервного набора данных.|  
    |**Тип файла**|Указывает тип данных в резервной копии: **Данные**, **журнала**, или **данные Filestream**. Данные, содержащиеся в таблицах, хранятся в файлах типа **Данные** . Данные журнала транзакций хранятся в файлах типа **Журнал** . Данные больших двоичных объектов (BLOB), которые хранятся в файловой системе, находятся в файлах типа **Данные Filestream** .|  
    |**Тип**|Тип выполненного резервного копирования: **Полное**, **Разностное**или **Журнал транзакций**.|  
    |**Server**|Имя экземпляра ядра СУБД, выполнившего операцию резервного копирования.|  
    |**Логическое имя файла**|Логическое имя файла.|  
    |**База данных**|Имя базы данных, участвовавшей в операции резервного копирования.|  
    |**Дата начала**|Дата и время начала операции резервного копирования, указанные в региональных настройках клиента.|  
    |**Дата завершения**|Дата и время завершения операции резервного копирования, указанные в формате, соответствующем региональным настройкам клиента.|  
    |**Размер**|Размер резервного набора данных в байтах.|  
    |**Имя пользователя**|Имя пользователя, выполнившего операцию резервного копирования.|  
  
6.  На панели **Выбор страницы** щелкните **Параметры** .  
  
7.  В сетке **Восстановить файлы базы данных как** укажите новое расположение для перемещаемых файлов.  
  
    |Заголовок столбца|Значения|  
    |-----------------|------------|  
    |**Имя исходного файла**|Полный путь исходного файла резервной копии.|  
    |**Тип файла**|Указывает тип данных в резервной копии: **Данные**, **журнала**, или **данные Filestream**. Данные, содержащиеся в таблицах, хранятся в файлах типа **Данные** . Данные журнала транзакций хранятся в файлах типа **Журнал** . Данные больших двоичных объектов (BLOB), которые хранятся в файловой системе, находятся в файлах типа **Данные Filestream** .|  
    |**Восстановить как**|Полный путь к файлу базы данных, который нужно восстановить. Чтобы указать новый восстанавливаемый файл, щелкните текстовое поле и измените предложенные путь и имя файла. Изменение пути или имени файла в столбце **Восстановить как** равнозначно использованию параметра MOVE в инструкции RESTORE языка [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-restore-files-to-a-new-location"></a>Восстановление файлов и групп файлов в новое место  
  
1.  При необходимости выполните инструкцию RESTORE FILELISTONLY, чтобы выяснить число и имена файлов в полной резервной копии базы данных.  
  
2.  Для восстановления полной резервной копии базы данных выполните инструкцию RESTORE DATABASE, указав:  
  
    -   Имя базы данных для восстановления.  
  
    -   Устройство резервного копирования, откуда будет восстановлена полная резервная копия.  
  
    -   Предложение MOVE для каждого восстанавливаемого в новое место файла.  
  
    -   Предложение NORECOVERY.  
  
3.  Если файлы были изменены после создания резервной копии, выполните инструкцию RESTORE LOG для применения резервной копии журнала транзакций, указав следующее:  
  
    -   Имя базы данных, к которой будет применен журнал транзакций.  
  
    -   Устройство резервного копирования, с которого будет восстановлена резервная копия журнала транзакций.  
  
    -   Предложение NORECOVERY, если существует другая резервная копия журналов транзакций для применения после текущего; в противном случае укажите предложение RECOVERY.  
  
         Резервные копии журналов транзакций, в случае их использования, должны включать в себя промежуток времени, в течение которого создавались резервные копии файлов и файловых групп.  
  
###  <a name="TsqlExample"></a> Примеры (Transact-SQL)  
 В этом примере восстанавливаются два файла базы данных `MyNwind` , первоначально находившиеся на диске C, в новое место на диске D. Также будут применены два журнала транзакций для восстановления базы данных на текущий момент времени. Количество восстанавливаемых файлов базы данных, а также их логические и физические имена можно определить с помощью инструкции `RESTORE FILELISTONLY` .  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
RESTORE FILELISTONLY  
   FROM MyNwind_1;  
-- Restore the files for MyNwind.  
RESTORE DATABASE MyNwind  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   MOVE 'MyNwind_data_1' TO 'D:\MyData\MyNwind_data_1.mdf',   
   MOVE 'MyNwind_data_2' TO 'D:\MyData\MyNwind_data_2.ndf';  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Восстановление резервной копии базы данных &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Копирование баз данных путем создания и восстановления резервных копий](../databases/copy-databases-with-backup-and-restore.md)   
 [Восстановление файлов и файловых групп (SQL Server)](restore-files-and-filegroups-sql-server.md)  
  
  
