---
title: Изменение свойства KeyColumn атрибута | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- binding attributes [Analysis Services]
- attributes [Analysis Services], binding
- key columns [Analysis Services]
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5c5effed34dda946d3c65028aa5834f4fbddf7cd
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077251"
---
# <a name="modify-the-keycolumn-property-of-an-attribute"></a>Изменение свойства KeyColumn атрибута
  Свойство **KeyColumns** атрибута можно изменить. Например, в качестве ключа атрибута может потребоваться не одиночный ключ, а составной.  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>Изменение свойства KeyColumns атрибута  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект, в котором необходимо изменить свойство **KeyColumns** .  
  
2.  Откройте конструктор измерений одним из следующих способов:  
  
    -   В **обозревателе решений**правой кнопкой мыши щелкните папку **Измерения** , а затем выберите либо **Открыть** , либо **Конструктор представлений**.  
  
         -или-  
  
    -   В конструкторе кубов на **Структура куба** вкладке, разверните измерение куба в **измерения** область и выберите команду **изменить \<измерения >**.  
  
3.  На вкладке **Структура измерения** , на панели **Атрибуты** , щелкните атрибут, для которого нужно изменить свойство **KeyColumns** .  
  
4.  В окне **Свойства** щелкните значение для свойства **KeyColumns** .  
  
5.  Нажмите кнопку обзора **(...)** , отображающуюся в ячейке значения поля свойства.  
  
     Откроется диалоговое окно **Ключевые столбцы** .  
  
6.  Для удаления существующего ключевого столбца выберите его в списке **Ключевые столбцы** и нажмите кнопку **\<** .  
  
7.  Для добавления ключевого столбца выберите его в списке **Доступные столбцы** и нажмите кнопку **>** .  
  
    > [!NOTE]  
    >  Если задано несколько ключевых столбцов, они отображаются в том же порядке, что и в списке **Ключевые столбцы** . Например, у атрибута «месяц» два ключевых столбца: месяц и год. Если столбец «год» появится в списке раньше столбца «месяц», службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] будут выполнять сортировку по годам, а затем по месяцам. Если столбец «месяц» будет в списке раньше столбца «год», службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] будут выполнять сортировку по месяцам, а затем по годам.  
  
8.  Чтобы изменить порядок ключевых столбцов, выберите столбец и нажмите кнопку **Вверх** или кнопку **Вниз** .  
  
## <a name="see-also"></a>См. также  
 [Справочник по свойствам атрибута измерения](dimension-attribute-properties-reference.md)  
  
  
