---
title: Задача Hadoop Hive | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoophivetask.f1
ms.assetid: 10ff37c0-9f3f-442a-889b-c351afbdc74c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1d9ae752dabee68d6fae786675e640773009f4b7
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727622"
---
# <a name="hadoop-hive-task"></a>Задача Hadoop Hive

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Задача Hadoop Hive используется для запуска скрипта Hive в кластере Hadoop.  
  
 Чтобы добавить задачу Hadoop Hive, перетащите ее в конструктор. Затем дважды щелкните задачу или щелкните правой кнопкой мыши и выберите команду **Изменить**, чтобы открыть диалоговое окно **Редактор задачи Hadoop Hive** .  
  
 ![Редактор задачи Hadoop Hive](../../integration-services/control-flow/media/hadoop-hive-task.png "Редактор задачи Hadoop Hive")  
  
## <a name="options"></a>Параметры  
 Настройте следующие параметры в диалоговом окне **Редактор задачи Hadoop Hive** .  
  
|Поле|Описание|  
|-----------|-----------------|  
|**Hadoop Connection (Подключение Hadoop)**|Укажите существующий диспетчер подключений Hadoop или создайте новый. Этот диспетчер указывает, где размещена служба WebHCat.|  
|**Тип источника**|Укажите тип источника запроса. Доступные значения: **ScriptFile** (Файл сценария) и **DirectInput**(Прямой ввод).|  
|**InlineScript (Встроенный сценарий)**|Если значение **SourceType** (Тип источника) — **DirectInput**(Прямой ввод), укажите скрипт hive.|  
|**HadoopScriptFilePath (Путь к файлу сценария Hadoop)**|Если значение **SourceType** (Тип источника) — **ScriptFile**(Файл сценария), укажите путь к файлу скрипта в Hadoop.|  
|**TimeoutInMinutes (Время ожидания в минутах)**|Укажите время ожидания в минутах. Задание Hadoop останавливается, если оно не завершилось до истечения времени ожидания. Укажите 0, чтобы запланировать асинхронное выполнение задания Hadoop.|  
  
## <a name="see-also"></a>См. также:  
 [Диспетчер подключений Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
