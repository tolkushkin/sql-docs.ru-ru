---
title: Функция SQLInstallTranslator | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de493cc42980390fee94ca4d86efc8f5cd40646c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242306"
---
# <a name="sqlinstalltranslator-function"></a>Функция SQLInstallTranslator
**Соответствие стандартам**  
 Представленные версии: 2.5, рекомендуется использовать ODBC  
  
 **Сводка**  
 В ODBC 3.0 **SQLInstallTranslator** был заменен классом [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Вызовы **SQLInstallTranslator** будут сопоставлены с **SQLInstallTranslatorEx**. Дополнительные сведения см. в разделе **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** вернет FALSE, если приложение вызывает его в ODBC 3 *.x* диспетчера драйверов с *lpszInfFile* аргументу присвоено значение, отличное от NULL. Файл Odbc.inf, используемый в ODBC 2. *x* больше не поддерживается в ODBC 3 *.x*, даже если для обеспечения обратной совместимости.
