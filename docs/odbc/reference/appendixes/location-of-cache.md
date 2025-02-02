---
title: Расположение кэша | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b1ffd8c56a6727a892cb518222c961bbb6c794c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181346"
---
# <a name="location-of-cache"></a>Расположение кэша
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этой функции в новых разработках и запланируйте изменение приложений, которые сейчас ее используют. Корпорация Майкрософт рекомендует использовать функциональные возможности драйвера курсора.  
  
 Библиотека курсоров кэширует данные в памяти и Windows® временные файлы. Это ограничивает размер результирующего набора, библиотека курсоров может обрабатывать только объемом свободного места. Временный файл используется в том случае, если для кэширования данных будет пересекает границы сегмента, если вставить в конце кэш библиотеки курсоров. Вместо этого для кэширования данных добавляется вместо последней сохраненной блок данных в кэше. Последняя сохраненная блок данных сохраняется во временном файле. Если библиотека курсоров завершается аварийно, например при сбое питания, его можно оставить Windows временные файлы на диске. Эти параметры назывались ~ CTT*nnnn*.tmp того на них, созданные в текущем каталоге.  
  
> [!NOTE]  
>  Если библиотека курсоров в Microsoft® WindowsNT®/Windows 2000 пытается кэшировать данные во временном файле на текущий каталог во время работы приложения из папки только для чтения или компакт-диске (например, образец библиотеки Microsoft Foundation Class) SQLSTATE HY000 (Общая ошибка-не удалось создать файловый буфер) будет возвращаться.
