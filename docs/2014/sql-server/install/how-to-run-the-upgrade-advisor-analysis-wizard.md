---
title: Практическое руководство. Запустить мастер анализа помощника по обновлению | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1464b55724e4305f2833ddce34e27170c7afd484
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094828"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>Практическое руководство. Запуск мастера анализа помощника по обновлению
  Мастер анализа помощника по обновлению запускается с начальной страницы помощника по обновлению. В этом разделе описывается запуск мастера анализа помощника по обновлению.  
  
> [!IMPORTANT]
>  При работе мастера анализа помощника по обновлению помощник по обновлению сохраняет отчеты в папку отчетов по умолчанию. Однако средство просмотра отчетов отображает только пять последних сохраненных отчетов. По умолчанию для отчетов находится в «Мои документы»\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \110\отчеты».  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>Запуск мастера анализа помощника по обновлению  
  
1.  На начальной странице помощника по обновлению щелкните ссылку **Запустить мастер анализа помощника по обновлению**.  
  
2.  На  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] компоненты** введите имя сервера в **имя_сервера** , а затем щелкните **найти**. Учитывайте следующие рекомендации при выборе имени сервера.  
  
    -   Чтобы проверить некластеризованные экземпляры, введите имя компьютера.  
  
    -   Для просмотра кластеризованных экземпляров введите виртуальное имя [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Для просмотра некластеризованных компонентов, установленных на узле кластера, введите имя узла.  
  
    > [!WARNING]  
    >  Помощник по обновлению не поддерживает соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , который не настроен на использование стандартного порта (1433) для соединений с клиентами. Если требуется установить соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , который не использует стандартный порт (1433), создайте псевдоним с помощью IP-адреса и порта. Дополнительные сведения о настройке клиентских протоколов и создании псевдонима для экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] см. в разделе [Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md).  
    >   
    >  Если у вас нет [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] установлен на компьютере, на котором выполняется помощник по обновлению, нажмите кнопку **запустить**, а затем запустите `cliconfg`. Откроется диалоговое окно **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client Network Utility** . Для создания псевдонима перейдите на вкладку **Псевдоним** .  
  
3.  Просмотрите список обнаруженных компонентов, при необходимости измените выбор и нажмите кнопку **Далее**.  
  
4.  На странице **Параметры соединения** выберите экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , который необходимо просмотреть, укажите метод проверки подлинности и при необходимости введите имя и пароль, после чего нажмите кнопку **Далее**.  
  
     Имя экземпляра по умолчанию — MSSQLSERVER.  
  
5.  Введите запрошенную информацию по выбранным компонентам. Дополнительные сведения об отдельных диалоговых окон, см. в разделе [Справочник по интерфейсу пользователя помощника по обновлению](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
6.  На странице **Подтверждение настроек помощника по обновлению** просмотрите введенную информацию. Можно выбрать **отправлять отчеты в [!INCLUDE[msCoName](../../includes/msconame-md.md)]**  Если вы хотите отправить свой отчет об обновлении. Здесь же можно просмотреть сведения о политике конфиденциальности.  
  
7.  Щелкните **Запуск** , чтобы проанализировать выбранный экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
8.  После завершения анализа щелкните **Запустить отчет** , чтобы просмотреть обнаруженные проблемы, связанные с обновлением.  
  
## <a name="see-also"></a>См. также  
 [Как Запустите помощник по обновлению](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Запуск помощника по обновлению &#40;пользовательского интерфейса&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Работа с помощником по обновлению](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
