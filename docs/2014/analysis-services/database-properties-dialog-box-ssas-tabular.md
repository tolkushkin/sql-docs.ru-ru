---
title: Базы данных диалоговое окно «Свойства» (службы SSAS — табличные) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.DatabaseProperties.f1
ms.assetid: 0f0ec02f-7b55-40ea-8a04-ed0deb1efd7a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8361508d678e407be9bed6eb18e8c221364daf61
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082354"
---
# <a name="database-properties-dialog-box-ssas---tabular"></a>Диалоговое окно «Свойства базы данных» (службы SSAS — табличные модели)
  Это диалоговое окно содержит отметки времени и другие описательные сведения, а также настраиваемые свойства, которые определяют, использует ли база данных кэшированные данные. Другие настраиваемые свойства включают изменение имени базы данных и задание параметров олицетворения.  
  
## <a name="options"></a>Параметры  
  
|Термин|Определение|  
|----------|----------------|  
|**Name**|**Имя** — это имя базы данных, которое уникальным образом идентифицирует базу данных на сервере. При изменении имени базы данных нужно учитывать влияние этого на отчеты и клиентские приложения, использующие текущее имя в существующих строках подключения. Чтобы избежать ошибок отказа в доступе, потребуется обновить строки подключения в существующих отчетах. Кроме того, табличная модель, которая является источником этой базы данных, скорее всего, использует исходное имя. Рекомендуется обновить свойства развертывания базы данных в модели, чтобы последующие обновления модели публиковались в соответствующей базе данных.|  
|**Идентификатор**|Отображает идентификатор базы данных.|  
|**Описание**|Введите новое описание базы данных вместо прежнего.|  
|**Отметка времени создания**|Отображает дату и время создания базы данных.|  
|**Последнее обновление схемы**|Отображает дату и время последнего обновления метаданных для базы данных.|  
|**Последнее обновление**|Отображает дату и время последнего обновления данных для базы данных.|  
|**Режим чтения и записи**|Это свойство, доступное только для чтения, однако его можно изменить с помощью последовательности команд **Detach** и **Attach** , так как это свойство является параметром команды **Attach** . Дополнительные сведения см. в разделе [Режимы ReadWriteModes базы данных](multidimensional-models/database-readwritemodes.md).|  
|**DirectQueryMode**|Указывает, использует ли база данных только хранение во внутренней памяти (без сохранения на диске), только хранение на диске или их сочетание. Допустимые значения — InMemory, DirectQuery, InMemoryWithDirectQuery (обычно при сохранении на диск с использованием разбиения на страницы) или DirectQueryWithInMemory (обычно при сохранении на диск с использованием хранения во внутренней памяти). Дополнительные сведения см. в разделе [сценарии развертывания DirectQuery &#40;табличные службы SSAS&#41;](directquery-deployment-scenarios-ssas-tabular.md).|  
|**Сведения об олицетворении источника данных**|Указывает учетную запись олицетворения, которая используется для подключений к базам данных во время обработки или обновления данных в локальных или удаленных секциях, запросов к реляционному хранилищу данных (через DirectQuery), внешних привязок и синхронизации баз данных между получателем и источником.<br /><br /> Допустимые значения включают учетную запись служб Analysis Services или конкретный набор учетных данных Windows. Не следует задавать параметр **Использовать учетные данные текущего пользователя**. Этот параметр учетных данных не поддерживается для базы данных табличной модели.|  
|**Последняя обработка**|Отображает дату и время последней обработки базы данных.|  
|**Предполагаемый размер**|Отображает предполагаемый размер базы данных.|  
|**Место хранения**|Указывает расположение базы данных. Если база данных находится в каталоге данных по умолчанию, это значение будет пустым.|  
  
  
