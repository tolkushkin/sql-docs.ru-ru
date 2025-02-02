---
title: Новый или редактирование регистрации сервера (вкладка "Общие") (службы Reporting Services) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0e6d6d3ad57726c42556c9ecc2662edce102e57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844280"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>Создание или редактирование регистрации сервера (вкладка «Общие») (службы Reporting Services)
  В этой вкладке указываются параметры при регистрации экземпляра служб [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Чтобы открыть эту страницу, нажмите кнопку **Службы Reporting Services** на панели инструментов **Зарегистрированные серверы** , щелкните правой кнопкой мыши любую зарегистрированную группу серверов, например **Службы Reporting Services**, выберите раздел **Создать**и выберите пункт **Регистрация сервера**.  
  
## <a name="options"></a>Параметры  
 **Тип сервера**  
 При регистрации сервера из окна "Зарегистрированные серверы" поле **Тип сервера** предназначено только для чтения и соответствует типу сервера, отображенному на панели **Зарегистрированные серверы** . Чтобы зарегистрировать другой тип сервера, щелкните нужный сервер на панели инструментов **Зарегистрированные серверы** , прежде чем регистрировать новый сервер.  
  
 **Имя сервера**  
 Укажите экземпляр сервера отчетов, к которому необходимо подключиться. В среде [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]возможно получить доступ к серверу отчетов, используя имя его экземпляра. Может иметься по одному экземпляру сервера отчетов для каждого устанавливаемого экземпляра SQL Server. Если используется экземпляр по умолчанию, введите имя экземпляра SQL Server. Если используется именованный экземпляр, укажите имя экземпляра в формате MSSQL$имя_экземпляра для подключения к серверу отчетов.  
  
 **Authentication**  
 Проверка подлинности для сервера отчетов производится через службы IIS. При подключении к службам Reporting Services выберите один из следующих режимов проверки подлинности.  
  
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
  
 **Запомнить пароль**  
 Сохранить введенный пароль. Этот параметр доступен, только если выбран режим **Обычная проверка подлинности** или **Проверка подлинности с помощью форм**.  
  
> [!NOTE]  
>  Чтобы пароль больше не запоминался, снимите этот флажок и нажмите кнопку **Сохранить**.  
  
 **Имя зарегистрированного сервера**  
 Имя, которое будет отображаться на панели «Зарегистрированные серверы». Это имя необязательно должно совпадать с именем, указанным в поле **Имя сервера** .  
  
 **Описание зарегистрированного сервера**  
 Введите необязательное описание сервера.  
  
 **Тест**  
 Нажмите для проверки соединения с сервером, заданным в поле **Имя сервера**.  
  
 **Сохранить**  
 Нажмите эту кнопку, чтобы сохранить настройки зарегистрированного сервера.  
  
  
