---
title: Добавление интерактивной сортировки в таблицу или матрицу (построитель отчетов и службы SSRS) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10121"
- sql12.rtp.rptdesigner.textboxproperties.intrctvsort.f1
ms.assetid: 05819637-729b-4cf6-82de-91a99f184ec6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 961a2a76f2a839ccc9fa8fb90027bec180d870d6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106634"
---
# <a name="add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs"></a>Добавление интерактивной сортировки в таблицу или матрицу (построитель отчетов и службы SSRS)
  Добавьте кнопки интерактивной сортировки, чтобы дать пользователям возможность менять порядок сортировки строк и столбцов в таблицах или матрицах. Эта возможность доступна только в форматах подготовки к просмотру, поддерживающих взаимодействие с пользователем, например HTML.  
  
 При создании кнопки интерактивной сортировки необходимо задать объект сортировки, ключ сортировки и область, к которой она применяется. Например, можно сортировать строки подробностей по фамилии клиента, значения группы подкатегории в группе категорий по продажам или объединенные значения категории и группы подкатегории по итогам.  
  
 При просмотре отчета в столбцах, поддерживающих интерактивную сортировку, отображаются значки-стрелки, указывающие порядок сортировки. Если нажать кнопку интерактивной сортировки в первый раз, элементы сортируются по возрастанию. Последующие нажатия кнопки позволяют переключать порядок сортировки по возрастанию на сортировку по убыванию и наоборот.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="BackToTop"></a> В данной статье  
 [Сортировка строк подробностей в таблице без групп](#SortingDetailRows)  
  
 [Сортировка родительской группы строк высшего уровня в таблице или матрице](#SortingTopLevelParent)  
  
 [Сортировка дочерних групп или строк подробностей в группе](#SortingChildGroups)  
  
 [Сортировка строк по сложному выражению группы](#SortingMultipleRowGroups)  
  
 [Синхронизация порядка сортировки в нескольких областях данных](#SynchronizingSortOrder)  
  
##  <a name="SortingDetailRows"></a> Сортировка строк подробностей в таблице без групп  
 Добавьте кнопку интерактивной сортировки в заголовок столбца, чтобы дать пользователю возможность щелкнуть заголовок столбца и отсортировать строки подробностей по значению этого столбца.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-the-table-by-value"></a>Добавление кнопки интерактивной сортировки в заголовок столбца для сортировки таблицы по значению этого столбца  
  
1.  В представлении конструктора отчета в таблице без групп щелкните правой кнопкой мыши текстовое поле заголовка нужного столбца и выберите **Свойства текстового поля**.  
  
2.  Щелкните **Интерактивная сортировка**.  
  
3.  Выберите **Включить интерактивную сортировку для этого текстового поля**.  
  
4.  В области **Выберите данные для сортировки**щелкните **Строки детализации**.  
  
5.  В поле **Сортировать по**укажите выражение сортировки. В раскрывающемся списке выберите поле, соответствующее столбцу, для которого определяется действие сортировки (например, для столбца "Title" выберите `[Title]`). Указание выражения сортировки обязательно.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Повторите шаги 1–6 для каждого столбца, в который нужно добавить кнопку интерактивной сортировки.  
  
 Чтобы проверить, как работает сортировка, нажмите кнопку **Выполнить** для предварительного просмотра отчета, а затем нажмите кнопку интерактивной сортировки.  
  
 ![Значок стрелки, используемый для ссылки возврата в начало](../../2014-toc/media/uparrow16x16.gif "Значок стрелки, используемый для ссылки возврата в начало") [В начало](#BackToTop)  
  
##  <a name="SortingTopLevelParent"></a> Сортировка родительской группы строк высшего уровня в таблице или матрице  
 Добавьте кнопку интерактивной сортировки в заголовок столбца, чтобы дать пользователю возможность щелкнуть заголовок столбца и отсортировать строки родительской группы в таблице или матрице по значению этого столбца. Порядок сортировки дочерних групп остается прежним.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-groups"></a>Добавление кнопки интерактивной сортировки в заголовок столбца для сортировки групп  
  
1.  В представлении конструктора отчета в таблице или матрице щелкните правой кнопкой мыши текстовое поле заголовка нужной группы и выберите **Свойства текстового поля**.  
  
2.  Щелкните **Интерактивная сортировка**.  
  
3.  Выберите **Включить интерактивную сортировку для этого текстового поля**.  
  
4.  В области **Выбор данных для сортировки**щелкните **Группы**.  
  
5.  В раскрывающемся списке выберите имя нужной группы. Для групп на основе простых выражений групп значение поля **Сортировать по** заполняется выражением группы.  
  
    > [!NOTE]  
    >  Для групп на основе сложных выражений вручную введите выражение группы в поле **Сортировать по** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Чтобы проверить, как работает сортировка, нажмите кнопку **Выполнить** для предварительного просмотра отчета, а затем нажмите кнопку интерактивной сортировки.  
  
 ![Значок стрелки, используемый для ссылки возврата в начало](../../2014-toc/media/uparrow16x16.gif "Значок стрелки, используемый для ссылки возврата в начало") [В начало](#BackToTop)  
  
##  <a name="SortingChildGroups"></a> Сортировка дочерних групп или строк подробностей в группе  
 Добавьте кнопку интерактивной сортировки в строку заголовка группы, чтобы дать пользователю возможность отсортировать значения дочерней группы из родительской или строки подробностей в дочерней группе самого нижнего уровня.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-text-box-in-a-group-row-header-to-sort-child-groups-or-detail-rows"></a>Добавление кнопки интерактивной сортировки в текстовое поле строки заголовка группы для сортировки дочерних групп или строк подробностей  
  
1.  В представлении конструктора отчета щелкните правой кнопкой мыши текстовое поле строки заголовка группы, к которой нужно добавить кнопку интерактивной сортировки, и выберите **Свойства текстового поля**.  
  
2.  Щелкните **Интерактивная сортировка**.  
  
3.  Выберите **Включить интерактивную сортировку для этого текстового поля**.  
  
4.  В области **Выбор данных для сортировки**выберите один из следующих параметров.  
  
    -   **Подробности** . Щелкните **Подробности** для сортировки строк подробностей. В раскрывающемся списке выберите нужное поле. Для этого параметра необходимо задать значение сортировки.  
  
    -   **Группы** .   Щелкните **Группы** для сортировки значений дочерних групп. Для этого параметра поле **Сортировать по** автоматически заполняется выражением группы.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Чтобы проверить, как работает сортировка, нажмите кнопку **Выполнить** для предварительного просмотра отчета, а затем нажмите кнопку интерактивной сортировки.  
  
 ![Значок стрелки, используемый для ссылки возврата в начало](../../2014-toc/media/uparrow16x16.gif "Значок стрелки, используемый для ссылки возврата в начало") [В начало](#BackToTop)  
  
##  <a name="SortingMultipleRowGroups"></a> Сортировка строк по сложному выражению группы  
 Добавьте кнопку интерактивной сортировки в заголовок столбца, чтобы дать пользователю возможность щелкнуть заголовок столбца и совместно отсортировать родительские и дочерние группы. Для этого необходимо изменить выражение группы так, чтобы оно включало обе группы. Например, предположим, что матрица содержит итоги запасов склада для элементов, сгруппированных как по цвету, так и по размеру. Чтобы отсортировать строки одновременно по цвету и размеру, вместо отдельных групп можно определить общую группу на основе комбинации размера и цвета. Дополнительные сведения об определении выражений групп см. в разделе [Примеры выражений групп &#40;построитель отчетов и службы SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
 В следующей процедуре выражения задают области данных табликса. Дополнительные сведения см. в разделе [Области данных табликса &#40;построитель отчетов и службы SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 Как правило, при сортировке строк по нескольким группам требуется просматривать итоги для отсортированных строк независимо от групп столбцов. В этой процедуре группы столбцов не используются. Она начинается с добавления матрицы и удаления группы столбцов по умолчанию. Можно также начать с добавления таблицы и удаления группы подробностей.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-multiple-groups"></a>Добавление кнопки интерактивной сортировки в заголовок столбца для сортировки нескольких групп  
  
1.  В представлении конструктора отчетов добавьте матрицу.  
  
2.  Перетащите числовое поле в ячейку данных, чтобы связать набор данных с матрицей.  
  
     Затем создается группа с выражением группы, в котором указывается несколько полей, и заголовок группы для отображения значений группы.  
  
3.  Убедитесь, что матрица выбрана в области конструктора. В панели группирования будут отображены группы столбцов и строк по умолчанию.  
  
4.  В панели "Группы строк" щелкните правой кнопкой мыши группу строк по умолчанию и выберите пункт **Изменить группу**. Откроется диалоговое окно **Свойства группы** .  
  
5.  В поле **Имя**замените имя по умолчанию именем, определяющим несколько групп, по которым нужно выполнить сортировку.  
  
6.  В **Выражения группы**в области **Группировать по**нажмите кнопку "Выражение" (**fx**), чтобы открыть диалоговое окно **Выражение** .  
  
7.  Введите выражение, указывающее все нужные поля. Например, следующее выражение группы объединяет поля "Цвет" и "Размер": `=Fields!Color.Value & Fields!Size.Value`.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Группа успешно определена. Затем перетащите поля для отображения в область текста табликса матрицы. Добавьте поля, выбранные для группирования на шаге 7, в область текста табликса, каждое в собственный столбец.  
  
     Для этого сценария не требуется первый столбец в области групп строк табликса. Чтобы удалить столбец, щелкните правой кнопкой мыши заголовок столбца и выберите команду **Удалить столбцы**. В диалоговом окне появится вопрос, нужно ли удалять связанные группы. Нажмите кнопку **Нет**. Область группы строк удаляется, и остается только область текста табликса.  
  
     После этого удаляется группа столбцов по умолчанию.  
  
9. В панели "Группы столбцов" щелкните правой кнопкой мыши группу столбцов по умолчанию и выберите пункт **Удалить группу**. В диалоговом окне появится вопрос, следует ли удалить группу и связанные строки и столбцы или только группу. Щелкните **Удалить только группу**. Удаляется группа столбцов и область группы столбцов. Остается только область текста табликса.  
  
     После этого добавляется кнопка интерактивной сортировки к текстовому полю, охватывающему эту матрицу.  
  
10. Щелкните правой кнопкой мыши текстовое поле первой строки и выберите **Свойства текстового поля**.  
  
11. Щелкните **Интерактивная сортировка**.  
  
12. Выберите **Включить интерактивную сортировку для этого текстового поля**.  
  
13. В области **Выбор данных для сортировки**щелкните **Группы**.  
  
14. В раскрывающемся списке выберите имя группы, созданной на шаге 5. Выражение группы автоматически копируется в текстовое поле **Сортировать по** .  
  
15. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Кнопка интерактивной сортировки успешно добавлена в текстовое поле.  
  
16. Можно запретить вывод дублирующихся значений в столбцах, отображающих значения группы (необязательно). В области конструктора отчета щелкните текстовое поле, где выводится значение, для которого нужно скрыть повторяющиеся значения. На панели "Свойства" перейдите к **HideDuplicates**и в раскрывающемся списке выберите имя набора данных, связанного с этой матрицей.  
  
 Чтобы проверить, как работает сортировка, нажмите кнопку **Выполнить** для предварительного просмотра отчета, а затем нажмите кнопку интерактивной сортировки. Матрица сортируется по объединенным значениям выражения группы, хотя каждое отдельное значение отображается в собственном столбце.  
  
 ![Значок стрелки, используемый для ссылки возврата в начало](../../2014-toc/media/uparrow16x16.gif "Значок стрелки, используемый для ссылки возврата в начало") [В начало](#BackToTop)  
  
##  <a name="SynchronizingSortOrder"></a> Синхронизация порядка сортировки в нескольких областях данных  
 Добавьте кнопку интерактивной сортировки, которая позволяет сортировать несколько областей данных. При создании кнопки интерактивной сортировки можно указать возможность синхронизации сортировки для нескольких областей данных на основе одного набора данных отчета. Например, отчет может включать матрицу и диаграмму, графически отображающую данные. Когда пользователь меняет порядок сортировки строк в матрице, он автоматически отображается на диаграмме.  
  
 Чтобы синхронизировать порядок сортировки, необходимо использовать идентичные выражения сортировки для областей данных или групп и определить область действия сортировки как общего предка обеих областей данных. Общим предком может быть набор данных, с которым связаны обе области данных, или область данных, в которой содержатся обе области данных. Например, предположим, что в отчете имеется матрица и диаграмма, отображающая данные из того же набора данных, содержащихся в списке. Чтобы синхронизировать действие сортировки, необходимо задать интерактивную сортировку в столбце матрицы и назначить список ее областью действия. Если пользователь сортирует матрицу, сортируется и диаграмма.  
  
#### <a name="to-synchronize-sort-order-with-a-chart-for-an-interactive-sort-button-on-a-matrix-data-region"></a>Синхронизация порядка сортировки с диаграммой для кнопки интерактивной сортировки в матричную область данных  
  
1.  В представлении конструктора отчетов добавьте матрицу в отчет.  
  
2.  Добавьте в ячейку матрицы числовое поле набора данных, например поле, представляющее количество продаж.  
  
3.  Определите группу строк. По умолчанию порядок сортировки группы равен выражению группы.  
  
4.  Добавьте к отчету диаграмму, например, круговую.  
  
5.  Перетащите поле, выбранное на шаге 2, в область **Значение** на панели **Данные диаграммы** .  
  
6.  Перетащите поле, по которому будет производиться группирование, в область **Группы категорий** .  
  
     Выражение группы для группы строк матрицы и группы категорий диаграммы должны быть одинаковыми.  
  
7.  Щелкните правой кнопкой мыши группу категорий и выберите пункт **Свойств группы категорий**.  
  
8.  Щелкните **Сортировка**.  
  
9. Нажмите кнопку **Добавить**. В сетку параметров сортировки добавится новая строка сортировки.  
  
10. В поле «Сортировать по» выберите из раскрывающегося списка то же поле, которое было добавлено на шаге 6 для группирования.  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
12. В матрице щелкните правой кнопкой мыши текстовое поле заголовка столбца, к которому нужно добавить кнопку интерактивной сортировки, и выберите **Свойства текстового поля**.  
  
13. Щелкните **Интерактивная сортировка**.  
  
14. Выберите **Включить интерактивную сортировку для этого текстового поля**.  
  
15. В области **Выбор данных для сортировки**щелкните **Группы**.  
  
16. В раскрывающемся списке **Группы**выберите имя нужной группы. Выражение этой группы автоматически принимает значение поля **Сортировать по** .  
  
17. Выберите **Также применять эту сортировку к другим группам и областям данных в:**. Введите в текстовое поле имя набора данных, например «SalesData».  
  
18. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Чтобы проверить, как работает сортировка, нажмите кнопку **Выполнить** для предварительного просмотра отчета, а затем нажмите кнопку интерактивной сортировки. Матрица сортируется по объединенным значениям выражения группы, хотя каждое отдельное значение отображается в собственном столбце.  
  
 ![Значок стрелки, используемый для ссылки возврата в начало](../../2014-toc/media/uparrow16x16.gif "Значок стрелки, используемый для ссылки возврата в начало") [В начало](#BackToTop)  
  
## <a name="see-also"></a>См. также  
 [Фильтрация, группирование и сортировка данных (построитель отчетов и службы SSRS)](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Интерактивная сортировка &#40;построитель отчетов и службы SSRS&#41;](interactive-sort-report-builder-and-ssrs.md)   
 [Сортировка данных в области данных (построитель отчетов и службы SSRS)](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Изучение возможностей области данных табликса &#40;построитель отчетов и службы SSRS&#41;](exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)  
  
  
