---
title: Создание вычисляемого столбца в службах Analysis Services | Документация Майкрософт
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 705428d2c2a6671452a1d95e06e500f4860574e0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472306"
---
# <a name="create-a-calculated-column"></a>Создание вычисляемого столбца
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Вычисляемые столбцы позволяют добавлять новые данные в модель. Вместо вставки или импорта значений в столбце, создается формула DAX, которая определяет значения уровня строк для столбца. Значения для каждой из строк вычисляемого столбца вычисляются и распространяются после создания допустимой формулы и нажатия клавиши ВВОД. После этого можно добавлять вычисляемый столбец в аналитическое приложение или приложение для создания отчетов, как и любой другой столбец данных. В этой статье описывается, как создать новый вычисляемый столбец с помощью строки формул DAX в конструкторе моделей.  
  
#### <a name="to-create-a-new-calculated-column"></a>Создание вычисляемого столбца  
  
1.  В представлении «Данные» конструктора моделей выберите таблицу, в которую необходимо добавить вычисляемый столбец, и в меню **Столбец** выберите пункт **Добавить столбец**.  
  
     Будет выделен пункт**Добавить столбец** над пустым крайним правым столбцом, и курсор переместится в строку формул.  
  
     Чтобы создать новый столбец между двумя существующими, щелкните существующий столбец правой кнопкой мыши и выберите пункт **Вставить столбец**.  
  
2.  В строке формул выполните одно из следующих действий.  
  
    -   Введите знак равенства, а затем формулу.  
  
    -   Введите знак равенства, а затем функцию DAX, аргументы и параметры для этой функции.  
  
    -   Нажмите кнопку функции (**fx**), а затем в диалоговом окне **Вставка функции** выберите категорию и функцию и нажмите кнопку **ОК**. В строке формул введите остальные аргументы и параметры для функции.  
  
3.  Нажмите клавишу ВВОД, чтобы принять формулу.  
  
     Весь столбец будет заполнен формулой, и для каждой строки будет вычислено значение.  
  
> [!TIP]  
>  Можно воспользоваться функцией автозаполнения формул DAX в середине существующей формулы с вложенными функциями. Текст, расположенный непосредственно перед точкой вставки, используется для отображения значений раскрывающегося списка, а остальной текст остается без изменений.  
  
## <a name="see-also"></a>См. также  
 [Вычисляемые столбцы](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Меры](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  
