---
title: Преобразование "Производный столбец" | Документы Майкрософт
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.derivedcolumntrans.f1
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 55da55b347037de5531b8409472ef4c405c55da6
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726126"
---
# <a name="derived-column-transformation"></a>Преобразование «Производный столбец»

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Преобразованием «Производный столбец» создаются новые значения столбцов путем применения выражений к входным столбцам преобразования. Выражения могут содержать любые сочетания переменных, функций, операторов и столбцов из входа преобразования. Результат добавляется в новый столбец или вставляется в существующий как замещающее значение. При преобразовании «Производный столбец» может быть определено несколько производных столбцов, и любая переменная или входные столбцы могут присутствовать в нескольких выражениях.  
  
 Преобразование можно применять для выполнения следующих задач.  
  
-   Объединение данных из различных столбцов в производный столбец. Например, можно объединять значения из столбцов **FirstName** и **LastName** в один производный столбец под названием **FullName**с помощью выражения `FirstName + " " + LastName`.  
  
-   Извлечение символов из строки данных с помощью таких функций, как SUBSTRING, и последующего сохранения результата в производном столбце. Например, можно извлечь инициалы сотрудника из столбца **FirstName** с помощью выражения `SUBSTRING(FirstName,1,1)`.  
  
-   Применение математических функций к числовым данным и сохранение результата в производном столбце. Например, можно заменить длину и точность числового столбца **SalesTax**на число с двумя десятичными знаками с помощью выражения `ROUND(SalesTax, 2)`.  
  
-   Создание выражений, сравнивающих входные столбцы и переменные. Например, можно сравнить переменную **Version** с данными в столбце **ProductVersion**и в зависимости от результата использовать либо значение переменной **Version** , либо значение **ProductVersion**с помощью выражения `ProductVersion == @Version? ProductVersion : @Version`.  
  
-   Извлечение частей из значений типа datetime. Например, с помощью функций GETDATE и DATEPART можно извлечь текущий год с помощью выражения `DATEPART("year",GETDATE())`.  
  
-   Конвертируйте строки даты в определенный формат, используя выражение.  
  
## <a name="configuration-of-the-derived-column-transformation"></a>Настройка преобразования «Производный столбец»  
 Можно настроить преобразование «Производный столбец» следующим образом.  
  
-   Указать выражение для каждого входного столбца или нового столбца, который будет изменен. Дополнительные сведения см. в разделе [Выражения служб Integration Services (SSIS)](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
    > [!NOTE]  
    >  Если выражение ссылается на входной столбец, перезаписанный преобразованием «Производный столбец», то выражение использует первоначальное, а не производное значение столбца.  
  
-   Добавляя результаты в новые столбцы с типом данных **string**, укажите кодовую страницу. Дополнительные сведения см. в разделе [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
 Преобразование "Производный столбец" содержит пользовательское свойство FriendlyExpression. Это свойство может быть обновлено выражением свойства при загрузке пакета. Дополнительные сведения см. в разделах [Использование выражений свойств в пакетах](../../../integration-services/expressions/use-property-expressions-in-packages.md)и [Пользовательские свойства преобразований](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Это преобразование содержит один вход, один обычный вывод и один вывод ошибок.  
  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами.  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Пользовательские свойства преобразований](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Дополнительные сведения о настройке свойств см. в следующих разделах.  
  
-   [Установление свойств компонента потока данных](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Связанные задачи  
  
-   [Получение значений столбцов с помощью преобразования «Производный столбец»](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="derived-column-transformation-editor"></a>редактор преобразования «Производный столбец»
  Используйте диалоговое окно **Редактор преобразования «Производный столбец»** для создания выражений, которые заполняют новые или замещающие столбцы.  
  
### <a name="options"></a>Параметры  
 **Переменные и столбцы**  
 Создайте выражение, которое использует переменную или входной столбец, путем перетаскивания переменной или столбца из списка в существующую строку таблицы на панели внизу или в новую строку внизу списка.  
  
 **Функции и операторы**  
 Создайте выражение, которое использует функцию или оператор, для расчета входных данных и прямых выходных данных, путем перетаскивания функций и операторов из списка на панель внизу.  
  
 **Имя производного столбца**  
 Введите имя производного столбца. По умолчанию используется нумерованный список производных столбцов, однако можно выбрать любое уникальное описательное имя.  
  
 **Производный столбец**  
 Выберите из списка производный столбец. Выберите, добавлять ли производный столбец как новый выходной столбец или заменять данные существующего столбца.  
  
 **Выражение**  
 Введите выражение или создайте его с помощью перетаскивания из предыдущего списка доступных столбцов, переменных, функций и операторов.  
  
 Значение этого свойства можно задать с помощью выражения свойства.  
  
 **См. также:** [Выражения служб Integration Services (SSIS)](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Операторы (выражение служб SSIS)](../../../integration-services/expressions/operators-ssis-expression.md) и [Функции (выражение служб SSIS)](../../../integration-services/expressions/functions-ssis-expression.md).  
  
 **Тип данных**  
 При добавлении данных в новый столбец диалоговое окно **Редактор преобразования "Производный столбец"** автоматически оценивает выражение и задает соответствующий тип данных. Значение этого столбца доступно только для чтения. Дополнительные сведения см. в разделе [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Длина**  
 При добавлении данных в новый столбец диалоговое окно **Редактор преобразования "Производный столбец"** автоматически оценивает выражение и задает длину столбца для строковых данных. Значение этого столбца доступно только для чтения.  
  
 **Точность**  
 При добавлении данных в новый столбец диалоговое окно **Редактор преобразования "Производный столбец"** автоматически задает точность для числовых данных, основываясь на типе данных. Значение этого столбца доступно только для чтения.  
  
 **Масштаб**  
 При добавлении данных в новый столбец диалоговое окно **Редактор преобразования "Производный столбец"** автоматически задает масштаб для числовых данных, основываясь на типе данных. Значение этого столбца доступно только для чтения.  
  
 **Кодовая страница**  
 При добавлении данных в новый столбец диалоговое окно **Редактор преобразования "Производный столбец"** автоматически задает кодовую страницу для типа данных DT_STR. Параметр **Кодовая страница**можно изменить.  
  
 **Настройка вывода ошибок**  
 Укажите способ обработки ошибок в диалоговом окне [Настройка вывода ошибок](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="related-content"></a>См. также  
 Техническая статья [Примеры выражений служб SSIS](https://go.microsoft.com/fwlink/?LinkId=220761)на сайте social.technet.microsoft.com  
