---
title: Как использовать записные книжки SQL в Azure Data Studio
titleSuffix: Azure Data Studio
description: Узнайте, как использовать записные книжки SQL в Azure Data Studio
ms.custom: seodec18
ms.date: 03/17/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 6ac15dcd6b440a8c3bcca0c468a79548469fe059
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798041"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Использование записных книжек в Azure Data Studio

В этой статье описывается, как запускать записные книжки в студии данных Azure и как начать создание собственных записных книжек. Также демонстрируется запись всех записных книжек, с помощью разных ядер.


## <a name="connect-to-sql-server"></a>Подключение к SQL Server

Вы можете подключиться к тип соединения Microsoft SQL Server в Azure Data Studio.
В Azure Data Studio, можно также нажать клавишу F1 и нажмите кнопку **новое подключение** и подключитесь к серверу SQL Server.

![изображение 1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>Запуск записных книжек

Существует несколько способов, чтобы запустить записную книжку.

1. Перейдите к **меню "файл"** в Azure Data Studio, а затем щелкните **новой записной книжки**.

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. Щелкните правой кнопкой мыши **SQL Server** подключения, а затем запустить **новой записной книжки**. 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. Откройте палитру команд (**Ctrl + Shift + P**)) и введите в **новой записной книжки**. Новый файл с именем `Notebook-1.ipynb` открывается.

## <a name="supported-kernels-and-attach-to-context"></a>Поддерживаемые версии ядра и присоединить к контексту

Установка записной книжки в Azure Data Studio изначально поддерживает ядра SQL. Если вы являетесь разработчиком SQL и хотели бы использовать записные книжки, то это будет выбранного ядра. 

Ядро SQL также может использоваться для подключения к экземплярам сервера PostgreSQL. Если вы являетесь разработчиком PostgreSQL и хотите подключиться к серверу PostgreSQL, загрузите [ **расширения PostgreSQL** ](postgres-extension.md) в marketplace с расширениями Studio данных Azure.

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>Ядро SQL

В ячейки кода в записной книжке, аналогичную редактор запросов мы поддерживаем современные SQL, облегчающая повседневных задач с помощью встроенных функций, таких как полнофункциональный редактор SQL, IntelliSense и фрагменты кода, встроенные процесс создания кода. Фрагменты кода позволяют создавать правильный синтаксис SQL для создания базы данных, таблицы, представления, хранимые процедуры, и т.д. и обновлять существующие объекты базы данных. Использование фрагментов кода для быстрого создания копии базы данных для разработки и тестирования, а также создания и выполнения скриптов.

Нажмите кнопку **запуска** для выполнения каждой ячейки.

Ядро SQL для подключения к экземпляру SQL Server

![image7](media/sql-notebooks/intellisense-code-cell.png)

Результаты запроса

![Image19](media/sql-notebooks/sql-cell-results.png)

Ядро SQL для подключения к экземпляру сервера PostgreSQL 

![Image18](media/sql-notebooks/pgsql-code-cell.png)

Результаты запроса

![Image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Настройка Python для записных книжек

При выборе ядра, помимо SQL из раскрывающегося списка ядра это предложит **Настройка Python для записных книжек**. Зависимости записной книжки, устанавливаются в указанном расположении, но можно решить, будет ли указать место установки. Эта установка может занять некоторое время, и мы рекомендуем не закрывать приложения до завершения установки. После завершения установки можно запустить, написание кода на поддерживаемых языках.

![Image21](media/sql-notebooks/configure-python.png)

После успешной установки вы увидите уведомление в журнале задания, а также расположение внутреннего сервера Jupyter, выполнив в окне терминала выходных данных.

![Image22](media/sql-notebooks/jupyter-backend.png)

|Ядра|Описание
|:-----|:-----
| Ядро SQL | Напишите код SQL, предназначенные для реляционной базы данных.
|PySpark3 и ядро PySpark| Пишите код Python, используя Spark вычислений из кластера.
|Ядро Spark|Напишите код для Scala и R с помощью Spark вычислений из кластера.
|Ядро Python|Напишите код Python для локальной разработки.

`Attach to` предоставляет контекст для ядра для присоединения. Если вы используете ядро SQL, то вы можете `Attach to` любой из экземпляров SQL Server.

Если вы используете ядро Python3 `Attach to` является `localhost`. Это ядро можно использовать для локальной разработки Python.

При подключении к кластеру больших данных SQL Server 2019, по умолчанию `Attach to` является конечной точки кластера и позволит вам отправить код Python, Scala и R, с помощью вычислений Spark кластера.

### <a name="code-cells-and-markdown-cells"></a>Код и ячейки Markdown

Добавьте новую ячейку кода, нажав кнопку **+ Code** команды на панели инструментов.

Добавьте новую ячейку текст, нажав кнопку **+ текст** команды на панели инструментов.

![image8](media/sql-notebooks/notebook-toolbar.png)

Изменения ячейки в режим редактирования и теперь введите markdown и вы увидите предварительной версии, в то же время

![image9](media/sql-notebooks/notebook-markdown-cell.png)

Щелкнув за пределами ячейки, текст будет показывать текст markdown.

![Image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>И не достоверный

Открыть в Studio данных Azure для записных книжек, по умолчанию **надежные**.

Если открыть записную книжку из другого источника, он будет открываться в **не доверенный** режиме, а затем сделать его **надежные**.

### <a name="save"></a>Сохранять 

Можно сохранить записную книжку, **Ctrl + S** или щелкнув **сохранения файла**, **файл "команды" Сохранить как...**  и **файл сохранить все** команды из меню "файл" и **файла: Сохранить** команд, введенных в палитре команд.

### <a name="pyspark3pyspark-kernel"></a>Ядро Pyspark3/PySpark

Выберите `PySpark Kernel` и в тип ячейки в следующем коде.

Нажмите кнопку **Запустить**.

Приложения Spark запускается и возвращает следующие выходные данные:

![Image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Ядро Spark | Язык Scala

Выберите `Spark|Scala Kernel` и в тип ячейки в следующем коде.

![Image13](media/sql-notebooks/spark-scala.png)

Вы также можете просмотреть «Параметры ячейки», при нажатии на значок "Параметры" ниже.

![Image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Ядро Spark | Язык R

Выберите Spark | R в раскрывающемся списке для ядра. В ячейке введите или вставьте в него код. Нажмите кнопку **запуска** чтобы увидеть следующие выходные данные.

![Image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>Локальное ядро Python

Выберите локальное ядро Python и в тип ячейки в -

![Image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>Управление пакетами
Одной из вещей, которые мы оптимизировали для локальной разработки Python было включают возможность установить пакеты, которые клиенты понадобится для своих сценариев. По умолчанию, мы включаем общие пакеты, такие как `pandas`, `numpy` и т.д., но если вы предполагаете, пакет, который не был включен затем написать следующий код в ячейку записной книжки: 

```python
import <package-name>
```

При выполнении этой команды `Module not found` возвращается. Если пакет существует, то не будет ошибка.

Если он возвращает `Module not Found` ошибки, а затем щелкните **управление пакетами** запуск терминал. Теперь можно установить пакеты локально. Чтобы установить пакеты, используйте следующие команды:

```bash
./pip install <package-name>
```

   > [!Tip]
   > На компьютере Mac выполните инструкции в окне терминала для установки пакетов. 

После установки пакета вы сможете перейдите в ячейку записной книжки и введите следующую команду:

```python
import <package-name>
```

Чтобы удалить пакет, используйте следующую команду из терминала:

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>Следующие шаги

Чтобы научиться работать с существующую записную книжку, см. в разделе [управление записных книжек в Azure Data Studio](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions).