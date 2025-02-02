---
title: Профили агентов | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.profiles.perfprofiles.f1
helpviewer_keywords:
- Agent Profiles dialog box
ms.assetid: 0422e99c-e688-419b-bb4c-c7bebeef1d8d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce4dff443e52ef214e7c43f5df7eb50140937c1e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140460"
---
# <a name="agent-profiles"></a>Профили агентов
  Диалоговое окно **Профили агентов** управляет профилями агентов. Профили агентов предоставляют удобный способ управления параметрами среды выполнения для каждого агента. Каждый агент имеет профиль по умолчанию, а некоторые агенты имеют и дополнительные предопределенные профили. Например, агент слияния имеет профиль «медленной связи», предназначенный для соединений с низкой пропускной способностью. Предопределенных профилей достаточно для создания большинства приложений, однако существует возможность создания пользовательских профилей, позволяющих настроить поведение агента.  
  
## <a name="options"></a>Параметры  
 **Выберите страницу**  
 Выберите в левой панели агент, и профили для этого агента отобразятся в правой панели.  
  
 **По умолчанию для нового**  
 Выберите профиль, который будет использован при создании заданий для агента заданного типа. Например, при создании подписок для публикации слиянием задание агента слияния для каждой подписки будет использовать выбранный профиль. Если нужно изменить профиль существующих заданий, выберите профиль и нажмите **Изменить существующие агенты**.  
  
 **Name**  
 Имя профиля.  
  
 **Тип**  
 Тип профиля: **Пользователь** (пользовательская) или **системы** (предустановленный).  
  
 **Свойства (...)**  
 Нажмите для просмотра значений каждого параметра в профиле агента.  
  
 **Создать**  
 Нажмите для создания нового профиля.  
  
 **Удаление**  
 Выберите пользовательский профиль и нажмите кнопку **Удалить** , чтобы удалить его. Предопределенные профили удалить нельзя.  
  
 **Изменить существующие агенты**  
 Выберите профиль и нажмите **Изменить существующие агенты** , чтобы указать, что все существующие задания для агента данного типа должны использовать выбранный профиль. Например, если создано несколько подписок на публикацию слиянием и нужно изменить профиль, чтобы указать, что задание агента слияния для каждой из этих подписок должно использовать **Профиль агента медленного канала связи**, то выберите этот профиль и нажмите **Изменить существующие агенты**.  
  
## <a name="see-also"></a>См. также  
 [Работа с профилями агента репликации](agents/work-with-replication-agent-profiles.md)   
 [Обзор агентов репликации](agents/replication-agents-overview.md)   
 [Профили агента репликации](agents/replication-agent-profiles.md)  
  
  
