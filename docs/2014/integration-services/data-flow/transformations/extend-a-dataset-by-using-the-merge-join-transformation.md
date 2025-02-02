---
title: Расширение набора данных с помощью преобразования "Соединение слиянием" | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Merge Join transformation
- datasets [Integration Services], joining
- datasets [Integration Services], extending
- joining datasets [Integration Services]
ms.assetid: 9e512c3c-f89b-45f3-8281-cdb8f35a2b1f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8009dcd369327941004fe220782c38d5602b4dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900307"
---
# <a name="extend-a-dataset-by-using-the-merge-join-transformation"></a>Расширение набора данных при помощи преобразования «Соединение слиянием»
  Чтобы добавить и настроить преобразование «Соединение слиянием», пакет должен содержать по крайней мере одну задачу потока данных и два компонента потока данных, которые используются в качестве входных для преобразования «Соединение слиянием».  
  
 Преобразование «Соединение слиянием» требует наличия двух отсортированных входов. Дополнительные сведения см. в разделе [Сортировка данных для преобразований "Слияние" и "Соединение слиянием"](sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="to-extend-a-dataset"></a>Расширение набора данных  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , содержащий необходимый пакет.  
  
2.  Чтобы открыть пакет, дважды щелкните его в обозревателе решений.  
  
3.  Перейдите на вкладку **Поток данных** и из окна **Область элементов**перенесите преобразование «Соединение слиянием» в область конструктора.  
  
4.  Подключите преобразование «Соединение слиянием» к потоку данных, перетащив соединитель из источника данных или предыдущего преобразования в текущее преобразование «Соединение слиянием».  
  
5.  Дважды щелкните преобразование «Соединение слиянием».  
  
6.  В диалоговом окне **Редактор преобразования «Соединение слиянием»** выберите тип объединения из списка **Тип объединения** .  
  
    > [!NOTE]  
    >  При выборе типа **Левое внешнее соединение** можно щелкнуть **Обменять выходы** для переключения входов и преобразования левого внешнего соединения в правое.  
  
7.  Задайте соединяемые колонки, перетащив столбцы левого входа к колонкам правого входа. Если у столбцов одинаковые имена, то при установке флажка **Ключ соединения** преобразование «Соединение слиянием» автоматически создаст объединение.  
  
    > [!NOTE]  
    >  Можно создавать объединения только между теми столбцами, которые имеют одинаковую позицию сортировки. Объединение должно быть создано согласно указанной позиции сортировки. Если попытаться создать соединения не по порядку, то **Редактор преобразования «Соединение слиянием»** предложит создать дополнительное объединение для пропущенных позиций порядка сортировки.  
  
    > [!NOTE]  
    >  По умолчанию выход отсортирован по столбцам соединения.  
  
8.  В левом и правом входах установите флажки для дополнительных столбцов, которые необходимо включить в выход. Столбцы соединения включаются по умолчанию.  
  
9. Существует дополнительная возможность обновления имен выходных столбцов в столбце **Псевдоним выхода** .  
  
10. Нажмите кнопку **ОК**.  
  
11. Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
## <a name="see-also"></a>См. также  
 [Merge Join Transformation](merge-join-transformation.md)   
 [Преобразования служб Integration Services](integration-services-transformations.md)   
 [Пути служб Integration Services](../integration-services-paths.md)   
 [Задача потока данных](../../control-flow/data-flow-task.md)  
  
  
