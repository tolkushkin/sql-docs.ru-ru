---
title: Пользовательские свойства задачи "Управление CDC" | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2a073699-79a2-4ea1-a68e-fc17a80b74ba
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 87aca78d68921b2f90cde68d52eff06df7044a4c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832896"
---
# <a name="cdc-control-task-custom-properties"></a>Пользовательские свойства задач управления CDC
  Пользовательские свойства задачи «Управление CDC» описаны в следующей таблице. Все свойства доступны для чтения и записи.  
  
|Имя свойства|Тип данных|Описание|  
|-------------------|---------------|-----------------|  
|Соединение|Соединение ADO.NET|Соединение ADO.NET с базой данных CDC [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] для доступа к таблицам изменений и к информации состояния CDC, если она хранится в той же базе данных.<br /><br /> Соединение должно быть установлено с базой данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которая включена для CDC и в которой находится выбранная таблица изменений.|  
|TaskOperation|Integer (перечисление)|Выбранная операция для задачи «Управление CDC». Возможными значениями являются **Отметить начало начальной загрузки**, **Отметить конец начальной загрузки**, **Отметить начало CDC**, **Получить диапазон обработки**, **Отметить обработанный диапазон**и **Сбросить состояние CDC**.<br /><br /> Если выбрано **MarkCdcStart**, **MarkInitialLoadStart**или **MarkInitialLoadEnd** при работе с CDC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (т е. с базой данных, отличной от Oracle), то пользователем, указанным в диспетчере соединений, должен быть  **db_owner** или **sysadmin**.<br /><br /> Дополнительные сведения об этих операциях см. в разделах [CDC Control Task Editor](../cdc-control-task-editor.md) и [CDC Control Task](cdc-control-task.md).|  
|OperationParameter|String|В настоящее время используется с операцией **MarkCdcStart** . Этот параметр допускает использование дополнительного ввода, требуемого для конкретной операции. Например, это может быть номер LSN, требуемый для операции **MarkCdcStart**|  
|StateVariable|String|Переменная пакета служб SSIS, которая сохраняет состояние CDC текущего контекста CDC. Задача «Управление CDC» выполняет чтение и запись состояния в **StateVariable** , но не загружает его и не сохраняет в постоянном хранилище, если не выбран параметр **AutomaticStatePersistence** . См. раздел [Определение переменной состояния](../data-flow/define-a-state-variable.md).|  
|AutomaticStatePersistence|Логическое значение|Задача «Управление CDC» выполняет чтение состояния CDC из переменной пакета «Состояние CDC». Вслед за выполнением операции задача «Управление CDC» обновляет значение переменной пакета «Состояние CDC». Свойство **AutomaticStatePersistence** служит для задачи «Управление CDC» указанием на то, кто отвечает за сохранение значения состояния CDC между прогонами пакета служб SSIS.<br /><br /> Если это свойство равно **TRUE**, то задача «Управление CDC» автоматически загружает значение переменной состояния CDC из таблицы состояний. Задача «Управление CDC» при обновлении значения переменной состояния CDC обновляет также ее значение в том же состоянии **table.stores**, обновляет состояние в специальной таблице и обновляет переменную состояния. Разработчик может управлять тем, в какой базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должна содержаться эта таблица состояний, и задавать ее имя. Структура этой таблицы состояний является стандартной.<br /><br /> Если задано значение **FALSE**, задача «Управление CDC» не обеспечивает сохранение значения состояния. Если задано значение TRUE, задача «Управление CDC» сохраняет значение состояния в специальной таблице и обновляет переменную StateVariable.<br /><br /> Значение по умолчанию равно **TRUE**, а это указывает, что сохраняемость состояния обновляется автоматически.|  
|StateConnection|Соединение ADO.NET|Соединение ADO.NET с базой данных, в которой находится таблица состояний при использовании параметра **AutomaticStatePersistence**. Значением по умолчанию является то же значение, что и для свойства **Connection**.|  
|StateName|String|Имя, связанное с хранимым состоянием. Пакеты полной загрузки и пакеты CDC, которые работают с тем же контекстом CDC, задают общее имя контекста CDC. Это имя используется для поиска строки состояния в таблице состояний.<br /><br /> Это свойство применимо, только если значение **AutomaticStatePersistence** задано равным **TRUE**.|  
|StateTable|String|Указывает имя таблицы, в которой хранится состояние контекста CDC. Эта таблица должна быть доступна при использовании соединения, настроенного для данного компонента. Эта таблица должна включать столбцы типа varchar, обозначенные как **name** и **state**. (Столбец **state** должен иметь длину по крайней мере 256 символов.)<br /><br /> Это свойство применимо, только если значение **AutomaticStatePersistence** задано равным **TRUE**.|  
|CommandTimeout|integer|Это значение указывает время ожидания (в секундах), которое используется при взаимодействии с базой данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Это значение используется в тех случаях, если время ответа из базы данных весьма продолжительно и значение по умолчанию (30 секунд) является недостаточным.|  
  
## <a name="see-also"></a>См. также  
 [CDC Control Task](cdc-control-task.md)   
 [CDC Control Task Editor](../cdc-control-task-editor.md)  
  
  
