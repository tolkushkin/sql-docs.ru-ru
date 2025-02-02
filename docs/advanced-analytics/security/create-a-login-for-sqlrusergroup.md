---
title: Создайте имя входа для SQLRUserGroup - службы машинного обучения SQL Server
description: Для замыкания соединений с помощью неявной проверки подлинности Создайте имя входа в SQL Server SQLRUserGroup, так что можете войти на сервер, для преобразования идентификаторов для вызывающего пользователя с рабочей учетной записью.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 62dd1ddf61c3cc2e1340619566ad9f4dcce062b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642101"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Создание учетных данных для SQLRUserGroup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Создание [входа в SQL Server](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) для [SQLRUserGroup](../concepts/security.md#sqlrusergroup) при [цикл замыкается](../../advanced-analytics/concepts/security.md#implied-authentication) в скрипте указывает *доверительное соединение*, и идентификатор, который использовался для выполнения объекта содержит код является учетной записью пользователя Windows.

Доверенные соединения являются те, которые `Trusted_Connection=True` в строке подключения. Когда SQL Server получает запрос, указав доверительное соединение, он проверяет, имеет ли удостоверение текущего пользователя Windows, имя входа. Для внешних процессов, выполнение с ключевым словом с рабочей учетной записью (например MSSQLSERVER01 из **SQLRUserGroup**), запрос завершится ошибкой, поскольку эти учетные записи не имеют имени входа по умолчанию.

Ошибка подключения можно обойти путем создания имени входа для **SQLServerRUserGroup**. Дополнительные сведения об удостоверениях и внешних процессов см. в разделе [Общие сведения о безопасности для инфраструктуры расширяемости](../concepts/security.md).

> [!Note]
> Убедитесь, что **SQLRUserGroup** имеет разрешения «Локальный вход в систему». По умолчанию это право предоставляется всем новым локальным пользователям, но некоторые организации более строгие групповые политики может отключить это право.

## <a name="create-a-login"></a>Создает вход

1. В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]в обозревателе объектов разверните узел **Безопасность**, щелкните правой кнопкой мыши **Имена входа**и выберите пункт **Создать имя входа**.

2. В **Создание имени входа** выберите **поиска**. (Ничего не вводите в поле еще.)
    
     ![Нажмите кнопку поиска, чтобы добавить новое имя входа для машинного обучения](media/implied-auth-login1.png "\"щелкните\" Поиск \", чтобы добавить новое имя входа для машинного обучения")

3. В **Выбор пользователя или группы** выберите **типы объектов** кнопки.

     ![Поиск типов объектов, чтобы добавить новое имя входа для машинного обучения](media/implied-auth-login2.png "поиска типов объектов, чтобы добавить новое имя входа для машинного обучения")

4. В **типы объектов** выберите **группы**. Снимите все остальные флажки.

     ![Выберите группы, в диалоговом окне типы объектов](media/implied-auth-login3.png "Выбор групп, в диалоговом окне типы объектов")

4. Нажмите кнопку **Дополнительно**, убедитесь, что расположение для поиска текущего компьютера, а затем нажмите кнопку **найти**.

     ![Чтобы получить список групп нажмите кнопку Найти](media/implied-auth-login4.png "нажмите кнопку Начать поиск, чтобы получить список групп")

5. В списке учетных записей групп на сервере, пока не найдете начинающееся `SQLRUserGroup`.
    
    + Имя группы, связанной со службой панели запуска для _экземпляр по умолчанию_ всегда **SQLRUserGroup**, независимо от того, что вы установили R, Python или оба. Выберите для экземпляра по умолчанию только этой учетной записи.
    + Если вы используете _именованный экземпляр_, имя экземпляра добавляется к имени рабочей группы по умолчанию, имя `SQLRUserGroup`. Например, если экземпляр имеет имя «MLTEST», имя группы пользователей по умолчанию для этого экземпляра будет **SQLRUserGroupMLTest**.
 
    ![Пример групп на сервере](media/implied-auth-login5.png "пример групп на сервере")
   
5. Нажмите кнопку **ОК** чтобы закрыть диалоговое окно расширенного поиска.

    > [!IMPORTANT]
    > Убедитесь, что вы выбрали правильная учетная запись для экземпляра. Каждый экземпляр может использовать только свою собственную службу панели запуска и группы, созданной для этой службы. Экземпляры не могут совместно использовать панель запуска службы или рабочих учетных записей.

6. Нажмите кнопку **ОК** еще раз, чтобы закрыть **Выбор пользователя или группы** диалоговое окно.

7. В **Создание имени входа** диалоговом окне щелкните **ОК**. По умолчанию имя входа назначается **общедоступной** роли и имеет разрешение на подключение к ядру СУБД.

## <a name="next-steps"></a>Следующие шаги

+ [Общие сведения о безопасности](../concepts/security.md)
+ [Инфраструктура расширяемости](../concepts/extensibility-framework.md)
