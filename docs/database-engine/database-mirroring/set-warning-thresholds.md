---
title: Установка порогов предупреждений | Документы Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbmmonitor.setwarningthreshold.f1
ms.assetid: 17f93147-e7d9-4092-b4c2-c11b38051171
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: bfebc4164264e2deeb02ab5f8e9f8b8b6ef64655
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795207"
---
# <a name="set-warning-thresholds"></a>Установка порогов предупреждений
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Это диалоговое окно позволяет разрешить и настроить один или несколько пороговых значений предупреждений для базы данных, выбранной в дереве навигации диалогового окна **Монитор зеркального отображения баз данных** .  
  
 В этом диалоговом окне предпринимается попытка подключиться к обоим экземплярам сервера. Эти соединения устанавливаются асинхронно. Диалоговое окно показывает состояние соединения каждого сервера-участника. Если сервер-участник не подключен, можно нажать кнопку **Соединить**.  
  
 **Наблюдение за зеркальным отображением базы данных с помощью среды SQL Server Management Studio**  
  
-   [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Параметры  
 *Экземпляр сервера и состояние его соединения*  
 Имя экземпляра сервера-участника в форме *SYSTEM***\\***INSTANCE_NAME*. Для экземпляра сервера по умолчанию отображается только имя системы.  
  
 Это поле также показывает, подключен ли в настоящее время монитор к этому экземпляру сервера. Возможные значения состояния соединения являются таковыми:  
  
-   **Не подключено к**  *server_instance_name*  
  
-   **Попытка подключения к**  *server_instance_name*  
  
-   **Подключено к**  *server_instance_name*  
  
    > [!NOTE]  
    >  Для пользователей, не являющихся элементами предопределенной роли сервера **sysadmin** , это значение состояния принимает вид **Подключен к** *имя_экземпляра_сервера* **(ограниченные разрешения)** .  
  
 Имя каждого экземпляра сервера-участника отображается в отдельном поле *Экземпляр сервера и состояние его соединения* . В верхнем поле со времени начала работы монитора отображается имя основного сервера.  
  
 **Подключение**/**Отмена**  
 Кнопка **Подключение**/**Отмена** связана с каждым из полей *Экземпляр сервера и состояние его соединения* . Текст надписи на этой кнопке зависит от состояния соединения:  
  
-   Если соединение с экземпляром сервера отсутствует, на кнопке отображается надпись **Соединить**. Нажмите кнопку, чтобы подключиться к экземпляру сервера.  
  
-   Если осуществляется попытка соединения, на кнопке отображается надпись **Отмена**. Нажмите кнопку, чтобы отменить попытку соединения.  
  
-   Если сервер подключен, на кнопке отображается надпись **Подключен**и кнопка затемнена.  
  
 **Пороги**  
 В сетке **Пороги** отображаются параметры предупреждений для двух экземпляров сервера.  
  
> [!NOTE]  
>  Если экземпляр сервера не подключен, относящиеся к нему столбцы отображаются с пустыми ячейками на сером фоне. После открытия соединения в сетке автоматически отображается содержимое, полученное от подключенного экземпляра.  
  
 Сетка содержит следующие столбцы:  
  
 **Предупреждения**  
 Отображает поддерживаемые предупреждения:  
  
|Предупреждение|Описание|  
|-------------|-----------------|  
|**Предупреждать, если размер неотправленного журнала превышает пороговое значение.**|Это пороговое значение показывает размер в килобайтах (КБ) неотправленного журнала в очереди отправки на экземпляре основного сервера.|  
|**Предупреждать, если размер невосстановленного журнала превысил пороговое значение.**|Это пороговое значение показывает размер в КБ очереди повторного выполнения на экземпляре зеркального сервера.|  
|**Предупреждать, если время хранения самой старой неотправленной транзакции превысило пороговое значение.**|Это пороговое значение показывает продолжительность времени в минутах, в течение которого сведения о транзакциях еще не были отправлены из очереди отправки на экземпляр зеркального сервера. Это значение позволяет оценить потенциальные потери данных по времени.|  
|**Предупреждать, если затраты на фиксирование изменений на зеркальном сервере превысили пороговое значение.**|Это пороговое значение показывает продолжительность задержки в расчете на одну транзакцию в миллисекундах (имеет смысл только в режиме высокой безопасности). Задержка — это объем дополнительной нагрузки во время ожидания экземпляром основного сервера экземпляра зеркального сервера для добавления записи журнала транзакции в очередь повтора.|  
  
 **Включено на "** *\<экземпляр сервера>* **"**  
 Неустановленный флажок указывает, что это предупреждение в настоящее время отменено на данном экземпляре сервера. Чтобы включить предупреждение, установите относящийся к нему флажок.  
  
 **Пороговое значение на "** *\<экземпляр сервера* **"**  
 Если предупреждение включено, задайте пороговое значение слева от этого столбца. Если при обновлении таблицы состояния достигается указанное пороговое значение, активируется определенное событие. Если отслеживание порогового значения будет отменено после ввода в настройку некоторого значения, это значение останется в указанном поле для дальнейшего использования в случае повторного ввода предупреждения в действие.  
  
 Если предупреждение не включено, это поле неактивно.  
  
 **ОК**  
 После нажатия кнопки **ОК** это диалоговое окно закрывается и заданные в настоящее время пороговые значения предупреждений отображаются в сетке **Пороги** страницы с вкладками **Предупреждения**.  
  
## <a name="remarks"></a>Remarks  
 Пороговое значение может применяться одновременно только на одном сервере-участнике, но мы рекомендуем задавать пороговое значение для каждого конкретного события на обоих серверах-участниках, чтобы обеспечить сохранение настройки предупреждения даже в случае переключения на другую базу данных. Соответствующий порог для каждого участника зависит от возможностей производительности системы участника.  
  
 Событие записывается в журнал событий по производительности только в случае, если его значение находится на границе порога или над порогом и если таблица состояния обновляется. Если пиковое значение немедленно достигает порога между обновлениями состояния, то данный пик опускается.  
  
## <a name="see-also"></a>См. также:  
 [Запуск монитора зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Наблюдение за зеркальным отображением базы данных (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Запуск мастера настройки безопасности зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
