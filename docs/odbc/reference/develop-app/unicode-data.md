---
title: Данные в Юникоде | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74de6c44aaf109a434f0cf76c6902abfba92efe1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305773"
---
# <a name="unicode-data"></a>Данные в Юникоде
Типы данных SQL в Юникоде предоставленный для описания данные, которые находятся в формате Юникод, изначально в СУБД. Тип данных Юникода C предоставляется позволяют приложениям для привязки данных в Юникоде буфер. Диспетчер драйверов можно преобразовать данные из типа C Юникод (SQL_C_WCHAR), чтобы сделать его функции с помощью драйвера ANSI.  
  
 ODBC 3.0 или 2. *x* приложения будет всегда выполнять привязку к типам данных ANSI. Для достижения оптимальной производительности приложения ODBC 3.5 (или более поздней версии) необходимо привязать к тип данных C ANSI, если тип столбца SQL ANSI и должен быть привязан к типу данных Юникода C, если тип столбца SQL Юникода.  
  
 Индикаторы типа SQL в Юникоде, SQL_WCHAR, SQL_WVARCHAR и SQL_WLONGVARCHAR. Данных SQL_WCHAR длина фиксированной строки, хотя переменной длины, не объявленных более имеет SQL_WVARCHAR и SQL_WLONGVARCHAR переменной длины с максимумом, зависит от источника данных.  
  
 Индикатор типа Юникода C является SQL_C_WCHAR. Это значение по умолчанию для каждого из индикаторов типа SQL в Юникоде. Можно преобразовать все SQL типы SQL_C_WCHAR, и SQL_C_WCHAR можно преобразовать все типы SQL. Приложение может получать данные в одном из трех способов:  
  
-   Извлечь данные как SQL_C_CHAR.  
  
-   Извлечение данных в виде SQL_C_WCHAR.  
  
-   Объявление этих данных как SQL_C_TCHAR. Это представляет собой макрос, который вставляет SQL_C_WCHAR в том случае, если приложение компилируется как приложение Юникода или вставляет SQL_C_CHAR в том случае, если оно компилируется как приложение ANSI.  
  
 SQL_C_TCHAR объявляется в функции следующим образом:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 При компиляции приложения как приложения с поддержкой Юникода, *ValueType* аргумент может быть изменено с SQL_C_TCHAR на SQL_C_WCHAR. Когда приложение компилируется как приложение ANSI *ValueType* аргумент будет изменено на SQL_C_CHAR.  
  
 Драйверы Юникода по-прежнему должны поддерживать типы данных ANSI, включая SQL_CHAR. Если приложение, которое работает с драйвером Юникода имеет привязку к SQL_CHAR, диспетчер драйверов не сопоставляются SQL_CHAR данных SQL_WCHAR. Драйвер Юникода необходимо принять данных SQL_CHAR.  
  
 Диспетчер драйверов драйвера и имена DSN хранятся в Юникоде и сопоставляет их с ANSI при необходимости. Если символ Юникода, не может быть сопоставлен знак ANSI (как это может произойти, если в драйвер и имена DSN используются символы из кодовой страницы, который не является страницей машинный код компьютера), символы, которые не могут быть преобразованы, представляются sup символ по умолчанию plied системой.
