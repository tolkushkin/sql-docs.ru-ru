---
title: Регистрация подключенного сервера (SQL Server Management Studio) | Документы Майкрософт
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], register connected servers
- connected server registrations [SQL Server]
ms.assetid: 77deb5f5-0f80-484f-8b8b-29afa67ec18f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b399f3d509f16390f4ceb2555420682019ae8ef7
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65104362"
---
# <a name="register-a-connected-server-sql-server-management-studio"></a>Регистрация подключенного сервера (среда SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  В этом разделе описывается регистрация подключенного сервера в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS). Регистрация сервера дает возможность сохранить данные о соединении для тех серверов, к которым часто осуществляется доступ. Сервер может быть зарегистрирован перед установкой соединения или во время соединения из обозревателя объектов.  Зарегистрированные серверы в среде SSMS можно просмотреть, выбрав пункты **Просмотр**\\**Зарегистрированные серверы** в меню.
  
 **В этом разделе**  
  
-   **Регистрация сервера с помощью:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-register-a-connected-server"></a>Регистрация подключенного сервера  
  
В обозревателе объектов щелкните правой кнопкой мыши имя сервера, с которым уже установлено соединение, а затем нажмите кнопку **Зарегистрировать**.
  
**Имя сервера**  
Значением по умолчанию для этого поля является имя сервера, к которому вы подключены.  Можно также ввести имя сервера или выбрать его из раскрывающегося списка.

**Проверка подлинности**  
При соединении с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]доступны два режима проверки подлинности. 

-    **Проверка подлинности Windows.**  
Режим проверки подлинности Windows позволяет пользователям подключаться с помощью учетных записей [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. 

-    **Проверка подлинности SQL Server**   
При подключении пользователя с указанным именем входа и паролем из ненадежных соединений [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняет проверку подлинности посредством проверки наличия учетной записи входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и проверки совпадения пароля с записанным ранее. Если в службе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не задана учетная запись входа, проверка подлинности завершается ошибкой, о которой пользователь получит сообщение.

     > [!IMPORTANT]  
     > [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] Дополнительные сведения см. в разделе [Выбор режима проверки подлинности](../../relational-databases/security/choose-an-authentication-mode.md).  

     -    **User name**  
Показывает текущее имя пользователя, с которым устанавливается соединение. Этот параметр только для чтения доступен лишь при соединении с использованием метода проверки подлинности Windows. Чтобы изменить **Имена пользователей**, войдите в систему под другим именем. 

     -    **Имя входа**  
Введите имя входа для подключения. Этот параметр доступен только в том случае, если выбрано соединение с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

     -    **Пароль**  
Введите пароль для этого имени входа. Этот параметр доступен для изменения только при соединении с использованием метода проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 

     -    **Запомнить пароль**  
Выберите для шифрования и сохранения введенного пароля в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Этот параметр отображается только в том случае, если выбрано подключение с проверкой подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

          > [!NOTE]  
          > Чтобы пароль больше не запоминался, снимите этот флажок и нажмите кнопку **Сохранить**.  

**Имя зарегистрированного сервера**  
Имя, которое будет отображаться на панели «Зарегистрированные серверы». Это имя не должно совпадать с именем, указанным в поле **Имя сервера** .  
  
**Описание зарегистрированного сервера**  
Введите необязательное описание сервера.  
  
**Тест**  
Нажмите для проверки соединения с сервером, заданным в поле **Имя сервера**.  
  
**Сохранить**  
Нажмите эту кнопку, чтобы сохранить настройки зарегистрированного сервера. 

## <a name="see-also"></a>См. также:  
[Создание нового зарегистрированного сервера (среда SQL Server Management Studio)](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)
  
  
