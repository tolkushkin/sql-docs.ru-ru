---
title: Назначение "Обработка измерений" | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dimensionprocessingdest.f1
- sql13.dts.designer.dimprocessingtransformation.connection.f1
- sql13.dts.designer.dimprocessingtransformation.mappings.f1
- sql13.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 257f4ebaba273ad465c259a9bdd633e6513cda53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726953"
---
# <a name="dimension-processing-destination"></a>назначение «Обработка измерений»

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Назначение «Обработка измерения» загружает и обрабатывает измерение служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Дополнительные сведения об измерениях см. в разделе [Измерения (службы Analysis Services — многомерные данные)](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 Назначение «Обработка измерений» включает следующие элементы:  
  
-   Параметры для выполнения добавочной обработки, полной обработки или обработки обновления.  
  
-   Конфигурация ошибок, определяющая, пропускает ли ошибки обработка измерений или останавливается после определенного числа ошибок.  
  
-   Сопоставление входных столбцов со столбцами в таблицах измерения.  
  
 Дополнительные сведения об обработке объектов [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] см. в разделе [Настройка параметров обработки (службы Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>Настройка назначения «Обработка измерения»  
 Назначение «Обработка измерений» использует диспетчер соединений служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , чтобы подключиться к проекту служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] или экземпляру служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , содержащему измерения, обрабатываемые назначением. Дополнительные сведения см. в статье [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Данное назначение имеет один вход. Вывод ошибок не поддерживается.  
  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые можно задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующем разделе:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 Дополнительные сведения о настройке свойств см. в разделе [Установление свойств компонента потока данных](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="dimension-processing-destination-editor-connection-manager-page"></a>Редактор назначения обработки измерений (страница «Диспетчер соединений»)
  Страница **Диспетчер соединений** в диалоговом окне **Редактор назначения обработки измерений** позволяет указать соединение с проектом служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] или с экземпляром служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="options"></a>Параметры  
 **Connection manager**  
 Выберите из списка существующий диспетчер соединений или нажмите кнопку **Создать** , чтобы создать диспетчер соединений.  
  
 **Создать**  
 Создайте новое соединение, воспользовавшись диалоговым окном **Добавление диспетчера соединений со службами Analysis Services** .  
  
 **Список доступных измерений**  
 Выберите измерение для обработки.  
  
 **Метод обработки**  
 Выберите метод обработки, применяемый к выбранному в списке измерению. Значение этого параметра по умолчанию — **Полная**.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Добавление (дополнительное)**|Выполнить добавочную обработку измерения.|  
|**Полная**|Выполнить полную обработку измерения.|  
|**Update**|Выполнить обновление обработки измерения.|  
  
## <a name="dimension-processing-destination-editor-mappings-page"></a>Редактор назначения «Обработка измерения» (страница «Сопоставления»)
  Используйте страницу **Сопоставления** в диалоговом окне **Редактор назначения обработки измерений** , чтобы сопоставить входные столбцы со столбцами измерений.  
  
### <a name="options"></a>Параметры  
 **Доступные входные столбцы**  
 Просмотрите список доступных входных столбцов. Для сопоставления доступных входных столбцов с целевыми столбцами используется операция перетаскивания.  
  
 **Доступные целевые столбцы**  
 Просмотрите список доступных целевых столбцов. Чтобы сопоставить доступные целевые столбцы с входными столбцами, воспользуйтесь операцией перетаскивания.  
  
 **Входной столбец**  
 Просмотрите выбранные входные столбцы из вышеприведенной таблицы. Сопоставления можно изменить с помощью списка **Доступные входные столбцы**.  
  
 **Целевой столбец**  
 Просмотреть все доступные целевые столбцы независимо от наличия сопоставления.  
  
## <a name="dimension-processing-destination-editor-advanced-page"></a>Редактор назначения обработки измерений (страница «Дополнительно»)
  Используйте страницу **Дополнительно** диалогового окна **Редактор назначения обработки измерений** для настройки обработки ошибок.  
  
### <a name="options"></a>Параметры  
 **Использовать конфигурацию ошибок по умолчанию**  
 Укажите, нужно ли использовать обработку ошибок в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] по умолчанию. По умолчанию, присваивается значение **True**.  
  
 **Действие при возникновении ошибки ключа**  
 Укажите способ обработки записей с недопустимыми ключевыми значениями.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**ConvertToUnknown**|Преобразует недопустимое ключевое значение в значение **UnknownMember** .|  
|**DiscardRecord**|Удаляет запись.|  
  
 **Пропускать ошибки**  
 Указывает, что ошибки должны пропускаться.  
  
 **Остановить при возникновении ошибки**  
 Указывает, что в случае ошибки обработка должна прерываться.  
  
 **Количество ошибок**  
 Выберите порог ошибок, при котором обработка должна прерываться, если выбран режим **Остановить при возникновении ошибок**.  
  
 **Действие при возникновении ошибки**  
 Если был выбран параметр **Остановить при возникновении ошибок**, укажите действие, которое нужно выполнить при достижении порога ошибок.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**StopProcessing**|Останавливает обработку.|  
|**StopLogging**|Останавливает ведение журнала ошибок.|  
  
 **Ключ не найден**  
 Укажите действие при ошибке «Ключ не найден». По умолчанию, присваивается значение **Сообщить и продолжить**.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Пропустить ошибку**|Пропустить ошибку и продолжить обработку.|  
|**Сообщить и продолжить**|Сообщить об ошибке и продолжить обработку.|  
|**Сообщить и остановиться**|Сообщить об ошибке и остановить обработку.|  
  
 **Повторяющийся ключ**  
 Указывает действие при ошибке «Повторяющийся ключ». По умолчанию, присваивается значение **Пропустить ошибку**.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Пропустить ошибку**|Пропустить ошибку и продолжить обработку.|  
|**Сообщить и продолжить**|Сообщить об ошибке и продолжить обработку.|  
|**Сообщить и остановиться**|Сообщить об ошибке и остановить обработку.|  
  
 **Ключ NULL преобразован в неизвестный**  
 Выберите действие для ситуации, когда ключ NULL был преобразован в значение **UnknownMember** . По умолчанию, присваивается значение **Пропустить ошибку**.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Пропустить ошибку**|Пропустить ошибку и продолжить обработку.|  
|**Сообщить и продолжить**|Сообщить об ошибке и продолжить обработку.|  
|**Сообщить и остановиться**|Сообщить об ошибке и остановить обработку.|  
  
 **Ключ NULL не допускается**  
 Указывает действие при обнаружении ключа NULL в случае запрета ключей NULL. По умолчанию, присваивается значение **Сообщить и продолжить**.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Пропустить ошибку**|Пропустить ошибку и продолжить обработку.|  
|**Сообщить и продолжить**|Сообщить об ошибке и продолжить обработку.|  
|**Сообщить и остановиться**|Сообщить об ошибке и остановить обработку.|  
  
 **Путь к журналу ошибок**  
 Введите путь к журналу ошибок или нажмите кнопку **Обзор(...)** для выбора назначения.  
  
 **Обзор (...)**  
 Укажите путь к журналу ошибок.  
  
## <a name="see-also"></a>См. также:  
 [Поток данных](../../integration-services/data-flow/data-flow.md)   
 [Преобразования служб Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
