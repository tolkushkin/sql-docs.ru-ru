---
title: Вызов SQLSetPos для вставки данных | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7424206318436532cad62690b01427f079a589
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159279"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Вызов SQLSetPos для вставки данных
Когда ODBC 2. *x* приложение, которое работает с ODBC 3 *.x* драйвер вызывает **SQLSetPos** с *операции* аргумент SQL_ADD, диспетчер драйверов не удается сопоставить этот вызов **SQLBulkOperations**. Если ODBC 3 *.x* драйвер должен работать с приложением, которое вызывает **SQLSetPos** с SQL_ADD, драйвер должен поддерживает эту операцию.  
  
 Одно из основных отличий в поведении при **SQLSetPos** вызове с параметром SQL_ADD возникает, когда он вызывается в состоянии S6. В ODBC 2. *x*, драйвер возвратил S1010 при **SQLSetPos** был вызван с SQL_ADD в состоянии S6 (после Позиционирует курсор с **SQLFetch**). В ODBC 3 *.x*, **SQLBulkOperations** с *операции* из SQL_ADD может быть вызван в состоянии S6. Это вторая основная разница в поведении **SQLBulkOperations** с *операции* SQL_ADD может быть вызван в состоянии S5, тогда как **SQLSetPos** с  **Операция** из SQL_ADD невозможно. Для переходов инструкции, которые могут возникнуть для одного вызова в ODBC 3 *.x*, см. в разделе [приложении б: Таблицы перехода состояния ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
