---
title: Редактор запросов расширений интеллектуального анализа данных (службы Analysis Services — Интеллектуальный анализ данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.dmx.f1
ms.assetid: 7ac877a1-0f29-46b9-9a51-73b02172bef1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3be28b0a402743e4d9c26b346386202127c5f74d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081571"
---
# <a name="dmx-query-editor-analysis-services---data-mining"></a>Редактор DMX-запросов (службы Analysis Services — интеллектуальный анализ данных)
  Используйте редактор запросов расширений интеллектуального анализа данных, чтобы проектировать и выполнять инструкции, написанные на языке расширений интеллектуального анализа данных.  
  
## <a name="features"></a>Компоненты  
  
-   Введите скрипты на панели редактора запросов расширений интеллектуального анализа данных.  
  
-   Чтобы выполнить скрипты, нажмите клавишу **F5**или кнопку **Выполнить** на панели инструментов либо в меню **Запрос** . При выборе части кода выполнена будет только выбранная часть. Если ни одна часть кода не была выбрана, содержимое редактора запросов расширений интеллектуального анализа данных выполняется целиком.  
  
-   Просмотрите метаданные для кубов и других объектов, содержащихся в базе данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] на панели метаданных.  
  
-   Чтобы получить справку по синтаксису расширений интеллектуального анализа данных, выберите ключевое слово в редакторе запросов расширений интеллектуального анализа данных, а затем нажмите клавишу **F1**.  
  
-   Чтобы получить динамическую справку по синтаксису расширений интеллектуального анализа данных, в меню **Справка** выберите пункт **Динамическая справка** , чтобы открыть компонент динамической справки. При вводе ключевых слов в редакторе запросов разделы справки отображаются в окне **Динамическая справка** .  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Панель инструментов редакторов служб SQL Server Analysis Services  
 Если открыт редактор запросов расширений интеллектуального анализа данных, панель инструментов **Редакторы служб SQL Server Analysis Services** отображается с кнопками, перечисленными в следующей таблице.  
  
|Термин|Определение|  
|----------|----------------|  
|**Подключить**|Открывает диалоговое окно **Соединиться с сервером** для установки соединения с экземпляром служб Analysis Services.|  
|**Отключить**|Отключает редактор запросов расширений интеллектуального анализа данных от экземпляра служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Изменить соединение**|Открывает диалоговое окно **Соединение с сервером** для установки соединения с другим экземпляром служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Создать запрос в текущем соединении**|Открывает новое окно редактора запросов расширений интеллектуального анализа данных, используя сведения о соединении из текущего окна редактора запросов расширений интеллектуального анализа данных.|  
|**Доступные базы данных**|Изменяет подключение и соединяет с другой базой данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] того же экземпляра.|  
|**Выполнение**|Выполняет выбранный код или, если код не выбран, выполняет весь код в редакторе запросов расширений интеллектуального анализа данных.|  
|**Синтаксический анализ**|Проверяет синтаксис выбранного кода. Если код не выбран, осуществляет проверку синтаксиса всего содержимого окна редактора запросов расширений интеллектуального анализа данных.|  
|**Отменить выполнение запроса**|Отправляет на сервер запрос отмены. Выполнение некоторых запросов не может быть отменено немедленно, для этого необходимо дождаться подходящих условий отмены. При отмене может произойти задержка, связанная с откатом транзакций.|  
  
## <a name="dmx-query-editor-window"></a>Окно редактора запросов расширений интеллектуального анализа данных  
 Параметры, перечисленные в следующей таблице, доступны в редакторе запросов расширений интеллектуального анализа данных.  
  
|Термин|Определение|  
|----------|----------------|  
|**Окно редактора запросов**|Введите инструкции и скрипты расширений интеллектуального анализа данных, которые должны быть выполнены редактором запросов расширений интеллектуального анализа данных.<br /><br /> Контекстное меню редактора запросов содержит следующие пункты.<br /><br /> **Вырезать**. Копирует текущее выделение в буфер обмена и удаляет выделение из окна редактора запросов.<br /><br /> **Копировать**. Копирует текущее выделение в буфер обмена.<br /><br /> **Вставить**. Вставляет содержимое буфера обмена в текущее выделение.<br /><br /> **Соединить**. Открывает диалоговое окно **Соединиться с сервером** для установки соединения с экземпляром служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Отключить**. Отключает текущий редактор запросов от экземпляра служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Отключить все запросы**. Отключает все открытые редакторы запросов.<br /><br /> **Изменить соединение**. Открывает диалоговое окно **Соединение с сервером** для установки соединения с другим экземпляром служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Открыть сервер в обозревателе объектов**. Открывает диалоговое окно [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , с которым соединен текущий редактор запросов, в **обозревателе объектов**.<br /><br /> **Выполнить**. Выполняет выбранный код или, если код не выбран, выполняет весь код в текущем редакторе запросов.<br /><br /> **Окно "Свойства"**. Отображает окно **Свойства** в среде [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] для текущего окна запроса.<br /><br /> **Параметры запроса**. Отображает диалоговое окно **Параметры запроса** .|  
|**Окно метаданных**|Отображает метаданные для базы данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , подключенной в настоящий момент.|  
|**Cube**|Выберите куб в подключенной на текущий момент базе данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , чтобы отобразить метаданные, связанные с кубом, на вкладке **Метаданные** .|  
|**Метаданные**|Отображает метаданные для куба, выбранного на вкладке **Куб**, включая группы мер и меры, ключевые показатели эффективности, измерения, иерархии, уровни, элементы и свойства элементов. Чтобы получить полный ключ объекта, выполните одно из следующих действий.<br /><br /> Перетащите объект из вкладки **Метаданные** на панель запроса.<br /><br /> или:<br /><br /> Щелкните правой кнопкой мыши объект и выберите команду **Копировать**, а затем щелкните правой кнопкой мыши на панели запроса и выберите команду **Вставить**.|  
|**Функции**|Отображает метаданные для функций расширений интеллектуального анализа данных, доступных для базы данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , в том виде, в каком они получены из набора строк схемы DMSCHEMA_MINING_FUNCTIONS.<br /><br /> Чтобы получить синтаксис функции, выполните одно из следующих действий.<br /><br /> Перетащите объект из вкладки **Функции** на панель запроса.<br /><br /> или:<br /><br /> Щелкните правой кнопкой мыши функцию и выберите команду **Копировать**, затем щелкните правой кнопкой мыши на панели запроса и выберите команду **Вставить**.|  
|**Окно "Результаты"**|Отображает результаты инструкции расширений интеллектуального анализа данных в виде сетки.|  
|**Окно «сообщения»**|Отображает сведения о выполнении инструкции расширений интеллектуального анализа данных. Например, это окно отображает любые ошибки, обнаруженные в процессе выполнения, или число ячеек, полученных после выполнения.|  
  
## <a name="see-also"></a>См. также  
 [Конструкторы и диалоговые окна служб Analysis Services &#40;многомерных данных&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Справочник по расширениям интеллектуального анализа данных (расширения интеллектуального анализа данных)](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Редактор запросов многомерных Выражений &#40;службы Analysis Services — многомерные данные&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [Редактор запросов XMLA &#40;службы Analysis Services — многомерные данные&#41;](xmla-query-editor-analysis-services-multidimensional-data.md)   
 [Редакторы запросов и текста &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [SQL Server Management Studio сочетания клавиш](../ssms/sql-server-management-studio-keyboard-shortcuts.md)   
 [Настройка меню и сочетаний клавиш](../ssms/customize-menus-and-shortcut-keys.md)   
 [Выделение цветом в редакторах запросов](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
