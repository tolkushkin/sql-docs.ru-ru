---
title: Работа с диаграммами в конструкторе представлений источников данных (службы Analysis Services) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.diagramorganizerpane.f1
- sql12.asvs.dsvdesigner.findtable.f1
- sql12.asvs.dsvdesigner.diagrampane.f1
helpviewer_keywords:
- data source views [Analysis Services], diagrams
- diagrams [Analysis Services]
ms.assetid: 491fdd22-2326-4f27-a0dd-0a02faae3fd8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1aa03174d82c7319ce0c7b1cf455916e37a1b117
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072383"
---
# <a name="work-with-diagrams-in-data-source-view-designer-analysis-services"></a>Работа с диаграммами в конструкторе представлений источника данных (службы Analysis Services)
  Диаграмма представления источников данных (DSV) — это визуальное представление объектов в виде DSV. С диаграммой можно работать интерактивно. Она позволяет добавить, скрыть, удалить или изменить определенные объекты. Можно также создать несколько диаграмм одного и того же представления DSV, чтобы сосредоточить внимание на подмножестве объектов.  
  
 Чтобы изменить зону диаграммы, которая появляется на панели диаграмм, нажмите четырехстороннюю стрелку в правом нижнем углу панели и перетащите поле выбора на эскиз диаграммы до тех пор, пока не будет выделена та область, которая должна появиться на панели диаграмм.  
  
 Этот раздел включает следующие подразделы:  
  
 [Добавление диаграммы](#bkmk_add)  
  
 [Изменение и удаление диаграммы](#bkmk_edit)  
  
 [Поиск таблиц в диаграмме](#bkmk_findtables)  
  
 [Упорядочение объектов в диаграмме](#bkmk_arrangeobjects)  
  
 [Сохранение упорядочивания объектов](#bkmk_preserve)  
  
##  <a name="bkmk_add"></a> Добавление диаграммы  
 Диаграммы DSV создаются автоматически при создании представления DSV. После создания представления DSV можно создавать дополнительные диаграммы, удалять их или скрывать определенные объекты для создания более управляемых представлений DSV.  
  
 Чтобы создать новую диаграмму, щелкните правой кнопкой мыши в любом месте на панели **Организатор диаграмм** и выберите пункт **Создать диаграмму**.  
  
 При первоначальном определении представления источника данных (DSV) в проекте служб Analysis Services, все таблицы и представления, добавленные в представление источника данных добавляются \<все таблицы > схемы. Эта диаграмма отображается на панели организатора диаграмм в конструкторе представлений источников данных, таблицы в этой диаграмме (а также их столбцы и связи) перечисляются на панели «Таблицы» и графически отображаются на панели «Диаграмма». Тем не менее, как добавить таблиц, представлений и именованных запросов, которые \<все таблицы > схема, большое число объектов на этой диаграмме затрудняет для визуализации связей, особенно в том случае, как добавляются к диаграмме несколько таблиц фактов и измерений таблицы связаны с множеством таблиц фактов.  
  
 Для уменьшения визуальных помех, если необходимо просмотреть только подмножество таблиц в представлении источника данных, можно определить подчиненные диаграммы (называемые просто диаграммами), состоящие из выбранных подмножеств таблиц, представлений и именованных запросов в представлении источника данных. Диаграммы можно использовать для группирования элементов в представлении источника данных в соответствии с потребностями бизнеса или решения.  
  
 Можно группировать связанные таблицы и именованные запросы в отдельные диаграммы для бизнес-целей и облегчить понимание представления источников данных, содержащего множество таблиц, представлений и именованных запросов. Той же таблице или именованный запрос могут быть включены в несколько диаграмм, за исключением \<все таблицы > схемы. В \<все таблицы > схема, все объекты, содержащиеся в представлении источника данных, отображаются однократно.  
  
##  <a name="bkmk_edit"></a> Изменение и удаление диаграммы  
 Во время работы с диаграммой обращайте внимание на команды, которые используются для добавления и удаления объектов. Например, если удалить объект из диаграммы, то этот объект будет удален и из представления DSV. Чтобы удалить объект только из диаграммы, воспользуйтесь командой **Спрятать таблицу** .  
  
 ![Снимок экрана: рабочее пространство диаграммы, щелкните правой кнопкой мыши меню](../media/ssas-olapdsv-diagram.gif "снимок экрана: рабочее пространство диаграммы, щелкните правой кнопкой мыши меню")  
  
 Хотя можно спрятать отдельные объекты, команда «Показать связанные таблицы» возвращает все объекты в диаграмме. Чтобы вернуть в рабочее пространство только отдельные объекты, перетащите их из панели «Таблицы» мышью.  
  
##  <a name="bkmk_findtables"></a> Поиск таблиц в диаграмме  
 Если схема большая, то прокрутка до конкретной таблицы на панели **Диаграмма** может быть затруднена. Однако следующие средства облегчают поиск таблицы в диаграмме.  
  
-   Выполните прокрутку списка таблиц на панели **Таблицы** .  
  
     Для включения таблицы в отображаемую в данный момент диаграмму перетащите ее мышью из панели **Таблицы** на панель диаграммы.  
  
     Для выравнивания по центру таблицы, уже включенной в диаграмму, выберите ее на панели **Таблицы** .  
  
-   Указатель таблиц на **схема** таблице панели указатель представляет собой значок четырьмя стрелками, расположенной на пересечении вертикальной и горизонтальной полос прокрутки в правом нижнем углу **схема** области. Он открывает уменьшенное представление текущей диаграммы на панели «Диаграмма». Это уменьшенное представление можно использовать для перемещения представления на панели «Диаграмма» в любое местоположение на диаграмме.  
  
-   Используйте **найти таблицу** диалогового окна поле-правых щелчком на свободную область на панели диаграмм и нажмите кнопку **найти таблицу**. Либо выберите команду **Найти таблицу** на панели инструментов или в меню **Представление источника данных** .  
  
     Можно вводить строки и символы-шаблоны в поле «Фильтр», чтобы просматривать подмножества таблиц в диаграмме.  
  
##  <a name="bkmk_arrangeobjects"></a> Упорядочение объектов в диаграмме  
 Хотя конструктор представлений источников данных позволяет задать несколько диаграмм, чтобы сделать представление источника данных более понятным, диаграммы, содержащие десятки таблиц, может быть трудно читать, а изменение макетов таблиц вручную — это трудоемкий процесс. Конструктор представлений источников данных может автоматически расположить таблицы в текущей диаграмме на основе связей между таблицами в ней, используя прямоугольный или диагональный макет.  
  
-   В прямоугольном макете линии связей чертятся между таблицами, а не между столбцами. Линии связей рисуются горизонтально и вертикально между таблицами.  
  
-   В диагональном макете линии связей чертятся по возможности непосредственно между связанными столбцами в таблицах. Связь с несколькими столбцами присоединяется к первому связанному столбцу в таблице. Если столбцы в таблице не видны, линии чертятся к верхней части таблицы.  
  
##  <a name="bkmk_preserve"></a> Сохранение упорядочивания объектов  
 После того как вы вручную расположили таблицы нужным образом, добавление других таблиц в диаграмму может привести к ее обновлению, при котором все изменения, внесенные в расположение объектов, могут быть потеряны.  
  
 С большей вероятностью это может произойти при добавлении таблицы, в результате которого организатор диаграмм переместит другие таблицы, чтобы разместить новую. Затем оптимизатор перерисовывает диаграмму, чтобы все таблицы и связывающие их линии были представлены правильно. В этот момент все внесенные вручную изменения в расположение конкретных объектов могут быть потеряны.  
  
 Чтобы избежать этой проблемы, добавьте все таблицы, прежде чем задавать окончательные настройки. При этом объекты сохранят свое положение на диаграмме, когда она будет открыта в следующий раз.  
  
## <a name="see-also"></a>См. также  
 [Представления источников данных в многомерных моделях](data-source-views-in-multidimensional-models.md)   
 [Конструктор представлений источников данных (службы Analysis Services — многомерные данные)](../data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
