---
title: Обработать структуру интеллектуального анализа данных | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], processing
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92793adcf2fd04b1dac0c26933c1d5969a31f1a5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083111"
---
# <a name="process-a-mining-structure"></a>обработать структуру интеллектуального анализа данных
  Перед тем как получить возможность просмотра или работы с моделями интеллектуального анализа данных, связанными со структурой интеллектуального анализа данных, необходимо развернуть проект служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и обработать структуру интеллектуального анализа данных, а также модель интеллектуального анализа данных. Также при внесении изменений в структуру интеллектуального анализа данных или модель интеллектуального анализа данных будет выдано приглашение к их повторному развертыванию и обработке. При обработке структуры на вкладке **Структура интеллектуального анализа данных** конструктора интеллектуального анализа данных в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] обрабатываются все связанные с ней модели.  
  
 Обработка структуры интеллектуального анализа данных производится с помощью следующих средств.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA: Process, команда  
  
 Дополнительные сведения об обработке отдельных моделей см. в разделе [Обработка модели интеллектуального анализа данных](process-a-mining-model.md).  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>Обработка структуры интеллектуального анализа данных и всех связанных с ней моделей интеллектуального анализа данных с помощью SQL Server Data Tools  
  
1.  Выберите пункт **Обработать структуру интеллектуального анализа данных и все модели** из пункта меню **Модель интеллектуального анализа данных** в среде [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
     При внесении изменений в структуру будет выдано приглашение к повторному развертыванию структуры перед обработкой моделей. Нажмите кнопку **Да**.  
  
2.  Нажмите кнопку **запуска** в **Обработка структуры интеллектуального анализа данных — \<структуры >** диалоговое окно.  
  
     Откроется диалоговое окно **Ход обработки** , отображающее подробные сведения об обработке модели.  
  
3.  Нажмите кнопку **Закрыть** в диалоговом окне **Ход обработки** после завершения обработки моделей.  
  
4.  Нажмите кнопку **закрыть** в **Обработка структуры интеллектуального анализа данных — \<структуры >** диалоговое окно.  
  
## <a name="see-also"></a>См. также  
 [Задачи и инструкции по структуре интеллектуального анализа данных](mining-structure-tasks-and-how-tos.md)  
  
  
