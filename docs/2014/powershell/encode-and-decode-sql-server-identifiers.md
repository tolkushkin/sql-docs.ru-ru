---
title: Шифрование и расшифровка идентификаторов SQL Server | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 57cab8512adb2f0377c932fbeb0140f1482ae454
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922923"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>Шифрование и расшифровка идентификаторов SQL Server
  Идентификаторы SQL Server с разделителями иногда содержат символы, не поддерживаемые в путях Windows PowerShell. Эти символы можно задавать путем кодирования их шестнадцатеричных значений.  
  
1.  **Перед началом:**  [Ограничения](#LimitationsRestrictions)  
  
2.  **Обработка специальных символов:**  [Кодирование идентификатора](#EncodeIdent), [декодирование идентификатора](#DecodeIdent)  
  
## <a name="before-you-begin"></a>Перед началом  
 Символы, неподдерживаемые в именах путей Windows PowerShell, могут быть представлены или закодированы в виде символа «%», за которым следует шестнадцатеричное значение для битового шаблона, представляющего символ, например «**%** xx». Для обработки символов, неподдерживаемых в обозначениях путей Windows PowerShell, всегда можно использовать кодировку.  
  
 Командлет **Encode-SqlName** принимает в качестве входных данных идентификатор [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Он возвращает строку, в которой все символы, не поддерживаемые языком Windows PowerShell, закодированы в виде «%xx». Командлет **Decode-SqlName** принимает в качестве входных данных закодированный идентификатор [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] и возвращает исходный идентификатор.  
  
###  <a name="LimitationsRestrictions"></a> Ограничения  
 Командлеты `Encode-Sqlname` и `Decode-Sqlname` обеспечивают только кодирование или декодирование символов, допустимых в идентификаторах SQL Server с разделителями, но не поддерживаемых в путях PowerShell. Символы, кодируемые командлетом **Encode-SqlName** и декодируемые командлетом **Decode-SqlName**, перечислены ниже.  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**Символ**|\ |/|, перечислены ниже.|%|\<|>|*|?|[|]|&#124;|  
|**Шестнадцатеричная кодировка**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> кодирование идентификатора  
 **Кодирование идентификатора SQL Server в пути PowerShell**  
  
-   Используйте один из двух методов для кодирования идентификатора SQL Server:  
  
    -   Укажите шестнадцатеричный код для неподдерживаемого символа, используя синтаксис %XX, где XX — шестнадцатеричный код.  
  
    -   Передайте идентификатор в виде строки, заключенной в кавычки, в командлет `Encode-Sqlname`  
  
### <a name="examples-encoding"></a>Примеры (кодирование)  
 В этом примере указана закодированная версия символа «:» (%3A):  
  
```  
Set-Location Table%3ATest  
```  
  
 Можно также использовать **Encode-SqlName** для формирования имени, поддерживаемого Windows PowerShell:  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> декодирование идентификатора  
 **Декодирование идентификатора SQL Server из пути PowerShell**  
  
 Используйте командлет `Decode-Sqlname` для замены шестнадцатеричных кодов символами, представленными этими кодами.  
  
### <a name="examples-decoding"></a>Примеры (декодирование)  
 В этом примере происходит возврат строки Table:Test:  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>См. также:  
 [Идентификаторы SQL Server в PowerShell](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell, поставщик](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
