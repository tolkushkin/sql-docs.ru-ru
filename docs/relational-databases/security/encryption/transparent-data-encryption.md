---
title: Прозрачное шифрование данных (TDE) | Документация Майкрософт
ms.custom: ''
ms.date: 05/09/2019
ms.prod: sql
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption
- database encryption key, about
- TDE
- database encryption key
- TDE, about
- Transparent Data Encryption, about
- encryption [SQL Server], transparent data encryption
ms.assetid: c75d0d4b-4008-4e71-9a9d-cee2a566bd3b
author: aliceku
ms.author: aliceku
ms.reviewer: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d944c2192e73fd0cb887d0491ecba707a90ff7b5
ms.sourcegitcommit: 6ab60b426fc6ec7bb9e727323f520c0b05a20d06
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2019
ms.locfileid: "65527353"
---
# <a name="transparent-data-encryption-tde"></a>Прозрачное шифрование данных (TDE)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  *Прозрачное шифрование данных* (TDE) позволяет шифровать файлы данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]и [!INCLUDE[ssSDWfull](../../../includes/sssdwfull-md.md)] ; это называется шифрованием хранящихся данных. Чтобы защитить базу данных, можно принять ряд мер предосторожности, например спроектировать систему безопасности, проводить шифрование конфиденциальных ресурсов и поместить серверы базы данных под защиту брандмауэра. Однако если будет похищен физический носитель (например, диск или ленты резервной копии), злоумышленник может легко восстановить или подключить базу данных и получить доступ к данным. Одним из решений может стать шифрование конфиденциальных данных в базе данных и защита ключей, используемых при шифровании, с помощью сертификата. Это не позволит использовать данные ни одному человеку, не имеющему ключей, но такой тип защиты следует планировать заранее.  
  
 Функция прозрачного шифрования данных выполняет шифрование и дешифрование ввода-вывода в реальном времени для файлов данных и журналов. При шифровании используется ключ шифрования базы данных (DEK), который хранится в загрузочной записи базы данных, где можно получить к нему доступ при восстановлении. Ключ шифрования базы данных является симметричным ключом, защищенным сертификатом, который хранится в базе данных master на сервере, или асимметричным ключом, защищенным модулем расширенного управления ключами. Функция прозрачного шифрования данных защищает "неактивные" данные, то есть файлы данных и журналов. Благодаря ей обеспечивается соответствие требованиям различных законов, постановлений и рекомендаций, действующих в разных отраслях. Это позволяет разработчикам программного обеспечения шифровать данные с помощью алгоритмов шифрования AES и 3DES, не меняя существующие приложения.  
  
> [!IMPORTANT]
>  Функция прозрачного шифрования данных не обеспечивает шифрование каналов связи. Дополнительные сведения о способах шифрования данных, передаваемых по каналам связи, см. в разделе [Включение шифрования соединений в ядре СУБД (диспетчер конфигурации SQL Server)](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
> 
>  **См. также:**  
> 
>  -   [Прозрачное шифрование данных в Базе данных SQL Azure](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
> -   [Начало работы с прозрачным шифрованием данных (TDE) в хранилище данных SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-encryption-tde-tsql/)  
> -   [Перемещение базы данных, защищаемой прозрачным шифрованием, в другой экземпляр SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
> -   [Включение прозрачного шифрования данных в SQL Server с помощью расширенного управления ключами](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)   
> -   [Использование соединителя SQL Server с компонентами шифрования SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)
> - [Блог по безопасности SQL Server в TDE с вопросами и ответами](https://blogs.msdn.microsoft.com/sqlsecurity/2016/10/05/feature-spotlight-transparent-data-encryption-tde/)
 
  
## <a name="about-tde"></a>Сведения о прозрачном шифровании данных (TDE)  
 Шифрование файла базы данных проводится на уровне страниц. Страницы в зашифрованной базе данных шифруются до записи на диск и дешифруются при чтении в память. Прозрачное шифрование данных не увеличивает размер зашифрованной базы данных.  
  
 **Сведения, применимые к [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]**  
  
 При использовании прозрачного шифрования данных с [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] версии 12 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] автоматически создает для вас сертификат на уровне сервера, хранящийся в базе данных master. Чтобы переместить базу данных TDE в [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], расшифровывать ее не нужно. Дополнительные сведения об использовании прозрачного шифрования данных с [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] см. в статье [Прозрачное шифрование данных в базе данных SQL Azure](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).  
  
 **Сведения, применимые к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
 После защиты базы данных ее можно восстановить с помощью правильного сертификата. Дополнительные сведения о сертификатах см. в разделе [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
 При включении функции прозрачного шифрования данных необходимо немедленно создать резервную копию сертификата и закрытого ключа, связанного с этим сертификатом. В случае если сертификат окажется недоступен или понадобится восстановить базу данных на другом сервере либо присоединить ее к другому серверу, необходимо иметь копии сертификата и закрытого ключа. Иначе будет невозможно открыть базу данных. Сертификат шифрования следует сохранить, даже если функция прозрачного шифрования в базе данных будет отключена. Даже если база данных не зашифрована, части журнала транзакций могут по-прежнему оставаться защищенными, а для некоторых операций будет требоваться сертификат до выполнения полного резервного копирования базы данных. Сертификат, который превысил свой срок хранения, все еще может быть использован для шифрования и расшифровки данных с помощью прозрачного шифрования данных.  
  
 **Иерархия шифрования**  
  
 На рисунке ниже показана архитектура прозрачного шифрования данных. При использовании прозрачного шифрования данных в [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]пользователь может настраивать только элементы уровня базы данных (ключ шифрования базы данных и фрагменты ALTER DATABASE).  
  
 ![Отображает иерархию, описанную в разделе. ](../../../relational-databases/security/encryption/media/tde-architecture.png "Отображает иерархию, описанную в разделе.")  
  
## <a name="using-transparent-data-encryption"></a>Использование прозрачного шифрования данных  
 Чтобы использовать прозрачное шифрование данных, выполните следующие действия.  
  
**Область применения**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Создайте главный ключ  
  
-   Создайте или получите сертификат, защищенный главным ключом  
  
-   Создайте ключ шифрования базы данных и защитите его с помощью сертификата  
  
-   Задайте ведение шифрования базы данных  
  
 В следующем примере демонстрируется шифрование и дешифрование базы данных `AdventureWorks2012` с помощью сертификата с именем `MyServerCert`, установленного на сервере.  
  
```sql  
USE master;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
go  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
go  
USE AdventureWorks2012;  
GO  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ENCRYPTION ON;  
GO  
```  
  
 Операции шифрования и дешифрования запланированы в фоновых потоках [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Состояние этих операций можно просмотреть в представлениях каталога и динамических административных представлениях в списке, представленном далее в этом разделе.  
  
> [!CAUTION]  
>  Файлы резервных копий баз данных, в которых включено TDE, также шифруются с помощью ключа шифрования базы данных. Поэтому для восстановления таких резервных копий необходимо иметь сертификат, защищающий ключ шифрования базы данных. Это значит, что помимо резервного копирования базы данных обязательно необходимо сохранять резервные копии сертификатов серверов, чтобы не допустить потери данных. Если сертификат станет недоступным, это приведет к потере данных. Дополнительные сведения см. в статье [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
## <a name="commands-and-functions"></a>Команды и функции  
 Чтобы в следующих инструкциях можно было использовать сертификаты TDE, они должны быть зашифрованы главным ключом базы данных. Если они зашифрованы только паролем, то они будут отклонены инструкциями как шифраторы.  
  
> [!IMPORTANT]  
>  Если после использования сертификатов в TDE включить защиту паролем, база данных станет недоступной после перезапуска.  
  
 В следующей таблице представлены ссылки и объяснения команд и функций TDE.  
  
|Команда или функция|Назначение|  
|-------------------------|-------------|  
|[CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)|Создает ключ, используемый для шифрования базы данных.|  
|[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Изменяет ключ, используемый для шифрования базы данных.|  
|[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Удаляет ключ, использовавшийся для шифрования базы данных.|  
|[Параметры ALTER DATABASE SET &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql-set-options.md)|Объясняет параметр **ALTER DATABASE** , который используется для включения TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Представления каталога и динамические административные представления  
 В следующей таблице показаны представления каталогов и динамические административные представления TDE.  
  
|Представление каталога или динамическое административное представление|Назначение|  
|---------------------------------------------|-------------|  
|[sys.databases (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Представление каталога со сведениями о базе данных.|  
|[sys.certificates &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Представление каталога с сертификатами из базы данных.|  
|[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)|Динамическое административное представление со сведениями о ключах шифрования, используемых в базе данных, и состоянии шифрования базы данных.|  
  
## <a name="permissions"></a>Разрешения  
 Для каждой функции или команды TDE действуют отдельные требования к разрешениям, описанные в таблицах выше.  
  
 Для просмотра метаданных, связанных с TDE, необходимо разрешение VIEW DEFINITION на сертификат.  
  
## <a name="considerations"></a>Замечания  
 Во время проверки базы данных на повторное шифрование, выполняемой для операции шифрования, операции обслуживания базы данных отключаются. Для выполнения операции обслуживания базы данных можно использовать однопользовательский режим. Дополнительные сведения см. в разделе [Установка однопользовательского режима базы данных](../../../relational-databases/databases/set-a-database-to-single-user-mode.md).  
  
 Состояние шифрования базы данных можно определить с помощью динамического административного представления sys.dm_database_encryption_keys. Дополнительные сведения см. выше в подразделе "Представления каталога и динамические административные представления" этого раздела.  
  
 В режиме TDE все файлы и файловые группы зашифрованы. Если какие-либо файловые группы в базе данных помечены признаком READ ONLY, то операция шифрования базы данных завершится сбоем.  
  
 Если база данных используется в зеркальном отображении базы данных или в доставке журналов, то зашифрованы будут обе базы данных. Транзакции журналов при передаче между ними будут передаваться в зашифрованном виде.  
  
> [!IMPORTANT]  
>  Полнотекстовые индексы будут шифроваться после включения шифрования базы данных. Полнотекстовые индексы, созданные до версии SQL Server 2008, будут импортированы в базу данных во время обновления до SQL Server 2008 или более поздней версии, и к ним будет применено прозрачное шифрование данных.  

> [!TIP]  
> Чтобы отслеживать изменения в состоянии прозрачного шифрования для базы данных, используйте аудит базы данных SQL или подсистему аудита SQL Server. Для SQL Server прозрачное шифрование данных отслеживается в группе действий аудита DATABASE_CHANGE_GROUP, которую можно найти в списке [Действия и группы действий подсистемы аудита SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).
  
### <a name="restrictions"></a>Ограничения  
 При первом шифровании базы данных, изменении ключа или дешифровании базы данных не допускаются следующие операции:  
  
-   удаление файла из файловой группы в базе данных;  
  
-   удаление базы данных;  
  
-   перевод базы данных в режим «вне сети»;  
  
-   отсоединение базы данных;  
  
-   перевод базы данных или файловой группы в состояние READ ONLY.  
  
 При выполнении инструкций CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY или ALTER DATABASE...SET ENCRYPTION не допускаются следующие операции:  
  
-   удаление файла из файловой группы в базе данных;  
  
-   Удаление базы данных.  
  
-   перевод базы данных в режим «вне сети»;  
  
-   отсоединение базы данных;  
  
-   перевод базы данных или файловой группы в состояние READ ONLY;  
  
-   использование команды ALTER DATABASE;  
  
-   запуск резервного копирования базы данных или файла базы данных;  
  
-   запуск восстановления базы данных или файла базы данных;  
  
-   создание моментального снимка.  
  
 Следующие операции или условия запрещают выполнение инструкций CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY или ALTER DATABASE...SET ENCRYPTION.  
  
-   база данных предназначена только для чтения, или в ней есть файловые группы, доступные только для чтения;  
  
-   выполняется команда ALTER DATABASE;  
  
-   выполняется какая-либо операция резервного копирования;  
  
-   база данных находится в состоянии восстановления или в состоянии «вне сети»;  
  
-   идет создание моментального снимка;  
  
-   выполняется задача обслуживания базы данных.  
  
 При создании файлов базы данных быстрая инициализация файлов недоступна при включенном TDE.  
  
 Чтобы зашифровать ключ шифрования базы данных с помощью асимметричного ключа, используемый асимметричный ключ должен находиться в поставщике расширенного управления ключами.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Прозрачное шифрование данных и журналы транзакций  
 Включение TDE в базе данных приводит к «обнулению» оставшейся части виртуального журнала транзакций и принудительному началу нового виртуального журнала транзакций. Это гарантирует, что после включения шифрования базы данных в журналах транзакций не останется простого текста. Состояние шифрования файла журнала можно определить, просмотрев столбец `encryption_state` в представлении `sys.dm_database_encryption_keys`, как показано в примере:  
  
```  
USE AdventureWorks2012;  
GO  
/* The value 3 represents an encrypted state   
   on the database and transaction logs. */  
SELECT *  
FROM sys.dm_database_encryption_keys  
WHERE encryption_state = 3;  
GO  
```  
  
 Дополнительные сведения об архитектуре файлов журнала [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] см. в разделе [Журнал транзакций (SQL Server)](../../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Все данные, записанные в журнале транзакций до изменения ключа шифрования базы данных, будут зашифрованы с помощью предыдущего ключа шифрования базы данных.  
  
 После двукратного изменения ключа шифрования базы данных необходимо выполнить резервное копирование журнала перед следующим изменением ключа шифрования базы данных.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Прозрачное шифрование данных и системная база данных tempdb  
 Системная база данных tempdb будет шифроваться, если с помощью TDE шифруется любая другая база данных в экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Это может влиять на производительность незашифрованных баз данных в том же экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Дополнительные сведения о системной базе данных tempdb см. в разделе [База данных tempdb](../../../relational-databases/databases/tempdb-database.md).  
  
### <a name="transparent-data-encryption-and-replication"></a>Прозрачное шифрование данных и репликация  
 Репликация данных не выполняется автоматически в зашифрованном виде из базы данных с включенным TDE. Необходимо отдельно включить TDE, если нужно защитить базы данных распространителя и подписчика. При репликации моментальных снимков и начальном распределении данных для репликации транзакций и репликации слиянием данные могут храниться в незашифрованных промежуточных файлах, например файлах BCP.  Во время репликации транзакций или репликации слиянием шифрование можно включить для защиты каналов связи. Дополнительные сведения см. в разделе [Включение шифрования соединений в компоненте Database Engine (диспетчер конфигураций SQL Server)](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
### <a name="transparent-data-encryption-and-filestream-data"></a>Прозрачное шифрование данных и данные FILESTREAM  
 Данные FILESTREAM не шифруются, даже если включено прозрачное шифрование данных.  

<a name="scan-suspend-resume"></a>

## <a name="transparent-data-encryption-tde-scan"></a>Сканирование — прозрачное шифрование данных (TDE)

Чтобы включить прозрачное шифрование данных (TDE) для базы данных, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] должен выполнить сканирование шифрования. При этом каждая страница считывается из файлов данных в буферный пул, после чего зашифрованные страницы записываются обратно на диск. Для предоставления пользователю большего контроля над сканированием шифрования в [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] появился синтаксис приостановки и возобновления сканирования TDE. Он позволяет приостанавливать сканирование, когда система сильно загружена, или в критически важные периоды времени, а затем возобновлять сканирование.

Чтобы приостановить сканирование шифрования TDE, используйте следующий синтаксис:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

Чтобы возобновить сканирование шифрования TDE, используйте следующий синтаксис:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

Для определения текущего состояния сканирования шифрования в динамическое административное представление `sys.dm_database_encryption_keys` добавлен столбец `encryption_scan_state`. Кроме того, появился столбец `encryption_scan_modify_date`, который содержит дату и время последнего изменения состояния сканирования шифрования. Кроме того, обратите внимание на то, что если экземпляр [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] перезапускается, когда сканирование шифрования приостановлено, при запуске в журнал ошибок записывается сообщение о том, что имеется приостановленное сканирование.
  
## <a name="transparent-data-encryption-and-buffer-pool-extension"></a>Прозрачное шифрование и расширение буферного пула  
 Файлы, касающиеся расширения буферного пула, не шифруются, если база данных зашифрована с помощью прозрачного шифрования данных. Необходимо использовать средства шифрования на уровне файловой системы, такие как BitLocker или файловая система EFS для файлов с расширением BPE.  
  
## <a name="transparent-data-encryption-and-in-memory-oltp"></a>Прозрачное шифрование данных и In-Memory OLTP  
 Прозрачное шифрование данных можно включить в базе данных, которая содержит объекты OLTP в памяти. В [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] и [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] записи журнала выполняющейся в памяти OLTP шифруются, если включено TDE. В [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] записи журнала выполняющейся в памяти OLTP шифруются, если включено TDE, однако файлы в файловой группе MEMORY_OPTIMIZED_DATA не шифруются.  
  
## <a name="related-tasks"></a>Связанные задачи  
 [Перемещение базы данных, защищаемой прозрачным шифрованием, в другой экземпляр SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
 [Включение прозрачного шифрования данных в SQL Server с помощью расширенного управления ключами](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
 [Расширенное управление ключами с помощью хранилища ключей Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="related-content"></a>См. также  
 [Прозрачное шифрование данных в Базе данных SQL Azure](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
 [Начало работы с прозрачным шифрованием данных (TDE) в хранилище данных SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-encryption-tde-tsql/)  
 [Шифрование SQL Server](../../../relational-databases/security/encryption/sql-server-encryption.md)  
 [Ключи шифрования базы данных и SQL Server &#40;ядро СУБД&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
   
## <a name="see-also"></a>См. также:  
 [Центр обеспечения безопасности для базы данных Azure SQL и SQL Server Database Engine](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)  
  
  
