---
title: При рассмотрении возможности использования функций базы данных | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92eeb64b95d666b15c03c70d656d2309a63eabf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042190"
---
# <a name="considering-database-features-to-use"></a>Оценка возможности использования функций базы данных
После известен базовый уровень взаимодействия, необходимо учитывать функции базы данных, используемых приложением. Например какие инструкции SQL приложение выполнит? Будет ли приложение использовать Прокручиваемые курсоры? Транзакции? Процедуры? Длинные данные? Понять, какие функции могут поддерживаться не все СУБД, см. в разделе [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), и [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) описаний функций и [ Приложение c. Грамматика SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Возможности, необходимые для приложения может решить некоторые СУБД из списка целевой СУБД. Они также показывают, что приложение может легко выбирать целевые многие СУБД.  
  
 К примеру Если необходимые компоненты являются простыми, они обычно применяется с высокой степенью совместимости. Приложение, которое выполняется простой **ВЫБЕРИТЕ** инструкции и извлекает результаты с помощью однонаправленного курсора может не поддерживает возможность взаимодействия благодаря своей простоте: Практически все драйверы и СУБД поддерживают функциональные возможности, которые необходимы.  
  
 Тем не менее если необходимые компоненты являются более сложными, например Прокручиваемые курсоры, позиционированного обновления и инструкций delete и процедуры, преимущества и недостатки должно часто выполняться. Существует несколько вариантов:  
  
-   **Нижний взаимодействие, больше возможностей.** Приложение включает функции, но работает только с СУБД, которые их поддерживают.  
  
-   **Выше взаимодействие, сократить количество устанавливаемых компонентов.** Приложение удаляет функции, но работает с дополнительные СУБД.  
  
-   **Взаимодействие выше дополнительных функций.** Приложение включает возможности, но делает их доступными только с этими СУБД, которые их поддерживают.  
  
-   **Выше взаимодействие, больше возможностей.** Приложение использует возможности с СУБД, которые их поддерживают и эмулирует их для СУБД, которые этого не делают.  
  
 Первые две ситуации довольно прост в реализации, так как функции используются все поддерживаемые СУБД или none. Двух последних случаях, с другой стороны, более сложны. Он необходим в обоих случаях, чтобы проверить, поддерживает ли СУБД средства, а также в последнем случае для записи потенциально большого объема кода для эмуляции эти функции. Таким образом эти схемы может потребоваться больше времени разработки и может выполняться медленнее во время выполнения.  
  
 Рассмотрим приложение универсальный запрос, который может подключиться к одного источника данных. Приложение принимает запрос от пользователя и отображает результаты в окне. Теперь предположим, что это приложение имеет один компонент, который позволяет выводить результаты нескольких запросов одновременно. Т. е они можно выполнить запрос и рассмотрим некоторые результаты, выполните другой запрос и рассмотрим некоторые из его результаты и затем вернитесь к первый запрос. Это представляет из-за проблемы взаимодействия, так как некоторые драйверы поддерживают только один активный оператор.  
  
 Приложение имеет несколько вариантов, в зависимости от того, что драйвер возвращает параметр SQL_MAX_CONCURRENT_ACTIVITIES в **SQLGetInfo**:  
  
-   **Всегда поддерживать несколько запросов.** После подключения к драйверу, приложение проверяет число активных инструкций. Если драйвер поддерживает только одну активную инструкцию, приложение закрывает подключение и информирует пользователя о том, что драйвер не поддерживает требуемые функции. Приложение просто реализовать и имеет полный набор функций, но имеет нижней взаимодействия.  
  
-   **Никогда не поддерживает несколько запросов.** Приложение полностью удаляет функцию. Он прост в реализации и имеет высокий уровень взаимодействия, но с меньшим количеством функций.  
  
-   **Поддерживает несколько запросов, только в том случае, если драйвер выполняет.** После подключения к драйверу, приложение проверяет число активных инструкций. Приложение позволяет пользователю начать новую инструкцию, если она уже активным, только в том случае, если драйвер поддерживает несколько активных инструкций. Приложение имеет выше функции и возможности взаимодействия, но гораздо труднее реализовать.  
  
-   **Всегда поддерживать несколько запросов и эмулировать их при необходимости.** После подключения к драйверу, приложение проверяет число активных инструкций. Приложение всегда позволяет пользователю начать новую инструкцию, когда один уже активен. Если драйвер поддерживает только одну активную инструкцию, приложение открывается дополнительное подключение к этому драйверу и выполняет новый оператор для этого соединения. Приложение имеет полный набор функций и высокий уровень взаимодействия, но гораздо труднее реализовать.
