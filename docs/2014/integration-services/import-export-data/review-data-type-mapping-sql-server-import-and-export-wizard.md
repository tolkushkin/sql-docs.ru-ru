---
title: Просмотр сопоставления типов данных (мастер импорта и экспорта SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.reviewissues.f1
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6472ff165894937d31366e47651ada64af38ae1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767946"
---
# <a name="review-data-type-mapping-sql-server-import-and-export-wizard"></a>Просмотр сопоставления типов данных (мастер импорта и экспорта SQL Server)
  Используйте **Просмотр сопоставления типов данных** страницу, чтобы просмотреть подробные сведения о преобразованиях типов данных, которые необходимо выполнить, чтобы сделать данные источника совместимыми с назначением мастера. Эти сведения включают в себя визуальные отличия преобразований, для которых ожидается успешное выполнение, от преобразований, которые могут вызвать ошибки или усечения. Для каждого преобразования можно указать, принимать ли предлагаемое мастером преобразование, а также способ обработки возможных ошибок.  
  
 Дополнительные сведения о работе этого мастера см. в разделе [Мастер импорта и экспорта SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Дополнительные сведения о параметрах запуска этого мастера и о разрешениях, необходимых для успешного запуска мастера, см. в разделе [запустить мастер экспорта и импорта SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Мастера импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предназначен для копирования данных из исходного расположения в целевое. Этот мастер может также создать целевую базу данных и целевые таблицы. Однако если нужно скопировать несколько баз данных, таблиц или других объектов базы данных, следует использовать мастер копирования баз данных. Дополнительные сведения см. в статье [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Параметры  
 Страница **Просмотр сопоставления типов данных** содержит список **Таблица** , список **Сопоставление типов данных** и параметры обработки ошибок.  
  
### <a name="table-list"></a>Список «Таблица»  
 В верхней части **Просмотр проблем с типами данных** страница **таблицы** список, таблиц для передачи из источника в место назначения. В следующей таблице описываются столбцы этого списка.  
  
|Столбец|Описание|  
|------------|-----------------|  
|Значок источника|Показывает вероятность успеха при преобразовании типа данных.<br /><br /> Значок в виде зеленого флажка указывает, что ожидается успешное выполнение всех преобразований типов данных в соответствующей таблице.<br /><br /> Желтый предупредительный значок указывает, что следует просмотреть планируемые к выполнению отдельные преобразования. Для этого выберите таблицу и просмотрите преобразования по отдельным столбцам в списке **Сопоставление типов данных** .<br /><br /> Красный значок ошибки указывает, что мастеру, скорее всего, не удастся выполнить некоторые преобразования в данной таблице.|  
|**Source**|Отображает имя исходной таблицы.|  
|Значок назначения|Указывает, существует ли в данный момент назначение или оно будет создано мастером.<br /><br /> Значок таблицы означает, что назначение является существующей таблицей.<br /><br /> Значок таблицы с солнечными лучами означает, что назначение является новой таблицей, которую создаст мастер.|  
|**Назначение**|Отображает имя целевой таблицы.|  
  
 Чтобы просмотреть сведения об отдельной таблицы преобразования, выберите таблицу, в этом **таблицы** сетки. Сведения о преобразовании для выбранной таблицы появятся в столбцах сетки **Сопоставление типов данных** в нижней части страницы.  
  
### <a name="data-type-mapping-list"></a>Список «Сопоставление типов данных»  
 В нижней части **Просмотр проблем с типами данных** страница **сопоставление типов данных** списка. Здесь отображаются подробные сведения о преобразовании столбцов таблицы, выбранной в списке **Таблица** . В следующей таблице описываются столбцы этого списка.  
  
|Столбец|Описание|  
|------------|-----------------|  
|Значок преобразования|Показывает вероятность успеха при преобразовании типа данных.<br /><br /> Значок в виде зеленого флажка указывает, что ожидается успешное выполнение преобразования типа данных в соответствующем столбце.<br /><br /> Желтый предупредительный значок указывает, что следует просмотреть планируемое к выполнению преобразование. Для этого дважды щелкните столбец, чтобы открыть диалоговое окно **Сведения о преобразовании столбца** .<br /><br /> Красный значок ошибки указывает, что мастеру, скорее всего, не удастся выполнить преобразование.|  
|**Исходный столбец**|Отображает имя исходного столбца.|  
|**Исходный тип**|Отображает тип данных исходного столбца.|  
|**Целевой столбец**|Отображает имя целевого столбца.|  
|**Тип назначения**|Отображает тип данных целевого столбца.|  
|**Преобразовать**|Указывает, следует ли продолжать планируемое преобразование.<br /><br /> Чтобы продолжить планируемое преобразование, установите этот флажок.<br /><br /> Чтобы отменить преобразование типа данных, снимите флажок.|  
|**В случае ошибки**|Укажите порядок обработки ошибок мастером:<br /><br /> Используйте **на ошибки (используется глобально)** параметр.<br /><br /> завершить с ошибкой и прекратить процесс импорта или экспорта;<br /><br /> пропустить ошибку.|  
|**В случае усечения**|Укажите порядок обработки усечений мастером:<br /><br /> Используйте **в случае усечения (используется глобально)** параметр.<br /><br /> завершить работу с ошибкой и прекратить процесс импорта или экспорта;<br /><br /> пропустить усечение.|  
  
 Чтобы просмотреть подробные сведения о преобразовании определенного столбца данных, дважды щелкните какую-либо строку в списке. Откроется диалоговое окно **Сведения о преобразовании столбца** с более подробными сведениями о преобразовании столбца.  
  
### <a name="error-handling-options"></a>Параметры обработки ошибок  
 **В случае ошибки (используется глобально)**  
 Укажите порядок обработки ошибок мастером:  
  
-   завершить с ошибкой и прекратить процесс импорта или экспорта;  
  
-   пропустить ошибку и продолжить процесс импорта или экспорта.  
  
 Эта настройка применяется ко всем преобразованиям с выбранным параметром **Использовать глобально** в столбце **В случае ошибки** списка **Сопоставление типов данных** .  
  
 **В случае усечения (используется глобально)**  
 Укажите порядок обработки усечений мастером:  
  
-   завершить с ошибкой и прекратить процесс импорта или экспорта;  
  
-   пропустить усечение и продолжить процесс импорта или экспорта.  
  
 Эта настройка применяется ко всем преобразованиям с выбранным параметром **Использовать глобально** в столбце **В случае усечения** списка **Сопоставление типов данных** .  
  
  
