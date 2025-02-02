---
title: Руководство. Использование сравнения схем для сопоставления разных определений баз данных | Документация Майкрософт
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.schemacompare.SchemaCompareOptionsDialog
- sql.data.tools.schemacompare.watermark.f1
- sql.data.tools.schemacompare.f1
- sql.data.tools.schemacompare.connectiondialog.f1
- sql.data.tools.schemacompare.connectiondialog.error.f1
ms.assetid: 7f0905a4-081c-46e2-bd7d-325b63e5c675
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cd48c91bee175e3cc2bdb0031d70a9d8e68d95c4
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095934"
---
# <a name="how-to-use-schema-compare-to-compare-different-database-definitions"></a>Руководство. использовать сравнение схем для сопоставления различных определений баз данных
В SQL Server Data Tools (SSDT) входит программа сравнения схем, которая позволяет сравнивать два определения базы данных.  Источником и целью сравнения может быть любое сочетание подключенной базы данных, проекта базы данных SQL Server, файла моментального снимка и файла DACPAC.  Результаты сравнения выводятся в виде набора действий, которые необходимо выполнить с целевой базой, чтобы сделать ее идентичной исходной базе.  После завершения сравнения вы можете обновить целевую базу непосредственно (если это проект или база данных) или создать скрипт обновления, выполняющий те же действия.  
  
Различия между источником и целью представляются в виде сетки для удобства просмотра.  Для каждого различия поддерживается детализация в сетке результатов или в форме скрипта.  Затем вы можете выборочно исключить отдельные различия.  
  
Результаты сравнения вы можете сохранять в составе проекта базы данных SQL Server или в отдельном файле.  Также вы можете задать параметры, управляющие областью сравнения и аспектами обновления.  Затем вы можете сохранить сравнение, чтобы проще было повторить его с теми же параметрами или использовать в качестве отправной точки для нового сравнения.  
  
В следующей процедуре схема проекта базы данных сравнивается со схемой подключенной базы данных.  
  
> [!WARNING]  
> Если проект указан как целевой для сравнения, то максимальная поддерживаемая длина пути (не считая буквы диска, двоеточия и обратной косой черты) для проекта составляет 256 символов. Если путь к проекту превышает 256 символов, то все-таки есть возможность сравнить его схему со схемой базы данных или другого проекта. Однако в таком случае нельзя обновить его схему.  
  
> [!WARNING]  
> В следующих процедурах используются сущности, созданные с помощью процедур, которые описывались ранее в разделах [Connected Database Development](../ssdt/connected-database-development.md) (Разработка подключенной базы данных) и [Project-Oriented Offline Database Development](../ssdt/project-oriented-offline-database-development.md) (Разработка базы данных вне сети с учетом проекта).  
  
### <a name="to-compare-database-definitions"></a>Сравнение определений баз данных  
  
1.  В меню **SQL** последовательно выберите **Сравнение схем**и **Новое сравнение схем**.  
  
    Также можно щелкнуть правой кнопкой мыши проект **TradeDev** в **обозревателе решений** и выбрать пункт **Сравнение схем**.  
  
    Откроется окно **Сравнение схем**, и Visual Studio автоматически назначит сравнению имя, например `SqlSchemaCompare1`.  
  
    Под панелью инструментов в окне **Сравнение схем** выводятся два раскрывающихся меню, разделенные зеленой стрелкой. Эти меню позволяют выбрать определения базы данных в качестве источника и цели сравнения.  
  
2.  В раскрывающемся списке **Выбор источника** выберите команду **Выбрать источник**. Откроется диалоговое окно **выбора исходной схемы**.  
  
    Обратите внимание, что если окно **Сравнение схем** открывалось из контекстного меню для имени проекта, то исходная схема уже заполнена и можно переходить к шагу 4.  
  
3.  Выберите вариант **Проект**, а затем выберите проект базы данных **TradeDev**, созданный в предыдущей процедуре.  
  
4.  В раскрывающемся списке **Выбор цели** в окне **Сравнение схем** выберите команду **Select Target** (Выбрать цель). Откроется диалоговое окно **выбора целевой схемы**. В разделе **Схема** выберите вариант **База данных** и нажмите кнопку **Создать соединение**.  
  
5.  В диалоговом окне **Свойства соединения** введите имя сервера, на котором размещается база данных `TradeDev`, и проверьте правильность введенных учетных данных для аутентификации. Затем выберите базу **TradeDev** в разделе **Соединение с базой данных** и нажмите кнопку **ОК**.  
  
    Также вы можете нажать кнопку **Параметры** на панели инструментов в окне **Сравнение схем**, чтобы указать объекты для сравнения, пропускаемые типы различий и другие параметры.  
  
6.  Нажмите кнопку **Сравнить** на панели инструментов в окне **Сравнение схем**, чтобы запустить процесс сравнения.  
  
    Когда сравнение будет завершено, структурные различия между проектом и базой данных отобразятся на панели **Результаты** в верхней части окна. По умолчанию в результатах сравнения все различия группируются по действию (удалить, изменить или добавить). На панели **Результаты** отображается строка для каждого объекта базы данных, который различается в двух определениях базы данных. Каждая строка определяет объект в исходной или целевой схеме и действие, которое нужно выполнить в целевой схеме, чтобы целевой объект стал идентичным исходному объекту.  Если объект в ходе рефакторинга был переименован или перемещен в новую схему, то исходное и целевое имя будут различны и исходное имя будет выделено полужирным шрифтом.  
  
    По умолчанию в списке результатов остаются скрытыми объекты, которые совпадают в обеих схемах или не поддерживаются для обновления (например, встроенные объекты).  Чтобы показать эти объекты, вы можете нажать соответствующие кнопки фильтров на панели инструментов.  
  
    Чтобы изменить порядок группирования, щелкните раскрывающийся список **Группировать результаты** на панели инструментов.  Выберите пункт **Тип**, чтобы сгруппировать результаты по типу объекта (например, по таблицам, представлениям или хранимым процедурам).  
  
7.  Найдите таблицу `Products` в группе `Tables`. Щелкните строку и обратите внимание, что исходное и целевое определения таблицы выводятся на панели **Определения объектов** с выделением различий. Также можно развернуть строку таблицы `Products` на панели **Результаты**, чтобы проверить отдельные различающиеся элементы таблицы.  
  
8.  По умолчанию все различия включаются в область действия «Обновить целевую схему». Вы можете исключить любые различия, которые не нужно синхронизировать. Для этого снимите флажок в столбце **Действие** в центре каждой строки. Кроме того, можно щелкнуть правой кнопкой мыши строку на панели "Схема" и выбрать пункт **Исключить**. Обратите внимание, что эта строка сразу станет неактивной. Когда придет время обновления целевой базы данных, эта строка не будет учитываться среди отложенных изменений.  
  
    Также вы можете щелкнуть правой кнопкой мыши строку группы и выбрать пункт **Исключить все** или **Включить все**, что равносильно снятию или установке флажков для всех различий в данной группе. Если результаты сгруппированы по схеме, это действие позволяет быстро включить или исключить все изменения, относящиеся к определенной схеме.  
  
    > [!WARNING]  
    > Если у исключаемой строки есть зависимые объекты (например, строка **Таблица**, на которую ссылается строка **Представление**), то исключаемая строка будет отключена, но ее флажок не будет снят. После того как будут сняты флажки у всех зависимых строк, флажок отключенной строки будет снят. Кроме того, если строка прошла рефакторинг (переименована или перемещена в другую схему), то флажок будет недоступен и для этой строки, и для всех зависимых дочерних строк.  
    >   
    > Обратите внимание, что, если обновить сравнение, то различия, которые были отмечены как пропускаемые, не будут обрабатываться.  
  
Существует два способа обновления схемы целевой базы данных. Вы можете непосредственно обновить целевую схему в окне **Сравнение схем**, если целью является база данных или проект, или создать скрипт обновления, если целью является база данных или файл базы данных.  Созданный скрипт появляется в редакторе Transact\-SQL, где вы можете проверить выполнение скрипта в базе данных. В следующих процедурах эти возможности описаны подробно.  
  
> [!WARNING]  
> Обновление завершится ошибкой, поскольку изменение подразумевает изменение типа столбца с NOT NULL на NULL, что приводит к потере данных. Чтобы продолжить обновление, нажмите кнопку **Параметры** (пятая слева) на панели инструментов в окне "Сравнение схем" и снимите флажок **Блокировать добавочное развертывание при потере данных**.  
  
### <a name="to-update-directly-in-the-schema-compare-window"></a>Прямое обновление в окне «Сравнение схем»  
  
1.  Нажмите кнопку **Обновить** на панели инструментов в окне "Сравнение схем".  
  
2.  Проверьте созданный скрипт изменений. Этот скрипт вы можете сохранить с помощью меню «Файл/создать». Это может быть удобно в ситуациях, когда недостаточно полномочий для обновления производственной базы данных. В этом случае вы можете передать скрипт администратору баз данных для последующего развертывания.  
  
3.  При наличии необходимого разрешения на обновление базы данных нажмите кнопку **Выполнить запрос** на панели инструментов в области редактирования, чтобы выполнить скрипт.  
  
### <a name="to-update-by-script"></a>Обновление с помощью скрипта  
  
1.  Нажмите кнопку **Создать скрипт** (четвертую слева) на панели инструментов в окне "Сравнение схем".  
  
    Созданный скрипт откроется в новом окне редактора Transact\-SQL.  
  
    > [!WARNING]  
    > Этот режим поддерживается только для DACPAC-файлов, созданных в процессе создания моментальных снимков SSDT.  В этой версии нельзя выбрать DACPAC-файл, созданный платформой или средствами приложения уровня данных (DAC) SQL.  
  
2.  Проверьте созданный скрипт изменений. Скрипт вы можете сохранить с помощью команды "Сохранить" или "Сохранить как" в меню **Файл**.  
  
    Сохраненный скрипт может быть удобен в ситуациях, когда недостаточно полномочий для обновления рабочей базы данных. В этом случае вы можете передать скрипт администратору базы данных для последующего развертывания.  
  
    Также вы можете подключить редактор Transact\-SQL к нужному серверу и непосредственно выполнить скрипт. Перед выполнением этой процедуры необходимо получить необходимое разрешение на создание или обновление базы данных. При наличии необходимого разрешения на обновление базы данных нажмите кнопку **Выполнить запрос** на панели инструментов в области редактирования, чтобы выполнить скрипт.  
  
3.  Нажмите кнопку **Подключить**. Это действие устанавливает соединение с текущим сервером либо предлагает ввести новый сервер или выбрать сервер в диалоговом окне «Соединение с сервером».  Обратите внимание, что имя базы данных определяется в скрипте как переменная команды.  
  
4.  Проверьте скрипт и в случае необходимости измените переменные команды, которые определяют имя целевой базы данных, соответствующий префикс и пути к файлам.  
  
5.  Нажмите кнопку **Выполнить** на панели инструментов в области редактирования, чтобы выполнить скрипт.  
  
