---
title: Расширенная настройка нескольких веб-сайта (собственный режим служб SSRS) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.advancedmultiplewebsiteconfig.F1
ms.assetid: af4ede43-2225-45b5-ae7e-9202411551ba
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 01ed7ed806cc064b05180347fa41905b57c4c98e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096831"
---
# <a name="advanced-multiple-web-site-configuration-ssrs-native-mode"></a>Расширенная настройка нескольких веб-сайтов (службы Reporting Services в собственном режиме)
  Данное диалоговое окно позволяет создавать URL-адреса, используемые для доступа к серверу отчетов и диспетчеру отчетов, и управлять ими. Диалоговое окно **Расширенная настройка нескольких веб-сайтов** позволяет создавать дополнительные URL-адреса, пользовательские URL-адреса, содержащие имя заголовка сайта, а также указывать IP-адреса в формате IPv4 или IPv6.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в собственном режиме.  
  
 Создание нескольких URL-адресов может оказаться целесообразным при необходимости настроить различные способы доступа к серверу отчетов. Например, при доступе к серверу отчетов из внутренней сети и из экстрасети требуются, как правило, различные URL-адреса.  
  
 Чтобы открыть диалоговое окно **Расширенная настройка нескольких веб-сайтов** , щелкните **Дополнительно** на странице **URL-адрес веб-службы** или **URL-адрес диспетчера отчетов** в диспетчере конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Когда диалоговое окно **Расширенная настройка нескольких веб-сайтов** открыто, задать новые URL-адреса или изменить или удалить существующие можно при помощи кнопок **Добавить** или **Изменить** .  
  
 Нажмите кнопку **ОК** , чтобы сохранить внесенные изменения. Если после добавления или удаления URL-адресов диалоговое окно закрыто без предварительного нажатия кнопки **OK**, изменения не сохраняются.  
  
## <a name="options"></a>Параметры  
 **IP-адрес**  
 Идентифицирует компьютер сервера отчетов в сети TCP/IP. Допустимы следующие значения.  
  
-   Значение**Все назначенные** указывает на то, что в URL-адресе, который указывает на приложение сервера отчетов, может быть указан любой IP-адрес, указывающий на компьютер сервера отчетов. Сюда также включаются понятные имена узлов (например, имя компьютера), которые DNS-сервер разрешает в IP-адрес этого компьютера. Это значение URL-адреса служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] по умолчанию.  
  
-   Значение**Все неназначенные** указывает, что сервер отчетов будет принимать любые запросы, не имеющие точного совпадения с IP-адресом или именем узла. Не следует выбирать это значение, если оно уже используется другим веб-приложением. Это может привести к нарушению его работы.  
  
-   Значение**127.0.0.1** предназначено для доступа к узлу localhost. Используется для локального администрирования компьютера сервера отчетов. Если выбрать только это значение, то доступ к приложению будут иметь только пользователи, которые вошли в систему компьютера сервера отчетов локально.  
  
-   Значение*nnn.nnn.nnn.nnn* — адрес IPv4 платы сетевого адаптера компьютера. Если в сети используются адреса IPv6, IP-адрес будет 128-разрядное значение 8 4-байтных полей, аналогичный следующему формату: \<заголовок >:*nnnn:nnnn:nnnn:nnnn*.  
  
     Если в компьютере установлено несколько сетевых плат, то будут выведены IP-адреса для каждой из них. Если выбрано только это значение, то доступ для приложений будет ограничен только этим IP-адресом (и любым именем узла, которое сервер DNS с ним сопоставит). Доступ к компьютеру сервера отчетов ни по имени localhost, ни по IP-адресам других установленных на нем плат сетевых адаптеров будет невозможен.  
  
 **Порт**  
 Определяет порт, на котором сервер отчетов отслеживает запросы. По умолчанию используется порт 80. При использовании порта 80 не нужно указывать его в URL-адресе. При использовании любой другой номер порта, необходимо всегда включить его в URL-адрес (например, http://localhost:8181/reports).  
  
 **Заголовок узла**  
 Если заголовок узла, соответствующий компьютеру, уже определен на сервере доменных имен, его можно указать в URL-адресе, настраиваемом для доступа к серверу отчетов.  
  
 Заголовок узла представляет собой уникальное имя, позволяющее нескольким веб-сайтам совместно использовать один и тот же IP-адрес и порт. По сравнению с IP-адресами и номерами порта имена заголовков узлов легче запоминать и проще вводить. Пример имени заголовка узла: www.adventure-works.com.  
  
 **SSL-порт**  
 Задает порт для соединений по протоколу SSL. По умолчанию номер порта SSL равен 443.  
  
 **SSL-сертификат**  
 Определяет имя SSL-сертификата, установленного на компьютере. Если сертификат соответствует шаблону, его можно использовать для соединения с сервером отчетов.  
  
 Указывает полное имя компьютера, для которого регистрируется сертификат. Указанное имя должно быть идентично имени, на которое зарегистрирован этот сертификат.  
  
 Для данного параметра необходим установленный сертификат. Можно также изменить параметры конфигурации UrlRoot в файле RSReportServer.config, чтобы они указывали полное имя компьютера, для которого регистрируется сертификат. Дополнительные сведения см. в разделе [Настройка соединений SSL для сервера отчетов, работающего в собственном режиме](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) электронной документации по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Кому выдан**  
 Отображает имя компьютера, для которого создан сертификат.  
  
 **Добавить**  
 Используется для определения дополнительного URL-адреса.  
  
 **Изменить**  
 Используется для изменения любой части синтаксиса URL-адреса.  
  
 **Удалить**  
 Используется для удаления выбранного URL-адреса из списка.  
  
## <a name="see-also"></a>См. также  
 [Использование диспетчера конфигурации служб Reporting Services (собственный режим)](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Настройка URL-адреса (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Настройка URL-адресов сервера отчетов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
