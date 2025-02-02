---
title: Параметры (страница панели мониторинга SQL Server AlwaysOn) | Документы Майкрософт
description: Описание страницы "Параметры" на панели мониторинга Always On в SQL Server.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Alwayson.Dashboard
ms.assetid: 4369b588-e982-4b57-80a1-beb2e879ce0b
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: c08b28bfd888345e1fa5a88ef2a0e3d8aa912ac7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798237"
---
# <a name="options-sql-server-always-on-dashboard-page"></a>Параметры (страница панели мониторинга SQL Server AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Для настройки панели мониторинга AlwaysOn используйте страницу **SQL Server AlwaysOn Dashboard** (Панель мониторинга SQL Server) диалогового окна [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]Параметры**в среде**.  
  
 **Открытие этой страницы**  
  
 В меню **Сервис** выберите пункт **Параметры**, откройте папку **SQL Server AlwaysOn** и выберите **Панель мониторинга**.  
  
## <a name="on-this-page"></a>На этой странице  
 **Включить автоматическое обновление.**  
 Выберите, чтобы включить автоматическое обновление. Доступны следующие возможности:  
  
-   В поле **Интервал обновления (в секундах)** отображается количество секунд, через которое панель будет обновлена. Значение по умолчанию — 30. Если автоматическое обновление включено, значение в этом поле можно изменить, чтобы указать новый интервал обновления.  
  
-   В поле **Количество повторных попыток подключения** отображается, сколько раз панель мониторинга будет пытаться установить соединение с экземпляром [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , на котором расположена реплика доступности группы доступности, мониторинг которой выполняет панель. Значение по умолчанию — 65535. Если автоматическое обновление включено, значение в этом поле вы можете изменить, чтобы указать другое количество попыток.  
  
 **Включить собственную, определяемую пользователем политику AlwaysOn.**  
 Если вы определили собственную политику AlwaysOn, выберите этот параметр, чтобы включить ее.  
  
## <a name="see-also"></a>См. также:  
 [Использование панели мониторинга AlwaysOn (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
