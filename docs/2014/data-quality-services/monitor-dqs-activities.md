---
title: Мониторинг действий DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.administration.activitymonitoring.f1
helpviewer_keywords:
- monitoring activity
- activity monitoring
ms.assetid: 1d4c76f3-0d7b-498e-b792-4db4a0349814
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 860842ee5c6c946e6631abac23b229ca67d86334
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65484134"
---
# <a name="monitor-dqs-activities"></a>Мониторинг операций DQS
  В этом разделе описывается централизованный мониторинг следующих действий в [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS): обнаружение знаний, управление доменами, политика сопоставления, очистка данных, сопоставление данных и очистка на базе служб SSIS.  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="LimitationsRestrictions"></a> Ограничения  
 Только пользователи с ролью dqs_administrator в базе данных DQS_Main могут прерывать действие или останавливать процесс в составе действия.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
  
-   Для просмотра действий DQS необходимо иметь роль dqs_kb_editor или dqs_kb_operator в базе данных DQS_MAIN.  
  
-   Для завершения действия или остановки процесса в составе действия, помимо просмотра действий DQS, необходимо обладать ролью dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="View"></a> Просмотр действий DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запуск клиентского приложения Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] нажмите **Мониторинг активности**. Появится экран мониторинга активности.  
  
     ![Экран мониторинга активности](../../2014/data-quality-services/media/dqs-activitymonitoring.gif "Экран мониторинга активности")  
  
3.  На экране мониторинга активности отображаются сведения о каждом действии в сетке действий. В сетке действий показаны следующие сведения о каждом действии DQS:  
  
    |Сведения|Описание|  
    |-----------------|-----------------|  
    |**Идентификатор**|Целочисленное значение. Уникальный номер действия, формируемый системой для мониторинга активности.|  
    |**Name**|Имя базы знаний или проекта служб DQS, используемого этим действием.|  
    |**Активен**|Указывает, активно ли действие. Может иметь следующие значения.<br /><br /> **Активно**. Действие выполняется в данный момент.<br /><br /> **Закончено**. Действие завершено.<br /><br /> **Завершено**. Действие было прекращено с экрана мониторинга активности администратором служб DQS или отменено пользователем действие при запуске из соответствующей функциональной области в [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|  
    |**Тип**|Указывает тип действия. Отслеживаются следующие типы действий: **Управление набором знаний**, **проект DQ**, и **Очистка SSIS**.|  
    |**Подтип**|Указывает конкретный рабочий процесс, который выполняется для действия данного типа.<br /><br /> Объект **управление набором знаний** типа действия может инициировать следующие рабочие процессы или подтипы: **Обнаружение набора знаний**, **Управление доменами**, и **политика сопоставления**.<br /><br /> Объект **проект DQ** типа действия может инициировать следующие рабочие процессы или подтипы: **Очистка** и **сопоставления**.<br /><br /> У типа действий **Очистка на базе служб SSIS** может быть рабочий процесс или подтип только типа **Очистка** .|  
    |**Текущее состояние**|Указывает текущее состояние действия. Состояние действия определяется последним вычислительным процессом. Может иметь следующие значения.<br /><br /> **Выполняется**. Вычислительный процесс выполняется.<br /><br /> **Выполнено**. Перед запуском любой вычислительного процесса действие имеет состояние имеет значение **успешно**. После успешного завершения какого-либо вычислительного процесса действие также имеет состояние **Успешно завершено**.<br /><br /> **Ошибка**. Вычислительный процесс завершился с ошибкой.<br /><br /> **Остановлено**. Вычислительный процесс был приостановлен.<br /><br /> <br /><br /> Примечание. Может существовать несколько вычислительных процессов в одно действие, например для запуска процесса обнаружения несколько раз (в рамках операции обнаружения знаний). Таким образом, состояние в течение времени жизни действия может измениться несколько раз.|  
    |**DQKB**|Имя базы знаний, используемой этим действием.|  
    |**Пользователь**|Имя пользователя, который инициировал действие, либо последнего пользователя, который работал с действием (если они не совпадают).|  
    |**Время начала действия**|Дата и время запуска действия.|  
    |**Затраченное время**|Время, истекшее с момента запуска действия. Отображается в формате ЧЧ:ММ:СС.|  
    |**Время окончания действия**|Дата и время завершения действия.|  
  
##  <a name="Filter"></a> Фильтр сведений о действиях DQS  
 С помощью панели фильтрации (**Фильтровать по**, **Значение**, **От даты**и **До даты**) на экране мониторинга активности можно фильтровать и просматривать необходимые действия по тому или иному критерию. Для фильтрации записей действий:  
  
1.  Выберите критерий фильтрации: следует ли фильтровать записи действий по значению в одном из столбцов сетки действий (по значениям), по диапазону дат либо по обоим критериям.  
  
    1.  **Фильтрация на основе значений**. Выберите критерий фильтра в списке **Фильтровать по**, а затем выберите значение, по которому нужна фильтрация, в списке **Значение**. После выбора параметра в списке **Фильтровать по** список **Значение** заполняется возможными значениями. Вы можете отфильтровать по следующим полям в записях о действиях: **Активно**, **Тип**, **Подтип**, **Текущее состояние**, **DQKB** и **Пользователь**.  
  
    2.  **Фильтрация по диапазону дат**. Выбор нужных дат в элементах управления **От даты** и **До даты**. По умолчанию в поле **От даты** отображается дата на два дня раньше текущей, а в поле **До даты** — текущая дата. Фильтрация выполняется не по отдельным датам *От* и *До* , а по диапазону. Это означает, что будут отображены все действия, которые выполнялись в указанном диапазоне дат.  
  
2.  Щелкните значок **Обновить список действий** , чтобы применить фильтрацию, затем просмотрите только отфильтрованные действия DQS.  
  
##  <a name="ActivityDetails"></a> Просмотр подробных сведений о действиях DQS  
 На экране мониторинга активности можно просмотреть подробные сведения о действии DQS, например об этапах его выполнения, а также сведения профилировщика. Для этого:  
  
1.  Выберите действие DQS в сетке действий (на верхней панели).  
  
2.  На нижней панели отображаются подробные сведения о выбранном действии, они разбиты на две вкладки.  
  
    -   **Этапы действия**. Отображает сетку вычислительных процессов (этапов действия), которые связаны с выбранным действием. На этой вкладке для одного действия могут отображаться несколько различных этапов. Это может наблюдаться в том случае, если один этап действия запускался пользователем несколько раз. Например, этап действия был остановлен, а затем снова запущен. Сетка на этой вкладке отображает следующие сведения по каждому этапу действия, связанные с действием: **Тип**, **Текущее состояние**, **Время начала**, **Затраченное время** и **Время завершения**.  
  
    -   **Профилировщик**. Отображает профилировочные сведения для текущих и выполнявшихся ранее действий. Для текущих действий он содержит неполные, но согласованные сведения. Профилировочные сведения о действии экспортируются в файл Excel при экспорте соответствующих подробных сведений о действии в файл Excel. Сведения доступны на листах **Профилировщик — источник** и **Профилировщик — поля** в экспортированном файле Excel.  
  
##  <a name="Export"></a> Экспорт подробных сведений о действиях DQS  
 На экране мониторинга можно экспортировать в файл Excel свойства действий, процессы действий и профилировочные сведения для действия. Для этого:  
  
1.  Выберите действие в сетке действий (на верхней панели).  
  
2.  Щелкните значок **Экспортировать выбранное действие в Excel** . Можно также щелкнуть правой кнопкой мыши любое действие в сетке действий, а затем выбрать пункт **Экспортировать действие** в контекстном меню.  
  
3.  Будет предложено указать имя и расположение сохраняемого файла Excel. Экспортированный файл Excel содержит следующие листы:  
  
    |Имя листа|Описание|  
    |----------------|-----------------|  
    |Действие|Содержит сведения (столбцы) о действии, как в сетке действий.|  
    |Процессы|Содержит сведения (столбцы) о процессах в действии, как на вкладке **Этапы действия** .|  
    |Профилировщик — источник|Для подтипа **Очистка** содержит следующие сведения о действии:   Записи правильные записи, исправленный и недопустимые записи.<br /><br /> Для подтипов **Обнаружение знаний**, **Управление доменами**, **Политика сопоставления** и **Сопоставление** содержит следующие сведения о действии:   Записи, общем количестве значений, новые значения, уникальные значения и новые уникальные значения.|  
    |Профилировщик — поля|Для подтипов **Очистка** и **Очистка SSIS** содержит следующие сведения о действии:   Поле, домена, исправленные значения, предлагаемые значения, полноты и точности.<br /><br /> Для подтипов **Обнаружение знаний**, **Управление доменами**, **Политика сопоставления** и **Сопоставление** содержит следующие сведения о действии:   Поле, домена, новый, уникальный, допустимых в домене и полноту.|  
  
##  <a name="Terminate"></a> Прерывание действия DQS  
 Администраторы служб DQS (роль dqs_administrator) могут прервать запущенное (активное) действие, которое не относится к типу **Очистка на базе служб SSIS**. При прерывании действия будут остановлены все запущенные процессы в действии и удалится все, что относится к данному действию. Отменить эту операцию невозможно. Прерывание действия на экране мониторинга активности равносильно отмене соответствующего действия нажатием кнопки **Отмена** при запуске его в функциональной области [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Прерывание действия:  
  
1.  Выберите запущенное действие в сетке действий (на верхней панели).  
  
2.  Щелкните значок **Завершить выбранное действие** . Можно также щелкнуть правой кнопкой мыши любое действие в сетке действий, затем выбрать пункт **Прервать действие** в контекстном меню.  
  
3.  Появится сообщение с запросом на подтверждение. Нажмите кнопку **Да**.  
  
##  <a name="Stop"></a> Остановка процесса в составе действия DQS  
 Администраторы служб DQS (роль dqs_administrator) могут остановить запущенный (активный) процесс в действии, которое не относится к типу **Очистка на базе служб SSIS**. Остановка процесса в действии на экране мониторинга активности равносильна остановке процесса в соответствующем действии в функциональной области [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Например, это может быть остановка процесса автоматизированной очистки или остановка процесса сопоставления в составе действия сопоставления. Приостановленный процесс невозможно повторно запустить на экране мониторинга активности. Повторный запуск процесса возможен в соответствующей функциональной области [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. В этом случае в сетке процессов на вкладке **Этапы действия** появляется дополнительная строка. Состояние остановленного процесса по-прежнему отображается как **Остановлен**. Чтобы остановить процесс:  
  
1.  Выберите запущенный процесс в сетке подробных сведений о действиях (на нижней панели).  
  
2.  Щелкните значок **Остановить выбранный процесс** . Можно также щелкнуть правой кнопкой мыши любой процесс в сетке подробных сведений о действиях, затем выбрать пункт **Остановить процесс** в контекстном меню.  
  
3.  Появится сообщение с запросом на подтверждение. Нажмите кнопку **Да**.  
  
  
