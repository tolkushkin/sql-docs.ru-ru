---
title: Типы данных поддерживаются в табличных моделях служб Analysis Services | Документация Майкрософт
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 33618c019e59c044e681c45130130adc79d53122
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472203"
---
# <a name="data-types-supported-in-tabular-models"></a>Типы данных поддерживаются в табличных моделях
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  В этом разделе описаны типы данных, которые можно использовать в табличных моделях, и рассматривается неявное преобразование типов данных, выполняемое при вычислении данных или их использовании в формуле выражения анализа данных (DAX).  

  
##  <a name="bkmk_data_types"></a> Типы данных, используемые в табличных моделях  
При импорте данных или использовании значения в формуле, даже если исходный источник данных содержит другой тип данных, данные преобразуются в один из следующих типов. Эти типы данных также используются для значений, являющихся результатами вычисления формул.  
  
 В целом такие типы данных реализованы для поддержки точных вычислений в вычисляемых столбцах, а в целях обеспечения согласованности такие же ограничения применяются к остальным данным в моделях.  
  
 Форматы, используемые для чисел, валюты, значений даты и времени должны соответствовать формату локали, указанному на клиенте, используемом для работы с данными модели. Для управления отображением значения используются параметры форматирования в модели.  
  
||||  
|-|-|-|  
|**Тип данных в модели**|**Тип данных в DAX**|**Описание**|  
|Whole Number|64-разрядное (8-байтовое) целочисленное значение*<br /><br /> Примечание.<br />         В формулах DAX не поддерживаются типы данных, которые слишком малы для хранения минимального значения, указанного в описании.|Числа без десятичных разрядов. Целые числа могут быть положительными или отрицательными, но не могут содержать дробную часть в диапазоне -9,223,372,036,854,775,808 (-2^63) и 9,223,372,036,854,775,807 (2^63-1).|  
|Десятичное число|64-разрядное (8 байтовое) вещественное число *<br /><br /> Примечание.<br />         В формулах DAX не поддерживаются типы данных, которые слишком малы для хранения минимального значения, указанного в описании.|Вещественные числа — это числа, которые могут иметь знаки после запятой. Вещественные числа включают широкий диапазон значений.<br /><br /> Отрицательные числа от -1.79E +308 до -2.23E -308<br /><br /> Zero<br /><br /> Положительные числа от 2.23E -308 до 1.79E + 308<br /><br /> Однако количество значащих цифр ограничено 17 знаками после запятой.|  
|Логическое значение|Логическое значение|Значение True или False.|  
|Text|String|Строка символьных данных в Юникоде. Может быть строками, числами или датами, представленными в текстовом формате.|  
|Дата|Дата-время|Значения даты и времени в принятом представлении даты-времени.<br /><br /> Допустимый диапазон дат включает значения после 1 марта 1900г.|  
|CURRENCY|CURRENCY|Тип данных "Валюта" включает значения в диапазоне от -922,337,203,685,477.5808 до 922,337,203,685,477.5807 с четырьмя десятичными знаками заданной точности.|  
|Н/Д|Пусто|Тип данных с пустыми значениями в DAX представляет и заменяет пустые значения NULL в SQL. Пустое значение создается с помощью функции BLANK, а проверяется с помощью логической функции ISBLANK.|  
  
 \* Если вы попытаетесь импортировать данные с большими числовыми значениями, Импорт может завершиться со следующей ошибкой:  
  
 Ошибка базы данных в памяти: "\<Имя столбца >" столбец "\<имя таблицы >" таблица содержит значение "1.7976931348623157E + 308», которое не поддерживается. Операция была отменена.  
  
 Эта ошибка возникла из-за того, что конструктор моделей использует это значение для представления значений NULL. В следующем списке описаны значения, которые являются синонимами ранее упомянутого значения NULL:  
  
||  
|-|  
|Значение|  
|9223372036854775807|  
|-9223372036854775808|  
|1.7976931348623158e+308|  
|2.2250738585072014e-308|  
  
 Удалить значение из данных и повторите попытку импорта.  
  
> [!NOTE]  
>  Невозможен импорт данных из столбца **varchar(max)** , который содержит строку длиной более 131 072 символов.  
  
### <a name="table-data-type"></a>table, тип данных  
 Кроме того, в DAX используется тип данных *table* . Этот тип данных работает во многих функциях DAX, в том числе в агрегатах и в логике операций со временем. Для некоторых функций необходима ссылка на таблицу, а другие функции возвращают таблицу, которая может служить входным аргументом функций первого типа. В некоторых функциях, входным аргументом которых должна быть таблица, может быть указано выражение, результатом которого является таблица, а некоторым из функций требуется ссылка на базовую таблицу. Сведения о требованиях конкретных функций см. в [справочнике по функциям DAX](http://msdn.microsoft.com/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
##  <a name="bkmk_implicit"></a> Явное и неявное преобразование типов в формулах DAX
  
 Каждая функция DAX обладает особыми требованиями к типу входных и выходных данных. Например, часть аргументов некоторых функций должны быть целыми числами, а другая часть — значениями даты. Для других функций требуется текст или таблицы.  
  
 Если данные в столбце, указанном в качестве аргумента несовместим с типом данных, необходимых для функции, во многих случаях DAX возвращает ошибку. Тем не менее везде, где возможных DAX пытается выполнить неявное преобразование данных в требуемый тип данных. Пример:  
  
-   Можно ввести номер, например «123», как строка. DAX анализирует строку и попытается указать ее как числовой тип данных.  
  
-   Можно выполнить сложение TRUE + 1 и получить результат 2, поскольку значение TRUE неявно преобразуется в число 1, и выполняется операция 1 + 1.  
  
-   Если складываются значения из двух столбцов и одно из значений представлено в виде текста («12»), а другое — в виде числа 12, то DAX выполняет неявное преобразование строки в число, а затем выполнит сложение, чтобы получить числовой результат. Выражение = "22"+22 возвращает значение 44.  
  
-   Если выполнить попытку объединить два числа, они представлены в виде строки и затем сцепляются. Выражение = 12&34 возвращает значение "1234".  
  
 В следующей таблице представлены неявные преобразования типов данных, выполняемые в формулах. В целом конструктор семантических моделей работает аналогично Microsoft Excel, по возможности выполняя неявные преобразования всегда, где это необходимо для выполнения операции.  
  
### <a name="table-of-implicit-data-conversions"></a>Таблица неявных преобразований данных  
 Тип выполняемого преобразования определяется оператором, который приводит требуемые значения к нужному типу перед выполнением запрошенной операции. В следующих таблицах перечислены операторы и указано преобразование, выполняемое для каждого типа данных в столбце, когда этот тип встречается вместе с типом данных из пересекающейся строки.  
  
> [!NOTE]  
>  В эти таблицы не входят текстовые типы данных. Если число представлено в формате текста, в некоторых случаях конструктор моделей пытается определить числовой тип и представить значение в виде числа.  
  
#### <a name="addition-"></a>Сложение (+)  
  
||||||  
|-|-|-|-|-|  
|Оператор (+)|INTEGER|Измерение валют|real|Дата-время|  
|INTEGER|INTEGER|Измерение валют|real|Дата-время|  
|CURRENCY|CURRENCY|CURRENCY|real|Дата-время|  
|real|real|real|real|Дата-время|  
|Дата/время|Дата/время|Дата/время|Дата/время|Дата-время|  
  
 Например, если в операции сложения используется вещественное число со значением денежной единицы, то оба значения преобразуются в тип REAL и возвращаемый результат имеет тип REAL.  
  
#### <a name="subtraction--"></a>Вычитание (-)  
 В следующей таблице заголовок строки является уменьшаемым (слева) и заголовок столбца — вычитаемым (справа):  
  
||||||  
|-|-|-|-|-|  
|Оператор (-)|INTEGER|Измерение валют|real|Дата-время|  
|INTEGER|INTEGER|Измерение валют|real|real|  
|CURRENCY|CURRENCY|CURRENCY|real|real|  
|real|real|real|real|real|  
|Дата-время|Дата/время|Дата/время|Дата/время|Дата-время|  
  
 Например, если в операции вычитания дата используется вместе с любым другим типом данных, то оба значения преобразуются в значения даты и возвращаемое значение будет иметь тип даты.  
  
> [!NOTE]  
>  Табличные модели поддерживают также унарный оператор «-» (отрицание), однако этот оператор не изменяет тип данных операнда.  
  
#### <a name="multiplication-"></a>Умножение (*)  
  
||||||  
|-|-|-|-|-|  
|Оператор (*)|INTEGER|Измерение валют|real|Дата-время|  
|INTEGER|INTEGER|Измерение валют|real|INTEGER|  
|CURRENCY|CURRENCY|real|CURRENCY|CURRENCY|  
|real|real|CURRENCY|real|real|  
  
 Например, если в операции умножения целое число используется вместе с вещественным, то оба числа преобразуются в вещественные и возвращаемое значение также будет иметь тип REAL.  
  
#### <a name="division-"></a>Деление (/)  
 В следующей таблице заголовок строки содержит значение числителя, а заголовок столбца содержит знаменатель.  
  
||||||  
|-|-|-|-|-|  
|Оператор (/)<br /><br /> (Строка/столбец)|INTEGER|Измерение валют|real|Дата-время|  
|INTEGER|real|CURRENCY|real|real|  
|CURRENCY|CURRENCY|real|CURRENCY|real|  
|real|real|real|real|real|  
|Дата-время|real|real|real|real|  
  
 Например, если в операции деления целое число используется вместе со значением денежной единицы, то оба значения преобразуются в вещественные числа, при этом результат также будет вещественным числом.  
  
#### <a name="comparison-operators"></a>Операторы сравнения  
Поддерживается только ограниченный набор сочетаний смешанного типа данных для операций сравнения значений. Дополнительные сведения см. в статье [Справочник по операторам DAX](https://msdn.microsoft.com/library/ee634237.aspx).  
  
## <a name="bkmk_hand_blanks"></a> Обработка пустых значений, пустых строк и нулевых значений  
 В следующей таблице перечислены различия между DAX и в Microsoft Excel, в обработке пустых значений:  
  
||||  
|-|-|-|  
|Выражение|DAX|Excel|  
|BLANK + BLANK|BLANK|0 (ноль)|  
|BLANK +5|5|5|  
|BLANK * 5|BLANK|0 (ноль)|  
|5/ПУСТО|Бесконечность|Ошибка|  
|0/BLANK|NaN|Ошибка|  
|BLANK/BLANK|Пусто|Ошибка|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|BLANK|Ошибка|  
|BLANK AND BLANK|BLANK|Ошибка|  
  
 Подробные сведения об обработке пустых значений в отдельных функциях и операторах см. в статьях и разделах [справочника по функциям DAX](http://msdn.microsoft.com/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b), посвященных соответствующим функциям.  
  
