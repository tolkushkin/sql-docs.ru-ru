---
title: Embedded SQL | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47936b5c085514fca4ecc1c81057ef78a19f05c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628467"
---
# <a name="embedded-sql"></a>Embedded SQL
Внедряется первый метод для отправки инструкций SQL для СУБД SQL. Поскольку SQL не использует переменные и инструкции управления потоком, он часто используется в качестве базы данных варианта языка, который можно добавить в программу, написанную на обычной язык программирования, таких как C или COBOL. Это центральная идея из embedded SQL: размещение инструкций SQL в программу, написанную на узел языка программирования. Коротко говоря для внедрения инструкций SQL в базовый язык используются следующие методы:  
  
-   Внедренные инструкции SQL обрабатываются специальные предкомпилированного SQL. Все инструкции SQL начинаются с introducer и заканчиваются с признаком конца, для которых флаг инструкции SQL для предварительной компиляции. Introducer и признак конца, зависят от основного языка. Например, маркер является «EXEC SQL» в C и «& SQL ("в MUMPS, и знак завершения является точка с запятой (;) в C и закрывающей скобки в MUMPS.  
  
-   Переменные из прикладной программы, называются переменными узла может использоваться в инструкциях embedded SQL, везде константы допускаются. Их можно использовать во входных данных для настройки инструкции SQL для конкретной ситуации и на выходе для получения результатов запроса.  
  
-   Запросы, которые возвращают одну строку данных обрабатываются с помощью инструкции SELECT singleton. Эта инструкция указывает запрос и хост-переменных, в котором для возвращения данных.  
  
-   Запросы, которые возвращают несколько строк данных, обрабатываются с курсорами. Следит за текущую строку в результирующий набор курсора. Инструкция DECLARE CURSOR определяет запрос, оператор OPEN начинает обработку запроса, результаты инструкции FETCH извлекает последовательных строк данных и инструкцию CLOSE завершает обработку запроса.  
  
-   При открытом курсоре инструкций позиционированного обновления и удаления позиционированные можно использовать для обновления или удаления строки, выбранной в данный момент курсором.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Образец Embedded SQL](../../odbc/reference/embedded-sql-example.md)  
  
-   [Компиляция программы Embedded SQL](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [Статический SQL](../../odbc/reference/static-sql.md)  
  
-   [Динамический SQL](../../odbc/reference/dynamic-sql.md)
