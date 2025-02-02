---
title: Команда SQL - DELETE | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dac94d8bfb0e2bc0ab91f6a18e6f18606481b112
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198576"
---
# <a name="delete---sql-command"></a>DELETE (команда SQL)
Помечает записи для удаления.  
  
 Драйвер ODBC для Visual FoxPro поддерживает собственный синтаксис языка Visual FoxPro для этой команды. Сведения см. в разделе "Примечания".  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Аргументы  
 ИЗ [ *DatabaseName!*] *TableName*  
 Указывает таблицу, в котором записи помечены для удаления.  
  
 *Имя базы данных!* Задает имя базы данных, содержащую таблицу, в том случае, если содержащий база данных не является база данных, указанная с источником данных. Необходимо включить имя базы данных, содержащую таблицу, в том случае, если база данных не является база данных, указанная с источником данных. Включить в разделители восклицательный знак (!), после имени базы данных и перед именем таблицы.  
  
 ГДЕ *FilterCondition1*[AND &#124; или *FilterCondition2*...]  
 Указывает, что Visual FoxPro пометить определенные записи для удаления.  
  
 *FilterCondition* указывает критерии, которые должны удовлетворять помечена для удаления записи. Можно включить столько условий фильтрации, сколько требуется, подключая их к AND или оператор OR. Оператор NOT можно использовать и для отмены значения логического выражения или воспользоваться **пустой**() на наличие пустого поля.  
  
## <a name="remarks"></a>Примечания  
 Если НАБОР УДАЛЕН имеет значение ON, помеченные на удаление записи игнорируются все команды, включающие области.  
  
 Удаление — SQL использует блокировки записей, когда несколько записей для удаления в таблицах открыт для общего доступа. Это уменьшает конфликты записи в многопользовательских ситуациях, но может привести к снижению производительности. Для достижения максимальной производительности откройте таблицу для монопольного использования.  
  
## <a name="driver-remarks"></a>Драйвер "Примечания"  
 Когда приложение отправляет инструкцию ODBC SQL DELETE к источнику данных, драйвер ODBC для Visual FoxPro преобразует команды в команды Visual FoxPro DELETE без трансляции.  
  
## <a name="see-also"></a>См. также  
 [Команда SET DELETED](../../odbc/microsoft/set-deleted-command.md)
