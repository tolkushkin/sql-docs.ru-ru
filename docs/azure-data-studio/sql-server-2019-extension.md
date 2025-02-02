---
title: Расширение SQL Server 2019 (Предварительная версия)
titleSuffix: Azure Data Studio
description: Расширение 2019 г. версия SQL Server для данных в студии
ms.custom: seodec18
ms.date: 05/15/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: aa83e92fb62f9cb0ad00830d1e78e5367112899c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798056"
---
# <a name="sql-server-2019-extension-preview"></a>Расширение SQL Server 2019 (Предварительная версия)

Расширение SQL Server 2019 (Предварительная версия) обеспечивает поддержку предварительной версии новых функциях и средствах доставки поддержки [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Сюда входит поддержка предварительной версии [кластеров SQL Server 2019 больших данных](../big-data-cluster/big-data-cluster-overview.md), интегрированное [записная книжка](../big-data-cluster/notebooks-guidance.md)и PolyBase [мастера Create External Table](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json).

## <a name="install-the-sql-server-2019-extension-preview"></a>Установите расширение SQL Server 2019 (Предварительная версия)

Чтобы установить расширение SQL Server 2019 (Предварительная версия), загрузите и установите связанный VSIX-файл.

1. Загрузите VSIX-файл SQL Server 2019 расширения (Предварительная версия) в локальный каталог:

   |Платформа|Загрузить|Дата выпуска|Версия
   |:---|:---|:---|:---|
   |Windows|[.VSIX](https://go.microsoft.com/fwlink/?linkid=2092817)|15 мая 2019 г. |0.13.1
   |macOS|[.VSIX](https://go.microsoft.com/fwlink/?linkid=2092816)|15 мая 2019 г. |0.13.1
   |Linux|[.VSIX](https://go.microsoft.com/fwlink/?linkid=2092815)|15 мая 2019 г. |0.13.1

1. В Azure Data Studio выберите **установить расширения из пакета VSIX** из **файл** меню и выберите загруженный VSIX-файл.

1. Выберите **Да** при появлении запроса на подтверждение установки и появится уведомление об успешном завершении установки.

1. Выберите **перезагрузить** для включения расширения (только обязательно при первоначальной установке расширения).

1. После повторной загрузки расширения будут установлены зависимости. Вы увидите ход выполнения в окне вывода и может занять несколько минут.

1. После зависимостей завершить установку, закройте и снова откройте Studio данных Azure. **Кластера больших данных в SQL Server** тип подключения недоступен, необходимо перезапустить Studio данных Azure.

## <a name="changes-in-release-0121"></a>Изменения в выпуске 0.12.1

* **Кластера больших данных в SQL Server** тип подключения был удален в этом выпуске. Все функции, ранее доступные из подключение к кластеру больших данных SQL Server теперь доступна в подключении к SQL Server.
* Просмотр HDFS можно найти в разделе **Data Services** папки
* Для записных книжек ядрами PySpark и других больших данных работать при подключении к основной экземпляр SQL Server в кластере SQL Server больших данных.
* Создание внешних таблиц:
  * Поддержка создания внешней таблицы, используя внешний источник данных.
  * Повышение производительности по мастеру.
  * Улучшенная обработка имен объектов со специальными символами. В некоторых случаях это вызвало сбой мастера
  * Улучшения надежности для страницы объекта сопоставления.
  * Удаление системных баз данных - «: DWConfiguration», «DWDiagnostics», «DWQueue -» из раскрывающегося списка баз данных.
  * Поддержка для установки имя объекта формата внешнего файла **Create External Table из CSV-файлов** мастера.
  * Добавлена кнопка обновления на первой странице **Create External Table из CSV-файлов** мастера.

## <a name="release-notes-v0110"></a>Заметки о выпуске (v0.11.0)

* Поддержка записной книжки Jupyter, предназначенные для поддержки для ядра Python3 и Spark, была перемещена в Azure Data Studio. Это расширение больше не нужна для использования записными книжками.
* Большое количество ошибок в мастерах внешних данных:
  * Сопоставления типов Oracle были обновлены в соответствии с изменениями, встроенными в SQL Server 2019 CTP 2.3.
  * Устранена проблема, в которых были потери новых схем, введенные в элементы управления из таблицы сопоставления.
  * Устранена проблема, где проверка узел базы данных в таблице сопоставления не привел к все таблицы и представления, для которого проверяется.


## <a name="release-notes-v0102"></a>Заметки о выпуске (v0.10.2)
### <a name="sql-server-2019-support"></a>Поддержка SQL Server 2019
Поддержка SQL Server 2019 был обновлен. О подключении к кластеру больших данных SQL Server экземпляр новый _Data Services_ папка будет отображаться в дереве обозревателя. Это оказывает точки запуска для действия, такие как открытие записной книжки для подключения, отправка заданий Spark и работа с HDFS. Обратите внимание, что для некоторых действий, таких как _Создание внешних данных_ через HDFS файла или папки, _предварительной версии SQL Server 2019_ необходимо установить расширение.

### <a name="notebook-support"></a>Поддержка записной книжки
Мы внесли значительные изменения в пользовательский интерфейс записной книжки в этом выпуске. Мы сосредоточились на это упрощает чтение записных книжек, которые являются общими с вами. Это означало, удаляя все структуры поля вокруг ячеек, если не выбран или указателем мыши, добавления поддержки при наведении указателя мыши легко действия на уровне ячейки не нужно выбрать ячейку и прояснения состояние выполнения, добавив число выполнений, анимированного _остановки выполнения_ кнопки и многое другое. Мы также добавили сочетания клавиш для _новой записной книжки_ (`Ctrl+Shift+N`), _запуска ячейки_ (`F5`), _новую ячейку кода_ (`Ctrl+Shift+C`),  _Новый текст ячейки_ (`Ctrl+Shift+T`). В будущем, мы будет должны быть все ключевые действия можно будет запустить с ярлыка так что дайте нам знать, что вы пропустили!

Другие улучшения и исправления:
* _Предварительной версии SQL Server 2019_ расширения теперь использует запросы, чтобы выбрать каталог установки для зависимостей Python. Он также больше не включает в себя Python в `.vsix file`, уменьшая общий размер расширения. Для поддержки ядра Spark и Python3, поэтому установка этого расширения требуется использовать эти необходимы зависимостей Python.
* Добавлена поддержка для запуска новой записной книжки из командной строки. Запуск с аргументами `--command=notebook.command.new --server=myservername` должен открыть записную книжку и подключиться к этому серверу.
* Исправление производительности для записных книжек с большим объемом кода длиной в ячейках. Если ячейки кода более 250 строк, у него будет добавлена полоса прокрутки.
* Улучшенная поддержка .ipynb файл. Теперь поддерживается 3 или более поздней версии. Обратите внимание на то, что при сохранении файлов будет обновляться до версии 4 или более поздней версии.
* `notebook.enabled` Пользовательский параметр был удален теперь, встроенные в записной книжке стабильна, средство просмотра
* В этом случае темы высокой контрастности теперь поддерживается ряд исправлений для макета объекта.
* Исправлена 3680 # где выходных данных иногда показал ряд `,,,` символы неправильно
* Фиксированный редактор #3602 исчезает для ячеек после ухода studio данных azure
* Добавлена поддержка для использования представления сетки для `application/vnd.dataresource+json` MIME-тип выходных данных. Это означает, что множество записных книжек, которые используют данный (например, задав `pd.options.display.html.table_schema` в записной книжке Python) будет иметь лучше табличных выходных данных основных #3959 Azure Data Studio пытается завершить работу сервера записной книжки дважды, после закрытия записной книжки

#### <a name="known-issues"></a>Известные проблемы
* При открытии записной книжки будет отображаться диалоговое окно установки python. Отмена установки приведет к в ядрах и присоединение к раскрывающиеся списки не отображаются значения. Обойти это, чтобы завершить установку Python.
* При открытии записной книжки с ядром, не поддерживается, ядер и _присоединить к_ раскрывающиеся списки приведет к Azure Data Studio зависает. Необходимо будет закрыть Studio данных Azure и убедитесь, при использовании ядра, который поддерживается (Python3, Spark | R, Spark | Scala, PySpark, PySpark3)
* При использовании PySpark3 или других ядра Spark для конечной точки SQL Server, происходит сбой связи пользовательского интерфейса Spark. В качестве решения нажмите кнопку в пользовательском Интерфейсе Spark с помощью панели мониторинга или подключения с помощью тип подключения кластера больших данных SQL Server, как это свойство будет иметь правильный пользовательский Интерфейс Spark гиперссылки

### <a name="extensibility-improvements"></a>Расширяемость
Ряд улучшений, помогающих расширителей были добавлены в этом выпуске
* Новый `ObjectExplorerNodeProvider` API позволяет расширениям contribute папок в SQL Server или другие узлы подключения. Это как `Data Services` узел добавляется в группе экземпляров SQL Server 2019, но может использоваться в легко добавлять к пользовательскому Интерфейсу мониторинга или других папок.
* Доступны две новые значения для ключа контекста помогают Показать/скрыть вклад в панели мониторинга.
  * `mssql:iscluster` Указывает, является ли это кластер SQL Server 2019 больших данных
  * `mssql:servermajorversion` содержит версию сервера (15 для SQL Server 2019, 14 для SQL Server 2017 и т. д.). Это может помочь, если функции должно будет отображаться только SQL Server 2017 или более поздней версии, например.


## <a name="release-notes-v080"></a>Заметки о выпуске (версии 0.8.0)
*Записные книжки*:
* Добавление ячеек перед и после существующих ячеек теперь поддерживается, нажав кнопку «Дополнительные действия» ячейки
* **Добавить новое подключение** добавлен параметр к подключениям в раскрывающемся списке «Присоединить к»
* Объект **переустановка зависимости записной книжки** добавлена команда для облегчения обновления пакета Python и разрешения случаев, где Установка прервана получаться с помощью, закрыв приложение. Его можно запускать на палитре команд (использовать `Ctrl/Cmd+Shift+P` и тип `Reinstall Notebook Dependencies`)
* Пакет python PROSE будет обновлена для 1.1.0 и включает ряд исправлений ошибок. Используйте **переустановка зависимости записной книжки** команду, чтобы обновить этот пакет
* Объект **очистить выходные данные** команда теперь поддерживается, щелкнув **дополнительные действия** кнопка ячейки
* Устранены следующие клиентов сообщили о проблемах:
  * Не удалось запустить сеанс записной книжки на Windows из-за проблем с ПУТЕМ
  * Не удалось запустить записную книжку из корневой папки диска, например, C:\ или D:\
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) не удалось изменить записных книжек, созданный из ОБЪЯВЛЕНИЙ в VS Code
  * Ссылка на пользовательский Интерфейс Spark теперь работает при запуске ядра Spark
  * Переименовано «Управляемых пакетов» «Установка пакетов»

*Создание внешних данных*:

* Сообщения об ошибках можно копировать и были разделены на сводные и подробные представления для упрощения
* Улучшенный макет пользовательского интерфейса и значительно улучшенная надежность и обработка ошибок
* Устранены следующие клиентов сообщили о проблемах:
  * Таблицы с сопоставлениями недопустимого столбца будут отображаться в отключенном состоянии, и описывает ее предупреждение

## <a name="release-notes-v072"></a>Заметки о выпуске (v0.7.2)
* Обозреватель ресурсов Azure, теперь интегрирован в Studio данных Azure и был удален из этого расширения. Благодарим вас за отзыв об этом!
* Повышена производительность записных книжек с много ячеек Markdown.
* Код автоматически изменить размер ячейки в записной книжке. Это по-прежнему имеет минимальный размер, в зависимости от панели инструментов ячейки.
* Сообщите пользователю, при установке зависимостей записной книжки. В Windows в частности это может занять много времени, поэтому уведомления теперь отображаются в представление "задачи".
* Поддержка переустановки зависимостей записной книжки. Это полезно, если пользователь ранее закрывали Studio данных Azure во время установки.
* Поддержка отмены выполнения ячейки в записной книжке.
* Повышенная надежность при использовании мастера создания внешних данных, в частности подключение возникновения ошибок.
* Блокировать использование мастера создания внешних данных, если PolyBase не включены или не запущены на целевом сервере.
* Проверка орфографии и именования исправления, связанные с SQL Server 2019 и Создание внешних данных.
* Удалить большое количество ошибок из консоли отладки Studio данных Azure.

##  <a name="sql-server-2019-big-data-cluster-support"></a>Поддержка SQL Server 2019 больших данных кластера

* Нажмите кнопку **добавить подключение** в *обозревателя объектов* и выберите **кластера больших данных в SQL Server** типом подключения.

   > [!TIP]
   > Если вы не видите **кластера больших данных в SQL Server** тип соединения, перезапустите Azure Studio данных.

* Введите имя узла или IP-адрес конечной точки кластера, а также имя пользователя и пароль для подключения.
* При желании Допишите понятное отображаемое имя в **имя** поля.
* Нажмите кнопку **Connect** и могут запускать стандартные задачи с помощью панели мониторинга, Обзор **HDFS** в обозревателе объектов и выполнения задач в контексте оттуда.
* Отправка задания Spark для кластера, щелкните правой кнопкой мыши узел сервера в *обозревателя объектов* и выберите **отправить задание Spark** для открытия диалогового окна отправки.
* Чтобы открыть записную книжку, см. в разделе в следующем разделе.

Дополнительные сведения см. в разделе [кластерами больших данных](../big-data-cluster/big-data-cluster-overview.md).


## <a name="azure-data-studio-notebooks"></a>Записные книжки Studio данных Azure

* Откройте записную книжку в одном из следующих способов:
  * Откройте записную книжку из *палитру команд*.
  * Откройте дерева обозревателя объектов HDFS для кластера SQL Server 2019 больших данных и либо:
    * Щелкните правой кнопкой узел сервера и выберите **новой записной книжки Jupyter**.
    * Щелкните правой кнопкой в CSV-файл и выберите **анализ в записной книжке**.
  * Откройте существующий ipynb-файл, из **файл** меню или проводнике *(ipynb-файлы, необходимо обновить до версии 4 или более поздней, чтобы правильно загрузить)*
* Выберите ядро. Для выполнения локальной записной книжки выберите Python 3. Для удаленного выполнения выберите PySpark или Spark | Scala.
* Выберите конечную точку кластера SQL Server больших данных для подключения к, если удаленное выполнение (это не требуется для локальной разработки с помощью Python 3).
* Добавление кода или разметки ячеек с помощью кнопки в заголовке записной книжки. Удалите ячейки с значок корзины рядом с каждой ячейки.
* Выполнять ячейки с «воспроизвести» для ячейки кода и переключить редактирования разметки markdown и предварительного просмотра с значок с изображением глаза

## <a name="polybase-create-external-table-wizard"></a>Внешняя таблица мастер создания PolyBase

* Из экземпляра SQL Server 2019 *мастера создания внешней таблицы* можно открыть тремя способами:
  * Щелкните правой кнопкой мыши на сервере, выберите **управление**, перейдите на вкладку для SQL Server 2019 (Предварительная версия) и выберите **Create External Table**.
  * С экземпляром SQL Server 2019, выбранного в *обозревателя объектов*, подключите *Создание внешних мастер* через *палитру команд*.
  * Щелкните правой кнопкой мыши в базу данных SQL Server 2019 *обозревателя объектов* и выберите **Create External Table**.
* В этой версии расширения внешние таблицы могут быть созданы для доступа к удаленным таблицам SQL Server и Oracle.

  > [!NOTE]
  > Хотя функции внешних таблиц — это функция SQL 2019, удаленный экземпляр SQL Server может выполняться более ранней версии SQL Server.

* Выберите ли вы обращаетесь к SQL Server или Oracle на первой странице мастера и продолжить.
* Вам будет предложено создать главный ключ базы данных, если он уже не был создан (паролей или недостаточно сложности будет блокироваться).
* Создать соединение с источником данных и именованные учетные данные для удаленного сервера.
* Выберите объекты для сопоставления с новой внешней таблицы.
* Выберите **формирование скрипта** или **создать** для завершения работы мастера.
* После создания внешней таблицы, он сразу же отображается в дереве объектов базы данных, где он был создан.


## <a name="known-issues"></a>Известные проблемы

* Если пароль не сохраняется при создании подключения, некоторые действия, такие как Отправка задания Spark может завершиться неудачно.
* Существующие записных книжек .ipynb необходимо обновить до версии 4 или более поздней версии для загрузки содержимого в средстве просмотра.
* Под управлением **переустановка зависимости записной книжки** команда показывает 2 задачи в представление "задачи", один из которых завершается ошибкой. Это не приводит к сбою установки
* Выбор **Добавление нового соединения** в записной книжке и нажмите кнопку "Отмена", вызывают **выбрать подключение к** будет отображаться, даже если вы уже были подключены.
