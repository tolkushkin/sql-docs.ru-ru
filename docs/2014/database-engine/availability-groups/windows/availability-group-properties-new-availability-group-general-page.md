---
title: Свойства группы доступности и новой группы доступности (страница "Общие") | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroupproperties.general.f1
ms.assetid: 9af5379f-91b8-4729-9f75-4a80242a30e9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 248ffe57906052c0d7dafcd187bb1b2b34cd6e64
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62815657"
---
# <a name="availability-group-properties-and-new-availability-group-general-page"></a>Свойства группы доступности и создание группы доступности (страница "Общие")
  Приведенные в этом разделе сведения относятся к вкладке **Общие** диалоговых окон **Создание группы доступности** и **Свойства группы доступности** .  Диалоговое окно **Создание группы доступности** позволяет создать новую группу доступности, не прибегая к использованию [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]. Диалоговое окно **Свойства группы доступности** позволяет просматривать и изменять конфигурацию существующей группы доступности.  
  
 **Просмотр свойств группы доступности**  
  
-   [Просмотр свойств группы доступности (SQL Server)](view-availability-group-properties-sql-server.md)  
  
-   [Использование панели мониторинга AlwaysOn (среда SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>Список элементов пользовательского интерфейса  
 **Имя группы доступности**  
 Имя группы доступности. Определяемое пользователем имя, которое должно быть уникальным в отказоустойчивом кластере Windows Server (WSFC).  
  
## <a name="availability-databases"></a>Базы данных доступности  
 **Database Name**  
 Имя базы данных, добавленной к группе доступности.  
  
 **Добавить**  
 Нажмите, чтобы добавить новую базу данных в группу доступности.  
  
 **Удалить**  
 Нажмите, чтобы удалить выбранную базу данных из группы доступности.  
  
## <a name="availability-replicas"></a>Реплики доступности  
 **Экземпляр сервера**  
 Имя сервера экземпляра [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , на котором размещена данная реплика, а также имя экземпляра, если экземпляр не является используемым по умолчанию.  
  
 **Роль**  
 **Первичная**  
 В настоящее время — первичная реплика.  
  
 **Вторичная**  
 В настоящее время — вторичная реплика.  
  
 **Разрешение**  
 В настоящее время определяется, будет реплика выступать в роли основной или вторичной.  
  
 **Режим доступности**  
 Режим доступности реплики может быть одним из следующих.  
  
 **Асинхронная фиксация**  
 Первичная реплика может фиксировать транзакции, не ожидая, пока вторичная реплика запишет запись журнала транзакций на диск.  
  
 **Синхронная фиксация**  
 Первичная реплика ожидает возможности выполнения фиксации транзакции, пока вторичная реплика записывает транзакцию на диск.  
  
 Дополнительные сведения см. в разделе [режимы доступности (группы доступности AlwaysOn)](availability-modes-always-on-availability-groups.md).  
  
 **Режим отработки отказа**  
 Режим отработки отказа реплики доступности, одно из следующих значений:  
  
 **Автоматически**  
 Автоматический переход на другой ресурс. Реплика является целью для автоматического перехода на другой ресурс. Эта функция поддерживается только при использовании режима доступности с синхронной фиксацией.  
  
 **Вручную**  
 Переход на другой ресурс вручную. Отработка отказа для этой реплики может быть выполнена только администратором базы данных.  
  
 **Подключения в первичной роли**  
 Тип клиентских подключений, поддерживаемый тогда, когда реплика является первичной.  
  
 **разрешить все соединения.**  
 Разрешаются все соединения с базами данных в первичной реплике. Это параметр по умолчанию.  
  
 **разрешить соединения с доступом на чтение и запись;**  
 Соединения, у которых свойство "Назначение приложения" равно **ReadOnly** , не разрешены. Если свойство «Назначение приложения» имеет значение **ReadWrite** или не задано, то соединение разрешено. Дополнительные сведения о свойстве соединения «Назначение приложения» см. в разделе [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 **Доступные для чтения вторичные**  
 Указывает, могут ли базы данных заданной реплики доступности, играющей роль вторичной (т. е. служащей вторичной репликой), принимать соединения от клиентов. Может принимать одно из следующих значений:  
  
 **Нет**  
 Прямые подключения для баз данных-получателей этой реплики не разрешаются. Для них не разрешен доступ для чтения. Это параметр по умолчанию.  
  
 **Назначение — только чтение**  
 Для баз данных-получателей этой реплики разрешены исключительно прямые подключения только для чтения. Для всех баз данных-получателей разрешен доступ для чтения.  
  
 **Да**  
 Для баз данных-получателей этой реплики разрешены все соединения, но только с доступом для чтения. Для всех баз данных-получателей разрешен доступ для чтения.  
  
 **Время ожидания сеанса (секунды)**  
 Количество секунд, составляющее время ожидания сеанса для этой реплики.  
  
 **URL-адрес конечной точки**  
 URL-адрес конечной точки. Сведения о формате этих URL-адресов см. в разделе [Указание URL-адреса конечной точки при добавлении или изменении реплики доступности (SQL Server)](specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **Добавить**  
 Выберите, чтобы добавить новую вторичную реплику в группу доступности.  
  
 **Удалить**  
 Нажмите, чтобы удалить вторичную реплику из группы доступности.  
  
## <a name="see-also"></a>См. также  
 [Обзор групп доступности AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
