---
title: Поддержка транзакций | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be133079c1b6beffd484942eb9ae058c14dd5c1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63306037"
---
# <a name="transaction-support"></a>Поддержка транзакций
Степень поддержки транзакций, определяемым драйвером. ODBC должен быть реализован с одного пользователя или системной базой данных, не требуется управлять несколькими обновлениями со своими данными. Кроме того некоторые базы данных, поддерживающие транзакции будет поддерживаться только инструкции языка обработки данных DML SQL; Существуют ограничения или семантика специальные транзакций относительно использования языка определения данных (DDL), когда транзакция активна. То есть может быть поддержку транзакций для нескольких одновременных обновления таблиц, но не для изменения числа и определения таблиц во время транзакции.  
  
 Приложение определяет, поддерживаются ли транзакции, ли DDL могут быть включены в транзакции и любые специальные эффекты, в том числе DDL в транзакции, путем вызова **SQLGetInfo** с параметром SQL_TXN_CAPABLE. Дополнительные сведения см. в разделе [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) описание функции.  
  
 Если драйвер не поддерживает транзакции, но приложение имеет возможность (с помощью API-Интерфейс, отличный от ODBC) для блокирования и разблокирования данных, приложения можно добиться поддержки транзакций, блокировка и снятие блокировки записей и таблиц, при необходимости. Реализация примера переноса учетной записи, приложение будет блокировать записи для обеих учетных записей, копирует текущие значения, дебетовой первой учетной записи, кредит второй учетной записи и разблокировать записи. Если не удалось выполнить все шаги, приложение будет сбросить учетные записи, с помощью копии.  
  
 Источники даже данные, которые поддерживают транзакции не может быть поддерживать несколько транзакций одновременно в определенной среде. Приложения вызывают **SQLGetInfo** SQL_MULTIPLE_ACTIVE_TXN возможность определить, поддерживает ли источник данных одновременных активных транзакций в более чем одном соединении в той же среде. Так как одну транзакцию на соединение, только представляет интерес для приложений, имеющих несколько подключений к одному источнику данных.
