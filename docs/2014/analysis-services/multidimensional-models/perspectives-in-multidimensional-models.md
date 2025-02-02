---
title: Перспективы в многомерных моделях | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- default members
- hiding objects from perspective
- renaming perspectives
- attributes [Analysis Services], default members
- removing perspectives
- perspectives [Analysis Services]
- names [Analysis Services], perspectives
- cubes [Analysis Services], perspectives
- deleting perspectives
ms.assetid: 5a3d6577-6833-4c24-820c-b65bb856157b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d9c408f79dcecd0a7850c7361716cc29b07f4cf9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073349"
---
# <a name="perspectives-in-multidimensional-models"></a>Перспективы в многомерных моделях
  Перспектива представляет собой подмножество куба, созданное для отдельного приложения или группы пользователей. Перспективой по умолчанию является собственно куб. Перспектива открыта для клиента в виде куба. Когда пользователь просматривает перспективу, она отображается в виде другого куба. Изменения, выполненные с данными куба при обратной записи в перспективу, выполняются в исходном кубе. Дополнительные сведения о представлениях см. в разделах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]и [Перспективы](../multidimensional-models-olap-logical-cube-objects/perspectives.md).  
  
 Используйте вкладку **Перспективы** в конструкторе кубов для создания или измерения перспектив в кубе. Первый столбец на вкладке **Перспективы** — столбец **Объекты куба** , в котором перечислены объекты куба. Это соответствует перспективе куба по умолчанию, то есть собственно кубу.  
  
## <a name="creating-or-deleting-perspectives"></a>Создание или удаление перспектив  
 На вкладке **Перспективы** можно добавить перспективу с помощью команды **Создать перспективу** в меню **Куб** . Можно нажать кнопку **Создать перспективу** на панели инструментов или щелкнуть правой кнопкой мыши в любом месте панели и выбрать в контекстном меню пункт **Создать перспективу** . К кубу можно добавлять любое количество перспектив.  
  
 Для удаления перспективы сначала щелкните в любой ячейке столбца с перспективой, которую требуется удалить. Затем в меню **Куб** выберите пункт **Удалить перспективу**. Также можно нажать кнопку **Удалить перспективу** на панели инструментов или щелкнуть правой кнопкой мыши в любой ячейке перспективы, которую требуется удалить, и выбрать в контекстном меню пункт **Удалить перспективу** .  
  
## <a name="renaming-perspectives"></a>переименование перспектив  
 В первой строке перспектив представлено имя перспективы. При создании перспективы ее исходное имя — Perspective (далее следует порядковый номер, начинающийся с 1, если уже имеется проекция с именем Perspective). Щелкните имя для его редактирования.  
  
## <a name="hiding-objects-from-a-perspective"></a>Скрытие объектов в перспективе  
 Чтобы скрыть объект в перспективе, снимите флажок в строке, соответствующей объекту, в столбце перспективы. В перспективе можно скрыть следующие объекты куба:  
  
-   Группы мер  
  
-   меры  
  
-   Измерения  
  
-   Иерархии  
  
-   Именованные наборы  
  
-   Ключевые показатели эффективности  
  
-   Действия  
  
-   Вычисляемые элементы  
  
 Чтобы просмотреть объект, разверните категорию (**Группы мер**, **Измерения**, **Ключевые показатели эффективности**, **Вычисления**или **Действия**) для любого типа объекта в узле **Объекты куба**. Чтобы просмотреть иерархии или атрибуты в измерении, сначала разверните измерение, а затем строку **Иерархии** или **Атрибуты** . Чтобы просмотреть меры в группе мер, разверните группу.  
  
## <a name="see-also"></a>См. также  
 [Кубы в многомерных моделях](cubes-in-multidimensional-models.md)  
  
  
