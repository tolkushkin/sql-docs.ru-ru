---
title: Диалоговое окно «Свойства соединения» (службы SSAS — табличные) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26fa80cc770d4bee9163ec18c21b35bd8c807bde
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086984"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>Диалоговое окно «Свойства соединения» (SSAS — табличные)
  С помощью этой страницы в среде SQL Server Management Studio можно просматривать или изменять свойства соединения с источником данных, используемым базой данных табличной модели.  
  
 Это диалоговое окно содержит отметки времени и другие описательные сведения, а также настраиваемые свойства, которые определяют характеристики соединения.  
  
## <a name="options"></a>Параметры  
  
|Термин|Определение|  
|----------|----------------|  
|**Name**|Указывает имя источника данных.|  
|**Идентификатор**|Позволяет отобразить идентификатор объекта источника данных.|  
|**Описание**|Позволяет отобразить описание объекта источника данных.|  
|**Отметка времени создания**|Отображает дату и время создания базы данных.|  
|**Последнее обновление схемы**|Отображает дату и время последнего обновления метаданных для базы данных.|  
|**Строка подключения**|Отображает строку подключения, которая используется для подключения к источнику данных, предоставляющему данные в модель.|  
|**Максимальное число подключений**|Задает максимальное количество клиентских соединений с этой базой данных.|  
|**Изоляция**|Допустимые значения — ReadCommitted или Snapshot. Дополнительные сведения см. в разделе [Элемент Isolation (ASSL)](https://docs.microsoft.com/bi-reference/assl/properties/isolation-element-assl).|  
|**Время ожидания запроса**|Задает время в секундах, представляющее время ожидания попытки извлечения данных.|  
|**Управляемый поставщик**|Указывает имя управляемого поставщика. Если соединение с источником данных использует собственный поставщик данных OLE DB, это значение остается пустым.|  
|**Сведения об олицетворении**|Указывает учетную запись олицетворения, которая используется для подключений к базе данных во время обработки или обновления данных, запросов к реляционному хранилищу данных (через DirectQuery), внешних привязок, удаленных секций и синхронизации базы данных между получателем и источником.<br /><br /> Допустимые значения включают учетную запись служб Analysis Services или конкретный набор учетных данных Windows. Не следует задавать параметр **Использовать учетные данные текущего пользователя** или **Наследовать**. Эти параметры учетных данных не поддерживаются для базы данных табличной модели.|  
  
  
