---
title: Окно "Список ошибок" (среда Management Studio) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- error list window
- SQL Server Management Studio [SQL Server], error list window
ms.assetid: fae6327d-e268-44ae-a474-4a8f8f843129
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f7649875faf636d2bbc78834c13d4b5b1b99e72
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063434"
---
# <a name="error-list-window-management-studio"></a>Окно «Список ошибок» (среда Management Studio)
   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **среды** отображает синтаксические и семантические ошибки, сформированные из кода технологии IntelliSense в редакторе запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="features-of-the-error-list"></a>Функции списка ошибок  
 **Список ошибок** обеспечивает следующую функциональность.  
  
-   В процессе изменения скриптов **Список ошибок** отображает ошибки и предупреждения, формируемые технологией IntelliSense в редакторе запросов [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
-   Можно дважды щелкнуть на любом сообщении об ошибке на вкладке для файла скрипта, который формирует ошибку, и перейти к месту нахождения ошибки.  
  
-   Можно фильтровать отображаемые элементы и столбцы данных, которые будут показаны в каждом элементе.  
  
-   После устранения ошибки ошибочный элемент удаляется из **Списка ошибок**.  
  
-   После того как вкладка для файла скрипта [!INCLUDE[tsql](../../includes/tsql-md.md)] будет закрыта, ошибки для этого файла удаляются из **Списка ошибок**.  
  
## <a name="working-with-the-error-list"></a>Работа со списком ошибок  
 Для показа **Списка ошибок**сделайте следующее.  
  
-   В меню **Вид** выберите пункт **Список ошибок**.  
  
-   Нажмите клавиши CTRL+\\, CTRL+E.  
  
 Открыв **Список ошибок**, можно настроить представление, выполнив следующие действия.  
  
-   Для сортировки списка выберите любой заголовок столбца. Для повторной сортировки по дополнительному столбцу нажмите и удерживайте клавишу SHIFT, а затем выберите другой заголовок столбца.  
  
-   Чтобы выбрать отображаемые и скрываемые столбцы, выберите команду **Показать столбцы** из контекстного меню.  
  
-   Чтобы изменить порядок, в котором отображаются столбцы, перетащите любой заголовок столбца влево или вправо.  
  
 **Список ошибок** не содержит ссылок на дополнительные сведения о конкретных ошибках.  
  
## <a name="transact-sql-errors-in-management-studio"></a>Ошибки Transact-SQL в среде Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] отображает ошибки скриптов [!INCLUDE[tsql](../../includes/tsql-md.md)] в следующих местах.  
  
-   **Список ошибок** отображает все синтаксические и семантические ошибки, обнаруженные технологией IntelliSense в редакторе [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Этот список ошибок динамически обновляется по мере изменения скриптов [!INCLUDE[tsql](../../includes/tsql-md.md)] . В список входят все ошибки, обнаруженные редактором в каждом скрипте [!INCLUDE[tsql](../../includes/tsql-md.md)] . Редактор не прекращает разбор файла после обнаружения ошибок в скрипте. В [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]технология IntelliSense в редакторе [!INCLUDE[ssDE](../../includes/ssde-md.md)] не поддерживает все синтаксические элементы [!INCLUDE[tsql](../../includes/tsql-md.md)] . **Список ошибок** содержит только ошибки синтаксиса [!INCLUDE[tsql](../../includes/tsql-md.md)] , поддерживаемого технологией IntelliSense.  
  
-   Вкладка **Сообщения** в нижней части окна редактора запросов [!INCLUDE[ssDE](../../includes/ssde-md.md)] отображает все ошибки и сообщения, возвращаемые компонентом [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] при выполнении скрипта [!INCLUDE[tsql](../../includes/tsql-md.md)] . Список не изменяется до тех пор, пока скрипт не будет выполнен повторно. Компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] прекращает разбор пакета после того, как обнаруживает одну или две ошибки компиляции, поэтому на вкладке **Сообщения** могут быть перечислены не все ошибки в скрипте.  
  
 Иногда ошибки приводятся в обоих местах. Например, файл скрипта может содержать синтаксическую ошибку, которая приводится в **Списке ошибок**. Если выполнить скрипт, прежде чем будет исправлена ошибка, средство синтаксического анализа компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] может обнаружить такое же состояние и показать такое же сообщение об ошибке на вкладке **Сообщения** .  
  
> [!NOTE]  
>  **Список ошибок** содержит только ошибки из редактора запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] . В него не включаются ошибки из редакторов многомерных выражений, расширений интеллектуального анализа данных и XML/A. Все ошибки многомерных выражений, расширений интеллектуального анализа данных и XML/A выводятся на вкладке **Сообщения** в соответствующих редакторах.  
  
## <a name="uielement-list"></a>Список элементов пользовательского интерфейса  
 Если **Список ошибок** открыт, сведения отображаются в следующих столбцах.  
  
 **Порядок по умолчанию**  
 Отображает целочисленное значение, которое указывает порядковый номер создания элемента.  
  
 **Описание**  
 Отображает текст элемента ошибки. Длинные описания переносятся на дополнительные строки.  
  
 **Файл**  
 Отображает имя файла скрипта, сформировавшего ошибку.  
  
 **Линия**  
 Отображает целочисленное значение, которое указывает строку кода, в котором содержится ошибка.  
  
 **Столбец**  
 Отображает целочисленное значение, которое указывает положение ошибки в строке кода.  
  
 **Проект**  
 Отображает имя проекта, в который входит файл скрипта.  
