---
title: Базовый запрос многомерных Выражений (многомерные Выражения) | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61975b6b24cda25454d10eb1eeb5b452cad0f1ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63025568"
---
# <a name="mdx-query---the-basic-query"></a>Запрос многомерных выражений — базовый запрос
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Базовый запрос многомерных выражений (MDX) — это запрос SELECT инструкция наиболее часто используемые в многомерных Выражениях. Чтобы получить основательные знания о применении многомерных выражений для запроса многомерных данных, необходимо понять, как в инструкции многомерных выражений SELECT определяется результирующий набор, синтаксис инструкции SELECT и как с ее помощью создавать простые запросы.  
  
## <a name="specifying-a-result-set"></a>Указание результирующего набора  
 В многомерном выражении инструкция SELECT указывает результирующий набор, содержащий подмножество многомерных данных, возвращаемое из куба. Чтобы указать результирующий набор, запрос многомерных выражений должен содержать следующие данные.  
  
-   Число осей, которое должно содержаться в результирующем наборе. В многомерном запросе можно указать до 128 осей.  
  
-   Набор элементов или кортежей, включаемых в каждую ось многомерного запроса.  
  
-   Имя куба, задающего контекст многомерного запроса.  
  
-   Набор элементов или кортежей, включаемых в ось среза. Дополнительные сведения об осях среза и запроса см. в разделе [Ограничение запроса с помощью осей запроса и среза (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md).  
  
 Для указания осей запроса куба, к которому направлен запрос, и осей среза в инструкции многомерных выражений SELECT используются следующие предложения.  
  
-   Предложение SELECT, определяющее оси запроса в инструкции многомерных выражений SELECT. Дополнительные сведения о построении осей запроса в предложении SELECT см. в разделе [Определение содержимого оси запроса (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   Предложение FROM, определяющее, к какому кубу будет направлен запрос. Дополнительные сведения о предложении FROM см. в разделе [Инструкция SELECT (многомерные выражения)](../../../mdx/mdx-data-manipulation-select.md).  
  
-   Необязательное предложение WHERE, определяющее, какие элементы или кортежи используются на оси среза для ограничения возвращаемых данных. Дополнительные сведения о построении осей среза в предложении WHERE см. в разделе [Определение содержимого оси среза (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
> [!NOTE]  
>  Дополнительные сведения о различных предложениях инструкции SELECT см. в разделе [Инструкция SELECT (многомерные выражения)](../../../mdx/mdx-data-manipulation-select.md).  
  
## <a name="select-statement-syntax"></a>Синтаксис инструкции SELECT  
 В следующей конструкции иллюстрируется синтаксис базовой инструкции SELECT с использованием предложений SELECT, FROM и WHERE:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 Инструкция многомерных выражений SELECT поддерживает дополнительный синтаксис, например: ключевое слово WITH, использование функций многомерных выражений для создания вычисляемых элементов, включаемых в ось запроса или среза, а также возможность возвращать значения свойств определенных ячеек как части запроса. Дополнительные сведения об инструкции SELECT многомерных выражений см. в разделе [Инструкция SELECT (многомерные выражения)](../../../mdx/mdx-data-manipulation-select.md).  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>Сравнение синтаксиса инструкции многомерных выражений SELECT с синтаксисом SQL  
 Формат синтаксиса для инструкции многомерных выражений SELECT сходен с синтаксисом ее аналога в SQL. Тем не менее есть несколько серьезных отличий.  
  
-   В синтаксисе многомерных выражений наборы различаются путем заключения кортежей и элементов в фигурные скобки (символы { и }). Дополнительные сведения о элементах, кортежах и синтаксисе наборов см. в разделе [Работа с элементами, кортежами и наборами (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
-   Запросы многомерных выражений могут содержать 0, 1,2 или до 128 осей запросов в инструкции SELECT. Поведение всех осей одинаково, в отличие от SQL, где имеются значительные различия в поведении строк и столбцов в запросе.  
  
-   Как и в SQL-запросе, предложение FROM указывает источник данных для запроса многомерных выражений. Однако предложение многомерных выражений FROM ограничивается одним кубом. Сведения из других кубов могут быть получены по значению с помощью функции LookupCube.  
  
-   Предложение WHERE определяет ось среза в многомерном запросе. Оно действует наподобие невидимой дополнительной оси в запросе, создавая срезы значений в ячейках результирующего набора, в то время как в SQL предложение WHERE не влияет напрямую на ось строк в запросе. Функциональные возможности предложения SQL WHERE доступны через другие функции многомерных выражений, такие как функция FILTER.  
  
## <a name="select-statement-example"></a>Пример инструкции SELECT  
 В следующем примере показан базовый запрос многомерных выражений на основе инструкции SELECT. Этот запрос возвращает результирующий набор, содержащий продажи за 2002 и 2003 годы и сумму налогов для юго-западных областей продаж.  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 В этом примере запрос содержит следующие сведения о результирующем наборе:  
  
-   Предложение SELECT задает оси запроса как элементы Sales Amount и Tax Amount в измерении Measures и как элементы 2002 и 2003 в измерении Date.  
  
-   Предложение FROM указывает, что источником данных является куб Adventure Works.  
  
-   Предложение WHERE определяет ось среза как элемент Southwest измерения Sales Territory.  
  
 Обратите внимание, что в запросе используются псевдонимы осей COLUMNS и ROWS. Можно было бы обращаться к этим осям по их порядковым номерам. В следующем примере иллюстрируется запрос многомерных выражений с использованием порядковых номеров осей:  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 Дополнительные примеры см. в разделах [Определение содержимого оси запроса (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md) и [Определение содержимого оси среза (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
## <a name="see-also"></a>См. также  
 [Основные понятия многомерных выражений (службы Analysis Services)](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Инструкция SELECT (многомерные выражения)](../../../mdx/mdx-data-manipulation-select.md)  
  
  
