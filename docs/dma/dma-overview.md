---
title: Обзор помощника по миграции данных (SQL Server) | Документация Майкрософт
description: Узнайте, как использовать Data Migration Assistant для переноса баз данных SQL Server на другой сервер SQL или баз данных Azure
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: jroth
ms.openlocfilehash: 2766005287a522a84d209d995be0de9a94e45c02
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794346"
---
# <a name="overview-of-data-migration-assistant"></a>Общие сведения о Data Migration Assistant
Помогает Data Migration Assistant (DMA), при обновлении до современную платформу данных путем обнаружения проблем совместимости, которые могут повлиять на функциональность базы данных в новую версию SQL Server или базы данных SQL Azure. DMA рекомендует производительности и улучшения надежности вашей целевой среды и позволяет переносить схемы, данных и неавтономные объекты с исходного сервера на целевой сервер.

> [!NOTE] 
> Для крупной миграции (с точки зрения количества и размера баз данных), мы рекомендуем использовать [Azure Database Migration Service](/azure/dms/dms-overview), который можно перенести базы данных в нужном масштабе.
  
## <a name="get-data-migration-assistant"></a>Получение Data Migration Assistant
Чтобы установить DMA, загрузите последнюю версию средства из [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=53595), а затем запустите **DataMigrationAssistant.msi** файл.

## <a name="capabilities"></a>Возможности
- Оценка локальных экземпляров SQL Server, миграции баз данных Azure SQL. Рабочий процесс оценки поможет вам обнаружить следующие проблемы, которые могут повлиять на перенос базы данных Azure SQL и содержатся подробные указания по их устранению.

  - Проблемы, блокирующие миграцию: Обнаруживает проблемы совместимости, которые блокируют перенос базы данных на локальном SQL Server для баз данных SQL Azure. DMA предоставляет рекомендации, которые помогут вам решить эти проблемы.

  - Частично поддерживаемые или неподдерживаемые функции: Определяет частично поддерживаемые или неподдерживаемые функции, которые в настоящее время используются на исходный экземпляр SQL Server. DMA предоставляет полный набор рекомендаций, альтернативные подходы, доступные в Azure, а также меры по устранению, таким образом, чтобы их можно включить в ваших проектах миграции.

- Находят проблемы, которые могут повлиять на обновление на локальный сервер SQL Server. Они называются проблем совместимости и организованы в следующие категории:

  - Критические изменения
  - Изменения в поведении
  - Устаревшие функции

- Узнайте о новых функциях в целевую платформу SQL Server, базы данных могут использовать преимущества после обновления. Они называются рекомендации функций и организованы в следующие категории:

  - Производительность
  - безопасность
  - Память

- Миграция с локальным экземпляром SQL Server для современных SQL экземпляра, размещенного на локальном сервере или на виртуальной машине Azure (ВМ), доступный в локальной сети. На виртуальной Машине Azure может осуществляться с помощью VPN или других технологий. Рабочий процесс переноса поможет перенести следующие компоненты:

  - Схемы баз данных
  - Данные и пользователей
  - роли сервера;
  - Имена входа SQL Server и Windows

- После успешной миграции приложения могут подключаться к целевым базам данных SQL Server без проблем.

## <a name="prerequisites"></a>предварительные требования
Чтобы выполнить оценку, необходимо быть членом группы SQL Server **sysadmin** роли.

## <a name="supported-source-and-target-versions"></a>Поддерживаемые версии исходной и целевой
DMA заменяет все предыдущие версии SQL Server Upgrade Advisor и должен использоваться для обновления для большинства версий SQL Server. Ниже приведены поддерживаемые версии исходной и целевой.

**Источники**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 на Windows

**Целевые объекты**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 в Windows и Linux
- База данных SQL Azure
- Управляемый экземпляр Базы данных SQL Azure

## <a name="see-also"></a>См. также
[Оценка миграции SQL Server](../dma/dma-assesssqlonprem.md)     
[Помощник по миграции данных: Параметры конфигурации](../dma/dma-configurationsettings.md)     
[Служба "Миграция" на локальном сервере SQL Server с помощью Data Migration Assistant](../dma/dma-migrateonpremsql.md)     
[Помощник по миграции данных: Советы и рекомендации](../dma/dma-bestpractices.md)     
