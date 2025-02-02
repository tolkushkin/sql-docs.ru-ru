---
title: Параметры (преобразование) (MySQLToSQL) проекта | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 12e2e61c6b55bf3c549c08f2b090059d674ed83d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162025"
---
# <a name="project-settings-conversion-mysqltosql"></a>Параметры проекта (преобразование) (MySQLToSQL)
На странице преобразования **параметры проекта** диалоговое окно содержит настройки, установленные как SSMA преобразует синтаксис MySQL в синтаксис SQL Server или SQL Azure.  
  
Область преобразования доступна в **параметры проекта** и **параметры проекта по умолчанию** диалоговым окнам.  
  
-   Используйте **параметры проекта по умолчанию** диалоговое окно, чтобы задать параметры конфигурации для всех проектов. Чтобы открыть параметры преобразования, в **средства** меню, выберите **параметры проекта по умолчанию**, выберите тип проекта миграции, для которого требуются параметры просмотра или изменения из  **Целевой версии миграции** раскрывающийся список, нажмите кнопку **Общие** в нижней части левой панели, а затем выберите **преобразования**.  
  
-   Для задания параметров для текущего проекта на **средства** меню **параметры проекта**, нажмите кнопку **Общие** в нижней части левой панели и нажмите кнопку **Преобразование**.  
  
## <a name="options"></a>Параметры  
  
### <a name="collate-clause"></a>Предложение COLLATE  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**Явное преобразование предложение COLLATE**|Явные параметр преобразования предложение COLLATE способы преобразования явного предложения COLLATE в коде MySQL. Возможные варианты: Игнорировать и пометить предупреждение / выдает ошибку<br /><br />**Режим по умолчанию**:  Игнорировать и знак с предупреждением<br /><br />**Режим оптимистичного**:  Игнорировать и знак с предупреждением<br /><br />**Полный режим**:  Игнорировать и знак с предупреждением|  
  
### <a name="column-constraints"></a>Ограничения столбца  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**Создать ограничение для столбцов типа данных Перечисления**|Создает ограничение для столбцов типа данных Перечисления в таблице SQL Server или SQL Azure, если она отсутствует в таблице MySQL. Если Да, все преобразованные столбцы типа данных Перечисления будет сопровождаться ПРОВЕРОЧНОГО ограничения, управления значением.<br /><br />**Режим по умолчанию**:   Нет<br /><br />**Режим оптимистичного**:  Нет<br /><br />**Полный режим**:   Да|  
|**Создать ограничение для столбцов типа НАБОРА данных**|Создает ограничение для столбцов типа НАБОРА данных в таблице SQL Server или SQL Azure, если она отсутствует в таблице MySQL. Если Да, все столбцы преобразованный НАБОР данных типа будет сопровождаться ПРОВЕРОЧНОГО ограничения, управления значением.<br /><br />**Режим по умолчанию**:   Нет<br /><br />**Режим оптимистичного**:  Нет<br /><br />**Полный режим**:   Да|  
|**Создать ограничение для столбцов, содержащих столбцы типа без знака числовые данные**|Добавление проверки для неотрицательное значение для столбцов типов без знака числовых данных.<br /><br />**Режим по умолчанию**:   Нет<br /><br />**Режим оптимистичного**:  Нет<br /><br />**Полный режим**:   Да|  
|**Создать ограничение для столбцов типов данных за год**|Создает ограничение для столбцов типа данных года в таблице SQL Server или SQL Azure, если она отсутствует в таблице MySQL. Если Да, все преобразованы столбцы данных год тип будет сопровождаться ПРОВЕРОЧНОГО ограничения, управления значением.<br /><br />**Режим по умолчанию**:   Нет<br /><br />**Режим оптимистичного**:  Нет<br /><br />**Полный режим**:   Да|  
  
### <a name="data-types"></a>Типы данных  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**Преобразование типов Перечисления**|Указывает, как следует преобразовать тип данных Перечисления MySQL как преобразовать в NVARCHAR или преобразовать в числовые<br /><br />**Режим по умолчанию**:  Преобразование в NVARCHAR<br /><br />**Режим оптимистичного**:  Преобразование в NVARCHAR<br /><br />**Полный режим**:  Преобразование в NVARCHAR|  
|**Преобразование типа НАБОРА данных**|Указывает, как УСТАНОВИТЬ MySQL должен быть преобразован, преобразуйте NVARCHAR (L) / преобразовать BINARY(L)<br /><br />**Режим по умолчанию**: Преобразовать в NVARCHAR(L)<br /><br />**Режим оптимистичного**: Преобразовать в NVARCHAR(L)<br /><br />**Полный режим**: Преобразовать в NVARCHAR(L)|  
  
### <a name="generic"></a>Универсальный  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**Столбцы без значения по умолчанию в вставки и ЗАМЕНЫ**|Если «Да», все инструкции, ссылающиеся на таблицы, с помощью хранимых модулей, кроме MyISAM и InnoDb должны быть помечены преобразования предупреждающие сообщения.<br /><br />**Режим по умолчанию**:  Добавьте список столбцов<br /><br />**Режим оптимистичного**:  Добавьте список столбцов<br /><br />**Полный режим**:   Добавьте список столбцов|  
|**Деление на ноль преобразование создает**|Указывает, следует ли эмулировать MySQL без ERROR_FOR_DIVISION_BY_ZERO поведение.<br /><br />**Режим по умолчанию**:   Ошибка<br /><br />**Режим оптимистичного**:  Ошибка<br /><br />**Полный режим**:   NULL|  
|**Оператор IN**|Указывает, как преобразовать оператор MySQL IN.<br /><br />**Режим по умолчанию**:   Всегда преобразуются в<br /><br />**Режим оптимистичного**:  Всегда преобразуются в<br /><br />**Полный режим**:   При необходимости разверните|  
|**Преобразование функции MySQL**|Указывает, как преобразовать стандартные функции MySQL.<br /><br />**Режим по умолчанию**:   Optimistic<br /><br />**Режим оптимистичного**:  Optimistic<br /><br />**Полный режим**:   Точный|  
|**Не поддерживается подсистемы хранилища**|Если «Да», все инструкции, ссылающиеся на таблицы, с помощью хранимых модулей, кроме MyISAM и InnoDb должны быть помечены преобразования предупреждающие сообщения.<br /><br />**Режим по умолчанию**:   Нет<br /><br />**Режим оптимистичного**:  Нет<br /><br />**Полный режим**:   Да|  
|**Отключить создание ROWID дополнительный столбец**|Если Да, запрещает создание ROWD создания дополнительный столбец в целевых таблицах. Могут возникнуть при миграции некоторых структур.<br /><br />**Режим по умолчанию**:   Нет<br /><br />**Режим оптимистичного**:  Нет<br /><br />**Полный режим**:   Нет|  
|**Инструкция TRUNCATE преобразования**|Указывает, как преобразовать инструкциями УСЕЧЕНИЯ.<br /><br />**Режим по умолчанию**:   TRUNCATE<br /><br />**Режим оптимистичного**:  TRUNCATE<br /><br />**Полный режим**:   TRUNCATE|  
  
### <a name="misc"></a>Разное  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**Сопоставление схемы по умолчанию**|Указывает способ сопоставления баз данных MySQL в схемы SQL Server.<br /><br />**Режим по умолчанию**:  В базу данных<br /><br />**Режим оптимистичного**:  В базу данных<br /><br />**Полный режим**:  В базу данных|  
  
### <a name="procedures-and-functions"></a>Процедуры и функции  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**Функция преобразования по умолчанию**|Указывает, если функции должны быть по умолчанию преобразоваться функций T-SQL или хранимые процедуры.<br /><br />**Режим по умолчанию**:  Преобразование в функцию<br /><br />**Режим оптимистичного**:  Преобразование в функцию<br /><br />**Полный режим**:  Преобразование в функцию|  
|**Создать инструкция SET XACT_ABORT на**|Указывает, должна ли добавляться в начало преобразованный процедуры или триггера SET XACT_ABORT ON.<br /><br />**Режим по умолчанию**:  Да<br /><br />**Режим оптимистичного**:  Да<br /><br />**Полный режим**:  Да|  
|**Создание SET NOCOUNT о**|Указывает, должна ли добавляться в начало преобразованный процедуры или триггера SET NOCOUNT ON.<br /><br />**Режим по умолчанию**:  Да<br /><br />**Режим оптимистичного**:  Да<br /><br />**Полный режим**:  Да|  
  
### <a name="spatial-data-types"></a>Типы пространственных данных  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**По умолчанию, ограничивающий прямоугольник {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} для пространственных индексов**|Определяет значение по умолчанию для {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} параметр ограничивающий прямоугольник, используемые в пространственных индексах.<br /><br />**Режим по умолчанию**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Режим оптимистичного**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX:  100<br /><br />YMIN: 0<br /><br />**Полный режим**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0|  
|**Плотность сетки для пространственных индексов**|Определяет значение по умолчанию для LEVEL_1, LEVEL_2, LEVEL_3 и LEVEL_4 плотности сетки, используемых в пространственных индексах.<br /><br />**Режим по умолчанию**<br /><br />LEVEL_1: Значение по умолчанию<br /><br />LEVEL_2: Значение по умолчанию<br /><br />LEVEL_3: Значение по умолчанию<br /><br />LEVEL_4: Значение по умолчанию<br /><br />**Режим оптимистичного**<br /><br />LEVEL_1: Значение по умолчанию<br /><br />LEVEL_2: Значение по умолчанию<br /><br />LEVEL_3: Значение по умолчанию<br /><br />LEVEL_4: Значение по умолчанию<br /><br />**Полный режим**<br /><br />LEVEL_1: Значение по умолчанию<br /><br />LEVEL_2: Значение по умолчанию<br /><br />LEVEL_3: Значение по умолчанию<br /><br />LEVEL_4: Значение по умолчанию|  
  
### <a name="transactions"></a>Transactions  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**Нетранзакционный таблиц**|Указывает ли все ссылки на таблицы, которые не поддерживают транзакции должны быть помечены преобразования предупреждающие сообщения.<br /><br />**Режим по умолчанию**: Нет<br /><br />**Режим оптимистичного**: Нет<br /><br />**Полный режим**: Да|  
|**уровень изоляции транзакции**|Указывает, какой уровень изоляции транзакции должен использоваться для новых транзакций.<br /><br />**Режим по умолчанию**:   Значение по умолчанию<br /><br />**Режим оптимистичного**:  Значение по умолчанию<br /><br />**Полный режим**:   Уровень изоляции repeatable read|  
  
### <a name="value-control"></a>Значение элемента управления  
  
|||  
|-|-|  
|**Термин**|**Определение**|  
|**Символ, который числовое преобразование**|Указывает способ обработки явное и неявное преобразование из символьного типа данных в числовые типы данных.<br /><br />**Режим по умолчанию**:   Optimistic<br /><br />**Режим оптимистичного**:  Optimistic<br /><br />**Полный режим**:   Точный|  
|**Без знака числового значения элемента управления**|Элемент управления, присвоение значений без знака числовых переменных и параметров.<br /><br />**Режим по умолчанию**:   Нет<br /><br />**Режим оптимистичного**:  Нет<br /><br />**Полный режим**:   Да|  
|**Элемент управления без знака вычитания**|Измените отрицательных значениях, вставляемых в столбцы таблицы без знака типа данных.<br /><br />**Режим по умолчанию**:   Преобразование "как-является"<br /><br />**Режим оптимистичного**:  Преобразование "как-является"<br /><br />**Полный режим**:   Пометить предупреждение|  
|**Преобразование из типа двоичных данных**|Указывает способ обработки явное и неявное преобразование из типа двоичных данных.<br /><br />**Режим по умолчанию**:   Optimistic<br /><br />**Режим оптимистичного**:  Optimistic<br /><br />**Полный режим**:   Точный|  
|**Преобразование в тип данных даты и времени**|Указывает о том, как обрабатывать неявные и явные преобразования в даты и времени типа данных.<br /><br />**Режим по умолчанию**:   Эмуляция формат MySQL<br /><br />**Режим оптимистичного**:  Использование формата SQL Server<br /><br />**Полный режим**:   Эмуляция формат MySQL|  
|**Числовые литералы с точностью 38 превышение**|Указывает, как преобразовать числовые литералы с точностью 38 превышение.<br /><br />**Режим по умолчанию**:   Если это возможно округления<br /><br />**Режим оптимистичного**:  Если это возможно округления<br /><br />**Полный режим**:   Если это возможно округления|  
|**Ноль date в не столбцов со значением NULL**|Указывает способ обработки назначения не NULL столбцов ноль-Date, ноль по дате или недопустимые даты и времени значения.<br /><br />**Режим по умолчанию**:   GETDATE()<br /><br />**Режим оптимистичного**:  GETDATE()<br /><br />**Полный режим**:   GETDATE()|  
  
## <a name="see-also"></a>См. также  
[Справочник по пользовательскому интерфейсу &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
