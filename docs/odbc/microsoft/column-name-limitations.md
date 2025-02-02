---
title: Ограничения имен столбцов | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a80ed397ae494bc686ef76aaeeef10b61662f19
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301813"
---
# <a name="column-name-limitations"></a>Ограничения имен столбцов
Имена столбцов могут содержать любые допустимые символы (например, пробелы). Если имена столбцов содержат любые символы, кроме буквы, цифры и символы подчеркивания, имя должно быть выделено, заключив его в обратной кавычки (').  
  
 Если используется драйвер Microsoft Access или Microsoft Excel, имена столбцов являются длиннее 64 символов и более длинных имен создает ошибку. Если используется драйвер для Paradox, имя столбца максимальное состоит из 25 знаков. Если используется драйвер для текстовых, имя столбца, максимальное — 64 символа и более длинных имен усекаются.  
  
 Если используется драйвер для dBASE, символы значение ASCII-больше 127 преобразуются в символы подчеркивания.  
  
 При использовании драйвера Microsoft Excel, если присутствуют имена столбцов, они должны быть в первой строке. Имя, которое будет использоваться в Microsoft Excel «!» символ должен быть заключен в обратной кавычки ('). «!» Символ преобразуется в символ «$», так как «!» символ не допускается в имени ODBC, даже в том случае, если имя заключено в кавычки назад. Все остальные символы Microsoft Excel допустимым (за исключением знака вертикальной черты (&#124;)) можно использовать в имени столбца, включая пробелы. Идентификатором с разделителем должен использоваться для имени столбца Microsoft Excel для включения пробел. Имена столбцов неуказанных будет заменен сформированное драйвером имена, например, «Col1» для первого столбца.  
  
 Символ вертикальной черты (&#124;) нельзя использовать в имени столбца ли имя заключен в кавычки назад или нет.  
  
 Если используется драйвер для текстовых, драйвер предоставляет имя по умолчанию, если не указано имя столбца. Например драйвер вызывает первый столбец F1, F2 во втором и т. д.
