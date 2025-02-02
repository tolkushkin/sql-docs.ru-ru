---
title: Секции режимы хранения и обработка | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57c73e3ae9661058277a377b7d17b6a4af393ba0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640460"
---
# <a name="partitions---partition-storage-modes-and-processing"></a>Секции — режимы хранения и обработка секций
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Режим хранения секции определяет производительность выполнения запросов и обработки, требования к хранилищу и месту хранения секции, а также ее родительскую группу мер и куб. Кроме того, режим хранения влияет на выбор обработки.  
  
 Секция может использовать один из трех основных режимов хранения:  
  
-   Многомерный OLAP (MOLAP)  
  
-   Реляционный OLAP (ROLAP)  
  
-   Гибридный OLAP (HOLAP)  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] поддерживает все три основные режима хранения. Также поддерживается упреждающее кэширование, позволяющее совмещать характеристики хранилищ ROLAP и MOLAP для незамедлительного доступа к данным и высокой производительности запросов. Дополнительные сведения см. в разделе [Упреждающее кэширование (секции)](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="molap"></a>MOLAP  
 В режиме хранения MOLAP агрегаты секции и копия исходных данных при ее обработке сохраняются в многомерной структуре служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. В целях повышения производительности запросов структура MOLAP значительно оптимизирована. Местом хранения может быть либо компьютер, на котором определена секция, либо любой другой компьютер, на котором запущены службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Учитывая тот факт, что многомерные структуры содержат копию исходных данных, запрос может быть выполнен без обращения к секции исходных данных. При использовании статистической обработки время выполнения запроса может значительно возрасти. Данные в структуре секции MOLAP соответствуют последней обработке секции.  
  
 Так как исходные данные изменяются, для включения этих изменений и обеспечения доступа к ним пользователей объекты в хранилище MOLAP должны периодически обрабатываться. Обработка полностью или частично обновляет данные в структуре MOLAP. Время между обработками представляет собой период задержки, в течение которого объекты OLAP могут не соответствовать исходным данным. Можно полностью или частично обновить объекты в хранилище MOLAP, не переводя секцию или куб в режим вне сети. Однако в некоторых случаях это может оказаться необходимым при обработке определенных структурных изменений объектов OLAP. Можно свести к минимуму время простоя, требуемое для обновления хранилища MOLAP, с помощью обновления и обработки кубов на промежуточном сервере, а также использования синхронизации баз данных для копирования обработанных объектов на производственный сервер. Также для сокращения задержки и максимизации доступности можно использовать упреждающее кэширование, сохраняя при этом высокую производительность хранилища MOLAP. Дополнительные сведения см. в разделе [упреждающее кэширование &#40;секций&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md), [синхронизации баз данных Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md), и [обработка многомерной модели &#40; Службы Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="rolap"></a>ROLAP  
 В режиме хранения ROLAP агрегаты секции хранятся в индексированных представлениях реляционной базы данных, которая определена в источнике данных секции. В отличие от режима MOLAP, в режиме хранения ROLAP копия исходных данных в папках данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] не хранится. Напротив, если получить результаты из кэша запросов невозможно, для ответов на запросы выполняется доступ к индексированным представлениям в источнике данных. Как правило, в режиме ROLAP запрос выполняется дольше, чем в режимах хранения MOLAP или HOLAP. И время обработки в режиме ROLAP обычно тоже больше. Однако режим ROLAP дает пользователям возможность просматривать данные в режиме реального времени и сохранять пространство хранилища при работе с большими наборами данных, которые запрашиваются редко, например архивные данные.  
  
> [!NOTE]  
>  При использовании режима ROLAP службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] могут вернуть неправильные данные, связанные с неизвестным элементом, если соединение комбинируется предложением GROUP BY. Службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] исключают ошибки реляционной целостности вместо того, чтобы возвращать неизвестные значения элементов.  
  
 Если секция использует режим хранения ROLAP и его источник данных хранится в компоненте [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], то службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] пытаются создать индексированные представления для получения статистических схем секции. Если службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] не могут создать индексированные представления, то не создаются таблицы агрегатов. Несмотря на то, что службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] удовлетворяют требованиям к сеансам для создания индексированных представлений в компоненте [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], для создания службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] индексированных представлений агрегатов для секции ROLAP и таблиц в ее схеме необходимо выполнение следующих условий.  
  
-   Секция не может содержать меры, использующие **Min** или **Max** агрегатные функции.  
  
-   Все таблицы в схеме секции ROLAP должны использоваться только один раз. Например, схема не может содержать [dbo].[address] AS "Customer Address" и [dbo].[address] AS "SalesRep Address".  
  
-   Все таблицы должны быть таблицами, а не представлениями.  
  
-   Все имена таблиц в схеме секции должны содержать имя владельца, например [dbo].[customer].  
  
-   Все таблицы в схеме секции должны принадлежать одному владельцу. Например, не допускается, чтоб предложение FROM одновременно ссылалось на таблицы [tk].[customer], [john].[store] и [dave].[sales_fact_2004].  
  
-   Исходные столбцы мер секции не должны быть NULLABLE.  
  
-   Все таблицы, используемые в представлении, должны быть созданы с использованием следующих параметров со значением ON:  
  
    -   ANSI_NULLS  
  
    -   QUOTED_IDENTIFIER  
  
-   Общий размер ключа индекса в [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] не может превышать 900 байт. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] проверяет это условие, в зависимости от ключевых столбцов фиксированной длины при обработке инструкции CREATE INDEX. Тем не менее, если есть столбцы переменной длины в ключе индекса, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] также проверяет это условие при каждом обновлении базовых таблиц. Так как различные агрегаты имеют различные определения представлений, то обработка в режиме ROLAP с использованием индексированных представлений может быть удачной или нет, в зависимости от статистической схемы.  
  
-   В сеансе создания индексированного представления должен иметь значение ON следующие параметры: ARITHABORT, CONCAT_NULL_YEILDS_NULL, QUOTED_IDENTIFIER, ANSI_NULLS, ANSI_PADDING, and ANSI_WARNING. Эти настройки можно произвести в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   В сеансе создания индексированного представления должен иметь значение OFF следующий параметр: NUMERIC_ROUNDABORT. Эти настройки можно произвести в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="holap"></a>HOLAP  
 Режим хранения HOLAP объединяет атрибуты режимов MOLAP и ROLAP. Как и MOLAP, HOLAP агрегаты секции хранятся в многомерной структуре в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] экземпляра. В режиме HOLAP копия исходных данных не хранится. Для запросов, которые производят доступ только к сводным данным в агрегатах секции, режим HOLAP полностью эквивалентен режиму MOLAP. Запросы, которые обращаются к исходных данных — например, если вы хотите детализация ячейки атомарного куба для которого существует не статистической обработки данных – должен получить данные из реляционной базы данных и не будет так же быстро, как было бы, если исходные данные хранились в MOLAP structur e. В режиме хранения HOLAP пользователи, как правило, ощущают весомые различия во времени обработки запроса в зависимости от того, откуда разрешаются запросы: из кэша или из агрегатов источника данных.  
  
 Секции с режимом хранения HOLAP меньше аналогичных секций MOLAP, потому что в них не содержится источник данных, а для запросов со сводными данными они имеют меньшее время отклика, чем в секциях ROLAP. Режим хранения HOLAP, как правило, подходит для секций в кубах, требующих малого времени ответа на запросы сводных данных из большого количества исходных данных. Однако если пользователи создают запросы к данным конечного уровня, например вычисление средних значений, более предпочтительно использовать режим MOLAP.  
  
## <a name="see-also"></a>См. также  
 [Упреждающее кэширование &#40;секций&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Синхронизация баз данных служб Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Секции (службы Analysis Services — многомерные данные)](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
