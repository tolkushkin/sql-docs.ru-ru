---
title: Обработка ошибок в данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data conversion errors [Integration Services]
- errors [Integration Services], data flow components
- lookups [Integration Services]
- errors [Integration Services]
- errors [Integration Services], data flow outputs
- error outputs [Integration Services]
- data flow [Integration Services], errors
- expressions [Integration Services], errors
ms.assetid: c61667b4-25cb-4d45-a52f-a733e32863f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b5a98877e04a077bf1bb1c0c527500f3102b862
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827153"
---
# <a name="error-handling-in-data"></a>Обработка ошибок в данных
  Если компонент потока данных применяет преобразование к данным столбца, выделяет данные из источников или загружает данные в назначения, то может возникнуть ошибка. Ошибки часто возникают из-за непредвиденных значений данных. Например, преобразование данных не выполняется, так как столбец вместо числа содержит строку; вставка в столбец базы данных не выполняется, потому что данные имеют тип даты, а столбец содержит числовые данные; наконец, результат выражения не может быть определен, так как значение столбца равно нулю, поэтому математическая операция недопустима.  
  
 Обычно происходят ошибки следующих категорий.  
  
-   Ошибки преобразования данных, возникающие, если преобразование приводит к потере значащих разрядов, потере незначащих разрядов или к усечению строк. Ошибки преобразования данных также возникают, если запрашиваемое преобразование не поддерживается.  
  
-   Ошибки оценки выражений, возникающие, если выражения, оцениваемые во время исполнения, выполняют недействительные операции или становятся синтаксически неправильными из-за потери данных или их неверных значений данных.  
  
-   Ошибки поиска, возникающие, если операция поиска не может обнаружить соответствия в таблице уточняющих запросов.  
  
 Многие компоненты потока данных поддерживают выходы ошибок, которые позволяют пользователю контролировать обработку ошибок компонентом на уровне строки как во входных, так и в выходных данных. Заданием параметров на отдельных столбцах на входе или выходе определяется, какие действия выполняет компонент при возникновении усечения или ошибки. Например, можно указать, что компонент завершается ошибкой, если имя клиента усечено, но пропускает ошибки в другом столбце, содержащем менее важные данные.  
  
 Вывод ошибок может быть связан с входными данными другого преобразования или загружен в назначение, отличное от назначения выхода без ошибок. Например, выход ошибки может быть привязан к преобразованию «Производный столбец», которое формирует строку для пустого столбца.  
  
 На следующей диаграмме показан простой поток данных, содержащий выход ошибок.  
  
 ![Поток данных с выводом ошибок](../media/mw-dts-11.gif "Поток данных с выводом ошибок")  
  
 В дополнение к столбцам данных выход ошибок включает в себя столбцы **ErrorCode** и **ErrorColumn** . Столбец **ErrorCode** идентифицирует ошибку, а столбец **ErrorColumn** содержит идентификатор журнала обращений и преобразований столбца с ошибкой. Чтобы просмотреть метаданные этих столбцов, щелкните путь, соединяющий выход ошибок со следующим компонентом потока данных. В некоторых случаях значение столбца **ErrorColumn** устанавливается в ноль. Это происходит, если условие ошибки влияет на целую строку, а не один столбец. Например, если преобразование «Уточняющий запрос» завершилось неудачно.  
  
 Дополнительные сведения см. в статьях [Поток данных](data-flow.md) и [Пути служб Integration Services](integration-services-paths.md).  
  
 Список ошибок, предупреждений и других сообщений служб Integration Services см. в разделе [Integration Services Error and Message Reference](../integration-services-error-and-message-reference.md).  
  
## <a name="error-and-truncation-options"></a>Параметры ошибок и усечения  
 Ошибки разделяются на две категории: ошибки и усечения. Ошибка указывает на определенную неполадку и формирует результат NULL. Такие ошибки могут включать в себя ошибки преобразования данных или ошибки оценки выражений. Например, попытка преобразовать в число строку, содержащую буквенные символы, вызывает ошибку. Преобразования данных, вычисления выражений и назначения результатов выражений переменным, свойствам и столбцам данных могут завершиться неудачей вследствие неверного приведения типа или несовместимости типов данных. Дополнительные сведения см. в разделах [Приведение (выражение служб SSIS)](../expressions/cast-ssis-expression.md), [Типы данных в выражениях служб Integration Services](../expressions/integration-services-data-types-in-expressions.md) и [Типы данных служб Integration Services](integration-services-data-types.md).  
  
 Усечение менее серьезно, чем ошибка. Усечение формирует результаты, которые могут использоваться или даже быть желательными. Можно выбрать, интерпретировать усечения как ошибки или как приемлемые состояния. Например, при вставке 15-символьной строки в столбец шириной всего в один символ можно выбрать усечение строки.  
  
 Можно установить, как источники, преобразования и назначения обрабатывают ошибки и усечения. В следующей таблице приводятся описания дополнительных параметров.  
  
|Параметр|Описание|  
|------------|-----------------|  
|Компонент, завершившийся сбоем|Задача потока данных заканчивается сбоем, если возникли ошибка или усечение. Неудача является параметром по умолчанию для ошибки и усечения.|  
|Пропуск неудачи|Ошибка или усечение пропускаются, и строка данных направляется на выход преобразования или источника.|  
|Перенаправление строки|Ошибка или строка данных усечения направляется на выход ошибок источника, преобразования или назначения.|  
  
## <a name="adding-the-error-description"></a>Добавление описания ошибки  
 По умолчанию выходные данные по ошибкам предоставляют числовой код ошибки и, как правило, содержат идентификатор столбца, в котором эта ошибка возникла. Можно использовать компонент скрипта для включения описания ошибки в дополнительный столбец, используя одну строку скрипта для вызова метода <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> интерфейса <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 Компонент скрипта может быть добавлен в сегмент ошибки потока данных в любом месте выхода данных из компонента потока данных, чьи ошибки нужно перехватить, но обычно размещается непосредственно перед строками ошибок, которые пишутся в целевой объект. В этом случае скрипт просматривает только описание строк записанных ошибок. Например, сегмент ошибки потока данных может исправить некоторые ошибки и не писать эти строки в целевой объект ошибок. Дополнительные сведения см. в разделе [расширение вывода ошибок в компоненте скрипта](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
### <a name="to-configure-an-error-output"></a>Настройка выхода ошибок  
  
-   [Настройка вывода ошибок в компоненте потока данных](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="see-also"></a>См. также  
 [Поток данных](data-flow.md)   
 [Преобразование данных с помощью преобразований](transformations/transform-data-with-transformations.md)   
 [Соединение компонентов с путями](../connect-components-with-paths.md)   
 [Задача потока данных](../control-flow/data-flow-task.md)   
 [Поток данных](data-flow.md)  
  
  
