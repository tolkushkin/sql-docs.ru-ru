---
title: ИНДЕКС команды | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 864f6fa78ab1ef23b7db3a0be4c85738b95ea72d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471262"
---
# <a name="index-command"></a>Команда INDEX
Создает файл индекса для отображения и доступ к записям таблицы в логическом порядке.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>Аргументы  
 *eExpression*  
 Задает выражение индекса, которое может содержать имя поля или поля из текущей таблицы. Ключ индекса, основанное на выражении индекс создается в файле индекса для каждой записи в таблице. Visual FoxPro использует эти ключи для отображения и доступ к записям в таблице.  
  
> [!NOTE]  
>  Несмотря на то, что не рекомендуется, *eExpression* также может быть переменной памяти, элемент массива или поле или выражение поля из таблицы в другой рабочей области. MEMO поля не может использоваться только в выражениях файл индекса; они должны быть объединены с другими символьных выражений. Если вы обращаетесь в индекс, содержащий переменную или поле, которое больше не существует или не удается найти, Visual FoxPro выдает сообщение об ошибке.  
  
 При попытке создать индекс с ключом, который меняется длина ключа дополняются пробелами. Ключи индекса переменной длины не поддерживаются в Visual FoxPro.  
  
 Имеется возможность создать ключ индекса с нулевой длины. Например ключ индекса нулевой длины создается при выражение индекса является подстрокой memo пустые поля. Ключ индекса нулевой длины выдает сообщение об ошибке. Когда Visual FoxPro создает индекс, то она оценивает полей в первой записи в таблице. Если поле пусто, может потребоваться ввести некоторые временные данные в поле первой записи для предотвращения ключ индекса с нулевой длиной.  
  
 Чтобы *IDXFileName*  
 Создает файл .idx индекса. Индекс будет использовано .idx расширение по умолчанию.  
  
 ТЕГ *TagName*[OF *CDXFileName*]  
 Создает файл составного индекса. Файл составного индекса является файлом один индекс, который состоит из произвольного числа отдельных тегов (записи индекса). Каждый тег идентифицируется по его уникальное имя тега. Имена тегов должны начинаться с буквы или символа подчеркивания и может содержать любое сочетание до 10 буквы, цифры или символы подчеркивания. Число тегов в файле составного индекса ограничивается только доступной памяти и места на диске.  
  
 Файлы ввода нескольких составного индекса всегда являются compact. Нет необходимости включать COMPACT при создании файла составного индекса. Имена файлов комплексной индекса, получают расширение .cdx.  
  
 Можно создать два типа файлов комплексной индекса: структурные и nonstructural.  
  
 **Структурные составные файлы индекса** можно создать файл структурные составного индекса с ТЕГОМ *TagName* , исключив необязательно OF *CDXFileName* предложение. Файл структуры составного индекса всегда имеет такое же базовое имя таблицы и автоматически открывается при открытии таблицы.  
  
 **Nonstructural составные файлы индекса** можно создать файл nonstructural составной индекс, включив OF *CDXFileName* после ТЕГА *TagName*. В отличие от файла структурные составной индекс nonstructural составного индекса необходимо явно открыть файл с предложением индекс используется.  
  
 Если файл составного индекса уже создается и открывается, при выполнении ИНДЕКСА с ТЕГОМ *TagName* добавляет тег в файл составного индекса.  
  
 ДЛЯ *lExpression*  
 Задает условие, при котором только записи, которые удовлетворяют критерию фильтрации *lExpression* доступны для просмотра и доступа; ключи индекса создаются в файле индекс только те записи, отвечающих выражению для фильтра.  
  
 Технологии Visual FoxPro технологию Rushmore оптимизирует индекс... ДЛЯ *lExpression* команды, если *lExpression* оптимизируемыми выражение. Для наилучшей производительности используйте оптимизируемые выражения в предложении FOR.  
  
 COMPACT  
 Создает файл compact .idx.  
  
 ПО ВОЗРАСТАНИЮ  
 Указывает порядок сортировки по возрастанию .cdx файла. По умолчанию теги .cdx создаются в порядке возрастания. (Напоминаем заказа файл индекса можно установить по ВОЗРАСТАНИЮ.) Таблицы могут быть проиндексированы, включив по УБЫВАНИЮ в обратном порядке.  
  
 ПО УБЫВАНИЮ  
 Задает для файла .cdx по убыванию. При создании .idx файлы индекса, не может включать по УБЫВАНИЮ.  
  
 UNIQUE  
 Указывает, что только обнаружил со значением ключа конкретный индекс первой записи будут включены в файл .idx или тег .cdx. UNIQUE можно использовать для предотвращения отображения или доступа к повторяющиеся записи. Все записи, добавленные с помощью повторяющиеся ключи индекса, исключаются из файла индекса. С помощью параметра УНИКАЛЬНЫЙ индекс идентична выполнение SET UNIQUE ON перед выдачей REINDEX или ИНДЕКСА.  
  
 УНИКАЛЬНЫЙ индекс или индекс тег является активным и изменении повторяющиеся записи способом, который изменяет его ключ индекса, индекс или индекс тег будет обновлено. Тем не менее нельзя обращаться или отображаться, только если переиндексации файл с помощью REINDEX следующей повторяющиеся записи с исходного ключа индекса.  
  
 КАНДИДАТОВ  
 Создает тег структуры индекса кандидатов. Ключевое слово КАНДИДАТ может быть включено только в том случае, при создании тег структуры индекса; в противном случае Visual FoxPro выдает сообщение об ошибке.  
  
 Тег индекс кандидата предотвращает повторяющиеся значения в поле или сочетание полей, указанных в выражении индекса *eExpression*. Термин *кандидата* ссылается на тип индекса; из-за возможных кандидатур индексов избежать повторяющихся значений, они как «потенциального» могут использоваться в качестве первичного индекса.  
  
 Visual FoxPro приводит к ошибке при создании индекса тег кандидатом для поля или сочетание полей, который уже содержит повторяющиеся значения.  
  
 АДДИТИВНАЯ  
 Позволяет открыть любые файлы, ранее открывавшихся индекса. Если вы пропустите предложение АДДИТИВНЫЙ при создании файла индекса или файлы для таблицы с ИНДЕКСОМ, закрываются все ранее открытые индекса файлы (за исключением структурные составной индекс).  
  
## <a name="remarks"></a>Примечания  
 Записи в таблице с индексным файлом отображаются и в порядке, указанном выражение индекса. Физический порядок записей в таблице не изменяется с индексным файлом.  
  
## <a name="index-types"></a>Типы индексов  
 Visual FoxPro позволяет создавать два типа файлов индекса:  
  
-   Составные файлы .cdx индекс, содержащий несколько записей индекса, называемых тегами  
  
-   файлы индекса .idx, содержащие одну запись индекса  
  
 Можно также создать файл структурные составной индекс, который будет автоматически открыт с таблицей.  
  
> [!NOTE]  
>  Поскольку файлы структурные составного индекса автоматически открываются при открытии таблицы, они тип предпочтительный индекса.  
  
 Включить БЫСТРОЕ Создание compact .idx файлы индекса. Файлов комплексной индекса всегда являются compact.  
  
## <a name="index-order-and-updating"></a>Порядок индексов и обновление  
 Только один индекс файл (главный индекс) или тег (master) управляет порядком, в котором отображаются или получить доступ к таблице. Некоторые команды (например, поиск), используйте главный индекс файла или тег для поиска записей. Тем не менее, все открытые .idx и файлы индекса .cdx обновляются при внесении изменений в таблицу.  
  
## <a name="user-defined-functions"></a>Определяемые пользователем функции  
 Несмотря на то, что индексное выражение может содержать определяемой пользователем функции, определяемые пользователем функции не следует использовать в выражении индекса. Определяемые пользователем функции в выражении индекса увеличить время, необходимое для создания или обновления индекса. Кроме того обновления индекса не могут возникнуть при использовании определяемую пользователем функцию для выражения индекса.  
  
 Если вы используете определяемую пользователем функцию в выражении индекса, Visual FoxPro должен иметь возможность найти определяемой пользователем функции. Когда Visual FoxPro создает индекс, выражение индекса сохраняется в файле индекса, но только ссылку на пользовательскую функцию включается в выражении индекса.  
  
## <a name="see-also"></a>См. также  
 [ALTER TABLE - команда SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Команда DELETE TAG](../../odbc/microsoft/delete-tag-command.md)   
 [Команда SET COLLATE](../../odbc/microsoft/set-collate-command.md)   
 [Команда SET UNIQUE](../../odbc/microsoft/set-unique-command.md)
