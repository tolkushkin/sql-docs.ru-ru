---
title: Отзыва о телеметрии - Analytics Platform System | Документация Майкрософт
description: Отправка отзыва о телеметрии в корпорацию Майкрософт для Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 442505d470d1c7b7a82a02610d650d9f0b8c8d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678380"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Отправка отзыва о телеметрии в корпорацию Майкрософт для системы платформы аналитики
Система Analytics Platform System имеет функцию необязательные данные телеметрии, которая отправляет данные в консоли администрирования Microsoft. 
  
> [!NOTE]  
> В этом выпуске корпорация Майкрософт не следит за активно данные телеметрии. Данные собираются только в целях анализа.  
  
## <a name="privacy"></a>О конфиденциальности  
Чтобы обеспечить защиту конфиденциальности, максимальное, APS поставляется без Включение телеметрии. Прежде чем включать эту функцию, сначала ознакомьтесь с [заявлении о конфиденциальности системы платформы аналитики Майкрософт](https://go.microsoft.com/fwlink/?LinkId=400902). Несколько регионов, скрипт PowerShell, описанных ниже.  
  
## <a name="enable"></a>Включить Телеметрию  
**Перенаправление запросов DNS:** Отправка данных телеметрии в корпорацию Майкрософт требует Analytics Platform System для подключения к Интернету через DNS-сервера пересылки. Чтобы включить эту функцию, необходимо включить DNS перенаправление на всех узлах и виртуальных машин рабочих нагрузок. Вызвать `Enable-RemoteMonitoring` с `SetupDnsForwarder` параметр, чтобы правильно настроить перенаправление запросов DNS и включить телеметрию. Вызвать `Enable-RemoteMonitoring` без `SetupDnsForwarder` параметр, если перенаправление запросов DNS уже настроена и вы хотите включить мониторинг тактовых импульсов.  
  
> [!IMPORTANT]  
> Включение перенаправление запросов DNS открывает подключение к Интернету для всех узлов и виртуальных машин рабочих нагрузок.  
  
#### <a name="to-enable-feedback"></a>Чтобы включить отзыв  
  
1.  Используя учетную запись администратора домена устройство, подключение к узлу элемента управления (<strong>*appliance_domain*-CTL01</strong>) и откройте командную строку, используя учетные данные администратора Windows.  
  
2.  Перейдите к следующему каталогу: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Импорт модуля `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Для импорта, вам необходимо использовать две точки в команде.  
  
    **Пример.**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Вызвать `Enable-RemoteMonitoring` команды.  
  
    > [!NOTE]  
    > В скрипте предполагается, что подключение к Интернету работает правильно и не проверяет подключение к Интернету.  
  
    1.  При первом включении данные телеметрии, используйте следующую команду, чтобы убедиться, что все DNS-серверы пересылки правильно настроены. В этом примере замените IP-пересылки DNS адрес `xx.xx.xx.xx` с IP-адрес сервера пересылки DNS-адресом в вашей среде.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Когда DNS-серверы пересылки уже настроены, например, при повторном включении ранее отключенного телеметрии, используйте следующую команду Включить телеметрию без настройки пересылки DNS.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Вам будет предложено чтения и подтверждаете, что APS будет собирать сведения об устройстве. Будет ссылка на заявление о конфиденциальности APS, который можно скопировать и вставить в любом интернет-браузере для просмотра.  
  
6.  Введите **Y** принять и согласиться на отзывы или введите **N** не принимает.  
  
7.  Если вы ввели **Y** будет существовать ряд команд, которые будут выполняться, что позволит данные телеметрии (и, при необходимости, DNS-сервер пересылки) функция на устройстве. Если вы видите, все ошибки и сведения, которые помогают впечатление, что команда не выполнена успешно обратиться в службу поддержки.  
  
Если вы ввели **N**, команды не будет запускаться и эта функция не будет включен, и пользователи могут выполнять больше нечего.  
  
Нет никакого вреда от выполнения `Enable-RemoteMonitoring` команды несколько раз. Если DNS-сервер пересылки уже имеет вы получите предупреждение о том, что это так.  
  
## <a name="disable"></a>Отключить сбор данных телеметрии  
Отключение телеметрии остановит все операции, передающие информацию о состоянии устройства, APS, мониторинг службы в облаке.  
  
> [!IMPORTANT]  
> Выполнение этой операции не отключает вашего DNS-сервер пересылки или Интернету, который используется другими компонентами в устройстве.  
  
#### <a name="to-disable-telemetry"></a>Чтобы отключить сбор данных телеметрии  
  
1.  Используя учетную запись администратора домена устройство, подключение к узлу элемента управления (<strong>*appliance_domain*-CTL01</strong>) и откройте окно PowerShell с правами администратора.  
  
2.  Перейдите к следующему каталогу: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Импорт модуля `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Для импорта, вам необходимо использовать две точки в команде.  
  
    **Пример.**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Вызвать `Disable-RemoteMonitoring` команду без параметров. Эта команда будет остановлена, Отправка обратной связи. (Это не повлияет локального мониторинга.) Тем не менее команда будет не отключить DNS-сервер пересылки и/или отключить подключения к Интернету. Это необходимо сделать вручную после успешного отключения обратной связи.  
  
    **Пример.**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Если вы видите, все ошибки и сведения, которые помогают впечатление, что команда не выполнена успешно обратиться в службу поддержки.  
  
Нет никакого вреда от выполнения `Disable-RemoteMonitoring` команды несколько раз.  
  
## <a name="next-steps"></a>Следующие шаги
Дополнительные сведения см. в разделе:
- [Мониторинг устройства с помощью консоли администрирования &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Мониторинг устройства с помощью системных представлений &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Мониторинг устройства с помощью System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Используйте DNS-сервера пересылки для разрешения имен DNS не является специализированным &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
