---
title: Параметры редактора Transact-SQL | Документация Майкрософт
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_GRID
- sql.data.tools.SqlExecutionAdvancedSettingsOption
- sql.data.tools.SqlExecutionAnsiSettingsDlg
- sql.data.tools.SqlResultToTextSettingsDlg
- sql.data.tools.SqlExecutionGeneralSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.GENERAL
- sql.data.tools.unittesting.tsqleditor
- sql.data.tools.SqlResultsToGridSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.EDITOR_TAB_AND_STATUS_BAR
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_TEXT
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ANSI
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.ONLINE_EDITING
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ADVANCED
ms.assetid: fa9a250f-7feb-433e-91bd-a09779d74c8b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3d95c52bc55df0a7693ee698cc5f01252c05949f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65102061"
---
# <a name="transact-sql-editor-options"></a>Параметры редактора Transact-SQL
Этот раздел содержит сведения о некоторых параметрах редактора Transact-SQL. Чтобы настроить эти параметры, откройте меню **Средства/Параметры** и перейдите в диалоговое окно **Параметр**.  
  
[Выполнение запроса](#QueryExecution)  
  
[Результаты запроса](#QueryResults)  
  
## <a name="QueryExecution"></a>Выполнение запроса  
  
|Свойство|Описание|  
|------------|---------------|  
|**SET ROWCOUNT**|Значение по умолчанию, равное 0, указывает на то, что SQL Server будет продолжать ожидание результатов, пока все из них не будут получены. При установке значения больше 0 SQL Server прервет запрос после получения указанного числа строк. Для выключения этого параметра (чтобы возвращались все строки) задайте SET ROWCOUNT 0.|  
|**SET TEXTSIZE**|Значение по умолчанию, равное 2 147 483 647 байт, указывает на то, что SQL Server предоставит содержимое поля полностью вплоть до пределов для полей данных text, ntext, nvarchar(max) и varchar(max). Этот параметр не влияет на тип данных xml. Задав меньшее число, можно ограничить вывод результатов в случае больших значений. Содержимое столбцов большего размера, чем заданное число, будет усекаться.|  
|**Время ожидания выполнения**|Указывает число секунд ожидания перед отменой запроса. Значение, равное 0, указывает на неограниченное время ожидания или отсутствие времени ожидания.|  
|**По умолчанию открывать новые запросы в режиме SQLCMD**|При установке этого флажка новые запросы будут открываться в режиме SQLCMD. Этот флажок становится видимым только в случае, если диалоговое окно открыто из меню Средства.<br /><br />При выборе этого параметра следует учитывать следующие ограничения.<br /><br />– Технология IntelliSense в редакторе запросов ядра СУБД отключена.<br />– Так как редактор запросов не запускается из командной строки, невозможно передать ему такие параметры командной строки, как переменные.<br />– Так как редактор запросов не может отвечать на приглашения операционной системы, будьте внимательны и не запускайте интерактивные инструкции.|  
|**SET NOCOUNT**|Останавливает сообщение, указывающее количество строк, затронутых инструкцией Transact-SQL, из возвращаемых в составе результата. Дополнительные сведения см. в разделе [SET NOCOUNT](https://go.microsoft.com/fwlink/?LinkID=238731).|  
|**SET NOEXEC**|При значении **ON** инструктирует Microsoft® SQL Server™ компилировать все пакеты инструкций Transact-SQL, но не выполнять их. При значении **OFF** инструктирует Microsoft® SQL Server™ выполнять все пакеты после компиляции. Дополнительные сведения см. в разделе [SET NOEXEC (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238770).|  
|**SET PARSEONLY**|Проверяет синтаксис каждой инструкции Transact-SQL и возвращает сообщения об ошибках без компиляции или выполнения инструкции. Дополнительные сведения см. в разделе [SET PARSEONLY](https://go.microsoft.com/fwlink/?LinkId=238734).|  
|**SET CONCAT_NULL_YIELDS_NULL**|Управляет тем, как будут обрабатываться результаты объединения: как значения NULL или как пустые строковые значения. Дополнительные сведения см. в разделе [SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238733).|  
|**SET ARITHABORT**|Завершает запрос, если во время выполнения запроса возникает ошибка переполнения или деления на нуль. Дополнительные сведения см. в разделе [SET ARITHABORT](https://msdn.microsoft.com/library/aa259212(v=SQL.80).aspx).|  
|**SET SHOWPLAN_TEXT**|Предписывает Microsoft® SQL Server™ не выполнять инструкции Transact-SQL. Вместо этого SQL Server возвращает подробные сведения о ходе выполнения инструкций. Дополнительные сведения см. в разделе [SET SHOWPLAN_TEXT (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkID=238737).|  
|**SET STATISTICS TIME**|Отображает время в миллисекундах, необходимое для синтаксического анализа, компиляции и выполнения каждой инструкции.|  
|**SET STATISTICS IO**|Предписывает Microsoft® SQL Server™ отображать сведения об объеме дисковой активности, создаваемой инструкциями Transact-SQL.|  
|**SET TRANSACTION ISOLATION LEVEL**|Управляет режимом блокировки транзакций по умолчанию для всех инструкций Microsoft® SQL Server™ **SELECT** , выдаваемых соединением. Дополнительные сведения см. в разделе  [SET TRANSACTION ISOLATION LEVEL](https://go.microsoft.com/fwlink/?LinkId=238730).|  
|**SET LOCK_TIMEOUT**|Указывает количество миллисекунд, в течение которых инструкция ожидает снятия блокировки. Дополнительные сведения см. в разделе [SET LOCK_TIMEOUT (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238747).|  
|**SET QUERY_GOVERNOR_COST_LIMIT**|Переопределяет текущее настроенное значение для текущего соединения. Дополнительные сведения см. в разделе [SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238749).|  
|**SET ANSI_DEFAULTS**|Управляет группой параметров Microsoft® SQL Server™, которая задает определенное поведение стандарта SQL-92. Дополнительные сведения см. в разделе [SET ANSI_DEFAULTS (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238750).|  
|**SET QUOTED_IDENTIFIER**|Предписывает Microsoft® SQL Server™ следовать правилам SQL-92 относительно разделения кавычками идентификаторов и строк-литералов. Идентификаторы, разделенные двойными кавычками, могут либо быть зарезервированными ключевыми словами Transact-SQL, либо содержать символы, которые обычно не допускаются правилами синтаксиса языка Transact-SQL для идентификаторов. Дополнительные сведения см. в разделе [SET QUOTED_IDENTIFIER (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238751).|  
|**SET ANSI_NULL_DFLT_ON**|Изменяет поведение сеанса, чтобы переопределить допустимость значений NULL по умолчанию в новых столбцах, если параметр ANSI null базы данных по умолчанию имеет значение false. Дополнительные сведения см. в описании [SET ANSI_NULL_DFLT_ON](https://go.microsoft.com/fwlink/?LinkID=238752).|  
|**SET IMPLICIT_TRANSACTIONS**|При значении **ON**задается соединение в режиме неявных транзакций. При значении **OFF**возвращается соединение в режим с автоматической фиксацией транзакций. Дополнительные сведения см. в разделе [SET IMPLICIT_TRANSACTIONS (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238753).|  
|**SET CURSOR_CLOSE_ON_COMMIT**|Управляет тем, закрывается ли курсор при фиксации транзакции. Дополнительные сведения см. в описании [SET CURSOR_CLOSE_ON_COMMIT](https://go.microsoft.com/fwlink/?LinkId=238754).|  
|**SET ANSI_PADDING**|Управляет способом хранения в столбце значений короче, чем определенный размер столбца, и способом хранения в столбце значений, имеющих замыкающие пробелы, в данных **char**, **varchar**, **binary**и **varbinary** . Дополнительные сведения см. в описании [SET ANSI_PADDING](https://go.microsoft.com/fwlink/?LinkId=238755).|  
|**SET ANSI_WARNINGS**|Указывает поведение стандарта SQL-92 при некоторых ошибках. Дополнительные сведения см. в разделе [SET ANSI_WARNINGS (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238758).|  
|**SET ANSI_NULLS**|Задает совместимое со стандартом SQL-92 поведение операторов сравнения "равно" ( **=** ) и "не равно" ( **<>** ) при использовании со значениями NULL. Дополнительные сведения см. в разделе [SET ANSI_NULLS (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=238759).|  
  
## <a name="QueryResults"></a>Результаты запроса  
  
|Свойство|Описание|  
|------------|---------------|  
|**Включение запроса в результирующий набор**|Возвращает текст запроса как часть результирующего набора.|  
|**Включение заголовков столбцов при копировании или сохранении результатов**|Включает верхние колонтитулы столбцов (заголовки) при копировании результатов в буфер обмена или при сохранении файла. Снимите этот флажок, если нужно, чтобы при сохранении или копировании данных результатов они содержали только данные, без заголовков столбцов.|  
|**Сброс результатов после выполнения**|Освобождает память посредством сбрасывания результатов запроса после того, как они были выведены на экран.|  
|**Отображение результатов на отдельной вкладке**|Отобразить результирующий набор в новом окне документа, а не в нижней части окна документа запроса.|  
|**Переключение на вкладку результатов после выполнения запроса**|Автоматически переводит изображение на экране к результирующему набору.|  
|**Максимальное число полученных символов**|Данные не в формате XML:<br /><br />Введите число от 1 до 65 535, чтобы указать максимальное число символов, отображаемых в каждой ячейке. **Примечание.** Указание слишком большого числа символов может привести к тому, что результирующий набор будет отображаться усеченным. Максимальное число символов, отображаемых в каждой ячейке, зависит от размера шрифта. Высокое значение в этом окне может привести к нехватке памяти для среды SQL Server Management Studio и снижению производительности системы при возвращении больших результирующих наборов.<br /><br />XML-данные:<br /><br />Выберите 1 МБ, 2 МБ или 5 МБ. Выберите пункт «Без ограничений», чтобы вывести все символы.|  
|**Формат вывода**|По умолчанию выходные данные отображаются в столбцах, полученных дополнением результатов пробелами. Другие параметры используют для разделения столбцов запятые, символы табуляции и пробелы. Установите флажок **Другой** , чтобы задать иной разделяющий символ в поле **Произвольный разделитель** .|  
|**Пользовательский разделитель**|Задайте символ, которым будут разделяться столбцы. Этот параметр доступен, только если флажок **Другой** был выбран в поле **Выходной формат** .|  
|**Включение заголовков столбцов в результирующий набор**|Снимите этот флажок, если заголовки столбцов не нужны.|  
|**Прокрутка по мере получения результатов**|Установите этот флажок, чтобы в нижней части экрана отображались последние возвращаемые строки. Снимите этот флажок, чтобы на экране отображалась первая возвращенная строка.|  
|**Выравнивание числовых значений по правому краю**|Установите этот флажок, чтобы выровнять числовые значения по правому краю столбца. Этот параметр облегчает просмотр целочисленных значений и цифр с десятичными разрядами.|  
|**Сброс результатов после выполнения запроса**|Освобождает память, сбрасывая результаты выполнения запроса после того, как их получит экранное устройство отображения.|  
|**Отображение результатов на отдельной вкладке**|Установите этот флажок, чтобы вывести результирующий набор в окне нового документа, а не в нижней части окна документа запроса.|  
|**Переключение на вкладку результатов после выполнения запроса**|Нажмите, чтобы автоматически сфокусировать экран на результирующем наборе.|  
|**Максимальное число символов, отображаемых в каждом столбце**|По умолчанию это значение равно 256. Увеличьте это значение для вывода результирующих наборов большего размера без усечения.|  
|**Сброс до значений по умолчанию**|Позволяет вернуть исходные значения по умолчанию для всех параметров на данной странице.|  
  
