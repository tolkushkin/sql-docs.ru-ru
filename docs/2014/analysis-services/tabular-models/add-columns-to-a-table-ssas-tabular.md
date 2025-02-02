---
title: Добавление столбцов в таблицу (табличные службы SSAS) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5974a3cc-caf8-4558-8836-6e3c24b1ee23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a62460a63bab15499f9aeb4c6510c0e4a9652a7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067772"
---
# <a name="add-columns-to-a-table-ssas-tabular"></a>Добавление столбцов в таблицу (табличные службы SSAS)
  В этом разделе описано добавление столбцов в существующую таблицу.  
  
## <a name="add-columns-from-the-data-source"></a>Добавление столбцов из источника данных  
 Если производится импорт данных из таблицы источника данных с помощью мастера импорта таблиц, то в модели создается новая таблица, которая включает все столбцы исходной таблицы или, если пользователь выбирает фильтрацию некоторых столбцов с помощью функции «Просмотр и фильтрация», только эти столбцы и выбранные с помощью фильтра данные. Можно также создать SQL-запрос, который будет возвращать только столбцы, предназначенные для импорта. Позже может выясниться, что в исходной таблице есть дополнительные столбцы, которые нужно добавить в таблицу модели, или потребуется добавить вычисляемый столбец со значениями формул DAX.  
  
 Например, при начальном импорте данных из источника данных с помощью параметра «Просмотр и фильтрация» был выполнен импорт ограниченного числа столбцов исходной таблицы, а позже выяснилось, что нужно добавить еще один столбец, который существует в исходной таблице, но еще не существует в таблице модели. Или, например, новый столбец AdjustedProfit был добавлен в таблицу FactSales в источнике данных, и теперь нужно добавить такой же столбец AdjustedProfit с теми же данными в таблицу Sales модели.  
  
 В таких случаях можно в диалоговом окне «Изменение свойств таблицы» выбрать столбцы исходной таблицы и добавить их в таблицу модели. Диалоговое окно «Изменение свойств таблицы» включает окно предварительного просмотра таблицы. Окно предварительного просмотра таблицы показывает таблицу в источнике. Столбцы, уже включенные в таблицу модели, отмечены флажками. Столбцы, еще не включенные в таблицу модели, флажками не отмечены. Чтобы добавить столбцы из источника в определение таблицы модели, достаточно выбрать столбец и нажать кнопку «ОК». Окно предварительного просмотра таблицы в диалоговом окне «Изменение свойств таблицы» обеспечивает то же самое представление и те же самые функции, что и окно предварительного просмотра таблицы на странице «Просмотр и фильтрация» в мастере импорта таблиц.  
  
> [!IMPORTANT]  
>  Если столбец добавляется в таблицу, имеющую две или более секции, то, прежде чем добавлять столбец в определение таблицы, созданное с помощью диалогового окна «Изменение свойств таблицы», необходимо в диспетчере секций добавить столбец во все заданные секции. Когда столбец добавлен в заданные секции, то тот же самый столбец можно добавить в определение таблицы в диалоговом окне «Изменение свойств таблицы».  
  
> [!NOTE]  
>  Если при первоначальном импорте данных с помощью мастера импорта данных использовался SQL-запрос, то необходимо вновь воспользоваться SQL-запросом в диалоговом окне «Изменение свойств таблицы» для добавления столбцов в таблицу модели.  
  
#### <a name="to-add-a-column-from-the-data-source-by-using-the-edit-table-properties-dialog-box"></a>Добавление столбца из источника данных с помощью диалогового окна «Изменение свойств таблицы»  
  
1.  В конструкторе моделей выберите таблицу, в которую необходимо добавить столбец, и в меню **Таблица** выберите пункт  **Свойства таблицы**.  
  
2.  В диалоговом окне **Изменение свойств таблицы** в окне предварительного просмотра таблицы выберите столбец исходной таблицы, который необходимо добавить, и нажмите кнопку «ОК». Столбцы, уже включенные в таблицу модели, будут отмечены флажками.  
  
## <a name="add-a-calculated-column"></a>Добавление вычисляемого столбца  
 В вычисляемом столбце формула DAX используется для вычисления значения для каждой строки. Например, можно создать вычисляемый столбец с помощью простой формулы (=1), которая прибавляет единицу к каждой строке. Вычисляемые столбцы могут иметь и более сложные формулы, которые вычисляют значения на основе других данных модели. Вычисляемые столбцы более подробно описаны в других темах. Дополнительные сведения см. в разделе [Вычисляемые столбцы (табличные службы SSAS)](ssas-calculated-columns.md).  
  
#### <a name="to-create-a-calculated-column"></a>Создание вычисляемого столбца  
  
1.  В представлении данных конструктора моделей выберите таблицу, в которую необходимо добавить новый пустой вычисляемый столбец, прокруткой перейдите в самый правый столбец или в меню **Столбец** выберите пункт **Добавить столбец**.  
  
     Чтобы создать новый столбец между двумя существующими, щелкните существующий столбец правой кнопкой мыши и выберите пункт **Вставить столбец**.  
  
2.  В строке формул введите формулу DAX для добавления атрибутов для каждой строки.  
  
## <a name="add-a-blank-column"></a>Добавление пустого столбца  
 В таблице модели можно создать именованный пустой столбец. Пустые столбцы могут оказаться полезными в том случае, если необходимо вставить данные из другого источника. Помните, что вставленные данные хранятся не так, как импортированные. Дополнительные сведения см. в разделе [Копирование и вставка данных (табличные службы SSAS)](../copy-and-paste-data-ssas-tabular.md).  
  
#### <a name="to-create-a-named-blank-column"></a>Создание пустого именованного столбца  
  
1.  В представлении данных конструктора моделей выберите таблицу, в которую необходимо добавить пустой столбец, прокруткой перейдите в самый правый столбец или в меню **Столбец** выберите пункт **Добавить столбец**.  
  
     Чтобы создать новый столбец между двумя существующими, щелкните существующий столбец правой кнопкой мыши и выберите пункт **Вставить столбец**.  
  
2.  Щелкните верхнюю ячейку, введите имя и нажмите клавишу ВВОД.  
  
## <a name="see-also"></a>См. также  
 [Диалоговое окно "Изменение свойств таблицы" (службы SSAS)](../edit-table-properties-dialog-box-ssas.md)   
 [Изменение сопоставлений фильтров таблиц, столбцов и строк (табличные службы SSAS)](change-table-column-or-row-filter-mappings-ssas-tabular.md)  
  
  
