---
title: Определение формата текста (драйвер для текстовых файлов) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00d20f8a6dd4d79b3100549d9286e7534bc8ce6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240379"
---
# <a name="defining-text-format-text-file-driver"></a>Определение формата текста (драйвер для текстовых файлов)
Если используется драйвер для текстовых, можно использовать **определение формата текста** диалоговое окно для определения формата для столбцов в выбранном файле. Это диалоговое окно позволяет указать схему для каждой таблицы данных. Эта информация записывается в файл Schema.ini в каталоге источника данных. Для каждого каталога источника данных текста создается отдельный файл Schema.ini.  
  
> [!NOTE]  
>  Один и тот же формат файлов по умолчанию применяется для всех новых таблиц данных текста. Все файлы, созданные с помощью инструкции CREATE TABLE наследуют эти же по умолчанию формат значения, которые устанавливаются путем выбора значения формата файла в **определение формата текста** диалоговое окно с \<по умолчанию > выбранным в **Таблиц** списка. Драйвер для текстовых не изменяет формат существующего текстового файла в соответствии с форматом, определенные в этом диалоговом окне, но возвращает ошибку, если он использует формат, например при попытке получения данных из текстового файла.  
  
 Следующие пункты доступны в **определение формата текста** диалоговое окно:  
  
|Параметр|Сведения|  
|------------|-----------------|  
|**Добавить**|Добавляет столбец, используя значения в **тип данных**, **имя**, и **ширины** из диалогового окна, и если применимо, разделитель компонентов даты значение Schema.ini.|  
|**Символы**|**ANSI** или **OEM**. OEM указывает набор символов, не удовлетворяющую стандарту ANSI. По умолчанию используется OEM Если формат элемента, выбранного в **таблиц** списка не был определен ранее, это диалоговое окно.|  
|**Заголовок с именами столбцов**|Указывает, являются ли столбцы первой строки выбранной таблицы для использования в качестве имен столбцов. Либо **TRUE** или **FALSE**. По умолчанию используется значение FALSE, если формат элемента, выбранного в **таблиц** списка не был определен ранее, это диалоговое окно.|  
|**Столбцы**|Список имен столбцов для каждого столбца в выбранной таблице. Порядок столбцов соответствует порядку столбцов в таблице. Этот список доступен в том случае, если файл был выбран в **таблиц** списка.|  
|**Тип данных**|Может быть бит, BYTE, CHAR, валюты, даты, число с плавающей запятой, целое число, LONGCHAR, SHORT или ОДНИМ. Типы данных даты может быть в следующих форматах: «дд ммм гг», «мм дд гг», «мм дд гг», «гггг мм дд» или «гггг мм дд». «мм» обозначает числа месяцев; «mmm» обозначает буквы месяцев.|  
|**разделитель**|Указывает символ пользовательский разделитель, используемый для разделения столбцов. Включена, когда **разделители** выбран формат. Разделитель может быть только один символ и двойные кавычки ("") не может использоваться в качестве разделителя. (Разделитель не может быть указано в шестнадцатеричном или десятичном формате).|  
|**Формат**|С разделителями или фиксированной длины. Если с разделителями, указывает тип разделителя: запятыми (CSV), вкладки или специальный символ (настраиваемая). По умолчанию используется **CSV-ФАЙЛ с разделителями** Если формат элемента, выбранного в **таблиц** списка не был определен ранее, это диалоговое окно.<br /><br /> Если **формат** является фиксированной длины и **заголовок с именами столбцов** имеет значение TRUE, первая строка должна быть с разделителями запятыми.|  
|**Прогноз**|Автоматически создает значения данных столбца типа, имя и ширины для столбцов в выбранной таблице путем сканирования содержимого таблицы в соответствии с **формат** поле выбора. Включается, если формат таблицы в качестве разделителя используется. Любые ранее определенные столбцы в **столбцы** списка удаляются и заменяются новыми записями. Если **заголовок с именами столбцов** — не выбран, имена столбцов создаются автоматически как «F1», «F2» и т. д. Значение по умолчанию не отображается в **тип данных** поле.<br /><br /> Эта функция работает только на столбцы, которые являются превышает 64 513 байт.|  
|**Изменение**|Изменяет выбранный столбец, используя значения в **тип данных**, **имя**, и **ширины**.|  
|**Name**|Отображает имя выбранного столбца. Может использоваться для указания имени столбца для существующего или нового столбца.<br /><br /> Если **заголовок с именами столбцов** имеет значение TRUE, в столбце имени отображается учитывается.|  
|**Удалить**|Удаление выбранного столбца.|  
|**Строк для просмотра**|Число строк, программа установки или драйвер при настройке столбцов и типов данных столбцов, на основе существующих данных.<br /><br /> Можно ввести число от 1 до 32767 для числа строк для сканирования. По умолчанию используется значение 25, если формат элемента, выбранного в **таблиц** списка не был определен ранее, это диалоговое окно. (Лежащее за пределами ограничения возвратит ошибку.)|  
|**Таблицы**|Содержит список всех файлов в каталоге, выбранного в **Установка текстового** диалоговое окно, которое соответствует списку расширения.<br /><br /> Когда \<по умолчанию > выбран, и одно из следующих является true, значения атрибутов таблицы в **таблиц** группы записываются в файл Schema.ini (без других элементов в Schema.ini, менялись):<br /><br /> -Нет не Schema.ini в указанном каталоге.<br />— Файл Schema.ini существует, но нет раздела в Schema.ini для одного из текстовых файлов (с определенным расширением) в каталоге.<br />-Раздел в текстовый файл существует в Schema.ini, но текст ответа отсутствует.<br /><br /> Когда \<по умолчанию > выбран, **столбцы** группа отключена.|  
|**Width**|Для столбцов CHAR и LONGCHAR можно изменить ширину столбца. Ширина по умолчанию используется значение 1, если формат элемента, выбранного в **таблиц** списка не был определен ранее, это диалоговое окно.<br /><br /> Для других типов данных ширины элемент управления отключен и значение не отображается.|
