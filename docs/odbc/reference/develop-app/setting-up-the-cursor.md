---
title: Настройка курсора | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59ade343f282933e05619996b119bc08e2dfb2ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62445916"
---
# <a name="setting-up-the-cursor"></a>Настройка курсора
Приложение может задать тип курсора, прежде чем выполнение инструкцию, которая создает результирующий набор. Это делается с помощью атрибута SQL_ATTR_CURSOR_TYPE инструкции. Если приложение явно не задает тип, будет использоваться однопроходный курсор. Чтобы получить смешанной курсора, приложение указывает курсор, управляемый набором ключей, но объявляет размер набора ключей, меньше, чем размер набора результатов.  
  
 Для курсоров, управляемых набором ключей и смешанного приложение также можно указать размер набора ключей. Это делается с помощью атрибута SQL_ATTR_KEYSET_SIZE атрибут инструкции. Если размер набора ключей имеет значение 0, который используется по умолчанию, размер набора ключей имеет значение размера результирующего набора, и используется курсор, управляемый набором ключей. Размер набора ключей может изменяться после открытия курсора.  
  
 Приложение также может задать размер набора строк; Дополнительные сведения см. в разделе [использование блочных курсоров](../../../odbc/reference/develop-app/using-block-cursors.md)ранее в этом разделе.
