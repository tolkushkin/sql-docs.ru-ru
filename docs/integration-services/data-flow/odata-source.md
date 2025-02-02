---
title: Источник OData | Документы Майкрософт
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
- sql13.dts.designer.odatasource.connection.f1
- sql13.dts.designer.odatasource.columns.f1
- sql13.dts.designer.odatasource.erroroutput.f1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b1c9e39e4ccec7ab54229a8bbd0bf51b1d751207
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726669"
---
# <a name="odata-source"></a>Источник OData

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Компонент источника OData используется в пакете служб SSIS для получения данных от служб OData.

## <a name="supported-protocols-and-data-formats"></a>Поддерживаемые протоколы и форматы данных

Этот компонент поддерживает протоколы OData версии 3 и 4.  
  
-   Для протокола OData версии 3 компонент поддерживает форматы данных ATOM и JSON.  
  
-   Для протокола OData версии 4 компонент поддерживает формат данных JSON.  

## <a name="supported-data-sources"></a>Поддерживаемые источники данных

Источник OData поддерживает следующие источники данных:
-   Microsoft Dynamics AX Online и Microsoft Dynamics CRM Online.
-   Списки SharePoint. Просмотреть все списки на сервере SharePoint можно по следующему URL-адресу: https://\<сервер>/_vti_bin/ListData.svc. Дополнительные сведения о соглашениях об URL-адресах SharePoint см. в разделе [Интерфейс REST SharePoint Foundation](https://msdn.microsoft.com/library/ff521587.aspx).

## <a name="supported-data-types"></a>Поддерживаемые типы данных

Источник OData поддерживает следующие простые типы данных: int, byte[], bool, byte, DateTime, DateTimeOffset, decimal, double, Guid, Int16, Int32, Int64, sbyte, float, string и TimeSpan.

Чтобы просмотреть типы данных столбцов в источнике данных, проверьте страницу `https://<OData feed endpoint>/$metadata`.

> [!IMPORTANT]
> Компонент источника OData не поддерживает сложные типы в списках SharePoint, такие как элементы множественного выбора.

## <a name="odata-format-and-performance"></a>Формат OData и производительность
 Большинство служб OData могут возвращать результаты в различных форматах. Можно указать формат результирующего набора с помощью параметра запроса `$format`. Такие форматы, как JSON и JSON Light, более эффективны, чем ATOM или XML, и способны обеспечить более высокую производительность при передаче больших объемов данных. В следующей таблице отображаются результаты типовых тестов. Как видно, прирост производительности составил 30–53 % при переходе от ATOM к JSON и 67 % при переходе от ATOM к новому формату JSON Light (доступный в WCF Data Services 5.1).  
  
|Строки|ATOM|JSON|JSON (Light)|  
|-|-|-|-|  
|10000|113 секунд|74 секунды|68 секунд|  
|1000000|1110 секунд|853 секунды|665 с|  
  
## <a name="related-topics-in-this-section"></a>Связанные подразделы в этом разделе  
  
-   [Учебник. Использование источника OData](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [Изменение запроса источника OData во время выполнения](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [Свойства источника OData](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="odata-source-editor-connection-page"></a>Редактор источника OData (страница «Подключение»)
  Страница **Диспетчер соединений** диалогового окна **Редактор источника OData** служит для выбора диспетчера соединений OData для источника. На этой странице также можно задать путь к коллекции или ресурсу, а также параметры запроса, чтобы указать, какие данные нужно получить из источника OData. 
  
### <a name="static-options"></a>Статические параметры  
 **Диспетчер соединений OData**  
 Выберите из списка существующий диспетчер соединений или создайте новое соединение, нажав кнопку **Создать**.  
  
 После выбора или создания диспетчера подключений в диалоговом окне отображается версия протокола OData, которую использует диспетчер подключений.  
  
 **Создать**  
 Создайте новый диспетчер соединений с помощью диалогового окна **Редактор диспетчера соединений OData** .  
  
 **Использование пути к коллекции или ресурсу**  
 Укажите метод выбора данных из источника.  
  
|Параметр|Описание|  
|------------|-----------------|  
|Коллекция|Извлечение данных из источника OData с помощью имени коллекции.|  
|Путь к ресурсу|Извлечение данных из источника OData с помощью пути к ресурсу.|  
  
 **Параметры запроса**  
 Укажите параметры запроса. Например: `$top=5` 
  
 **URL-адрес канала**  
 Отображает доступный только для чтения URL-адрес веб-канала на основе параметров, выбранных в этом диалоговом окне.  
  
 **Предварительный просмотр**  
 Предварительный просмотр результатов в диалоговом окне **Предварительный просмотр** . В окне**Предварительный просмотр** может отображаться до 20 строк.  
  
### <a name="dynamic-options"></a>Динамические параметры  
  
#### <a name="use-collection-or-resource-path--collection"></a>Использование пути к коллекции или ресурсу = коллекция  
 **Коллекция**  
 Выберите коллекцию из раскрывающегося списка.  
  
#### <a name="use-collection-or-resource-path--resource-path"></a>Использование пути к коллекции или ресурсу = путь к ресурсу  
 **Resource path**  
 Введите путь к ресурсу. Пример: Employees  
  
## <a name="odata-source-editor-columns-page"></a>Редактор источника OData (страница «Столбцы»)
  На странице **Столбцы** диалогового окна **Редактор источника OData** можно выбрать внешние (исходные) столбцы, которые должны быть включены в выходные данные, и сопоставить их с выходными столбцами.  
  
### <a name="options"></a>Параметры  
 **Доступные внешние столбцы**  
 Просмотрите список доступных исходных столбцов источника данных. С помощью флажков в списке добавьте или удалите столбцы из таблицы в нижней части страницы. Выбранные столбцы добавляются в выходные данные.  
  
 **Внешний столбец**  
 Просмотрите исходные столбцы, выбранные для включения в выходные данные.  
  
 **Выходной столбец**  
 Введите уникальное имя для каждого выходного столбца. По умолчанию используется имя выбранного внешнего (исходного) столбца, однако можно выбрать любое уникальное описательное имя.  
  
## <a name="odata-source-editor-error-output-page"></a>Редактор источника OData (страница «Вывод ошибок»)
  Страница **Вывод ошибок** диалогового окна **Редактор источника OData** служит для выбора параметров обработки ошибок, а также для установки свойств выходных столбцов ошибок.  
  
### <a name="options"></a>Параметры  
 **Ввод-вывод**  
 Просмотр имени источника данных.  
  
 **Столбец**  
 Просмотрите внешние (исходные) столбцы, выбранные на странице **Диспетчер соединений** диалогового окна **Редактор источника OData** .  
  
 **Ошибка**  
 Задайте действие, которое необходимо выполнить при возникновении ошибки: пропустить ошибку, перенаправить строку или вызвать сбой компонента.  
  
 **См. также:** [Обработка ошибок в данных](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Усечение**  
 Укажите, что нужно сделать при усечении: пропустить ошибку, перенаправить строку или вызвать сбой компонента.  
  
 **Описание**  
 Просмотреть описание ошибки.  
  
 **Присвоить указанное значение выбранным ячейкам**  
 Укажите действие, которое необходимо применить ко всем выбранным ячейкам при возникновении ошибки или усечения: пропустить ошибку, перенаправить строку или вызвать сбой компонента.  
  
 **Применить**  
 Применить параметр обработки ошибок к выбранным ячейкам.  
  
## <a name="see-also"></a>См. также:  
 [Диспетчер подключений OData](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
