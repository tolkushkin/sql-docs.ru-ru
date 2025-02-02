---
title: Определение именованных вычислений в представлении источника данных (службы Analysis Services) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying named calculations
- data source views [Analysis Services], named calculations
- named calculations [Analysis Services]
ms.assetid: 729e7b12-6185-4b73-8bcb-cfe459b15355
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a69d5194c6eea3bc81676e8c0c3b1cac1d06270c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075567"
---
# <a name="define-named-calculations-in-a-data-source-view-analysis-services"></a>Определение именованных вычислений в представлении источника данных (службы Analysis Services)
  Именованное вычисление является выражением SQL, представленным в виде вычисляемого столбца. Данное выражение выглядит и работает как столбец таблицы. Именованное вычисление позволяет расширить реляционную схему таблиц или представлений, существующих в представлении источника данных, не изменяя таблицы или представления в базовом источнике данных. Рассмотрим следующие примеры:  
  
-   Создайте одно именованное вычисление, получаемое из нескольких столбцов таблицы фактов (например, вычисление суммы налога путем умножения налоговой ставки на стоимость продажи).  
  
-   Составьте для элемента измерения понятное имя.  
  
-   Для повышения производительности запросов создайте именованное вычисление в представлении источника данных вместо создания вычисляемого элемента в кубе. Именованные вычисления рассчитываются в процессе обработки, тогда как вычисляемые элементы рассчитываются во время запроса.  
  
## <a name="creating-named-calculations"></a>Создание именованных вычислений  
  
> [!NOTE]  
>  Именованное вычисление нельзя добавить в именованный запрос, а именованный запрос не может быть основан на таблице, которая содержит именованное вычисление.  
  
 При создании именованного вычисления указывается имя, выражение SQL и (необязательно) описание вычисления. Выражение SQL может ссылаться на другие таблицы в представлении источника данных. После определения именованного вычисления выражение в именованном вычислении отправляется поставщику источника данных и проверяется в виде указанной ниже инструкции SQL, в которой `<Expression>` содержит выражение, определяющее именованное вычисление.  
  
```  
SELECT   
   <Table Name in Data Source>.*,   
   <Expression> AS <Column Name>   
FROM   
   <Table Name in Data Source> AS <Table Name in Data Source View>  
```  
  
 Тип данных столбца определяется типом данных скалярного значения, возвращенного выражением. Если поставщик не обнаружит каких-либо ошибок в выражении, то столбец будет добавлен к таблице.  
  
 Столбцы, указанные в выражении, не должны иметь квалификатора вовсе или должны иметь только такой квалификатор, который соответствует имени таблицы. Например, для ссылки на столбец SaleAmount в таблице можно использовать `SaleAmount` или `Sales.SaleAmount` , но `dbo.Sales.SaleAmount` возвращает ошибку.  
  
 Выражение не заключается автоматически в скобки. Следовательно, если выражение, например инструкцию SELECT, необходимо заключить в скобки, то необходимо ввести скобки в поле **Выражение** . Например, следующее выражение допустимо только при наличии скобок.  
  
```  
(SELECT Description FROM Categories WHERE Categories.CategoryID = CategoryID)  
```  
  
## <a name="add-or-edit-a-named-calculation"></a>Добавление или изменение именованного вычисления  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект или подключитесь к базе данных, содержащей представление источника данных, в котором необходимо определить именованное вычисление.  
  
2.  В обозревателе решений откройте папку **Представления источников данных** и дважды щелкните представление источника данных.  
  
3.  На панели **Таблицы** или на панели **Диаграмма** щелкните правой кнопкой мыши таблицу, в которой необходимо определить именованное вычисление, и выберите пункт **Создать именованное вычисление**. Правой кнопкой мыши щелкните имя таблицы, но не атрибут. Меню должно иметь следующий вид.  
  
     ![Снимок экрана: рабочее пространство диаграммы, щелкните правой кнопкой мыши меню](../media/ssas-olapdsv-diagram.gif "снимок экрана: рабочее пространство диаграммы, щелкните правой кнопкой мыши меню")  
  
    > [!NOTE]  
    >  Чтобы найти таблицу или представление, можно использовать команду **Поиск таблицы** , выбрав меню **Представление источника данных** или щелкнув правой кнопкой мыши рабочую область панели **Таблицы** или панели **Диаграмма** .  
  
4.  В диалоговом окне **Создание именованных вычислений** выполните следующие действия:  
  
    -   В текстовом поле **Имя столбца** введите имя нового столбца.  
  
    -   В текстовом поле **Описание** введите описание нового столбца.  
  
    -   В текстовом поле **Выражение** введите выражение, которое возвращает содержимое нового столбца на приемлемой для поставщика данных разновидности языка SQL.  
  
5.  Нажмите кнопку **ОК**.  
  
     Столбец именованного вычисления появится как последний столбец в таблице представления источников данных. Значок калькулятора указывает на то, что столбец содержит именованное вычисление.  
  
## <a name="delete-a-named-calculation"></a>Удаление именованного вычисления  
 При попытке удалить именованное вычисление приложение выдаст список объектов, определенных в проекте или базе данных, которые при удалении станут недействительными. Внимательно просмотрите список перед удалением вычисления.  
  
## <a name="see-also"></a>См. также  
 [Определение именованных запросов в представлении источника данных (службы Analysis Services)](define-named-queries-in-a-data-source-view-analysis-services.md)  
  
  
