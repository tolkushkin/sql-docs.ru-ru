---
title: Архитектура драйвера | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b593c3bd8619f0fbba47357f312479c2cd14063b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254241"
---
# <a name="driver-architecture"></a>Архитектура драйвера
Архитектура драйвера подразделяется на две категории, в зависимости от того, какие процессы программного обеспечения инструкций SQL.  
  
-   **Драйверы на основе файла** драйвер обращается напрямую к физическими данными. В этом случае драйвер выступает в качестве драйвера и источником данных; то есть он обрабатывает вызовы ODBC и инструкций SQL. Например драйверов для dBASE являются драйверы на основе файла, поскольку может использовать изолированный компонент database engine драйвер для dBASE не поддерживает. Важно отметить, что разработчики драйверов на основе файлов должны создавать свои собственные модули базы данных.  
  
-   **Драйверы на основе СУБД** драйвер обращается к физическими данными через отдельное ядро СУБД. В этом случае драйвер обрабатывает только вызовы ODBC; он передает инструкции SQL database engine для обработки. Например драйверы Oracle являются драйверы на основе СУБД, поскольку Oracle имеет изолированный компонент database engine, драйвер использует. Где находится ядро базы данных не имеет значения. Он может располагаться на той же машине, что драйвер или на другом компьютере, в сети; Он даже может осуществляться через шлюз.  
  
 Архитектура драйвера обычно интересные только для записи драйверов; то есть архитектура драйвера обычно никак не влияет на приложения. Тем не менее архитектура может повлиять на приложения, могут ли использовать СУБД SQL. Например Microsoft Access предоставляет изолированный компонент database engine. Если драйвером Microsoft Access на основе СУБД — он обращается к данным через это ядро — инструкций SQL с Microsoft Access можно передать в модуль для обработки.  
  
 Тем не менее если драйвер основан на файлах — то есть, он содержит в собственный модуль, который обращается к MDB-файл Microsoft® Access непосредственно - любые попытки для передачи инструкций SQL, характерные для Майкрософт доступа к обработчику, скорее всего, с последующим получением синтаксических ошибок. Причина заключается в что собственный обработчик является скорее всего, реализуют только ODBC SQL.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Драйверы на основе файлов](../../odbc/reference/file-based-drivers.md)  
  
-   [Драйверы на основе СУБД](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Сетевой пример](../../odbc/reference/network-example.md)  
  
-   [Другие архитектуры драйверов](../../odbc/reference/other-driver-architectures.md)
