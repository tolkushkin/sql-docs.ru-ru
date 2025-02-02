---
title: Создать код для задачи по структурированию данных
titleSuffix: Azure Data Studio
description: В этой статье описывается использование сочетаний клавиш кода PROSE студии данных Azure для автоматического создания кода для распространенные задачи по структурированию данных.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f5406ce0e67322a8f7148fc83b83d0789f27e1ae
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770779"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>С помощью ускорителя кода PROSE Wrangling данных

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

PROSE Accelerator кода приводит к возникновению ошибки удобочитаемый код Python для вашей задачи по структурированию данных. При работе в записной книжке в Azure Data Studio можно смешивать созданный код с кодом рукописных простым способом. Статья содержит общие сведения о том, как можно использовать код ускорителя.

 > [!NOTE]
 > Программирование Synthesis using Examples, также называемые ПРОЗОЙ, — это технология Майкрософт, которая создает понятное код, с помощью искусственного Интеллекта. Это достигается путем анализа пользователя намерение а также данные, создание нескольких кандидатов программ и выбора наиболее подходящей программы с помощью алгоритмов ранжирования. Чтобы получить дополнительные сведения о технологии ПРОЗОЙ, посетите [Домашняя страница PROSE](https://microsoft.github.io/prose/).

Сочетания клавиш код поставляется предварительно установленным с помощью Azure Data Studio. Вы можете импортировать как и любой другой пакет Python в записной книжке. По соглашению мы импортируйте его как cx для краткости.

```python
import prose.codeaccelerator as cx
```

В текущем выпуске Accelerator код может интеллектуально генерировать код Python для выполнения следующих задач:

- Чтения файлов данных Pandas или кадр данных Pyspark.
- Исправление типов данных в кадр данных.
- Поиск регулярных выражений, представляющих собой шаблоны в список строк.

Чтобы получить общие сведения о методы код ускорителя, см. в разделе [документации](https://aka.ms/prose-codeaccelerator-overview).

## <a name="reading-data-from-a-file-to-a-dataframe"></a>Чтение данных из файла в кадр данных

Часто чтение файлов в кадр данных включает в себя обращения к содержимому файла и определить правильные параметры для передачи в библиотеку загрузки данных. В зависимости от сложности файл определяющий правильные параметры может потребоваться несколько итераций.

PROSE код ускорителя решает эту проблему путем анализа структура файла данных и автоматическим созданием кода для загрузки файла. В большинстве случаев созданный код правильно анализирует данные. В некоторых случаях может потребоваться изменить код в соответствии с требованиями.

Рассмотрим следующий пример.

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

Предыдущий блок кода выводит следующий код python для чтения файла с разделителями. Обратите внимание на то, каким образом PROSE автоматически определяет число строк, которые необходимо пропустить, заголовки, quotechars, разделители и т. д.

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

Ускоритель кода может создавать код для загрузки с разделителями, JSON и файлов с фиксированной шириной в кадр данных. Для чтения файлов с фиксированной шириной `ReadFwfBuilder` при необходимости принимает понятное схемы файла, его можно проанализировать для получения позиции столбца. Дополнительные сведения см. в разделе [документации](https://aka.ms/prose-codeaccelerator-docs).

## <a name="fixing-data-types-in-a-dataframe"></a>Устранение типы данных в кадр данных

Это часто используются pandas или pyspark кадр данных с типами данных. Часто это происходит из-за несколько несоответствующих значений в столбце. Таким образом как число с плавающей запятой или строки считываются целых чисел и дат считываются в виде строк. Затрачиваемые усилия, чтобы вручную исправить типы данных пропорционально числу столбцов.

Можно использовать `DetectTypesBuilder` в таких ситуациях. Он анализирует данные, и вместо того, чтобы исправлять типы данных в виде черного прямоугольника, он создает код для исправления типов данных. Код служит в качестве отправной точки. Можно просмотреть, использовать и измените нужным образом.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

Дополнительные сведения см. в разделе [документации](https://aka.ms/prose-codeaccelerator-fixtypes).

## <a name="identifying-patterns-in-strings"></a>Определение шаблонов в строках

Другим распространенным сценарием является для обнаружения закономерностей в строковый столбец для очистки и группирования. Например возможно столбец даты с датами в нескольких различных форматах. Чтобы стандартизировать значения, может потребоваться написать условные инструкции, с помощью регулярных выражений.


|   |Имя                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Неизвестно        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22 апреля 67      |
| 4 |Maya de Villiers          |19 – мар-60      |

В зависимости от объема и разнообразия в данных написание регулярных выражений для различных шаблонов в столбце может быть очень длительной задачи. `FindPatternsBuilder` — Это средство ускорения эффективные кода, предназначенных для решения этой проблемы путем создания регулярных выражений для получения списка строк.

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

Ниже приведены регулярные выражения, созданные `FindPatternsBuilder` для вышеуказанных данных.

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

Помимо создания регулярных выражений `FindPatternsBuilder` можно также создать код для кластеризации значения, основываясь на созданного регулярные выражения. Он может также подтвердить, что все значения в столбце соответствуют созданный регулярные выражения. Дополнительные сведения и другие полезные сценарии см. в разделе, см. в разделе [документации](https://aka.ms/prose-codeaccelerator-findpatterns).
