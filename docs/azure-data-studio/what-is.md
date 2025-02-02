---
title: Что такое студия данных Azure
titleSuffix: Azure Data Studio
description: Azure Data Studio — это бесплатные, облегченные средство, под управлением Windows, macOS и Linux, для управления SQL Server, базы данных SQL Azure и хранилище данных SQL Azure.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: overview
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.openlocfilehash: 1484d0bf2598cc3db8314c088b081ccd9327f5fe
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801917"
---
# <a name="what-is-azure-data-studio"></a>Что такое студия данных Azure?

Студия Azure данных — это кроссплатформенный базы данных средства для специалистов по базам данных с помощью семейства Microsoft локальных и облачных платформ данных в Windows, MacOS и Linux.

Ранее выпущены под именем предварительной версии SQL Operations Studio, Azure Data Studio предлагает возможности Современный редактор с Intellisense, фрагменты кода, интеграция системы управления версиями и интегрированный терминал. Оно разработано данных платформы пользователя, с помощью встроенных диаграмм в результирующих наборах запросов и настраиваемые панели мониторинга.

**[Скачайте и установите [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="sql-code-editor-with-intellisense"></a>Редактор кода SQL с использованием IntelliSense

[!INCLUDE[name-sos](../includes/name-sos-short.md)] предлагает современный, фокус ввода с клавиатуры SQL, написания кода, облегчающая повседневных задач с помощью встроенной функции, такие как несколько окон вкладку, полнофункциональный редактор SQL, IntelliSense, завершение ключевых слов, фрагменты кода, навигация по коду и системы управления версиями Интеграция (Git). Выполнение SQL-запросов по требованию, просмотреть и сохранить результаты в виде текста, JSON или Excel. Изменение данных, упорядочить свои подключения часто используемым базам данных и просматривать объекты баз данных в знакомом интерфейсе. Чтобы узнать, как с помощью редактора SQL, см. в разделе [редактор SQL для создания объектов базы данных](tutorial-sql-editor.md).

## <a name="smart-sql-code-snippets"></a>Смарт-фрагментов кода SQL

Фрагменты кода SQL создать правильный синтаксис SQL для создания базы данных, таблицы, представления, хранимые процедуры, пользователи, имена входа, ролей, и т.д. и обновлять существующие объекты базы данных. Использование смарт-фрагменты кода для быстрого создания копии базы данных для разработки и тестирования, а также создания и выполнения, создание и вставка скриптов.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] также предоставляет функциональные возможности для создания пользовательских фрагментов кода SQL. Дополнительные сведения см. в разделе [Создание и использование фрагментов кода](code-snippets.md).


## <a name="customizable-server-and-database-dashboards"></a>Настраиваемые сервера и панели мониторинга базы данных

Создание многофункциональных настраиваемые панели мониторинга для отслеживания и быстро устранять узкие места производительности в базах данных. Дополнительные сведения о insight мини-приложения и базы данных (и сервер) панели мониторинга, см. в разделе [управление серверами и базами данных с помощью мини-приложения insight](insight-widgets.md).

## <a name="connection-management-server-groups"></a>Управление соединениями (группы серверов)

Группы серверов предоставляют способ упорядочить сведения о соединении для серверов и баз данных, которыми вы работаете. Дополнительные сведения см. в разделе [групп серверов](server-groups.md).

## <a name="integrated-terminal"></a>Интегрированный терминал

Используйте привычные инструменты командной строки (например, Bash, PowerShell, sqlcmd и bcp и ssh) в окне интегрированного терминала, прямо из [!INCLUDE[name-sos](../includes/name-sos-short.md)] пользовательского интерфейса. Дополнительные сведения о встроенном терминале, см. в разделе [интегрированный терминал](integrated-terminal.md).

## <a name="extensibility-and-extension-authoring"></a>Расширяемость и создания расширений

Улучшения [!INCLUDE[name-sos](../includes/name-sos-short.md)] пользователя, расширения функциональных возможностей базовой установки. [!INCLUDE[name-sos](../includes/name-sos-short.md)] предоставляет точки расширяемости для действия по управлению данными, а также поддержку для создания расширений.

Дополнительные сведения о расширяемости в [!INCLUDE[name-sos](../includes/name-sos-short.md)], см. в разделе [расширяемости](extensibility.md).
Дополнительные сведения о создании расширений, см. в разделе [создания расширений](extension-authoring.md).

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>Сравнение функций с SQL Server Management Studio (SSMS)

**Использовать Azure Data Studio, если вы:**
- Должны выполняться на macOS или Linux
- При подключении к кластеру больших данных SQL Server 2019
- Большую часть своего времени, редактировании или выполнении запросов
- Необходима возможность быстро диаграммы и визуализировать результирующих наборов
- Можно выполнять большинство административных задач через интегрированный терминал, с помощью sqlcmd или Powershell
- Минимальный требуются для работы мастера
- Не обязательно делать глубоких административной конфигурации

**Используйте SQL Server Management Studio, если вы:**
- Большую часть времени на задачи администрирования базы данных
- Выполняете глубоких административной конфигурации
- Делают управление безопасностью, включая управление пользователями, оценка уязвимостей и настройки функций безопасности
- Использовать отчеты для SQL Server Query Store
- Нужно использовать настройки ак советников по производительности и панелей мониторинга
- Выполняете импорта и экспорта файлов DACPAC
- Требуется доступ зарегистрированные серверы и хотите управлять SQL Server, служб в Windows

### <a name="shell"></a>Shell

|Компонент|Azure Data Studio|SSMS|
|:---|:---|:---|
|Вход в Azure|Да|Да|
|Панель мониторинга|Да||
|Модули|Да||
|Интегрированный терминал|Да||
|обозревателе объектов|Да|Да|
|Скрипты объектов|Да|Да|
|Система проектов|Да||
|Выбрать из таблицы|Да|Да|
|Системы управления исходным кодом|Да||
|Область задач|Да||
|Темы|Да||
|Темно-режим|Да||
|Обозреватель ресурсов Azure|Предварительный просмотр||
|Мастер создания скриптов||Да|
|Помощью DACPAC||Да|
|Свойства объекта||Да|
|конструктор таблиц||Да|


### <a name="query-editor"></a>Редактор запросов

|Компонент|Azure Data Studio|SSMS|
|:---|:---|:---|
|Средства просмотра диаграмм|Да||
|Экспортировать результаты в CSV, JSON, XLSX|Да||
|технология IntelliSense|Да|Да|
|Фрагменты кода|Да|Да|
|Показать план|Предварительный просмотр|Да|
|Статистика клиента||Да|
|Динамическая Статистика запросов||Да|
|Параметры запроса||Да|
|В файл||Да|
|В виде текста||Да|
|Средство просмотра пространственных||Да|
|SQLCMD||Да|

### <a name="operating-system-support"></a>Поддержка операционных систем

|Компонент|Azure Data Studio|SSMS|
|:---|:---|:---|
|Linux|Да||
|macOS|Да||
|Windows|Да|Да|

### <a name="data-engineering"></a>Проектирование данных

|Компонент|Azure Data Studio|SSMS|
|:---|:---|:---|
|Создание внешних таблиц|Предварительный просмотр||
|Интеграция HDFS|Предварительный просмотр||
|Записные книжки|Предварительный просмотр||

### <a name="database-administration"></a>Администрирование базы данных

|Компонент|Azure Data Studio|SSMS|
|:---|:---|:---|
|Резервное копирование и восстановление|Да|Да|
|Импорт неструктурированного файла|Предварительный просмотр|Да|
|Агент SQL Server|Предварительный просмотр|Да|
|SQL Profiler|Предварительный просмотр|Да|
|AlwaysOn||Да|
|Постоянное шифрование||Да|
|Мастер копирования данных||Да|
|Помощник по настройке данных||Да|
|Просмотр журнала ошибок||Да|
|Планы обслуживания||Да|
|Запрос с несколькими серверами||Да|
|Управление на основе политик||Да|
|PolyBase||Да|
|Хранилище запросов||Да|
|зарегистрированные серверы||Да|
|Репликация||Да|
|Управление безопасностью||Да|
|Компонент Service Broker||Да|
|Служба SQL Mail||Да|
|Template Explorer||Да|
|Оценка уязвимостей||Да|
|Управление XEvent||Да|

## <a name="next-steps"></a>Следующие шаги

- [Скачайте и установите [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [Подключение и запрос SQL Server](quickstart-sql-server.md)
- [Подключение и запрос базы данных SQL Azure](quickstart-sql-database.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]