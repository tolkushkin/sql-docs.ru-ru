---
title: Импорт проекта интеллектуального анализа данных с помощью мастера импорта служб Analysis Services | Документация Майкрософт
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 52e98d6916b66c4ab26b2791d023d25bffc4cab8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043968"
---
# <a name="import-a-data-mining-project-using-the-analysis-services-import-wizard"></a>Импорт проекта интеллектуального анализа данных с помощью мастера импорта служб Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  В этом разделе описано, как создать новый проект интеллектуального анализа данных путем импорта метаданных из существующего проекта интеллектуального анализа данных на другом сервере, используя шаблон **Импорт с сервера (многомерные данные и интеллектуальный анализ данных)** , в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="import-data-sources-mining-structures-and-mining-models-from-an-existing-data-mining-project"></a>Импорт источников данных, структур интеллектуального анализа данных и моделей интеллектуального анализа данных из существующего проекта интеллектуального анализа данных  
 При использовании шаблона **Импорт с сервера (многомерные данные и интеллектуальный анализ данных)** среда [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] создает новый проект интеллектуального анализа данных, а затем копирует метаданные из указанного проекта интеллектуального анализа данных. Новый проект содержит те же источники данных, представления источников данных, структуры интеллектуального анализа данных и модели интеллектуального анализа данных, что и база данных ssASnoversion, из которой был выполнен импорт. Однако этот проект нельзя использовать до тех пор, пока некоторые свойства не будут обновлены, а объекты — обработаны согласно описанию.  
  
-   Сами данные не копируются с исходного сервера для нового интеллектуального анализа данных проекта только для определения источников данных и представления источников данных импортируются. Поэтому после завершения процесса импорта и создания объектов необходимо заполнить объекты данными, проведя обучение структур интеллектуального анализа и зависимых моделей. Для обучения моделей и структур можно воспользоваться командой **Обработать все** в конструкторе интеллектуального анализа данных.  
  
-   В случае импорта проекта, который был создан в предыдущей версии [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], в источнике данных могут использоваться поставщики, не установленные на сервере, на который импортируется проект. Если при обработке импортируемых структур интеллектуального анализа возникнут ошибки, щелкните правой кнопкой мыши каждый источник данных и выберите команду **Открыть конструктор** для изменения строки подключения и просмотра свойств поставщика.  
  
     На этом этапе может также потребоваться убедиться, что учетная запись, используемая для обработки объектов интеллектуального анализа данных или запроса моделей интеллектуального анализа данных, имеет необходимые разрешения для источника данных.  
  
-   По умолчанию при импорте проекта в качестве базы данных рабочей области устанавливается localhost или экземпляр, настроенный как **Целевой сервер по умолчанию** в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Чтобы установить это свойство, в меню **Параметры** выберите **Конструкторы бизнес-аналитики**, затем выберите **Службы Analysis Services**и **Общие**.  
  
     Обратите внимание, что в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]имеется еще один, отдельный параметр, который можно задать для настройки сервера развертывания по умолчанию для проектов табличной модели [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Эта настройка, **Сервер развертывания по умолчанию**, определяет базу данных рабочей области по умолчанию для проектов табличной модели. В проектах интеллектуального анализа данных нельзя использовать экземпляры, поддерживающие табличные модели  
  
     Если не удается изменить базу данных развертывания по умолчанию для использования экземпляра служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , запущенного в многомерном режиме или режиме интеллектуального анализа данных, всегда можно указать базу данных развертывания с помощью диалогового окна **Свойства проекта** .  
  
#### <a name="to-create-a-new-data-mining-project-by-importing-an-existing-data-mining-project"></a>Создание нового проекта интеллектуального анализа данных путем импорта существующего проекта интеллектуального анализа данных  
  
1.  В среде [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]в меню **Файл** выберите пункт **Создать**, а затем выберите пункт **Проект**.  
  
2.  В диалоговом окне **Создание проекта** в разделе **Установленные шаблоны**выберите **Бизнес-аналитика**, затем **Службы Analysis Services**, после чего выберите **Импорт с сервера (многомерные данные и интеллектуальный анализ данных)** .  
  
3.  В поле **Имя**введите имя проекта, укажите расположение и имя решения, а затем нажмите кнопку **ОК**.  
  
     Запустится **мастер импорта базы данных служб Analysis Services** . Для продолжения нажмите кнопку «ОК» на странице приветствия.  
  
4.  На странице **Выбор базы данных-источника**в качестве параметра **Сервер**укажите экземпляр [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , содержащий решение, которое необходимо импортировать.  
  
     В качестве параметра **База данных**выберите базу данных [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , которая содержит импортируемые объекты интеллектуального анализа данных.  
  
    > [!WARNING]  
    >  Импортируемые объекты указывать нельзя; при выборе существующей базы данных [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] импортируются все многомерные объекты и объекты интеллектуального анализа данных.  
  
     Нажмите кнопку **Далее**.  
  
5.  На странице **Завершение работы мастера**отображается ход выполнения операции импорта. Отменить операцию или изменить импортируемые объекты нельзя. По завершении нажмите кнопку **Готово** .  
  
     Новый проект будет автоматически открыт в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>См. также  
 [Свойства проекта](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
