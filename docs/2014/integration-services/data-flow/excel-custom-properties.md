---
title: Пользовательские свойства Excel | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8d556a199b608659a9ceaaeb3b7036155886d6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827237"
---
# <a name="excel-custom-properties"></a>Пользовательские свойства Excel
  **Пользовательские свойства источника**  
  
 Источник «Excel» обладает как пользовательскими свойствами, так и свойствами, общими для всех компонентов потока данных.  
  
 В следующей таблице описаны пользовательские свойства источника «Excel». Все свойства доступны для чтения и записи.  
  
|Имя свойства|Тип данных|Описание|  
|-------------------|---------------|-----------------|  
|AccessMode|Целочисленный|Режим, используемый для доступа к базе данных. Возможные значения: **открытый набор строк**, **открытый набор строк из переменной**, `SQL Command`, и **команда SQL из переменной**. Значение по умолчанию: **Открытый набор строк**.|  
|CommandTimeout|Целочисленный|Время ожидания для выполнения команды (в секундах).  Значение 0 указывает на бесконечное время ожидания.<br /><br /> **Примечание** Это свойство недоступно в диалоговом окне **Редактор источника «Excel»**, однако его можно установить при помощи окна **Расширенный редактор**.|  
|OpenRowset|String|Имя объекта базы данных, используемого для открытия набора строк.|  
|OpenRowsetVariable|String|Переменная, содержащая имя объекта базы данных, используемого для открытия набора строк.|  
|ParameterMapping|String|Сопоставление между параметрами в команде SQL и переменными.|  
|SqlCommand|String|Команда SQL для выполнения.|  
|SqlCommandVariable|String|Переменная, содержащая команду SQL для выполнения.|  
  
 Вывод и выходные столбцы источника «Excel» не имеют пользовательских свойств.  
  
 Дополнительные сведения см. в статье [Excel Source](excel-source.md).  
  
 **Пользовательские свойства назначений**  
  
 Назначение «Excel» обладает как пользовательскими свойствами, так и свойствами, общими для всех компонентов потока данных.  
  
 В следующей таблице описаны пользовательские свойства назначения «Excel». Все свойства доступны для чтения и записи.  
  
|Имя свойства|Тип данных|Описание|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (перечисление)|Значение, указывающее, как назначение получает доступ к целевой базе данных.<br /><br /> Это свойство может принимать одно из следующих значений:<br /><br /> `OpenRowset` (0) — необходимо указать имя таблицы или представления.<br /><br /> `OpenRowset from Variable` (1) — необходимо указать имя переменной, которая содержит имя таблицы или представления.<br /><br /> `OpenRowset Using Fastload` (3) — необходимо указать имя таблицы или представления.<br /><br /> `OpenRowset Using Fastload from Variable` (4) — необходимо указать имя переменной, которая содержит имя таблицы или представления.<br /><br /> `SQL Command` (2) — необходимо указать инструкцию SQL.|  
|CommandTimeout|Целочисленный|Максимальное время ожидания в секундах, в течение которого может выполняться команда SQL. Значение **0** указывает на бесконечное время работы. Значение этого свойства по умолчанию равно **0**.<br /><br /> Примечание. Это свойство недоступно в **редакторе назначения "Excel"**, но его можно задать с помощью **расширенного редактора**.|  
|FastLoadKeepIdentity|Логическое значение|Значение, которое указывает, следует ли при загрузке данных копировать значения идентификаторов. Это свойство доступно только при использовании одного из параметров быстрой загрузки. Это свойство имеет значение по умолчанию **False**.|  
|FastLoadKeepNulls|Логическое значение|Значение параметра указывает, следует ли при загрузке данных копировать значения NULL. Это свойство доступно только при использовании одного из параметров быстрой загрузки. Это свойство имеет значение по умолчанию **False**.|  
|FastLoadMaxInsertCommitSize|Целочисленный|Это значение указывает размер пакетов, который назначение «Excel» пытается фиксировать во время операций быстрой загрузки. Значение по умолчанию ― **2147483647**. Значение **0** указывает, что используется единая операция фиксации после обработки всех строк.|  
|FastLoadOptions|String|Коллекция параметров быстрой загрузки. К параметрам быстрой загрузки относятся параметры блокировки таблиц и проверки ограничений. Можно указать один, оба или не указывать ни одного параметра.<br /><br /> Примечание. Некоторые свойства недоступны в **редакторе назначения "Excel"**, но их можно задать с помощью **расширенного редактора**.|  
|OpenRowset|String|Если свойство AccessMode имеет `OpenRowset`, имя таблицы или представления, к которому обращается назначение Excel.|  
|OpenRowsetVariable|String|Если свойство AccessMode имеет `OpenRowset from Variable`, имя переменной, содержащей имя таблицы или представления, к которому обращается назначение Excel.|  
|SqlCommand|String|Если свойство AccessMode имеет `SQL Command`, инструкции Transact-SQL, который использует назначение «Excel» для указания целевых столбцов для данных.|  
  
 У ввода и входных столбцов назначения «Excel» нет пользовательских свойств.  
  
 Дополнительные сведения см. в статье [Excel Destination](excel-destination.md).  
  
## <a name="see-also"></a>См. также:  
 [Common Properties](../common-properties.md)  
  
  
