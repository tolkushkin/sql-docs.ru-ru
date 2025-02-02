---
title: Панель SQL (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], SQL pane
- View Designer, SQL pane
- SQL pane [Visual Database Tools]
ms.assetid: dbabab18-0614-415b-a2ef-9bcd0d320d5c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 89c1d77d7c231b96381d8a2f9f9edb70f02b08a5
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105620"
---
# <a name="sql-pane-visual-database-tools"></a>Панель SQL (визуальные инструменты для баз данных)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Панель SQL можно использовать для создания собственных инструкций SQL; можно также создать инструкцию на панели критериев или панели диаграмм, и на панели SQL будут созданы инструкции SQL. После того как запрос построен, панель SQL его автоматически обновляет и меняет его формат для удобства чтения.  
  
Чтобы открыть панель SQL, сначала откройте конструктор запросов и представлений (с объектом базы данных, выбранным в обозревателе серверов в меню **База данных** , выберите пункт **Создать запрос**). Затем в меню **Конструктор запросов** укажите пункт **Панель** и щелкните элемент **SQL**.  
  
На панели SQL можно:  
  
-   создать новые запросы с помощью ввода инструкций SQL;  
  
-   изменить инструкцию SQL, созданную конструктором запросов и представлений, на основании собственных параметров на панелях диаграмм и критериев;  
  
-   ввести инструкции, которые пользуются преимуществами функций, характерных для использующейся базы данных.  
  
> [!NOTE]  
> Убедитесь, что известны правила идентификации объектов в использующейся базе данных. Подробные сведения см. в документации по системе управления базой данных.  
  
## <a name="statements-in-the-sql-pane"></a>Инструкции на панели SQL  
Текущий запрос можно редактировать непосредственно на панели SQL. При переходе на другую панель конструктор запросов и представлений автоматически форматирует инструкцию и затем изменяет панели диаграмм и критериев для соответствия этой инструкции.  
  
Если инструкция не может быть представлена на панелях диаграмм и критериев, учитывая, что эти панели видимы, конструктор запросов и представлений выводит ошибку и предлагает два выхода:  
  
-   не учитывать невозможность представления инструкции на панелях диаграмм и критериев;  
  
-   отменить изменения, которые не могут быть представлены, и восстановить до недавней версии инструкции SQL.  
  
Если не учитывается невозможность представления инструкции на панелях диаграмм и критериев, конструктор запросов и представлений затемняет другие панели, чтобы показать, что они больше не отражают содержимое панели SQL.  
  
Можно продолжить изменение и выполнение инструкции, также как и других инструкций SQL.  
  
> [!NOTE]  
> Если была введена инструкция SQL, но потом были внесены изменения в запрос, с изменением панелей диаграмм и критериев, конструктор запросов и представлений перестроит и заново отобразит инструкцию SQL. В некоторых случаях это приводит к тому, что инструкция SQL строится отлично от той, которая была введена изначально (хотя результат получится одинаковый). Эта разница особенно возможна, если ведется работа с условиями поиска, содержащими несколько предложений, связанных AND и OR.  
  
## <a name="see-also"></a>См. также:  
[Создание запросов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[Выполнение запросов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Разделы по конструированию запросов и представлений (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Панель диаграммы (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[Панель критериев (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[Панель результатов (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
  
