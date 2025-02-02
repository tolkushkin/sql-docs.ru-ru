---
title: Файловые источники данных | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 733b958ee883aa62034b4acc1eec67100b35a74d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628457"
---
# <a name="file-data-sources"></a>Файловые источники данных
*Файловые источники данных* хранятся в файле и разрешить сведения о подключении для использования в несколько раз одним пользователем или совместно использовать несколько пользователей. При использовании источника данных, диспетчер драйверов устанавливает подключение к источнику данных, используя сведения в файле .dsn. Этот файл можно управлять как любой другой файл. Источника данных имеет имя источника данных, так как не машинные источники данных и не зарегистрирована для любого одного пользователя или компьютера.  
  
 Файл источника данных упрощает процесс подключения, так как файл .dsn содержит строку подключения, в противном случае пришлось бы быть построен для вызова **SQLDriverConnect** функции. Еще одним преимуществом .dsn файл является то, что его можно скопировать на любой машине, идентичные данные источников можно использовать в число компьютеров, до тех пор, пока они имеют установлены соответствующие драйверы. Файл источника данных также может использоваться приложениями. Совместного использования источника данных можно разместить в сети и использоваться одновременно несколькими приложениями.  
  
 Файл .dsn также может быть непригоден для совместного использования. Файл такие .dsn находится на одном компьютере и указывает на источник данных компьютера. Такие источники данных существуют главным образом, чтобы разрешить простое преобразование машинных источников данных для файловых источников данных, таким образом, приложения могут быть предназначены для работы исключительно с файловые источники данных. Если диспетчер драйверов отправляется информацию в такие источники данных, он подключается при необходимости для источника данных, указывающий файл .dsn.  
  
 Дополнительные сведения о файловых источников данных, см. в разделе [подключение с использованием файловых источников данных](../../odbc/reference/develop-app/connecting-using-file-data-sources.md), или [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) описание функции.
