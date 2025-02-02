---
title: Уровень совместимости (табличные службы SSAS пакета обновления 1) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57a1e67db8bcbf17dc964f7341df25a396c36ad0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067600"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>Уровень совместимости (службы SSAS с пакетом обновления 1 (SP1) — табличные модели)
  Можно указать *уровень совместимости* при создании новых проектов табличных моделей, во время обновления существующих проектов табличных моделей, при обновлении существующих развернутых баз данных табличных моделей либо при импорте книг PowerPivot.  
  
## <a name="compatibility-level"></a>Уровень совместимости  
 Распространенной практикой является установка новых версий и пакетов обновления на компьютеры, используемые для разработки и тестирования, перед их установкой на производственные компьютеры. В таких случаях важно понимать особенности уровней совместимости и их установки в новых проектах табличной модели, а также проектах, которые уже были развернуты в рабочей среде.  
  
 Экземпляр служб Analysis Services [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] поддерживает следующие уровни совместимости (версии базы данных).  
  
-   SQL Server 2012 (1100)  
  
-   SQL Server 2012 с пакетом обновления 1 (SP1) (1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>Задание уровня совместимости при создании нового проекта табличной модели  
 При создании нового проекта табличной модели в SQL Server Data Tools (SSDT), на **параметры нового табличного проекта** диалоговое окно можно указать уровень совместимости. При создании нового проекта можно задать его развертывание в экземпляре служб Analysis Services [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] или более поздней версии или в экземпляре служб Analysis Services SQL Server 2012 (без пакета обновления 1 (SP1)).  
  
 Также вы можете задать уровень совместимости по умолчанию, выбрав параметр **Больше не показывать это сообщение** . Во всех последующих проектах будет использоваться заданный уровень совместимости. Уровень совместимости по умолчанию в SSDT вы можете изменить в «Параметрах».  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>Обновление существующего проекта табличной модели до уровня совместимости 1103.  
 Можно обновить проект табличной модели, созданный в SSDT до установки [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] или более поздней версии для версии базы данных 1103 совместимости с помощью **уровень совместимости** свойства в модели **свойства**окно. Для обновления проекта табличной модели на компьютере, где установлен SSDT, должен быть установлен [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] или более поздней версии; на экземпляре служб Analysis Services, на котором находится база данных рабочей области, тоже должен быть установлен [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] или более поздней версии. Перейти на более раннюю версию невозможно.  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>Обновление развернутой базы данных табличной модели до уровня совместимости с 1103  
 Можно обновить существующую версию базы данных для базы данных развернутой табличной модели 1103, совместимых в SQL Server Management Studio (SSMS) с помощью **уровень совместимости** свойство в **свойства базы данных**. Для выполнения обновления на компьютере, на котором установлен экземпляр служб SQL Server Analysis Services, должен быть установлен [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] или более поздней версии. Невозможно перейти на более раннюю версию базы данных развернутой табличной модели.  
  
### <a name="import-from-powerpivot"></a>Импорт из PowerPivot  
 При создании нового проекта табличной модели путем импорта из PowerPivot можно указать, следует ли обновить уровень совместимости до уровня по умолчанию (если он был ранее задан в SSDT) или оставить тот уровень совместимости, который уже указан в книге PowerPivot.  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>Проверка уровня совместимости для базы данных табличной модели в среде SSMS  
 Уровень совместимости для базы данных табличной модели в среде SSMS можно проверить, просмотрев **уровень совместимости** свойство (возможности [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) в **свойства базы данных**.  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>Проверка поддерживаемого уровня совместимости для экземпляра служб Analysis Services в среде SSMS  
 Поддерживаемый уровень совместимости в среде SSMS можно проверить, просмотрев **поддерживаемый уровень совместимости** свойство **сведения** страницы (возможности [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) в **анализа Свойства служб**. Поддерживаемый уровень совместимости 1103 показывает, что установлен SQL Server с пакетом обновления 1 (SP1) или более поздняя версия. Поддерживаемый уровень совместимости нельзя изменить.  
  
  
