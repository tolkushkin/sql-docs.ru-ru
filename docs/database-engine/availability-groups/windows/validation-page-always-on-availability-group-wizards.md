---
title: Страница проверки (мастера групп доступности AlwaysOn) | Документы Майкрософт
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.validation.f1
- sql13.swb.adddatabasewizard.validation.f1
- sql13.swb.newagwizard.validation.f1
helpviewer_keywords:
- ', listeners'
ms.assetid: c8971556-240c-491a-bc86-9cc72f71a3dd
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 281306cece913e4386a1ca6059b738c9fa20e058
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780135"
---
# <a name="validation-page-always-on-availability-group-wizards"></a>Страница проверки (мастера групп доступности AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
  В этом разделе описываются параметры, приведенные на странице **Проверка** . Эта тема относится к [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)], [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]и [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Используйте эту страницу для проверки поддержки средой всех вариантов конфигурации, выбранных на предыдущей странице мастера.  
  
##  <a name="PageOptions"></a> Параметры страницы проверки  
 **Результаты проверки группы доступности.**  
 В этой сетке отображаются результаты каждого завершенного этапа проверки. Сетка содержит следующие столбцы.  
  
 **Название**  
 Отображает фразу, которая описывает конкретный шаг.  
  
 **Результат**  
 Отображает один из следующих текстов гиперссылки. Дополнительные сведения данного шага проверки можно просмотреть, щелкнув гиперссылку.  
  
|Результат|Описание|  
|------------|-----------------|  
|**Ошибка**|Указывает, что шаг проверки выполнен неудачно. Щелкните ссылку, чтобы просмотреть сообщение об ошибке.|  
|**Пропущено**|Указывает, что шаг проверки был пропущен, поскольку он не был отмечен в параметрах как необходимый. Щелкните ссылку для просмотра причины, по которой шаг был пропущен.|  
|**Успешно**|Указывает, что шаг проверки завершен удачно.|  
|**Предупреждение**|Указывает на наличие потенциальной проблемы с конфигурацией группы доступности.  Щелкните ссылку, чтобы просмотреть предупреждение.|  
  
 **Запустите проверку повторно**  
 Щелкните, чтобы повторить шаги проверки, если в ответ на выявленную ошибку были внесены изменения без использования средств мастера.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Использование диалогового окна "Создание группы доступности" (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Использование мастера добавления реплики в группу доступности (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Использование мастера добавления базы данных в группу доступности (среда SQL Server Management Studio)](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
  
## <a name="see-also"></a>См. также:  
 [Обзор групп доступности AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
