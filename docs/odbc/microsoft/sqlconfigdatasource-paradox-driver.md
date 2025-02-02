---
title: SQLConfigDataSource (драйвер для Paradox) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad9c944af33da86e0d4f85769288f4ab7b6c369f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62665346"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (драйвер для Paradox)
> [!NOTE]  
>  Здесь приведены сведения об особенностях драйвер для Paradox. Общие сведения об этой функции см. в соответствующем разделе [Справочник по API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLConfigDataSource** функцию, которая используется для добавления, изменения или удаления источника данных динамически используются следующие ключевые слова.  
  
|Ключевое слово|Описание|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Последовательность, в которой сортируется поля.<br /><br /> Если используется драйвер для Paradox, последовательность может быть ASCII (по умолчанию), международный, Шведский финский или Norwegian-Danish.<br /><br /> Таким образом задается один и тот же параметр как **упорядочивания последовательности** в диалоговом окне программы установки.|  
|DBQ|Имя файла базы данных.<br /><br /> Таким образом задается один и тот же параметр как **базы данных** в диалоговом окне программы установки.|  
|ЕГО ЗНАЧЕНИЯ|Строка пути к каталогу.|  
|DESCRIPTION|Описание данных в источнике данных.<br /><br /> Таким образом задается один и тот же параметр как **описание** в диалоговом окне программы установки.|  
|DRIVER|Строка пути к DLL-Библиотека драйвера.|  
|DRIVERID|Целочисленный идентификатор для драйвера.<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|ЭКСКЛЮЗИВНЫЕ|Определяет, будет открыт в монопольном режиме (открыт только один пользователь одновременно) базы данных или общем режиме (открыт более чем одним пользователем одновременно). Может быть true (монопольный режим) или false (режиме общего доступа).<br /><br /> Таким образом задается один и тот же параметр как **эксклюзивные** в диалоговом окне программы установки.|  
|FIL|Тип для Paradox файла 3.x, Paradox 4.x или Paradox 5.x|  
|ТИП ФАЙЛА|Тип файла для драйвера Text (текст).|  
|PAGETIMEOUT|Указывает период времени, в десятых долях секунды страницы (если не используется), остаются в буфере до их удаления. Значение по умолчанию — 600 десятые доли секунды (60 секунд). Обратите внимание на то, что этот параметр применяется ко всем источникам данных, использующие драйвер ODBC.<br /><br /> Таким образом задается один и тот же параметр как **время ожидания страницы** в диалоговом окне программы установки.|  
|PARADOXNETPATH|Полный путь к каталогу, содержащему Paradox блокировки базы данных, так как она содержит файл PDOXUSRS.net (в Paradox 4. *x*) или файл PARADOX.net (на Paradox 5. *x*). Если каталог не содержит один из этих файлов, драйвер для Paradox создаст его. Сведения об этих файлах см. в документации для Paradox.<br /><br /> Прежде чем могут быть выбраны в сетевую папку, необходимо ввести имя пользователя для Paradox.<br /><br /> Таким образом задается один и тот же параметр как **выберите сетевую папку** в диалоговом окне программы установки.|  
|PARADOXNETSTYLE|Для драйвера для Paradox, сети, доступ к стиль, используемый при доступе к данным Paradox: либо «3.x» для Paradox 3. *x* или «4» для Paradox 4. *x* или 5. *x*. Можно присвоить «3.x» или «4» Если версия Paradox 4. *x* или 5. *x*; Если версия Paradox 3. *x*, необходимо выбрать «3.x».<br /><br /> Таким образом задается один и тот же параметр как **Net стиля** в диалоговом окне программы установки.|  
|PARADOXUSERNAME|Для драйвера для Paradox, имя пользователя для Paradox.<br /><br /> Таким образом задается один и тот же параметр как **имя пользователя** в диалоговом окне программы установки.|  
|PWD|Пароль.<br /><br /> Необязательное ключевое слово и никогда не записываются в файл с помощью драйвера. Он используется в вызове **SQLDriverConnect** Paradox файлов, защищенные паролем. Пароль, используемый будет применяться при каждом открытии таблицы. Если пароль не передается в строке подключения, пароль не будет установлено для этой таблицы. Если таблицы имеют разные пароли, более одного нельзя открывать в том же сеансе, а также можно объединить таблицы.|  
|READONLY|Значение TRUE, чтобы сделать файл доступным только для чтения; Значение FALSE, чтобы сделать файл не только для чтения.<br /><br /> Таким образом задается один и тот же параметр как **только для чтения** в диалоговом окне программы установки.|  
|ПОТОКИ|Число фоновых потоков для ядра, которые будут использоваться. Это значение равно 3 и не может быть изменено.<br /><br /> Таким образом задается один и тот же параметр как **потоков** в диалоговом окне программы установки.|
