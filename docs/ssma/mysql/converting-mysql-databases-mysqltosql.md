---
title: Преобразование баз данных MySQL (MySQLToSQL) | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1211a1d5f22758b5c3732aa1b9843fe11ef8b3db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63132293"
---
# <a name="converting-mysql-databases-mysqltosql"></a>Преобразование баз данных MySQL (MySQLToSQL)
После подключения к MySQL, подключенных к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или SQL Azure и задание проекта и параметры сопоставления данных, можно преобразовать объекты базы данных MySQL для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или объекты базы данных SQL Azure.  
  
## <a name="the-conversion-process"></a>Процесс преобразования  
Преобразование объектов базы данных принимает определения объектов из MySQL, преобразует их в аналогичные [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или SQL Azure объектов и затем загружает эту информацию в метаданные SSMA. Она не загружает данные в экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Затем можно просмотреть объекты и их свойства с помощью [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или обозреватель метаданных SQL Azure.  
  
Во время преобразования SSMA выводит сообщения об ошибках на панели списка ошибок и выходных сообщений в области вывода. Чтобы определить, есть ли у вас для изменения своих баз данных MySQL или процесс преобразования, чтобы получить результаты требуемое преобразование, используйте выходные данные и сведения об ошибке.  
  
## <a name="setting-conversion-options"></a>Установка параметров преобразования  
Прежде чем выполнять преобразование объектов, просмотрите параметры преобразования проекта в **параметры проекта** диалоговое окно. В этом диалоговом окне, можно задать как SSMA преобразует таблиц и индексов. Дополнительные сведения см. [параметры проекта &#40;преобразования&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>Результаты преобразования  
В следующей таблице показаны объекты MySQL преобразуются, в результате чего [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] объектов:  
  
|||  
|-|-|  
|**Объекты MySQL**|**Полученные объекты SQL Server**|  
|Таблицы с зависимых объектов, таких как индексы|SSMA создает таблицы с зависимые объекты. Таблица преобразуется с помощью всех индексов и ограничений. Индексы, преобразуются в отдельные [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] объектов.<br /><br />**Сопоставление типов пространственных данных** может выполняться только на уровне узла таблицы.<br /><br />Дополнительные сведения о параметрах преобразования таблицы, см. в разделе [параметры преобразования](conversion-settings-mysqltosql.md)|  
|Функции|Если функция может быть преобразован в Transact-SQL непосредственно, SSMA создает функцию. В некоторых случаях функции необходимо преобразовать в хранимую процедуру. Это можно сделать с помощью **преобразование функции** в параметрах проекта. В этом случае SSMA создает хранимую процедуру и функции, которая вызывает хранимую процедуру.<br /><br />**Учитывая варианты:**<br /><br />Преобразовать в соответствии с параметрами проекта<br /><br />Преобразование в функцию<br /><br />Преобразовать в хранимую процедуру<br /><br />Дополнительные сведения о параметрах функции преобразования, см. в разделе [параметры преобразования](conversion-settings-mysqltosql.md)|  
|Процедуры|Если процедура может быть преобразован в Transact-SQL непосредственно, SSMA создает хранимую процедуру. В некоторых случаях в автономных транзакций должен вызываться хранимой процедуры. В этом случае SSMA создает две хранимые процедуры: с реализацией, процедуры и другой, который используется для вызова реализации хранимой процедуры.|  
|Преобразование базы данных|Базы данных в качестве объектов MySQL не преобразуются непосредственно с SSMA для MySQL. Базы данных MySQL обрабатываются скорее как имена схем и все физические параметры будут потеряны во время преобразования. SSMA для MySQL использует [сопоставление баз данных MySQL со схемами SQL Server &#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) для сопоставления объектов из базы данных MySQL в соответствующие пары/схемы базы данных SQL Server.|  
|Преобразование триггера|**SSMA создает триггеры на основе следующих правил:**<br /><br />Прежде ЧЕМ триггеры преобразуются в триггерах INSTEAD OF T-SQL<br /><br />Триггеры AFTER, преобразуются в триггеры AFTER T-SQL с или без итераций на строки.|  
|Преобразование представления|SSMA создает представления с зависимых объектов|  
|Оператор преобразования|— Каждый объект инструкции SQL может содержать одну инструкцию MySQL (например, DDL, DML и прочих типов операторов) или BEGIN... КОНЕЧНЫЙ блок.<br />-   **Преобразование из нескольких инструкций: BEGIN... КОНЕЦ блока преобразования**инструкция SQL может также содержать BEGIN... КОНЕЧНЫЙ блок, например, в определении процедуры, функции или триггера. Эти блоки должны быть преобразованы так же, они преобразуются для отдельных объектов инструкции MySQL.|  
  
## <a name="converting-mysql-database-objects"></a>Преобразование объектов базы данных MySQL  
Для преобразования объектов базы данных MySQL, сначала выберите объекты, которые требуется преобразовать и затем имеют SSMA выполнить преобразование. Просмотр выходных сообщений во время преобразования, на **представление** меню, выберите **вывода**.  
  
**Для преобразования объектов MySQL в синтаксис SQL Server или SQL Azure**  
  
1.  В обозревателе метаданных MySQL, разверните узел сервера MySQL и раскройте **баз данных**.  
  
2.  Выберите объекты для преобразования:  
  
    -   Чтобы преобразовать все схемы, установите флажок рядом с полем **баз данных**.  
  
    -   Чтобы преобразовать или опустить базы данных, установите флажок рядом с именем базы данных.  
  
    -   Для преобразования или пропустить категории объектов, разверните схему и затем установите или снимите флажок рядом с категорией.  
  
    -   Чтобы преобразовать или исключить отдельные объекты, разверните папку «категория» и выберите или снимите флажок рядом с объектом.  
  
3.  Для преобразования всех выбранных объектов, щелкните правой кнопкой мыши **баз данных** и выберите **преобразования схемы**.  
  
    Можно также преобразовать отдельных объектов или категории объектов, щелкнув правой кнопкой мыши объект или ее родительскую папку, а затем выбрав **преобразования схемы**.  
  
## <a name="viewing-conversion-problems"></a>Просмотр проблемы с преобразованием  
Некоторые объекты MySQL не могут быть преобразованы. Успех конверсии можно определить, просмотрев отчет сводки преобразования.  
  
**Чтобы просмотреть сводный отчет**  
  
1.  В обозревателе метаданных MySQL выберите **баз данных**.  
  
2.  В области справа выберите **отчетов** вкладки.  
  
    Этот отчет показывает отчет об оценке сводки для всех объектов базы данных, оценивается ли или преобразованы. Можно также просмотреть сводный отчет по отдельным объектам:  
  
    -   Чтобы просмотреть отчет для отдельную схему, выберите базу данных в обозревателе метаданных MySQL.  
  
    -   Чтобы просмотреть отчет, для отдельного объекта, выберите объект в обозревателе метаданных MySQL. Объекты, имеющие проблемы с преобразованием иметь красный значок ошибки.  
  
Для объектов, которые не удалось выполнить преобразование можно просмотреть синтаксис, вызвавшую ошибку преобразования.  
  
**Для просмотра отдельных преобразования проблем**  
  
1.  В обозревателе метаданных MySQL разверните **баз данных**.  
  
2.  Разверните базу данных, показывающий красный значок ошибки.  
  
3.  В базе данных разверните папку с красным значком ошибки.  
  
4.  Выберите объект, который имеет красный значок ошибки.  
  
5.  В области справа щелкните **отчетов** вкладки.  
  
6.  В верхней части **отчетов** вкладка — стрелку раскрывающегося списка. Если в списке отображается **статистики**, выделение **источника**.  
  
    SSMA отобразит исходный код и несколько кнопок, расположенный непосредственно над кодом.  
  
7.  Нажмите кнопку **следующая проблема** кнопки. Это красный значок ошибки с стрелка, указывающая вправо.  
  
    SSMA будут выделите первый проблемных исходного кода, найденных в текущем объекте.  
  
Для каждого элемента, которые не могут быть преобразованы необходимо определить, что нужно сделать с помощью этого объекта:  
  
-   Можно изменить объект в базе данных MySQL, чтобы удалить или изменить неисправного кода. Чтобы загрузить обновленный код в SSMA, необходимо обновить метаданные. Дополнительные сведения см. в разделе [подключение к MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Объект можно исключить из миграции. В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или обозреватель метаданных SQL Azure и обозреватель метаданных MySQL, снимите флажок рядом с элементом перед загрузкой объектов в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или SQL Azure, так и перенос данных из MySQL.  
  
## <a name="next-step"></a>Следующий шаг  
Следующим шагом в процессе миграции является [загрузка преобразовать объекты базы данных в SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>См. также  
[Миграция MySQL базы данных в SQL Server — база данных Azure SQL &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
