---
title: Указатели дескрипторов | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3aa085cc0a098f557ca7a8cbddcd787a178b79d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760772"
---
# <a name="descriptor-handles"></a>Указатели дескрипторов
Объект *дескриптор* является коллекцией метаданных, описывающих параметры инструкции SQL или столбцы результирующего набора, как явствует приложение или драйвер (также известный как *реализации*). Таким образом дескриптор может заполнить любой из четырех ролей:  
  
-   **Дескрипторе параметра приложения (APD).** Содержит сведения о буферах приложений, связанных с параметрами в инструкции SQL, например адреса, длины и типы данных C.  
  
-   **Дескриптор параметра реализации (IPD).** Содержит сведения о параметрах в инструкции SQL, например типы данных SQL, длины и допустимости значений NULL.  
  
-   **Дескриптор строки приложения (Отменить).** Содержит сведения о буферах приложения, привязанные к столбцам в результирующем наборе, например адреса, длины и типы данных C.  
  
-   **Дескриптор строки реализации (IRD).** Содержит сведения о столбцах в результирующем наборе, например, их типы данных SQL, длины и допустимости значений NULL.  
  
 Четыре дескрипторы (один заполнения каждой роли) автоматически выделяются при выделении инструкцию. Они известны как *автоматически выделяется дескрипторы* и всегда связаны с этой инструкции. Приложения, кроме того, можно выделять дескрипторы с **SQLAllocHandle**. Они известны как *явно выделенные дескрипторы*. Они выделяются для подключения и могут быть связаны с одной или нескольких инструкций для этого соединения для выполнения роли APD или Отменить в этих инструкциях.  
  
 Большинство операций в ODBC могут выполняться без явного использования дескрипторов для приложения. Однако дескрипторы обеспечивают удобный ярлык для некоторых операций. Например предположим, что приложению требуется вставить данные из двух разных наборов буферов. Чтобы использовать первый набор буферов, компилятор вызовет многократно **SQLBindParameter** для их привязки к параметрам в **вставить** инструкцию и затем выполняется инструкция. Чтобы использовать второй набор буферов, ее необходимо повторить эту процедуру. Кроме того он может настроить привязки первый набор буферов в один дескриптор и второй набор буферов в другом дескрипторе. Чтобы переключиться между наборами привязок, приложение просто вызвала бы **SQLSetStmtAttr** и связать правильный дескриптор с помощью инструкции в дескрипторе параметра приложения.  
  
 Дополнительные сведения о дескрипторах, см. в разделе [типы из дескрипторов](../../../odbc/reference/develop-app/types-of-descriptors.md).
