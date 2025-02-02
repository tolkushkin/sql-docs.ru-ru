---
title: Смена пароля программным способом | Документация Майкрософт
description: Изменение паролей, программно с помощью драйвера OLE DB для SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], password expiration
- OLE DB Driver for SQL Server, passwords
- passwords [SQL Server], expiration
- MSOLEDBSQL, password expiration
- expiration [OLE DB Driver for SQL Server]
- passwords [SQL Server], modifying
- expired passwords [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, password expiration
- modifying passwords
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: fdf5afb7cc9eea9beed43726d3c107c9fde9b6e2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777893"
---
# <a name="changing-passwords-programmatically"></a>Смена пароля программным способом
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  В версиях, предшествующих [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], при истечении пароля пользователя переустановить его мог только администратор. Начиная с версии [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], драйвер OLE DB для SQL Server поддерживает обработка срока действия пароля программным способом с помощью драйвера OLE DB и через изменения в **имя входа SQL Server** диалоговым окнам.  
  
> [!NOTE]  
>  По возможности следует предлагать пользователям вводить свои учетные данные во время выполнения, избегая их сохранения. Если необходимо сохранить учетные данные пользователей, зашифруйте их с помощью [интерфейса API шифрования Win32](https://go.microsoft.com/fwlink/?LinkId=64532). Дополнительные сведения об использовании паролей см. в разделе [Надежные пароли](../../../relational-databases/security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Коды ошибок имени входа SQL Server  
 Если соединение нельзя установить из-за проблем проверки подлинности, то для диагностики и восстановления приложению будет доступен один из существующих кодов ошибок SQL Server.  
  
|Код ошибки SQL Server|Сообщение об ошибке|  
|---------------------------|-------------------|  
|15113|Ошибка входа пользователя "%. * ls. Причина: не удалось проверить пароль. Учетная запись заблокирована.|  
|18463|Ошибка входа пользователя «%.*ls». Причина: не удалось изменить пароль. В данный момент этот пароль не может быть использован.|  
|18464|Ошибка входа пользователя «%.*ls». Причина: не удалось изменить пароль. Пароль слишком короткий и не отвечает требованиям политики.|  
|18465|Ошибка входа пользователя «%.*ls». Причина: не удалось изменить пароль. Пароль слишком длинный и не отвечает требованиям политики.|  
|18466|Ошибка входа пользователя «%.*ls». Причина: не удалось изменить пароль. Пароль недостаточно сложный и не отвечает требованиям политики.|  
|18467|Ошибка входа пользователя «%.*ls». Причина: не удалось изменить пароль. Пароль не отвечает требованиям динамической библиотеки фильтрации паролей.|  
|18468|Ошибка входа пользователя «%.*ls». Причина: не удалось изменить пароль. В процессе проверки пароля произошла непредвиденная ошибка.|  
|18487|Ошибка входа пользователя «%.*ls». Причина: истек срок действия пароля для этой учетной записи.|  
|18488|Ошибка входа пользователя «%.*ls». Причина: пароль для данной учетной записи необходимо изменить.|  
  
## <a name="ole-db-driver-for-sql-server"></a>Драйвер OLE DB для SQL Server  
 Драйвер OLE DB для SQL Server поддерживает истечение срока действия пароля, но пользовательский интерфейс и программным способом.  
  
### <a name="ole-db-user-interface-password-expiration"></a>Пользовательский интерфейс OLE DB для истечения срока действия пароля  
 Драйвер OLE DB для SQL Server поддерживает истечение срока действия пароля через изменения в диалоговых окнах **Имя входа SQL Server**. Если свойство DBPROP_INIT_PROMPT установлено в значение DBPROMPT_NOPROMPT, то в случае истечения срока действия пароля попытка начального соединения завершится с ошибкой.  
  
 Если свойство DBPROP_INIT_PROMPT установлено в любое другое значение, диалоговое окно **Имя входа SQL Server** появится независимо от того, истек срок действия пароля или нет. Чтобы сменить пароль, пользователь может нажать кнопку **Параметры** и установить флажок **Сменить пароль**.  
  
 Если срок действия пароля истек, а пользователь нажимает кнопку "ОК", [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] предложит ему ввести и подтвердить новый пароль с помощью диалогового окна **Изменить пароль SQL Server**.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>Поведение подсказки OLE DB и заблокированные учетные записи  
 Попытки соединения могут окончиться неудачей, если учетная запись заблокирована. В этом случае вслед за выводом диалогового окна **Имя входа SQL Server** для пользователя отображается сообщение об ошибке сервера, и попытка соединения аварийно завершается. Это может также произойти после отображения диалогового окна **Изменить пароль SQL Server**, если пользователь неправильно ввел старый пароль. В этом случае будет выведено то же сообщение об ошибке, а попытка соединения отменяется.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>Пул соединений OLE DB, истечение срока действия пароля и заблокированные учетные записи  
 Учетная запись может оказаться заблокированной или может истечь срок действия пароля, в то время как соединение останется активным в пуле соединений. Сервер проверяет наличие паролей с истекшим сроком действия и заблокированных учетных записей в двух случаях. Во-первых, при первоначальном создании соединения. Во-вторых, после восстановления соединения, при получении соединения из пула.  
  
 Если попытка восстановления завершилась неудачно, то соединение удаляется из пула и возвращается ошибка.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Программное истечение срока действия пароля OLE DB  
 Драйвер OLE DB для SQL Server поддерживает истечение срока действия пароля с помощью свойства SSPROP_AUTH_OLD_PASSWORD (типа VT_BSTR), которое было добавлено в набор свойств DBPROPSET_SQLSERVERDBINIT.  
  
 Существующее свойство «Password» ссылается на свойство DBPROP_AUTH_PASSWORD и используется для хранения нового пароля.  
  
> [!NOTE]  
>  В строке подключения свойство «Old Password» устанавливает значение свойства SSPROP_AUTH_OLD_PASSWORD, являющееся текущим паролем (возможно, с истекшим сроком действия), недоступным через свойство строки поставщика.  
  
 Поставщик не сохраняет значение этого свойства. Когда это свойство установлено, при первом соединении поставщик не использует пул соединений, поскольку это вызовет новое соединение. Если пароль успешно изменен, текущее соединение нельзя использовать повторно, поскольку оно все еще содержит старый пароль, который будет недопустимым после изменения пароля. Кроме того, при успешном входе поставщик очистит данное свойство. Дальнейшие попытки получения старого пароля вернут значение VT_EMPTY.  
  
> [!NOTE]  
>  Свойство SSPROP_AUTH_OLD_PASSWORD не нужно сохранять, поскольку оно используется только при истечении срока действия пароля.  
  
 Обратите внимание, что при установке свойства «Old Password» поставщик предполагает, что была сделана попытка изменить пароль, если не была также указана проверка подлинности Windows, имеющая приоритет.  
  
 Если используется проверка подлинности Windows, при указании старого пароля возвращается либо DB_E_ERRORSOCCURRED, либо DB_S_ERRORSOCCURRED в зависимости от того, был ли указан старый пароль как REQUIRED или OPTIONAL соответственно, а значение состояния DBPROPSTATUS_CONFLICTINGBADVALUE возвращается в параметре *dwStatus*. Это определяется при вызове метода **IDBInitialize::Initialize**.  
  
 Если попытка смены пароля завершилась непредвиденной ошибкой, то сервер возвращает код ошибки 18468. Попытка соединения возвращает стандартный код ошибки OLEDB.  
  
 Дополнительные сведения о наборе свойств DBPROPSET_SQLSERVERDBINIT, см. в разделе [свойства инициализации и авторизации](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>См. также:  
 [Возможности драйвера OLE DB для SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
