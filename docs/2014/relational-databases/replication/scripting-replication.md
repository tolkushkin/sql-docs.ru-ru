---
title: Создание скриптов репликации | Документация Майкрософт
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server replication], replication objects
- merge replication scripting [SQL Server replication]
- replication [SQL Server], scripting
- snapshot replication [SQL Server], scripting
- scripts [SQL Server replication]
- transactional replication, scripting
ms.assetid: e50fac44-54c0-470c-a4ea-9c111fa4322b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55407c52c5fb7bf0c9537eaf8fb7a7d31d2675e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250526"
---
# <a name="scripting-replication"></a>Создание сценариев репликации
  Все компоненты репликации в топологии должны использоваться в скриптах как часть плана аварийного восстановления, а скрипты могут также использоваться для автоматизации повторяющихся задач. Скрипт содержит системные хранимые процедуры Transact-SQL, необходимые для выполнения элементов скрипта репликации, таких как публикация или подписка. Скрипты могут быть созданы с помощью мастера (например, мастера создания публикаций) или в [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] после создания компонента. Скрипт можно просмотреть, изменить и запустить с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или **sqlcmd**. Скрипты могут сохраняться с файлами резервных копий для использования в случае, если необходимо перенастроить топологию репликации.  
  
 Компонент должен быть заново включен в сценарий при внесении изменений любого из его свойств. Если с репликацией транзакций используются специальные хранимые процедуры, копия каждой процедуры должна сохраняться со скриптами. Если процедура изменяется, ее копия должна обновляться (процедуры обычно обновляются в связи с изменениями схемы или изменениями требований приложения). Дополнительные сведения о хранимых процедурах см. в статье [Указание способа распространения изменений для статей транзакций](transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 Для публикаций слиянием, использующих параметризованные фильтры, скрипты публикации содержат вызовы хранимых процедур для создания секций данных. Скрипт содержит справочную информацию для созданных секций и способ воссоздания одной или нескольких секций в случае необходимости.  
  
## <a name="example-of-automating-a-task-with-scripts"></a>Пример автоматизации задачи с помощью скриптов  
 Рассмотрим компанию [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)], которая реализует репликацию слиянием, чтобы передавать данные своим удаленным торговым подразделениям. Представитель отдела продаж загружает все данные клиентов на территории своей ответственности с помощью подписки по запросу. При работе в режиме «в сети» представитель отдела продаж обновляет данные и вводит новых клиентов и заказы. Так как [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] имеет более пятидесяти коммерческих представителей в разных территориях, то использование мастера создания подписки отнимало бы слишком много времени при создании подписок на каждом подписчике. Вместо этого администратор репликации может выполнить следующие шаги:  
  
1.  Настроить необходимые публикации слиянием с использованием секций, разделенных по представителям отдела продаж или их территориям.  
  
2.  Создать подписку по запросу для одного подписчика.  
  
3.  Создать скрипт на основе этой подписки по запросу.  
  
4.  Изменить скрипт, изменяя такие значения, как имя подписчика.  
  
5.  Выполнить скрипт на нескольких подписчиках для создания необходимых подписок по запросу.  
  
## <a name="script-replication-objects"></a>Создать скрипт репликации объектов  
 Создание скриптов для репликации объектов производится при помощи мастеров репликации или из папки **Репликация** в среде [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. При создании скриптов при помощи мастеров можно выбрать создание объектов и скриптов для них или только создание скриптов.  
  
> [!IMPORTANT]  
>  Все пароли в сценариях имеют значение NULL. По возможности предлагайте пользователям вводить учетные данные системы безопасности во время выполнения приложения. При хранении учетных данных в файле скрипта необходимо защитить этот файл во избежание несанкционированного доступа.  
  
 Дополнительные сведения об использовании мастеров репликации см. в следующих разделах:  
  
-   [Настройка публикации и распространения](configure-publishing-and-distribution.md)  
  
-   [Create a Publication](publish/create-a-publication.md)  
  
-   [Создание принудительной подписки](create-a-push-subscription.md)  
  
-   [Создание подписки по запросу](create-a-pull-subscription.md)  
  
#### <a name="to-script-an-object-from-a-replication-wizard"></a>Создание скрипта объекта при помощи мастера репликации  
  
1.  На странице **Действия мастера** установите флажок, соответствующий мастеру.  
  
    -   **Создать файл скрипта, содержащий шаги по созданию публикации.**  
  
    -   **Создать файл скрипта, содержащий шаги по созданию подписки (подписок).**  
  
    -   **Создать файл скрипта, содержащий шаги по настройке распространения.**  
  
2.  Задайте параметры на странице **Свойства файла скрипта** .  
  
3.  Завершите работу мастера.  
  
#### <a name="to-script-an-object-from-management-studio"></a>Создание скрипта объекта из среды Management Studio  
  
1.  Подключитесь к распространителю, издателю или подписчику [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], затем разверните узел сервера.  
  
2.  Раскройте папку **Репликация** , затем раскройте папку **Локальные публикации** или **Локальные подписки** .  
  
3.  Щелкните правой кнопкой мыши публикацию или подписку, затем щелкните **Сформировать скрипты**.  
  
4.  Укажите параметры в диалоговом окне **Формирование скрипта SQL — \<объект_репликации>**.  
  
5.  Щелкните **Вывести скрипт в файл**.  
  
6.  Введите имя файла в диалоговом окне **Расположение файла скрипта** , а затем нажмите кнопку **Сохранить**. Будет выведено сообщение о состоянии.  
  
7.  Нажмите кнопку **ОК**, затем кнопку **Закрыть**.  
  
#### <a name="to-script-multiple-objects-from-management-studio"></a>Создание скрипта нескольких объектов из среды Management Studio  
  
1.  Подключитесь к распространителю, издателю или подписчику [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], затем разверните узел сервера.  
  
2.  Щелкните правой кнопкой мыши папку **Репликация** , затем щелкните **Сформировать скрипты**.  
  
3.  Укажите параметры в диалоговом окне **Формирование скрипта SQL** .  
  
4.  Щелкните **Вывести скрипт в файл**.  
  
5.  Введите имя файла в диалоговом окне **Расположение файла скрипта** , а затем нажмите кнопку **Сохранить**. Будет выведено сообщение о состоянии.  
  
6.  Нажмите кнопку **OK** , затем кнопку **Закрыть**.  
  
  
