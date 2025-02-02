---
title: Совместимость драйверов для баз данных на настольном | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], Unicode
- Unicode [ODBC], desktop database drivers
- ODBC desktop database drivers [ODBC], Unicode
- backward compatibility [ODBC], Unicode
- desktop database drivers [ODBC], Unicode
- Jet-based ODBC drivers [ODBC], Unicode
ms.assetid: dd695638-1a0b-4e27-8a6a-9510ebb5a5ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d081d53458ec59eb2ac9f05c5c1d47d6991b5010
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240360"
---
# <a name="desktop-database-driver-compatibility"></a>Совместимость драйверов для баз данных на настольном компьютере
Юникод является метод программного обеспечения кодировки символов, считает все символы с фиксированной ширины в два байта. Этот метод используется в качестве альтернативы для кодировки Windows ANSI, являющийся, так как он представляет символы в один байт, ограничена 256 символами. Поскольку Юникода может представлять более 65 000 символов, его можно использовать для многих языков, символы которой не представлены в кодировке ANSI.  
  
 Диспетчер драйверов ODBC 3.5 (или более поздней версии) с поддержкой Юникода. Это влияет на двух основных областях: вызовами функции и строковые типы данных. Диспетчер драйверов карты строку аргументы функций и строковых данных в соответствии с требованиями приложений и драйверов, каждый из которых может быть поддержкой ANSI или Юникод.  
  
 Диспетчер драйверов ODBC 3.5 (или более поздней версии) поддерживает использование драйвера Юникода с помощью приложения с поддержкой Юникода и ANSI приложения. Он также поддерживает использование драйвера ANSI с приложением ANSI. Диспетчер драйверов предоставляет ограниченный сопоставление Unicode-ANSI для приложения с поддержкой Юникода, работе с драйвером ANSI. Это обеспечивает доступ к базы данных Jet 3.5 и поддержку всех существующих типов файла ISAM.  
  
 Когда приложение ANSI, использует базы данных драйвера ODBC Desktop 4.0 и обращается к Microsoft Access 4.0 или более поздней версии, драйвер предоставляет тип данных SQL_CHAR, SQL_VARCHAR или SQL_LONGVARCHAR, несмотря на то, что Jet 4.0 поддерживает широкий версии. Более старые версии Jet не поддерживают SQL_WCHAR, SQL_WVARCHAR и SQL_WLONGVARCHAR. Это ограничение также применяется в случаях, где используются старые форматы с ядром СУБД Jet 4.0.  
  
 Дополнительные сведения, касающиеся проблемы Юникода с ODBC, см. в разделе [Юникода](../../odbc/reference/develop-app/unicode.md) в замечания по программированию.
