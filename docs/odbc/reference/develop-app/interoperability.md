---
title: Взаимодействие | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d5e4fbee458bec88461d3e2945a466c848d3345
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446491"
---
# <a name="interoperability"></a>Совместимость
*Взаимодействие* — это способность одного приложения для работы с много разных СУБД. Потребность в написании универсальный, с возможностью взаимодействия приложений был одним из основных факторов, ведущих к разработке ODBC. Тем не менее, взаимодействие не простой путь из «не поддерживает взаимодействие» для «полностью совместим.» Путь есть много ветвей, и каждый требует плюсы и минусы функций, скорость, сложность кода и время разработки.  
  
 Процесс записи с возможностью взаимодействия приложения состоит из нескольких этапов:  
  
1.  Решить, будет ли приложение использовать ODBC.  
  
2.  Выбор уровня взаимодействия и решить, какие преимущества и недостатки необходимы для достижения этого уровня.  
  
3.  Написание кода с возможностью взаимодействия и как полностью его тестирование.  
  
 Следует отметить, что взаимодействие — это главным образом домен, разработчик приложения. Драйверы, предназначены для работы с одной СУБД и по определению не являются функционально совместимыми. Они играют роль при взаимодействии с правильной реализации и предоставления ODBC через единый СУБД.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Есть ли смысл использовать ODBC?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Выбор уровня взаимодействия](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Определение целевых СУБД и драйверов](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Оценка возможности использования функций базы данных](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Продолжительность цикла продукта](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Создание приложений с поддержкой взаимодействия](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Тестирование приложений с поддержкой взаимодействия](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
