---
title: sqlmaint, программа | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- database maintenance plans [SQL Server]
- sqlmaint utility
- maintaining databases [SQL Server]
- backups [SQL Server], sqlmaint utility
- command prompt utilities [SQL Server], sqlmaint
- maintenance plans [SQL Server], command prompt
- backing up [SQL Server], sqlmaint utility
ms.assetid: 937a9932-4aed-464b-b97a-a5acfe6a50de
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2e15dbb5b7cb21d29936fce5c9b0d1f215d244ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187010"
---
# <a name="sqlmaint-utility"></a>sqlmaint, программа
  Программа**sqlmaint** выполняет заданный набор операций обслуживания с одной или несколькими базами данных. Программа **sqlmaint** используется для выполнения проверок DBCC, создания резервных копий базы данных и ее журнала транзакций, обновления статистики и перестроения индексов. При всех действиях по обслуживанию базы данных формируется отчет, который можно записать в указанный текстовый файл, в HTML-файл или отправить по электронной почте. Программа**sqlmaint** выполняет планы обслуживания баз данных, созданные в предыдущих версиях [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Для запуска планов обслуживания [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] из командной строки используйте программу [dtexec utility](../integration-services/packages/dtexec-utility.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../includes/ssnotedepnextavoid-md.md)] Вместо этого используйте функцию плана обслуживания [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Дополнительные сведения о планах обслуживания см. в разделе [Планы обслуживания](../relational-databases/maintenance-plans/maintenance-plans.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
      sqlmaint   
[-?] |  
[  
     [-Sserver_name[\instance_name]]  
     [-Ulogin_ID [-Ppassword]]  
     {  
          [-Ddatabase_name | -PlanNamename | -PlanIDguid ]  
          [-Rpttext_file]  
          [-Tooperator_name]  
          [-HtmlRpthtml_file [-DelHtmlRpt <time_period>] ]  
          [-RmUnusedSpacethreshold_percentfree_percent]  
          [-CkDB | -CkDBNoIdx]  
          [-CkAl | -CkAlNoIdx]  
          [-CkCat]  
          [-UpdOptiStatssample_percent]  
          [-RebldIdxfree_space]  
          [-SupportComputedColumn]  
          [-WriteHistory]  
          [  
               {-BkUpDB [backup_path] | -BkUpLog [backup_path] }  
               {-BkUpMedia  
                    {DISK [  
                           [-DelBkUps<time_period>]   
                           [-CrBkSubDir ]   
                           [-UseDefDir ]   
                          ]  
                     | TAPE   
                    }  
               }  
               [-BkUpOnlyIfClean]  
               [-VrfyBackup]  
          ]  
     }  
]  
<time_period> ::=  
number[minutes | hours | days | weeks | months]  
```  
  
## <a name="arguments"></a>Аргументы  
 Параметры и их значения должны разделяться пробелами. Например, пробел должен быть между **-S** и аргументом *server_name*.  
  
 **-?**  
 Указывает, что должна быть возвращена диаграмма синтаксиса **sqlmaint** . При использовании этого параметра использование других параметров не допускается.  
  
 **-S** _server_name_[ **\\**_instance_name_]  
 Указывает целевой экземпляр [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Укажите значение *server_name* , чтобы подключиться к экземпляру компонента [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] по умолчанию на этом сервере. Укажите *server_name**_\\_** instance_name* , чтобы подключиться к именованному экземпляру компонента [!INCLUDE[ssDE](../includes/ssde-md.md)] на этом сервере. Если сервер не указан, **sqlmaint** подключается к экземпляру [!INCLUDE[ssDE](../includes/ssde-md.md)] по умолчанию на локальном компьютере.  
  
 **-U** _login_id_  
 Указывает используемый идентификатор входа при соединении с сервером. Если этот параметр не указан, **sqlmaint** пытается использовать проверку подлинности [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Если аргумент *login_ID* содержит специальные символы, он должен быть заключен в двойные кавычки ("). В противном случае использование двойных кавычек необязательно.  
  
> [!IMPORTANT]  
>  По возможности используйте аутентификацию Windows.  
  
 **-P** _пароль_  
 Указывает пароль для идентификатора имени входа. Используется только вместе с параметром **-U** . Если аргумент *password* содержит специальные символы, он должен быть заключен в двойные кавычки. В противном случае использование двойных кавычек необязательно.  
  
> [!IMPORTANT]  
>  Маскировка пароля не производится. По возможности используйте аутентификацию Windows.  
  
 **-D** _database_name_  
 Указывает имя базы данных, с которой будут производиться операции обслуживания. Если аргумент *database_name* содержит специальные символы, он должен быть заключен в двойные кавычки. В противном случае использование двойных кавычек необязательно.  
  
 **-PlanName** _name_  
 Указывает имя плана обслуживания базы данных, определенного с помощью мастера планов обслуживания баз данных. Единственные сведения, которые программа **sqlmaint** использует из этого плана, — это список баз данных в плане. Любые действия по обслуживанию, которые указываются в других параметрах **sqlmaint** , применяются ко всем базам данных из этого списка.  
  
 **-PlanID** _guid_  
 Указывает идентификатор GUID плана обслуживания базы данных, определенного с помощью мастера планов обслуживания баз данных. Единственные сведения, которые программа **sqlmaint** использует из этого плана, — это список баз данных в плане. Любые действия по обслуживанию, которые указываются в других параметрах **sqlmaint** , применяются ко всем базам данных из этого списка. Значение должно совпадать со значением аргумента plan_id в таблице msdb.dbo.sysdbmaintplans.  
  
 **-Rpt** _text_file_  
 Указывает полный путь и имя файла, в котором будет сформирован отчет. Отчет также выводится на экран. В отчете сведения о версии отражаются при помощи добавления даты к имени файла. Дата формируется следующим образом: в конце имени файла, но перед точкой в формате _*ггггММддччмм*. *гггг* = год, *ММ* = месяц, *дд* = день, *hh* = часы, *мм* = минуты.  
  
 При запуске программы в 10:23 1 декабря 1996 года аргумент *text_file* будет иметь следующее значение:  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.rpt  
```  
  
 Имя создаваемого файла:  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint_199612011023.rpt  
```  
  
 Когда *sqlmaint* обращается к удаленному серверу, в качестве аргумента **text_file** необходимо указывать полное UNC-имя.  
  
 **-** _Имя_оператора_  
 Указывает оператора, которому будет отправлен сформированный отчет через службу SQL Mail.  
  
 **-HtmlRpt** _html_file_  
 Указывает полный путь и имя файла, в котором будет сформирован HTML-отчет. Программа**sqlmaint** формирует имя файла, добавляя к нему строку в формате _*ггггММддччмм* (как и в случае с параметром **-Rpt** ).  
  
 Когда *sqlmaint* обращается к удаленному серверу, в качестве аргумента **html_file** необходимо указывать полное UNC-имя файла.  
  
 **-DelHtmlRpt** \<*time_period*>  
 Задает удаление всех отчетов в формате HTML в каталоге отчетов, если интервал времени с момента создания отчета превысит значение аргумента \<*time_period*>. **-DelHtmlRpt** ищет файлы, имена которых соответствуют шаблону, сформированному на основе параметра *html_file*. Если значение аргумента *html_file* равно C:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.htm, параметр **-DelHtmlRpt** предпишет программе **sqlmaint** удалить все файлы, имена которых соответствуют шаблону C:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint\*.htm и которые являются более старыми, чем указано в значении аргумента \<*time_period*>.  
  
 **-RmUnusedSpace** _threshold_percent free_percent_  
 Указывает, что нужно удалить неиспользуемое пространство из базы данных, указанной в параметре **-D**. Этот параметр полезен только для тех баз данных, в которых задан автоматический рост. Аргумент*Threshold_percent* задает размер в мегабайтах, которого должна достичь база данных, прежде чем **sqlmaint** попытается удалить неиспользованное пространство данных. Если база данных меньше значения *threshold_percent*, никакие действия не выполняются. Значение*free_percent* задает размер сохраняемого неиспользуемого пространства в базе данных, указываемого в виде процента от конечного размера базы данных. Например, если база данных размером 200 MБ содержит 100 MБ данных, то указание значения 10 в качестве аргумента *free_percent* приводит к тому, что конечный размер базы данных будет составлять 110 MБ. Обратите внимание, что увеличения базы данных не происходит, если ее размер меньше суммы значения *free_percent* и объема данных в базе. Например, если база данных размером 108 MБ содержит данные размером 100 MБ, то указание 10 в качестве значения *free_percent* не приведет к увеличению базы данных до 110 MБ, ее размер останется равным 108 MБ.  
  
 **-CkDB** | **- CkDBNoIdx**  
 Запускает выполнение инструкции DBCC CHECKDB или DBCC CHECKDB с параметром NOINDEX в базе данных, указанной в параметре **-D**. Дополнительные сведения см. в разделе DBCC CHECKDB.  
  
 Если при запуске *sqlmaint* база данных уже используется, в **text_file** записывается предупреждение.  
  
 **-CkAl** | **- CkAlNoIdx**  
 Запускает выполнение инструкции DBCC CHECKALLOC с параметром NOINDEX в базе данных, указанной в параметре **-D**. Дополнительные сведения см. в разделе [DBCC CHECKALLOC (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-checkalloc-transact-sql).  
  
 **-CkCat**  
 Запускает выполнение инструкции DBCC CHECKCATALOG (Transact-SQL) в базе данных, указанной в параметре **-D**. Дополнительные сведения см. в разделе [DBCC CHECKCATALOG (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-checkcatalog-transact-sql).  
  
 **-UpdOptiStats** _sample_percent_  
 Задает применение следующей инструкции к каждой таблице базы данных:  
  
```  
UPDATE STATISTICS table WITH SAMPLE sample_percent PERCENT;  
```  
  
 Если в таблицах есть вычисляемые столбцы, при использовании параметра **-UpdOptiStats** необходимо также задавать аргумент **-SupportedComputedColumn**.  
  
 Дополнительные сведения см. в разделе [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql).  
  
 **-RebldIdx** _free_space_  
 Задает перестройку индексов в таблицах базы данных-получателя с использованием процентного значения *free_space* , которое составляет 100 % в сумме с коэффициентом заполнения. Например, если процент *free_space* равен 30, то используемый коэффициент заполнения равен 70. Если заданное значение процентов *free_space* равно 100, то повторное создание индексов происходит с использованием начального коэффициента заполнения.  
  
 Если индексы построены на вычисляемых столбцах, при использовании параметра **-RebldIdx** необходимо также задавать аргумент **-SupportComputedColumn**.  
  
 **-RebldIdx**  
 Обязательно указывается, если программа **sqlmaint** должна выполнить команды обслуживания DBCC для вычисляемых столбцов.  
  
 **-WriteHistory**  
 Задает создание записи журнала в msdb.dbo.sysdbmaintplan_history для каждой операции обслуживания, выполненной программой **sqlmaint**. Если указано значение **-PlanName** или **-PlanID** , то в записях журнала в sysdbmaintplan_history присутствует идентификатор указанного плана. Если указано значение **-D** , то в записи журнала в sysdbmaintplan_history в качестве значения идентификатора плана содержатся нули.  
  
 **-BkUpDB** [ *backup_path*] |  **-BkUpLog** [ *backup_path* ]  
 Задает действие резервного копирования. **-BkUpDb** выполняет резервное копирование всей базы данных. **-BkUpLog** создает резервную копию только журнала транзакций.  
  
 *backup_path* указывает каталог для резервной копии. Аргумент*backup_path* не нужно указывать, если указан параметр **-UseDefDir** . Если указать аргумент и параметр, параметр **-UseDefDir** переопределит аргумент. Резервная копия может размещаться в каталоге или по адресу ленточного устройства (например, \\\\.\TAPE0). Имя файла резервной копии базы данных создается автоматически следующим образом:  
  
```  
dbname_db_yyyyMMddhhmm.BAK  
  
```  
  
 где  
  
-   *dbname* — имя базы данных, резервная копия которой создается.  
  
-   *ггггММддччмм* — время операции резервного копирования, где *гггг* = год, *ММ* = месяц, *дд* = день, *hh* = часы, а *мм* = минуты.  
  
 Имя файла резервной копии журнала транзакций автоматически создается в аналогичном формате:  
  
```  
dbname_log_yyyymmddhhmm.BAK  
  
```  
  
 При использовании параметра **-BkUpDB** необходимо также указать носитель данных (указывается с помощью параметра **-BkUpMedia** ).  
  
 **-BkUpMedia**  
 Задает тип носителя для резервной копии, DISK (диск) или TAPE (лента).  
  
 **DISK;**  
 Указывает, что носителем данных резервных копий является диск.  
  
 **-DelBkUps**\< *time_period* >  
 Задает удаление всех файлов резервных копий в каталоге резервных копий в том случае, если интервал времени с момента создания резервной копии превысил значение \<*time_period*>.  
  
 **-CrBkSubDir**  
 При резервном копировании дисков, если указан параметр *-UseDefDir*, создает вложенный каталог в каталоге [ **backup_path** ] или в каталоге резервных копий по умолчанию. Имя вложенного каталога создается на основе имени базы данных, указанной в параметре **-D**. Чтобы быстро перенести все резервные копии различных баз данных в отдельные вложенные каталоги, не изменяя параметр **-CrBkSubDir** , задайте параметр *-CrBkSubDir* .  
  
 **-UseDefDir**  
 Для резервного копирования на диск задает создание файла резервной копии в каталоге резервных копий по умолчанию. Параметр**UseDefDir** переопределяет значение *backup_path* , если они указаны одновременно. При установке [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] с параметрами по умолчанию каталогом резервных копий является C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\Backup.  
  
 **TAPE;**  
 Указывает, что носителем данных резервных копий является ленточный накопитель.  
  
 **-BkUpOnlyIfClean**  
 Указывает, что операция резервного копирования производится только в том случае, если заданные проверки **-Ck** не обнаружили ошибок в данных. Действия по обслуживанию запускаются в порядке, в котором они указаны в командной строке. Если вы хотите указать параметр **-BkUpOnlyIfClean**, укажите перед параметром **-BkUpDB**-BkUpLog **параметр**-CkDB **,**-CkDBNoIdx **,**-CkAl **,** -CkAlNoIdx **,**/**-CkTxtAl** или **-CkCat**. Иначе резервное копирование будет выполняться независимо от наличия ошибок.  
  
 **-VrfyBackup**  
 Задает выполнение RESTORE VERIFYONLY на резервной копии по завершении ее создания.  
  
 *number*[**minutes**| **hours**| **day**| **weeks**| **months**]  
 Задает интервал времени, используемый для определения, является ли отчет или файл резервной копии достаточно старым для его удаления. *number* — целое число, за которым (без пробела) следует единица измерения времени. Допустимые варианты:  
  
-   **12недель**  
  
-   **3месяца**  
  
-   **15дней**  
  
 Если указано только *number* , то используемой по умолчанию частью даты будут **недель**.  
  
## <a name="remarks"></a>Примечания  
 Программа **sqlmaint** выполняет операции обслуживания с одной или несколькими базами данных. Если указан параметр **-D** , операции, заданные в остальных параметрах, выполняются только с указанной базой данных. Если указан параметр **-PlanName** или **-PlanID** , **sqlmaint** получает из указанного плана обслуживания только сведения о списке баз данных. Все операции, указанные в остальных параметрах **sqlmaint** , применяются ко всем базам данных, которые указаны в полученном из плана списке. Программа **sqlmaint** не выполняет операции обслуживания, определенные в самом плане.  
  
 В случае успешного выполнения **sqlmaint** возвращает 0, а в случае ошибки — 1. Сообщение об ошибке выводится:  
  
-   в случае неудачи любой из операций обслуживания;  
  
-   если проверка **-CkDB**, **-CkDBNoIdx**, **-CkAl**, **-CkAlNoIdx**, **-CkTxtAl**или **-CkCat** обнаруживает ошибки в данных;  
  
-   в случае общего сбоя.  
  
## <a name="permissions"></a>Разрешения  
 Программу **sqlmaint** может выполнить любой пользователь Windows, у которого есть разрешения на **чтение и выполнение** файла `sqlmaint.exe`(по умолчанию находится в папке `x:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER1\MSSQL\Binn` ). Кроме того, учетные данные [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , указанные в параметре **-login_ID** , должны иметь разрешения [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , необходимые для выполнения указанного действия. Если соединение с [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] использует проверку подлинности Windows, имя входа [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , сопоставленное с прошедшим проверку пользователем Windows, должно иметь разрешения [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , достаточные для выполнения указанного действия.  
  
 Например, для параметра **-BkUpDB** требуется разрешение на выполнение инструкции BACKUP, а использование аргумента **-UpdOptiStats** предполагает наличие разрешения на выполнение инструкции UPDATE STATISTICS. Дополнительные сведения см. в подразделах «Разрешения» соответствующих разделов электронной документации.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-performing-dbcc-checks-on-a-database"></a>A. Выполнение проверок DBCC в базе данных  
  
```  
sqlmaint -S MyServer -D AdventureWorks2012 -CkDB -CkAl -CkCat -Rpt C:\MyReports\AdvWks_chk.rpt  
```  
  
### <a name="b-updating-statistics-using-a-15-sample-in-all-databases-in-a-plan-also-shrink-any-of-the-database-that-have-reached-110-mb-to-having-only-10-free-space"></a>Б. Обновление статистики, используя в качестве образца 15 % данных из всех баз данных, содержащихся в плане. Также сжимает все базы данных, размер которых достиг 110 MБ, чтобы свободное пространство в них составляло только 10%  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -UpdOptiStats 15 -RmUnusedSpace 110 10  
```  
  
### <a name="c-backing-up-all-the-databases-in-a-plan-to-their-individual-subdirectories-in-the-default-xprogram-filesmicrosoft-sql-servermssql12mssqlservermssqlbackup-directory-also-delete-any-backups-older-than-2-weeks"></a>В. Создает резервные копии всех баз данных, содержащихся в плане, в отдельных каталогах, вложенных в каталог по умолчанию «x:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup». Кроме того, удаляет резервные копии, созданные ранее чем две недели назад  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -BkUpDB -BkUpMedia DISK -UseDefDir -CrBkSubDir -DelBkUps 2weeks  
```  
  
### <a name="d-backing-up-a-database-to-the-default-xprogram-filesmicrosoft-sql-servermssql12mssqlservermssqlbackup-directory"></a>Г. Создание резервной копии базы данных по умолчанию x:\Program Files\Microsoft SQL Server\MSSQL12. Каталог MSSQLSERVER\MSSQL\Backup. \  
  
```  
sqlmaint -S MyServer -BkUpDB -BkUpMedia DISK -UseDefDir  
```  
  
## <a name="see-also"></a>См. также  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [UPDATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/update-statistics-transact-sql)  
  
  
