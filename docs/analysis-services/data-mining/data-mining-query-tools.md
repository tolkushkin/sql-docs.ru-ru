---
title: Средства запросов интеллектуального анализа данных | Документация Майкрософт
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 697a1c06a2d30d5721c122c557f3e41836335b02
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449951"
---
# <a name="data-mining-query-tools"></a>Средства запросов интеллектуального анализа данных
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Все запросы интеллектуального анализа данных используют язык расширений интеллектуального анализа данных (DMX). DMX-запросы используются для создания всех видов задач машинного обучения, в том числе для классификации, анализа рисков, формирования рекомендаций и линейной регрессии. Можно также написать DMX-запросы для извлечения данных о закономерностях и получения статистики, сформированной при обработке модели.  
  
 Можно написать собственные расширения интеллектуального анализа данных или построить базовые расширения с помощью средства, такого как **построитель прогнозирующих запросов** , а затем изменить их. В средах [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] и [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] предусмотрены средства, позволяющие строить прогнозирующие запросы расширений интеллектуального анализа данных. В этом разделе содержатся сведения о создании и выполнения запросов интеллектуального анализа данных с помощью этих средств.  
  
-   [построитель прогнозирующих запросов](#bkmk_Builder)  
  
-   [Редактор запросов](#bkmk_QueryEditor)  
  
-   [Шаблоны расширений интеллектуального анализа данных](#bkmk_Templates)  
  
-   [Службы Integration Services](#bkmk_SSIS)  
  
-   [API-интерфейсы](#bkmk_API)  
  
##  <a name="bkmk_Builder"></a> построитель прогнозирующих запросов  
 Построитель прогнозирующих запросов находится на вкладке **Прогнозирование для моделей интеллектуального анализа данных** в конструкторе интеллектуального анализа данных, который доступен как в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], так и в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Работая с построителем запросов, можно выбирать модели интеллектуального анализа данных, добавлять новые данные вариантов, а также прогнозирующие функции. Затем можно переключиться в текстовый редактор, чтобы изменить запрос вручную, или переключиться на панель **Результаты** для просмотра результатов запроса.  
  
##  <a name="bkmk_QueryEditor"></a> Редактор запросов  
 Редактор запросов в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] также позволяет создавать и выполнять запросы расширений интеллектуального анализа данных. Вы можете подключиться к экземпляру служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]и выбрать базу данных, столбцы структуры интеллектуального анализа данных и модель интеллектуального анализа данных. **Обозреватель метаданных** содержит список прогнозирующих функций, который можно просмотреть.  
  
##  <a name="bkmk_Templates"></a> Шаблоны расширений интеллектуального анализа данных  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] предусмотрены интерактивные шаблоны DMX-запросов, которые могут быть использованы при создании. Если список шаблонов не отображается, щелкните **Вид** на панели инструментов и выберите команду **Обозреватель шаблонов**. Чтобы просмотреть все шаблоны служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , в том числе шаблоны для DMX, MDX и XMLA, щелкните значок куба.  
  
 Чтобы построить запрос с помощью шаблона, шаблон можно перетащить в открытое окно запроса либо дважды щелкнуть его для открытия нового соединения и новой панели запросов.  
  
 Пример создания прогнозирующего запроса с помощью шаблона см. в разделе [Создание одноэлементного прогнозирующего запроса из шаблона](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md).  
  
> [!WARNING]  
>  Надстройка интеллектуального анализа данных для Microsoft Office Excel содержит несколько шаблонов, а также интерактивный построитель запросов, с помощью которого можно составлять сложные инструкции расширений интеллектуального анализа данных. Для работы с шаблонами в клиенте интеллектуального анализа данных щелкните **Запрос**, а затем **Дополнительно** .  
  
##  <a name="bkmk_SSIS"></a> Компоненты интеллектуального анализа данных служб Integration Services  
 Можно также включать прогнозирующие запросы в состав пакета служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Создание и выполнение инструкций и прогнозирующих запросов расширений интеллектуального анализа данных поддерживается следующими задачами и преобразованиями служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Компонент|Описание|  
|---------------|-----------------|  
|Задача «Запрос интеллектуального анализа данных»|Выполняет DMX-запросы и другие инструкции DMX в рамках потока управления.<br /><br /> Редактор задач содержит построитель прогнозирующих запросов и текстовое поле для ручного изменения DMX-запроса. Но при этом редактор задач не может проверить запрос по объектам из решения служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Поэтому запросы лучше создать в среде [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] или [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , а затем вставить текст инструкции или запроса в редактор задач.|  
|преобразование «Запрос интеллектуального анализа данных»|Выполняет прогнозирующий запрос внутри потока данных с помощью данных источника, определенного в источнике потока данных.<br /><br /> Редактор задач содержит построитель прогнозирующих запросов и текстовое поле для ручного изменения DMX-запроса.<br /><br /> Это преобразование можно использовать для создания запросов, которые используют данные из потока данных. Иными словами, запросов, которые используют синтаксис PREDICTION JOIN. Этот компонент не может использоваться для выполнения запросов содержимого или других видов инструкций DMX.|  
  
##  <a name="bkmk_API"></a> API-интерфейсы  
 Можно создавать пользовательские приложения, выполняющие запросы к моделям интеллектуального анализа данных с использованием различных сочетаний языков программирования и сетевых протоколов, например OLE DB или клиента ADOMD служб Analysis Services. Дополнительные сведения см. в разделе [Программирование интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-programming.md).  
  
 Однако XMLA представляет собой базовый формат сообщений для всех взаимодействий на сервере служб Analysis Service. В сообщении XMLA запросы представляются по-разному, в зависимости от того, на чем основан отправляемый прогнозирующий запрос: DMX, запрос содержимого либо запрос на получение метаданных модели через наборы строк схемы интеллектуального анализа данных.  
  
-   Текст **прогнозирующих запросов** (и всех других инструкций расширений интеллектуального анализа данных) отправляется в формате XMLA с помощью метода [Execute (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute), при этом DMX-запрос размещается как текст внутри элемента [Statement (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) элемента [Command (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla).  
  
-   Чтобы получить **содержимое модели** и **метаданные модели**, например число кластеров, атрибутов, использованных в деревьях принятия решений, даты последней обработки модели и параметров алгоритма, заданные при создании модели, можно воспользоваться методом [Discover (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover), а также указать один из наборов строк схемы интеллектуального анализа данных в заголовке элемента [RequestType (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/requesttype-element-xmla). Чтобы сузить область действия запроса, введите такие критерии, как ограничения, внутри элемента [RestrictionList (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla).  
  
## <a name="see-also"></a>См. также  
 [Справочник по расширениям интеллектуального анализа данных (расширения интеллектуального анализа данных)](../../dmx/data-mining-extensions-dmx-reference.md)   
 [Решения для интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Общие сведения об инструкции расширения интеллектуального анализа данных SELECT](../../dmx/understanding-the-dmx-select-statement.md)   
 [Структура и методы использования прогнозирующих запросов расширений интеллектуального анализа данных](../../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Создание прогнозирующего запроса с помощью построителя прогнозирующих запросов](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)   
 [Создание DMX-запроса в среде SQL Server Management Studio](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
