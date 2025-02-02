---
title: Пользовательские свойства ADO NET | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e062a9ab-1e6b-4061-845a-4f8a0552b09d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b1ff09c90aece19ea306ec91b8d5cb0d95da937c
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727233"
---
# <a name="ado-net-custom-properties"></a>Пользовательские свойства ADO NET

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Пользовательские свойства источника**  
  
 Источник «ADO NET» обладает как пользовательскими свойствами, так и свойствами, общими для всех компонентов потока данных.  
  
 В следующей таблице описаны пользовательские свойства источника «ADO NET». Все свойства доступны для чтения и записи.  
  
|Имя свойства|Тип данных|Описание|  
|-------------------|---------------|-----------------|  
|CommandTimeout|String|Задает число секунд до истечения времени ожидания команды SQL. Значение 0 означает, что время выполнения команды не ограничено.|  
|SqlCommand|String|Инструкция SQL, используемая источником «ADO NET» для извлечения данных.<br /><br /> При загрузке пакета можно динамически обновлять это свойство инструкцией SQL, которая будет использована источником «ADO NET». Дополнительные сведения см. в разделах [Выражения служб Integration Services (SSIS)](../../integration-services/expressions/integration-services-ssis-expressions.md) и [Использование выражений свойств в пакетах](../../integration-services/expressions/use-property-expressions-in-packages.md).|  
|AllowImplicitStringConversion|Логическое значение|Значение, указывающее, происходят ли следующие события.<br /><br /> — Отмена формирования ошибки проверки в случае несоответствия типов внешних метаданных и типов выходных столбцов, являющихся строковыми (DT_WSTR или DT_NTEXT).<br /><br /> — Неявное преобразование типов внешних метаданных к строковому типу данных, используемому в выходном столбце.<br /><br /> <br /><br /> Значение по умолчанию — TRUE.<br /><br /> Дополнительные сведения см. в статье [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).|  
  
 Выход и выходные столбцы источника «ADO NET» не имеют пользовательских свойств.  
  
 Дополнительные сведения см. в статье [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Пользовательские свойства назначений**  
  
 Назначение [!INCLUDE[vstecado](../../includes/vstecado-md.md)] обладает как пользовательскими свойствами, так и свойствами, общими для всех компонентов потока данных.  
  
 В следующей таблице описаны пользовательские свойства назначения « [!INCLUDE[vstecado](../../includes/vstecado-md.md)] ». Все свойства доступны для чтения и записи. Эти свойства недоступны в диалоговом окне **Редактор назначения «ADO.NET»**, однако их можно установить при помощи окна **Расширенный редактор**.  
  
|Свойство|Тип данных|Описание|  
|--------------|---------------|-----------------|  
|BatchSize|Целочисленный|Количество строк в пакете, отправленном серверу. Значение **0** означает, что размер пакета соответствует размеру внутреннего буфера. Значение этого свойства по умолчанию равно **0**.|  
|CommandTimeOut|Целочисленный|Максимальное время ожидания в секундах, в течение которого может выполняться команда SQL. Значение **0** указывает на бесконечное время работы. Значение этого свойства по умолчанию равно **0**.|  
|TableOrViewName|String|Имя целевой таблицы или представления.|  
  
 Дополнительные сведения см. в статье [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md).  
  
## <a name="see-also"></a>См. также:  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
