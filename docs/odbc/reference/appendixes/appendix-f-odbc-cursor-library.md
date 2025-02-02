---
title: Приложение Е. Библиотека курсоров ODBC | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c27845976651b0d68b91b6269a21d1cae3518df8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267802"
---
# <a name="appendix-f-odbc-cursor-library"></a>Приложение Е. Библиотека курсоров ODBC
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этой функции в новых разработках и запланируйте изменение приложений, которые сейчас ее используют. Корпорация Майкрософт рекомендует использовать функциональные возможности драйвера курсора.  
  
 Библиотека курсоров ODBC (Odbccr32.dll) поддерживает прокручиваемые курсоры блок для любой драйвер, который соответствует уровню API 1 уровень соответствия и может свободно распространяться разработчиками приложений или драйверов. Библиотека курсоров также поддерживает инструкций позиционированного обновления и удаления для результирующих наборов, созданных **ВЫБЕРИТЕ** инструкций. Несмотря на то, что он поддерживает только статические и однонаправленные курсоры, библиотека курсоров удовлетворяет требованиям многих приложений. Кроме того оно обеспечит хорошую производительность, особенно для небольшого и среднего размера результирующих наборов, а также для приложений, у которых нет поддержки хорошо курсора.  
  
 Библиотека курсоров является библиотеку динамической компоновки (DLL), расположенный между диспетчера драйверов и драйвер. Когда приложение вызывает функцию, диспетчер драйверов вызывает функцию в библиотеку курсоров, который выполняет функцию или вызывает его в указанный драйвер. Для данного соединения приложение указывает ли библиотека курсоров всегда используется, если драйвер не поддерживает прокручиваемые курсоры или никогда не используется.  
  
 Библиотека курсоров появляется как драйвер для диспетчера драйверов. Если библиотека курсоров находится между диспетчера драйверов и ODBC 2. *x* драйвера, библиотека курсоров появляется как ODBC 2. *x* драйвера. Если библиотека курсоров находится между диспетчера драйверов, а ODBC 3 *.x* драйвера, библиотека курсоров появляется как ODBC 3 *.x* драйвера. Поведение, демонстрируемое библиотекой курсоров зависит от версии драйвера, с которым идет работа, за исключением смещения привязки, который поддерживается для обоих ODBC 2. *x* и ODBC 3. *x* драйверы.  
  
 Для реализации блочных курсоров в **SQLFetch** и **SQLFetchScroll**, многократно вызывает библиотеку курсоров **SQLFetch** в драйвере. Чтобы реализовать прокрутка, он кэширует данные, извлеченные в памяти и файлы на диске. Когда приложение запрашивает новый набор строк, библиотека курсоров извлекает его при необходимости из драйвера или из кэша.  
  
 Чтобы реализовать позиционированного обновления и удаления, создает библиотеку курсоров **обновление** или **удалить** инструкции с **ГДЕ** предложение, определяющее кэшированные значение для каждого привязанного столбца в строке. При выполнении инструкции позиционированного обновления, библиотека курсоров обновляет свой кэш на основе значений в буферах набора строк.  
  
 Дополнительные сведения о библиотеку курсоров ODBC см. в следующих разделах в этом приложении:  
  
-   [Использование библиотеки курсоров ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Выполнение инструкций позиционированного обновления и удаления](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Пример кода библиотеки курсоров](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Примечания по реализации](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Коды ошибок для библиотеки курсоров ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
