---
title: Создание отчетов (OracleToSQL) | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Report Generation in Oracle Console, synchronize-target
- Report Generation in Oracle Console,refresh-from-database
- Report Generation in Oracle Console,write-summary-report-to
ms.assetid: ccad6262-01e1-447a-bd2b-c105154c80ce
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: a1f175de4b205b6af98ea9bcc29e7679711b0943
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192383"
---
# <a name="generating-reports-oracletosql"></a>Создание отчетов (OracleToSQL)
В консоли SSMA на уровне дерева объектов создаются отчеты определенных действий, выполняемых с помощью команд.  
  
Используйте следующую процедуру для создания отчетов:  
  
1.  Укажите **записи — Сводка отчет в** параметра. Связанный отчет хранится в виде имени файла (Если указано) или в папке вами. Имя файла — системы предопределенные как уже упоминалось в таблице ниже места расположения, **&lt;n&gt;** — номер уникального файла, которое увеличивается с цифрой при каждом выполнении той же команды.  
  
    Команды vis а по диагонали отчеты представлены ниже.  
  
    ||||  
    |-|-|-|  
    |**SL. Нет.**|**Command**|**Заголовок отчета**|  
    |1|Создание оценка отчета|AssessmentReport&lt;n&gt;. XML|  
    |2|преобразовать схему|SchemaConversionReport&lt;n&gt;. XML|  
    |3|Перенос данных|DataMigrationReport&lt;n&gt;. XML|  
    |4|sql инструкцию Convert|ConvertSQLReport&lt;n&gt;. XML|  
    |5|синхронизировать целевой объект|TargetSynchronizationReport&lt;n&gt;. XML|  
    |6|обновление из базы данных|SourceDBRefreshReport&lt;n&gt;. XML|  
  
    > [!IMPORTANT]  
    > В выходной отчет отличается от отчет об оценке. Первое из них является отчет о производительности во время выполнения команды, последний отчет в формате XML для программного использования.  
  
    Для параметров вывода отчетов за (Sl. Нет. 2 – 4 выше), см. [выполнение команд консоли SSMA &#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) раздел.  
  
2.  Укажите степень детализации в выходной отчет, используя параметры детализации отчета:  
  
    ||||  
    |-|-|-|  
    |**SL. Нет.**|**Команд и параметров**|**Описание выходных данных**|  
    |1|verbose="false"|Создает приведен сводный отчет действия.|  
    |2|verbose="true"|Создает отчет о состоянии сводные и подробные для каждого действия.|  
  
    > [!NOTE]  
    > Параметры детализации отчета, указанных выше применимы для формирования--отчет об оценке, convert схемы, перенос данных, команды sql инструкцию convert.  
  
3.  Указывает степень подробности, необходимые при работе в отчеты об ошибках, с помощью параметров отчетов об ошибках:  
  
    ||||  
    |-|-|-|  
    |**SL. Нет.**|**Команд и параметров**|**Описание выходных данных**|  
    |1|report-errors="false"|Нет сведений об ошибке / предупреждение / сообщения info.|  
    |2|report-errors="true"|Подробные сведения об ошибке / предупреждение / сообщения info.|  
  
    > [!NOTE]  
    > Параметры отчета об указанных выше применимы для формирования--отчет об оценке, convert схемы, перенос данных, команды sql инструкцию convert.  
  
**Пример.**  
  
```  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"/>  
```  
  
### <a name="synchronize-target"></a>синхронизировать target:  
Команда **синхронизировать целевой** имеет **отчета ошибки в** параметр, который указывает расположение отчет об ошибках для операции синхронизации. Затем файл с именем **TargetSynchronizationReport&lt;n&gt;. XML** создается в указанном месте, где **&lt;n&gt;** — номер уникального файла, которое увеличивается с цифрой при каждом выполнении той же команды.  
  
**Примечание.** Если указан путь к папке, параметр «отчета ошибки в» становится необязательный атрибут для «синхронизация — целевой объект команды».  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**Имя объекта:** Задает объекты для синхронизации (он также может иметь имена отдельных объектов или имя объекта группы).  
  
**в случае ошибки:** Указывает, следует ли для указания ошибок синхронизации в качестве предупреждения или ошибки. Доступные параметры для при ошибке:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Сбой скрипта  
  
### <a name="refresh-from-database"></a>обновления из-база данных:  
Команда **обновления из базы данных** имеет **отчета ошибки в** параметр, который указывает расположение отчет об ошибках для операции обновления. Затем файл с именем **SourceDBRefreshReport&lt;n&gt;. XML** создается в указанном месте, где **&lt;n&gt;** — номер уникального файла, которое увеличивается с цифрой при каждом выполнении той же команды.  
  
**Примечание.** Если указан путь к папке, параметр «отчета ошибки в» становится необязательный атрибут для «синхронизация — целевой объект команды».  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**Имя объекта:** Задает объекты для обновления (он также может иметь имена отдельных объектов или имя объекта группы).  
  
**в случае ошибки:** Указывает, следует ли для указания ошибки обновления как предупреждения или ошибки. Доступные параметры для при ошибке:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Сбой скрипта  
  
## <a name="see-also"></a>См. также  
[Выполнение команд консоли SSMA (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
