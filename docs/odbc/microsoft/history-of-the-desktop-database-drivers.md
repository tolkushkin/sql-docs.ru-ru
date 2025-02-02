---
title: Журнал драйверов для настольных баз данных | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a77aeafff6b27b2de0b947700cef1c7251cd7548
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127269"
---
# <a name="history-of-the-desktop-database-drivers"></a>Журнал драйверов для баз данных на настольном компьютере
В следующей таблице показаны журнал версий драйверов базы данных.  
  
|Version|Дата выпуска|Описание|  
|-------------|------------------|-----------------|  
|1.0|Август 1993 г.|Использовать обработчик SIMBA запросов, полученных при PageAhead программного обеспечения. SIMBA полученных вызовов ODBC и инструкций SQL, их обработки в устанавливаемый ISAM вызовы Microsoft Jet, а затем вызывает слоя диспетчеризации Microsoft Jet ISAM для загрузки и вызывать соответствующий драйвер устанавливаемый ISAM.|  
|2.0|Декабрь 1994|Используется с ODBC 2.0, которая значительно расширен функции ODBC. Основное изменение в версии 2.0 была, что базы данных Microsoft Jet заменить обработчик запросов SIMBA. С ядром СУБД Microsoft Jet драйверы для баз данных Desktop гораздо более тесно интегрирован с Microsoft Jet устанавливаемые драйверы ISAM и технологии Microsoft Access. Значительные улучшения были:<br /><br /> -Встроенная поддержка Прокручиваемые курсоры.<br />-Встроенная поддержка внешних соединений, обновляемую и разнородных соединения и транзакции.<br />-32-разрядные версии драйверов для Microsoft Windows NT.|  
|3.0|Октябрь 1995|Обеспечивает поддержку для Windows 95 и Windows NT Workstation или NT 3.51 сервера. Только 32-разрядные драйверы были включены в этом выпуске; 16-разрядные драйверы для Windows версии 3.1 были удалены.|  
|3.5|Октябрь 1996|Эти драйверы были двухбайтовой кодировки (DBCS)-включен, чем предыдущие версии программы были лучше подходят для использования с веб-приложений и размещено использование файла имена источников данных (DSN). Драйвер Microsoft Access была выпущена в версии RISC для использования на платформах альфа-версия для Windows 95/98 и Windows NT 3.51 и более поздних операционных системах.|  
|4.0|Позднее 1998|Обеспечивает поддержку формата Юникода ядро Jet Microsoft вместе с совместимости для формата ANSI из более ранних версий.|  
  
> [!NOTE]  
>  Драйверы version3.5 были разработаны для работы с ODBC2. *x*. Несмотря на то, что они также работают с ODBC 3.0, они не поддерживают все функции ODBC 3.0. Дополнительные сведения о том, как эти драйверы работают с ODBC 3.0 см. в разделе [обратной совместимости и соответствия стандартам](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).
