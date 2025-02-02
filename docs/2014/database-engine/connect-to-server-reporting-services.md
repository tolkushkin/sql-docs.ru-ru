---
title: Соединение с сервером (службы Reporting Services) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.reportserver.f1
ms.assetid: ef81b658-8eb5-4636-ac81-eead10cc7b9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41e0ca3ee7ccaa7bb57e5667092c0660e35c4c52
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808683"
---
# <a name="connect-to-server-reporting-services"></a>Соединение с сервером (службы Reporting Services)
  Используйте это диалоговое окно для просмотра или задания параметров при соединении со службами [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
## <a name="options"></a>Параметры  
 **Тип сервера**  
 При регистрации сервера из **обозревателя объектов**выберите тип сервера для подключения: [!INCLUDE[ssDE](../includes/ssde-md.md)], службы Analysis Services, службы Reporting Services или службы Integration Services. В остальной части диалогового окна показаны параметры, которые применяются только к выбранному типу сервера. При регистрации сервера c панели **Зарегистрированные серверы**поле **Тип сервера** не может быть изменено и совпадает с типом сервера, показанного в компоненте **Зарегистрированные серверы** . Чтобы зарегистрировать сервер другого типа, выберите компонент [!INCLUDE[ssDE](../includes/ssde-md.md)], службы Analysis Services, службы Reporting Services или службы Integration Services на панели инструментов **Зарегистрированные серверы** , прежде чем начать регистрацию нового сервера.  
  
 **Имя сервера**  
 Значение, которое необходимо ввести, определяется серверным режимом того экземпляра сервера отчетов, с которым производится соединение.  
  
 Для сервера отчетов, работающего в собственном режиме, задайте экземпляр сервера отчетов, с которым производится соединение. При использовании экземпляра по умолчанию имя сервера обычно совпадает с именем компьютера. Если устанавливался именованный экземпляр, добавьте имя экземпляра, то к имени сервера в следующем формате: \<servername >\\< имя_экземпляра\>. Службы Reporting Services используют в качестве ограничителя для имени экземпляра обратную косую черту.  
  
 Для сервера отчетов, работающего в режиме интеграции с SharePoint, необходимо указать сайт SharePoint. Можно указать любой сайт из семейства сайтов, интегрированного со службами [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Введенный URL-адрес должен содержать префикс HTTP или HTTPS. Чтобы подключиться к сайту SharePoint из среды Management Studio, необходимо иметь разрешение на доступ к нему. Уровень разрешений определяет набор объектов, которые доступны для просмотра и управления. Дополнительные сведения см. в разделе [соединиться с сервером отчетов в среде Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
 **Authentication**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] можно настроить для принятия запросов проверки подлинности Windows или запросов проверки подлинности с помощью форм, обрабатываемых нестандартным модулем проверки подлинности. При соединении со службами [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]выберите один из следующих режимов проверки подлинности.  
  
 **Режим проверки подлинности Windows (проверка подлинности Windows)**  
 Подключитесь к экземпляру сервера отчетов, используя учетные данные [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows.  
  
 **Обычная проверка подлинности**  
 Установите соединение, используя **Обычную проверку подлинности** , если экземпляр служб Reporting Services настроен на использование обычной проверки подлинности.  
  
 **Проверка подлинности с помощью форм**  
 Установите соединение, используя **Проверку подлинности с помощью форм** , если экземпляр служб Reporting Services настроен на использование пользовательского модуля проверки подлинности.  
  
 **Имя пользователя**  
 Введите имя входа, которое будет использоваться при соединении. Этот параметр доступен только в том случае, если выбран режим **Обычная проверка подлинности** или **Проверка подлинности с помощью форм**.  
  
 **Пароль**  
 Введите пароль для имени пользователя. Этот параметр может редактироваться только в том случае, если выбран режим **Обычная проверка подлинности** или **Проверка подлинности с помощью форм**.  
  
 **Подключить**  
 Нажмите, чтобы подключиться к выбранному выше серверу.  
  
 **Параметры**  
 Нажмите, чтобы вывести дополнительные параметры соединения с сервером, такие как регистрация сервера и запоминание пароля.  
  
## <a name="see-also"></a>См. также  
 [Настройка подключения к базе данных сервера отчетов (диспетчер конфигураций служб Reporting Services)](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Подключение к серверу отчетов в среде Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Проверка подлинности с использованием сервера отчетов](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
