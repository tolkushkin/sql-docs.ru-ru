---
title: Средства интеллектуального анализа данных | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tools [Analysis Services]
- mining models [Analysis Services], tools
- data mining [Analysis Services], tools
- data mining [Analysis Services], development
ms.assetid: 003ada6a-0bcd-4f16-8c34-1a9ffc75cd2c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dd0e6b696e692a9e88edd234d22f41983acbe961
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66084829"
---
# <a name="data-mining-tools"></a>Средства интеллектуального анализа данных
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] включены следующие средства создания решений интеллектуального анализа данных.  
  
-   **Мастер интеллектуального анализа данных** , который является компонентом среды [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Он упрощает создание структур и моделей интеллектуального анализа данных либо в реляционных источниках данных, либо в многомерных данных в кубах.  
  
     С помощью этого мастера пользователь выбирает нужные данные и затем применяет необходимые методы интеллектуального анализа — кластеризацию, нейронные сети или моделирование временных рядов.  
  
-   **Средства просмотра моделей** доступны как в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , так и в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]и предназначены для исследования моделей интеллектуального анализа после их создания.  Можно просматривать модели с помощью средств, специально созданных для каждого алгоритма, либо выполнить более глубокий анализ с помощью средства просмотра содержания модели.  
  
-   **Построитель прогнозирующих запросов** доступен как в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , так и в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] и предназначен для создания прогнозирующих запросов. Чтобы оценить качество набора данных, можно проверить точность моделей по набору контрольных или внешних данных либо выполнить перекрестную проверку.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] представляет собой интерфейс, предназначенный для работы с существующими решениями интеллектуального анализа данных, развернутыми в экземпляре служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Чтобы обновить данные структур и моделей, необходимо выполнить их повторную обработку.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] включают средства, которые могут быть использованы для очистки данных, для автоматизации различных задач, таких как создание прогнозов и обновление моделей, а также для создания решений в области интеллектуальной обработки текста.  
  
 Следующие разделы содержат более подробные сведения о средствах интеллектуального анализа данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="data-mining-wizard"></a>Мастер интеллектуального анализа данных  
 Чтобы перейти к созданию решения по интеллектуальному анализу данных, запустите мастер интеллектуального анализа данных. Мастер прост для освоения и призван помочь пользователю в процессе создания структуры интеллектуального анализа данных и связанной с ней исходной модели интеллектуального анализа данных, а также включает задачи по выбору типа алгоритма, выбору источника данных и определению данных варианта, используемого для анализа.  
  
 **Дополнительные сведения:** [Мастер интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](data-mining-wizard-analysis-services-data-mining.md)  
  
## <a name="data-mining-designer"></a>Конструктора моделей интеллектуального анализа данных  
 После создания структуры и модели интеллектуального анализа с помощью мастера интеллектуального анализа данных работать с существующими моделями и структурами можно с помощью конструктора интеллектуального анализа данных приложений в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] или [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Конструктор содержит средства для решения следующих задач.  
  
-   Изменение свойств структур интеллектуального анализа данных, добавление столбцов и создание их псевдонимов, изменение метода привязки или ожидаемого распределения значений.  
  
-   Добавление новых моделей в существующую структуру; копирование моделей, изменение свойств или метаданных модели или определение фильтров на модели интеллектуального анализа данных.  
  
-   Просмотр шаблонов и правил в рамках модели. Исследование связей или деревьев принятия решений. Получение подробной статистики  
  
     Имеются специализированные средства просмотра для каждого отдельного времени модели, которые помогают анализировать данные и исследовать закономерности, выявленные в процессе интеллектуального анализа данных.  
  
-   Проверка модели путем создания диаграммы точности прогнозов или анализ кривой прибыли для моделей. Сравнение моделей с помощью классификационных матриц либо проверка набора данных и его моделей путем перекрестной проверки.  
  
-   Создание прогнозов и запросы содержания существующей модели интеллектуального анализа данных. Построение запросов с неизвестным компонентом, а также настройка запросов для формирования прогнозов для полных таблиц внешних данных.  
  
 **Дополнительные сведения:** [Конструктор интеллектуального анализа данных](data-mining-designer.md)  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 После создания и развертывания моделей интеллектуального анализа данных на сервере можно в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] работать с базой данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , в которой размещены объекты интеллектуального анализа базы данных. Можно также продолжить выполнять задачи, в которых используется созданная модель, — исследование моделей, обработку новых данных и создание прогнозов.  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] также содержит редакторы запросов, которые могут быть использованы для проектирования и выполнения расширений интеллектуального анализа данных либо для работы с объектами интеллектуального анализа данных средствами XMLA.  
  
## <a name="integration-services-data-mining-tasks-and-transformations"></a>Преобразования и задачи интеллектуальной обработки данных служб Integration Services  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] включают множество компонентов, которые поддерживают интеллектуальный анализ данных.  
  
 Некоторые средства служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] направлены на автоматизацию наиболее часто выполняемых задач интеллектуального анализа данных — прогнозирования, построения и обработки моделей. Пример:  
  
-   Создание пакетов служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , которые будут автоматически обновлять модель при каждом пополнении набора данных новыми клиентами.  
  
-   Выполнение сегментации клиентов или задание нестандартных настроек выборки записей вариантов.  
  
-   Автоматическое создание моделей на основе переданных параметров.  
  
 В пакетном рабочем процессе интеллектуальный анализ данных можно использовать в качестве вводных данных для других процессов. Пример:  
  
-   Вероятностные значения, созданные моделью, могут использоваться для оценки показателей интеллектуального анализа текстовых данных, а также для других задач, требующих классификации.  
  
-   Автоматическое создание прогнозов на основе предыдущих данных и использование полученных значений для оценки достоверности новых данных.  
  
-   Использование логистической регрессии для сегментирования новых клиентов по уровням риска.  
  
 **Дополнительные сведения:** [Связанные проекты для решений интеллектуального анализа данных](data-mining-solutions.md)  
  
## <a name="see-also"></a>См. также  
 [Справочник по расширениям интеллектуального анализа данных (расширения интеллектуального анализа данных)](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Задачи и инструкции по модели интеллектуального анализа данных](mining-model-tasks-and-how-tos.md)   
 [Задачи и инструкции средства просмотра моделей интеллектуального анализа данных](mining-model-viewer-tasks-and-how-tos.md)   
 [Решения для интеллектуального анализа данных](data-mining-solutions.md)  
  
  
