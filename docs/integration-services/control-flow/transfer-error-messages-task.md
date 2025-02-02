---
title: Задача "Передача сообщений об ошибках" | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfererrormessagestask.f1
- sql13.dts.designer.transfererrormessagestask.general.f1
- sql13.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cc7a5b230120f7f392d33793a18994932ce8f05c
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727405"
---
# <a name="transfer-error-messages-task"></a>Задача «Передача сообщений об ошибках»

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Задача "Передача сообщений об ошибках" передает одно или несколько пользовательских сообщений об ошибках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] между экземплярами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Пользовательские сообщения имеют идентификатор, больший или равный 50000. Сообщения с идентификаторами, меньшими 50000, являются системными и не могут передаваться с помощью задачи «Передача сообщений об ошибках».  
  
 Задачу «Передача сообщений об ошибках» можно настроить на передачу как всех сообщений об ошибках, так и только определенных. Пользовательские сообщения об ошибках могут быть на нескольких языках. Задача может быть настроена на передачу сообщений только на выбранных языках. Чтобы передавать на целевой сервер версии сообщения на других языках, на сервере должна существовать англоязычная версия сообщения (кодовая страница 1033, us_english).  
  
 Таблица sysmessages главной базы данных содержит все системные и пользовательские сообщения об ошибках, используемые в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Передаваемые пользовательские сообщения могут уже существовать в целевом объекте. Сообщение об ошибке определяется как повторяющееся, если его идентификатор и язык совпадают. Задача «Передача сообщений об ошибках» может быть настроена на работу с существующими сообщениями об ошибках следующим образом.  
  
-   Перезаписывать существующие сообщения об ошибках.  
  
-   При обнаружении повторяющегося сообщения завершать задачу сбоем.  
  
-   Пропускать повторяющиеся сообщения об ошибках.  
  
 Во время выполнения задача «Передача сообщений об ошибках» подключается к источнику и целевым серверам, используя один или два диспетчера соединений SMO. Диспетчер соединений SMO настраивается отдельно от задачи «Передача сообщений об ошибках», а затем используется этой задачей. Диспетчер соединений SMO определяет сервер и режим проверки подлинности, используемый для доступа к серверу. Дополнительные сведения см. в статье [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Задача «Передача сообщений об ошибках» поддерживает источники и целевые объекты [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ограничений в отношении использования определенных версий источника или целевого объекта не существует.  
  
## <a name="events"></a>События  
 Задача вызывает информационное событие, в котором сообщается о количестве переданных сообщений об ошибках.  
  
 В ходе выполнения задачи «Передача сообщений об ошибках» сведения о состоянии передачи не отображаются, появляются только сообщения о 0% и 100% выполнении.  
  
## <a name="execution-value"></a>Значение выполнения  
 Значение выполнения, определенное свойством задачи **ExecutionValue** , возвращает количество переданных сообщений об ошибках. С помощью выделения пользовательской переменной для свойства **ExecValueVariable** задачи "Передача сообщений об ошибках" сведения об ошибках передачи становятся доступными для других объектов пакета. Дополнительные сведения см. в разделах [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md) и [Использование переменных в пакетах](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Записи журнала  
 Задача «Передача сообщений об ошибках» включает в себя следующие пользовательские записи журнала.  
  
-   TransferErrorMessagesTaskStartTransferringObjects. Это запись журнала о начале передачи. В записях журнала указывается время запуска.  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects. Это запись журнала об окончании передачи. В записях журнала указывается время завершения.  
  
 Также запись журнала о событии **OnInformation** содержит информацию о количестве переданных сообщений об ошибках. Запись журнала для **OnWarning event** сохраняется в обновляемом файле для каждого сообщения об ошибке.  
  
## <a name="security-and-permissions"></a>Безопасность и разрешения  
 Чтобы создать новое сообщение об ошибке, пользователь, запускающий пакет, должен являться членом роли сервера sysadmin или serveradmin на целевом сервере.  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>Настройка задачи «Передача сообщений об ошибках»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующем разделе:  
  
-   [Страница «Выражения»](../../integration-services/expressions/expressions-page.md)  
  
 Сведения о задании этих свойств программными средствами см. в следующем разделе:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Связанные задачи  
 Дополнительные сведения об установке этих свойств в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в следующем разделе:  
  
-   [Задание свойств задач или контейнеров](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-error-messages-task-editor-general-page"></a>Редактор задачи «Передача сообщений об ошибках» (страница «Общие»)
  Используйте страницу **Общие** диалогового окна **Редактор задачи «Передача сообщений об ошибках»** , чтобы задать имя и описание для задачи «Передача сообщений об ошибках». Задача "Передача сообщений об ошибках" передает одно или несколько пользовательских сообщений об ошибках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] между экземплярами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   
  
### <a name="options"></a>Параметры  
 **Название**  
 Введите уникальное имя для задачи «Передача сообщений об ошибках». Это имя используется в качестве метки для значка задачи.  
  
> [!NOTE]  
>  Имена задач в пределах пакета должны быть уникальными.  
  
 **Описание**  
 Введите описание для задачи «Передача сообщений об ошибках».  
  
## <a name="transfer-error-messages-task-editor-messages-page"></a>Редактор задачи «Передача сообщений об ошибках» (страница «Сообщения»)
  Используйте страницу **Сообщения** диалогового окна **Редактор задачи "Передача сообщений об ошибках"** , чтобы указать свойства копирования одного или более определенных пользователем сообщений об ошибках [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из одного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в другой. 
  
### <a name="options"></a>Параметры  
 **SourceConnection**  
 Выберите в списке диспетчер подключений SMO или нажмите кнопку **\<Создать подключение...>**, чтобы создать подключение к исходному серверу.  
  
 **DestinationConnection**  
 Выберите в списке диспетчер подключений SMO или нажмите кнопку **\<Создать подключение...>**, чтобы создать подключение к целевому серверу.  
  
 **IfObjectExists**  
 Выберите, следует ли при выполнении задачи перезаписать существующие пользовательские сообщения об ошибках, оставить их без изменения или зарегистрировать сбой в случае, если сообщения об ошибках с тем же именем уже существуют на целевом сервере.  
  
 **TransferAllErrorMessages**  
 Выберите, следует ли при выполнении задачи копировать все или только указанные пользовательские сообщения с исходного сервера на целевой сервер.  
  
 Параметры этого свойства приведены в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**True**|Копировать все пользовательские сообщения.|  
|**False**|Копировать только указанные пользовательские сообщения.|  
  
 **ErrorMessagesList**  
 Нажмите кнопку обзора, обозначенную многоточием **(...)**, чтобы выбрать сообщения об ошибках для копирования.  
  
> [!NOTE]  
>  Необходимо указать значение параметра **SourceConnection** прежде, чем можно будет выбрать сообщения об ошибках для копирования.  
  
 **ErrorMessageLanguagesList**  
 Нажмите кнопку обзора, обозначенную многоточием **(...)**, чтобы выбрать языки, для которых должны быть скопированы на целевой сервер пользовательские сообщения об ошибках. Прежде чем можно будет передать на целевой сервер версии сообщения на других языках, на нем должна существовать англоязычная версия сообщения (кодовая страница 1033, us_english).  
  
> [!NOTE]  
>  Необходимо указать значение параметра **SourceConnection** прежде, чем можно будет выбрать сообщения об ошибках для копирования.  
  
## <a name="see-also"></a>См. также:  
 [Задачи служб Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Поток управления](../../integration-services/control-flow/control-flow.md)  
  
  
