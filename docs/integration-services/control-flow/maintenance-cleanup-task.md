---
title: Задача "Очистка после обслуживания" | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.maintenancecleanuptask.f1
helpviewer_keywords:
- deleting files
- removing files
- Maintenance Cleanup task
ms.assetid: 73ad3cd6-9a6d-44cf-905f-c56aa658bf42
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0cdbaa7d265720cc85966180811221d5883ffc66
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727538"
---
# <a name="maintenance-cleanup-task"></a>задача «Очистка после обслуживания»

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Задача «Очистка после обслуживания» удаляет файлы, относящиеся к планам обслуживания, включая файлы резервных копий баз данных и отчеты, созданные планами обслуживания. Дополнительные сведения см. в разделах [Планы обслуживания](../../relational-databases/maintenance-plans/maintenance-plans.md) и [Резервное копирование и восстановление баз данных SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 С помощью задачи «Очистка после обслуживания» пакет может удалять файлы резервных копий или отчеты планов обслуживания на указанном сервере. Задача «Очистка после обслуживания» имеет параметр удаления специфических файлов или удаления группы файлов в папке. При необходимости можно указать расширение удаляемых файлов.  
  
 При настройке задачи «Очистка после обслуживания» для удаления файлов резервных копий по умолчанию установлено расширение файла BAK. Для файлов отчета расширение по умолчанию — TXT. При необходимости расширение можно изменить; единственное ограничение: расширение должно иметь меньше 256 символов.  
  
 Если необходимо удалить старые ненужные файлы, задача «Очистка после обслуживания» может быть настроена для удаления файлов, существующих определенный период времени. Например, задача может быть настроена на файлы, существующие дольше двух недель. Можно указать давность удаляемых файлов, используя дни, недели, месяцы и годы. Если минимальный срок для удаления файлов не устанавливается, удаляются все файлы указанного типа.  
  
 В отличие от ранних версий задачи «Очистка после обслуживания» версия [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] этой задачи не удаляет автоматически файлы во вложенных каталогах указанной папки. Это ограничение сокращает контактную зону любой атаки, использующей функции задачи «Очистка после обслуживания» для умышленного удаления файлов. Для удаления вложенных папок первого уровня необходимо выбрать это действие, установив флажок **Включить вложенные папки первого уровня** в диалоговом окне **Задача "Очистка после обслуживания"** .  
  
## <a name="configuration-of-the-maintenance-cleanup-task"></a>Настройка задачи «Очистка после обслуживания»  
 Свойства задаются с помощью конструктора служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Эта задача находится в разделе **Задачи плана обслуживания** **области элементов** в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующем разделе:  
  
-   [Задача "Очистка после обслуживания" (план обслуживания)](../../relational-databases/maintenance-plans/maintenance-cleanup-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Связанные задачи  
 Дополнительные сведения о настройке свойств этих свойств в конструкторе [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в разделе [Задание свойств задач или контейнеров](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="see-also"></a>См. также:  
 [Задачи служб Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Поток управления](../../integration-services/control-flow/control-flow.md)  
  
  
