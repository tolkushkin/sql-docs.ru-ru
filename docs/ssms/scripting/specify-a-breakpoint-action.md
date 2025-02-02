---
title: Указание действия в точке останова | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint action
- Transact-SQL debugger, breakpoint when hit action
ms.assetid: f97f0097-6f51-40c1-b2e0-294a93ce1e1b
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 011dcadf2fba4343ae5b0a4642d243faabc6ea3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65821197"
---
# <a name="specify-a-breakpoint-action"></a>Задание действия в точке останова
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Действие точки останова **При попадании** задает пользовательское действие, которое отладчик [!INCLUDE[tsql](../../includes/tsql-md.md)] выполняет для точки останова. Если достигнуто указанное число попаданий или удовлетворяется любое из указанных условий для точки останова, то отладчик выполняет действие, заданное для точки останова.  
  
##  <a name="BKMK_ActionConsiderations"></a> Обзор действий  
 Действие для точки останова по умолчанию — прекращение выполнения, если достигнуто число попаданий и удовлетворяется условие для точки останова. А действие **При попадании** в отладчике [!INCLUDE[tsql](../../includes/tsql-md.md)] , напротив, главным образом используется для вывода информации в окне отладчика **Вывод** в виде сообщения.  
  
 Сообщение указывается в параметре **Вывод сообщения** в виде текстовой строки, которая включает выражения с данными из кода [!INCLUDE[tsql](../../includes/tsql-md.md)] , отладка которого выполняется. Выражения могут включать следующие элементы.  
  
-   Выражение [!INCLUDE[tsql](../../includes/tsql-md.md)] , заключенное в фигурные скобки ({}). В выражении могут использоваться переменные, параметры и встроенные функции [!INCLUDE[tsql](../../includes/tsql-md.md)] . Например: {@MyVariable}, {@NameParameter}, {@@SPID} или {SERVERPROPERTY(ProcessID)}.  
  
-   Одно из следующих ключевых слов:  
  
    1.  $ADDRESS возвращает имя хранимой процедуры или определяемой пользователем функции, для которой установлена точка останова. Если точка останова задана в окне редактора, $ADDRESS возвращает имя редактируемого файла скрипта. $ADDRESS и $FUNCTION возвращают одинаковые данные в отладчике [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
    2.  $CALLER возвращает имя блока кода [!INCLUDE[tsql](../../includes/tsql-md.md)] , который вызвал хранимую процедуру или функцию. Если точка останова задана в окне редактора, $CALLER возвращает \<Вызывающий объект недоступен>. Если точка останова задана в хранимой процедуре или определяемой пользователем функции, которая вызывается из кода в окне редактора, то $CALLER возвращает имя редактируемого файла. Если точка останова задана в хранимой процедуре или определяемой пользователем функции, которая вызывается из другой процедуры или функции, то $CALLER возвращает имя вызывающей процедуры или функции.  
  
    3.  $CALLSTACK возвращает стек вызова в цепочке, которые вызывали текущую хранимую процедуру или определяемую пользователем функцию. Если точка останова задана в окне редактора, $CALLSTACK возвращает имя редактируемого файла скрипта.  
  
    4.  $FUNCTION возвращает имя хранимой процедуры или определяемой пользователем функции, для которой установлена точка останова. Если точка останова задана в окне редактора, $FUNCTION возвращает имя редактируемого файла скрипта.  
  
    5.  $PID и $PNAME возвращают идентификатор и имя процесса операционной системы, выполняющего экземпляр компонента Database Engine, где выполняется [!INCLUDE[tsql](../../includes/tsql-md.md)] . $PID возвращает такой же идентификатор, что и SERVERPROPERTY(ProcessID), за исключением того, что $PID имеет шестнадцатеричное, а SERVERPROPERTY(ProcessID) — десятичное значение.  
  
    6.  $TID и $TNAME возвращают идентификатор и имя потока операционной системы, в котором выполняется пакет [!INCLUDE[tsql](../../includes/tsql-md.md)] . Этот поток связан с процессом, в котором выполняется экземпляр ядра СУБД. $TID возвращает такое же значение, как и инструкция SELECT kpid FROM sys.sysprocesses WHERE spid = @@SPID, за одним исключением: $TID содержит шестнадцатеричное значение, а kpid — десятичное.  
  
-   Для включения в сообщение фигурных скобок и символов обратной косой черты можно воспользоваться символом обратной косой черты (\\) в качестве escape-символа: \\{, \\} и \\\\.  
  
#### <a name="to-specify-a-when-hit-action"></a>Установка действия «При попадании»  
  
1.  В окне редактора щелкните глиф точки останова правой кнопкой мыши и выберите в контекстном меню пункт **При попадании** .  
  
     -или-  
  
     В окне **Точки останова** щелкните глиф точки останова правой кнопкой мыши и выберите в контекстном меню пункт **При попадании** .  
  
2.  В диалоговом окне **При попадании в точку останова** выберите нужное поведение:  
  
    1.  Выберите **Вывод сообщения** для вывода сообщения в окне отладчика «Вывод» при попадании в точку останова.  
  
    2.  Параметр **Запуск макроса** в отладчике [!INCLUDE[tsql](../../includes/tsql-md.md)] недоступен и отображается серым.  
  
    3.  Выберите **Продолжить выполнение** , чтобы точка останова не приводила к приостановке выполнения. Этот параметр доступен только в том случае, если выбран параметр **Вывод сообщения** .  
  
3.  Нажмите кнопку **ОК** , чтобы внести изменения, либо кнопку **Отмена** , чтобы выйти без их применения.  
  
## <a name="see-also"></a>См. также:  
 [Задание условия точки останова](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [Настройка счетчика числа попаданий](../../relational-databases/scripting/specify-a-hit-count.md)  
