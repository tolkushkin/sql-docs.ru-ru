---
title: Вертикальные приложения | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df7a2d036692cefcd1b2ea2338d51938a11ea85a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208439"
---
# <a name="vertical-applications"></a>Вертикальные приложения
Вертикальные приложения обычно выполняют четко определенной задачи от одной СУБД. Например приложение для ввода заказов отслеживает заказов в компании. Что общего у этих типов приложений, что схемы базы данных обычно создаются разработчиком приложения и, хотя приложение может работать с количеством разных СУБД, он работает с одной СУБД для одного клиента.  
  
 Поскольку вертикальные приложения обычно требуют определенных функций, таких как Прокручиваемые курсоры и транзакции, они редко поддерживают все СУБД. Вместо этого они обычно поддерживают возможность взаимодействия между ограниченный набор СУБД. Обычно разработчикам приложений вертикальной выбрать для поддержки этих СУБД, представляющие большую часть рынка и пропускают остальные. Они даже выбрать специальные драйверы, поддержка этих СУБД для уменьшения их тестирование и затраты на поддержку продукта.  
  
 Так как по вертикали приложения могут поддерживать известный набор СУБД, иногда они содержат код специфические для драйвера или СУБД. Тем не менее такой код лучше всего свести к минимуму, поскольку требуется дополнительное время на обслуживание.
