---
title: Сведения о публикации, вкладка "Агенты" (публикация транзакций) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.downlevelagents.tran.f1
ms.assetid: 38ef2f54-53bb-4053-876d-86f8f06a4519
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a4542370eff5ad631701f0bf988929ad56e8799
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63021801"
---
# <a name="publication-information-agents-transactional-publication"></a>Сведения о публикации, агенты (публикация транзакций)
  На вкладке **Агенты** отображаются общие сведения об агентах для выбранной публикации. Сведения об агенте моментальных снимков и агенте чтения журнала выводятся для всех публикаций транзакций. Сведения об агенте чтения очереди отображается только для тех публикаций транзакций, которые включены для очереди обновляемых подписок.  
  
## <a name="options"></a>Параметры  
 Чтобы получить дополнительные сведения и задачи, связанные с агентом, щелкните правой кнопкой мыши строку агента и в контекстном меню выберите нужный пункт Чтобы изменить способ отображения данных в сетке, щелкните правой кнопкой мыши сетку, а затем один из следующих параметров.  
  
-   **Сортировать**: сортировка по одному или нескольким столбцам в диалоговом окне **Сортировка столбцов**.  
  
-   **Выберите столбцы для отображения**: выбор столбцов для отображения и порядка их отображения в диалоговом окне **Выбор столбцов**.  
  
-   **Фильтр**: фильтрация строк в сетке на основании значений столбцов в диалоговом окне **Параметры фильтра**.  
  
-   **Очистить фильтр**: Удаление всех параметров фильтра для сетки.  
  
 Настройки фильтра уникальны для каждой сетки. Выбор и сортировка столбцов применяются ко всем сеткам одного типа, как, например, сетка публикаций для каждого издателя.  
  
 **Состояние**  
 Состояние каждого агента репликации, связанного с публикацией. Возможные значения состояния показаны в следующем списке:  
  
-   Ошибка  
  
-   Попытка повторно выполнить неудачно завершившиеся команды  
  
-   Не выполняется  
  
-   Запущен  
  
-   Завершено  
  
 **Агент**  
 Имя каждого агента репликации, связанного с публикацией. Агент распространителя связан с подписками на эту публикацию. Дополнительные сведения см. в статье [Просмотр сведений и выполнение задач с помощью монитора репликации](monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 **Время последнего запуска**  
 Время последнего запуска агента.  
  
 **Длительность**  
 Продолжительность выполнения агента. Этот параметр представляет собой время, прошедшее с момента начала сеанса, если агент запущен в данный момент, или общее время, если агент был запущен ранее.  
  
 **Последнее действие**  
 Последнее действие выполнено во время самого последнего выполнения агента.  
  
## <a name="see-also"></a>См. также  
 [Запуск монитора репликации](monitor/start-the-replication-monitor.md)   
 [Просмотр сведений и выполнение задач с помощью монитора репликации](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Наблюдение за репликацией](monitoring-replication.md)  
  
  
