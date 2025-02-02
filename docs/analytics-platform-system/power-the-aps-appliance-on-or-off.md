---
title: Питания устройства, включить или отключить - Analytics Platform System | Документация Майкрософт
description: Power устройства, включить или отключить для Analytics Platform System
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 994b0f94448b7fb7901734b2ae737e26be23900f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678632"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Power устройства, включить или отключить для Analytics Platform System
В этом разделе описывается, как степень вашей Systemappliance платформы Analytics включения и выключения питания, на котором выполняется Parallel Data Warehouse. Используйте этот раздел при перемещении в Analytics Platform System appliance, или степень устройство с поддержкой после разрушительного сбоя.  
  
Включение и выключение питания устройства не так же, как запуск и остановка служб устройства. Сведения по этой теме см. в разделе [состояние служб PDW &#40;Analytics Platform System&#41;](pdw-services-status.md). Сведения о включением или отключением параллельного хранилища данных SQL Server 2008 см. в файле справки параллельное хранилище данных SQL Server 2008. Сведения о включением или отключением SQL Server 2012 AU1 или AU2 Parallel Data Warehouse см. в разделе файла справки для этих версий.  
  
При эти инструкции указывать на подключение к узлу SQL Server PDW, соединение может быть локальным, с помощью подключенных устройств (KVM) или удаленного доступа с помощью удаленного рабочего стола. Некоторые действия должны быть физически (включение питания коммутатор), а также некоторые (например, завершение работы) могут быть физические или с помощью Windows команды.  
  
Подключения к SQL Server PDW узлы можно при помощи IP-адресов, назначенных на узлах или с **HST01** компьютера либо при помощи **Диспетчер отказоустойчивости кластеров** (**cluadmin.msc**) или **диспетчера Hyper-V** (**virtmgmt.msc**) приложения и щелкните правой кнопкой мыши имя узла.  
  
## <a name="PowerOff"></a>Выключение устройства  
  
### <a name="before-you-begin"></a>Перед началом  
Перед выключение устройства, завершите все действия на устройстве. Чтобы завершить все действия:  
  
-   Используйте **сеансы** странице консоли администрирования для идентификации текущих пользователей. Свяжитесь с ним и попросите его выход.  
  
-   При необходимости можно использовать **KILL** инструкцию, чтобы принудительно завершить клиентского соединения. Будьте внимательны при уничтожении подключений. При перебоях в работе, некоторые транзакций процессы, такие как долго выполняющегося обновления, необходимо действие отката до SQL Server можно выполнить восстановление базы данных. Откат частично завершенной update или delete, может занять много времени.  
  
### <a name="to-power-off-the-appliance"></a>Чтобы отключить питание устройства  
  
> [!WARNING]  
> Все действия должны выполняться в порядок, и каждый шаг необходимо выполнить, прежде чем будет выполнен следующий шаг, если не указано иное. Выполнив действия, не по порядку или без ожидания завершения выполнения каждого шага может вызывать ошибки при модуль включен в дальнейшем.  
  
1.  Подключитесь к узлу управления PDW (**_PDW_region_-CTL01** ) и войдите, используя учетную запись администратора домена Analytics Platform System appliance.  
  
2.  Запустите `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` открыть **Configuration Manager**.  
  
3.  В Configuration Manager в разделе **топологии хранилище параллельных данных** меню, нажмите кнопку **состояние служб** , а щелкните **остановить регион** для остановки службы PDW.   
  
4.  Подключение к  **_appliance_domain_-HST01** и войдите, используя учетную запись администратора домена устройства.  
  
5.  С помощью **Диспетчер отказоустойчивости кластеров** подключиться к  **_appliance_domain_-WFOHST01** кластера, если подключение не автоматически, а затем в области навигации нажмите кнопку **Ролей**. В **ролей** области:  
  
    1.  Множественный выбор всех виртуальных машин. Щелкните их правой кнопкой мыши и выберите **завершение работы**.  
  
    2.  Дождитесь завершения, завершения работы всех выбранных виртуальных машин.  
  
6.  Закрыть **Диспетчер отказоустойчивости кластеров** приложения.  
  
7. Завершите работу всех серверов, за исключением  **_appliance_domain_-HST01**.  
  
8. Завершение работы  **_appliance_domain_-HST01** сервера.  
  
9. Завершите работу блокам распределения питания (PDU).  
  
## <a name="PowerOn"></a>Питания на устройстве  
  
### <a name="to-power-on-the-appliance"></a>Для включения устройства  
  
> [!WARNING]  
> Все действия должны выполняться в порядок, и каждый шаг необходимо выполнить, прежде чем будет выполнен следующий шаг, если не указано иное. Выполнив действия, не по порядку или без ожидания завершения выполнения каждого шага может вызвать ошибки запуска.  
  
1.  Включите блокам распределения питания (PDU) и дождитесь переключатели для автоматического запуска.  
  
2.  Включите  **_appliance_domain_-HST01** сервера.  
  
3.  Войдите в  **_appliance_domain_-HST01** как администратор домена приложения.  
  
4.  Запуск **диспетчера Hyper-V** программы (**virtmgmt.msc**) и подключитесь к  **_appliance_domain_-HST01** Если не подключены по умолчанию.  
  
    1.  Если не удается подключиться по имени, так как  **_PDW_region_-AD01** является не запущена, попробуйте подключиться с помощью IP-адрес.  
  
    2.  В **виртуальных машин** панели найдите  **_PDW_region_-AD01** и убедитесь, что он работает. Если нет, запустите эту виртуальную Машину и дождитесь ее полного запуска.  
  
5.  Возможности на остальных серверах в устройстве.  
  
6.  Хотя на **HST01** войти в систему как администратор домена приложения, из **диспетчера Hyper-V**:  
  
    1.  Подключение к  **_appliance_domain_-HST02**.  
  
    2.  В **виртуальных машин** панели найдите  **_PDW_region_-AD02** и убедитесь, что он работает.  Если нет, запустите эту виртуальную Машину и дождитесь ее полного запуска.  
  
7.  С помощью **Диспетчер отказоустойчивости кластеров** подключиться к  **_appliance_domain_-WFOHST01** кластера, если подключение не автоматически, а затем в  **Навигации** панели щелкните **ролей**. В **ролей** области:  
  
    1.  Множественный выбор, все виртуальные машины, щелкните их правой кнопкой мыши и нажмите кнопку **запустить**.  
  
    2.  Подождите, пока все выбранные виртуальные машины, завершить запуск перед переходом к следующему шагу.  
  
    3.  При необходимости для виртуальных машин, при отработке отказа, завершать их работу, переместите их и перезапустить их на соответствующие основного узла.  
  
8. Отключиться от **HST01** при необходимости.  
  
9. Подключение к  **_PDW_region_-CTL01** с помощью учетной записи администратора устройства.  
  
10. Запустите `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` для запуска **Configuration Manager**.  
  
11. В **Configuration Manager**в **топологии хранилище параллельных данных** меню, нажмите кнопку **состояние служб** , а щелкните **запустить регион**запуск служб PDW.  
  
### <a name="to-verify-the-appliance-health"></a>Чтобы проверить работоспособность устройства  
После запуска устройства, откройте **консоли администрирования** и проверьте страницу работоспособности для оповещений, которые могут указывать условия сбоя. Дополнительные сведения см. в разделе [мониторинг устройства с помощью консоли администрирования &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>См. также  
[Задачи управления устройствами &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
