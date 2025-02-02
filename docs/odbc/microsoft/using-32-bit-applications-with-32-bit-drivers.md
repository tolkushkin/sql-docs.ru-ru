---
title: Использование 32-разрядных приложений с 32-разрядными драйверами | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c4f0b21bba9e56cad076ae08f5a561cc972d2ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213480"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Использование 32-разрядных приложений с 32-разрядными драйверами
Можно запустить 32-разрядных приложений с 32-разрядные драйверы. 32-разрядных приложений и 32-разрядные драйверы используют Win32® API.  
  
## <a name="architecture"></a>Architecture  
 На следующем рисунке показано, как 32-разрядным приложениям взаимодействовать с 32-разрядные драйверы. Приложение вызывает 32-разрядного диспетчера драйверов, который в свою очередь вызывает 32-разрядные драйверы.  
  
 ![Как 32&#45;взаимодействия разрядных приложений с 32&#45;разрядные драйверы](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Не следует использовать преобразования установщика 32-разрядной библиотеки DLL на другая/Windows 2000. Несмотря на то, что он имеет то же имя файла как 32-разрядный установщик библиотеки DLL, это разные библиотеки DLL.  
  
## <a name="administration"></a>Администрирование  
 Источники данных для 32-разрядные драйверы можно управлять с помощью администратора источника данных ODBC. Открытие администратора ODBC на компьютерах под управлением Windows 2000, откройте панель управления Windows, дважды щелкните **Администрирование**, а затем дважды щелкните **источники данных (ODBC)** . На компьютерах под управлением предыдущих версий Microsoft Windows, называется значок **32-разрядная версия ODBC** или просто **ODBC**.  
  
## <a name="components"></a>Компоненты  
 Компонент ODBC включает следующие файлы для запуска 32-разрядных приложений с 32-разрядные драйверы. Эти компоненты находятся в каталоге \Redist.  
  
|Имя файла|Описание|  
|---------------|-----------------|  
|Odbc32.dll|32-разрядного диспетчера драйверов|  
|Odbccp32.dll|32-разрядный установщик DLL|  
|Odbcad32.exe|Администратор ODBC 32-разрядной программы|  
|Odbcinst.hlp|Файл справки установщика|  
|Msvcrt40.dll|Библиотеки времени выполнения C|
