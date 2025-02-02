---
title: Использование режима EXPLICIT для FOR XML | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- EXPLICIT FOR XML mode
- FOR XML clause, EXPLICIT mode
- FOR XML EXPLICIT mode
ms.assetid: 8b26e8ce-5465-4e7a-b237-98d0f4578ab1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8976b77bf0823c9735e6e6e67fc3159bcb54ecdf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63231277"
---
# <a name="use-explicit-mode-with-for-xml"></a>Использование режима EXPLICIT совместно с предложением FOR XML
  Как описано в подразделе [Конструирование XML используя FOR XML](../xml/for-xml-sql-server.md), режимы RAW и AUTO не предоставляют больших возможностей контроля формы XML, порождаемого из результата запроса. Однако режим EXPLICIT предоставляет наибольшую гибкость при формировании желаемого XML из результатов запроса.  
  
 Запрос в режиме EXPLICIT должен быть написан особым способом, при котором в запросе явно задаются дополнительные сведения о требуемом XML, такие как ожидаемый уровень вложенности в XML. В зависимости от запрашиваемого XML написание запросов режима EXPLICIT может оказаться весьма трудоемким. Может оказаться, что [использование режима PATH](../xml/use-path-mode-with-for-xml.md) с вложениями является более простой альтернативой написанию запросов в режиме EXPLICIT.  
  
 Поскольку требуемый XML описывается в режиме EXPLICIT в самом запросе, следует убедиться в том, что порождаемый XML имеет необходимую форму и является корректным.  
  
## <a name="rowset-processing-in-explicit-mode"></a>Обработка наборов строк в режиме EXPLICIT  
 Режим EXPLICIT преобразует набор строк, получаемый в результате выполнения запроса, в XML-документ. Для того чтобы режим EXPLICIT создал XML-документ, набор строк должен иметь определенный формат. То есть необходимо написать запрос SELECT для создания набора строк, **универсальной таблицы**, имеющей определенный формат, так чтобы логика обработки могла создать желаемый XML.  
  
 Во-первых, запрос должен создавать следующие два столбца метаданных:  
  
-   первый столбец должен предоставлять номер тега текущего элемента (целочисленного типа), с именем столбца **Tag**. В запросе должен быть указан уникальный номер тега для каждого элемента, который будет создан из набора строк;  
  
-   второй столбец должен задавать номер тега для родительского элемента, и этот столбец должен иметь имя **Parent**. Таким образом, столбцы Tag и Parent предоставляют сведения об иерархии.  
  
 Значения этих столбцов метаданных вместе со сведениями в именах столбцов используются для создания желаемого XML. Обратите внимание на то, что имена столбцов в запросе должны задаваться особым образом. Также обратите внимание на то, что значение 0 или NULL в столбце **Parent** указывает на то, что у соответствующего элемента нет родителя. Такой элемент добавляется в XML в качестве элемента верхнего уровня.  
  
 Для понимания того, как универсальная таблица, сформированная запросом, преобразуется в результат XML, предположим, что написан запрос, который создает универсальную таблицу.  
  
 ![Образец универсальной таблицы](../../database-engine/media/xmlutable.gif "Образец универсальной таблицы")  
  
 Обратите внимание на следующие особенности этой универсальной таблицы:  
  
-   Первые два столбца **Tag** и **Parent** являются метастолбцами. Эти значения определяют иерархию.  
  
-   Имена столбцов задаются особым образом, как описано выше в данном подразделе.  
  
-   При формировании XML из этой универсальной таблицы данные таблицы секционируются вертикально на группы столбцов. Группировка определяется на основании значения **Tag** и имен столбцов. При конструировании XML логика обработки выбирает одну группу столбцов для каждой строки и создает элемент. В данном примере происходит следующее:  
  
    -   для значения столбца **Tag**, равного 1 в первой строке, столбцы, имена которых включают тот же номер тега, **Customer!1!cid** и **Customer!1!name**, образуют группу. Эти столбцы используются при обработке строки, и, как можно заметить, формируемый элемент приобретает вид <`Customer id=... name=...`>. Формат имени столбца описан ниже в этом подразделе;  
  
    -   для строк со значением столбца **Tag**, равным 2, столбцы **Order!2!id** и **Order!2!date** образуют группу, которая далее используется при конструировании элементов: <`Order id=... date=... /`>;  
  
    -   для строк со значением столбца **Tag**, равным 3, столбцы **OrderDetail!3!id!id** и **OrderDetail!3!pid!idref** образуют группу. Каждая из этих строк формирует из данных столбцов элемент <`OrderDetail id=... pid=...`>;  
  
-   обратите внимание на то, что при формировании иерархии XML строки обрабатываются по порядку. Иерархия XML определяется так, как показано далее.  
  
    -   Первая строка задает значение **Tag** , равное 1, и значение **Parent** , равное NULL. Поэтому соответствующий элемент <`Customer`> добавляется в качестве элемента верхнего уровня XML.  
  
        ```  
        <Customer cid="C1" name="Janine">  
        ```  
  
    -   Вторая строка задает значение **Tag** , равное 2, и значение **Parent** , равное 1. Поэтому элемент <`Order`> добавляется в качестве дочернего к элементу <`Customer`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
        ```  
  
    -   Следующие две строки задают значение **Tag** , равное 3, и значение **Parent** , равное 2. Поэтому два элемента <`OrderDetail`> добавляются в качестве дочерних к элементу <`Order`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
        ```  
  
    -   Последняя строка задает 2 в качестве номера **Tag** и 1 в качестве номера тэга **Parent** . Поэтому другой элемент-потомок <`Order`> добавляется к родительскому элементу <`Customer`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
           </Order>  
           <Order id="O2" date="3/29/1997">  
        </Customer>  
        ```  
  
 В итоге, значения в метастолбцах **Tag** и **Parent** , сведения, указанные в именах столбцов, и правильный порядок строк создают желаемый XML при использовании режима EXPLICIT.  
  
### <a name="universal-table-row-ordering"></a>Упорядочение строк универсальной таблицы  
 При конструировании XML строки в универсальной таблице обрабатываются по порядку. Поэтому для получения правильных экземпляров потомков, ассоциированных с их родителями строки в наборе строк должны быть упорядочены так, чтобы за каждым родительским узлом следовали его потомки.  
  
## <a name="specifying-column-names-in-a-universal-table"></a>Указание имен столбцов в универсальной таблице  
 При написании запросов в режиме EXPLICIT имена столбцов в результирующем наборе строк должны быть заданы с использованием описанного далее формата. Они предоставляют сведения о преобразовании, включая имена элементов и атрибутов и другие дополнительные сведения, задаваемые при помощи директив.  
  
 Общий формат имеет вид:  
  
```  
  
ElementName!TagNumber!AttributeName!Directive  
```  
  
 Далее следует описание частей формата.  
  
 *ElementName*  
 Результирующий общий идентификатор элемента. Например, если **Customers** задано в качестве *ElementName*, формируется элемент \<Customers>.  
  
 *TagNumber*  
 Уникальное значение тега, присвоенное элементу. Это значение с помощью двух метастолбцов, **Tag** и **Parent**, определяет вложенность элементов в результирующем XML.  
  
 *AttributeName*  
 Предоставляет имя создаваемого атрибута для указанного элемента *ElementName*. Это поведение используется, если не задано значение *Directive* .  
  
 Если задано значение *Directive* , имеющее тип **xml**, **cdata**или **element**, оно используется для создания дочернего элемента *ElementName*, к которому добавляется значение столбца.  
  
 При указании значения *Directive*значение *AttributeName* может быть пустым. Например: ElementName!TagNumber!!Directive. В этом случае значение столбца напрямую содержится в *ElementName*.  
  
 *Directive*  
 Значение*Directive* является необязательным и может использоваться с целью предоставления дополнительных сведений для создания XML. Значение*Directive* служит двум целям.  
  
 Одной из целей является кодирование значений в виде ID, IDREF и IDREFS. Можно указать ключевые слова **ID**, **IDREF**и **IDREFS** в качестве значений *Directive*. Эти директивы переопределяют типы атрибутов. Это позволяет создавать связи внутри документа.  
  
 Также можно использовать значение *Directive* для указания того, как сопоставлять строковые данные с XML. Ключевые слова **hide**, **element, elementxsinil**, **xml**, **xmltext**и **cdata** также могут быть использованы в качестве значения *Directive*. Директива **hide** скрывает узел. Это полезно, если некоторые значения извлекаются только в целях сортировки и не должны появляться в результирующем XML.  
  
 Директива **element** формирует содержащийся элемент вместо атрибута. Содержащиеся данные кодируются как сущность. Например, символ **<** превращается в &lt;. Для значений столбцов, равных NULL, элемент не формируется. Если требуется, чтобы для столбцов со значениями NULL формировался элемент, можно указать директиву **elementxsinil** . При этом будет сформирован элемент с атрибутом xsi:nil=TRUE.  
  
 Директива **xml** аналогична директиве **element** , однако при ее использовании не происходит кодирования сущности. Обратите внимание на то, что директива **element** может быть совмещена с **ID**, **IDREF**или **IDREFS**, в то время как директива **xml** не допускает совмещения с любой другой директивой, кроме **hide**.  
  
 Директива **cdata** содержит данные путем упаковывания их с помощью раздела CDATA. Содержимое не кодируется в виде сущности. Первоначальный тип данных должен быть текстовым, например **varchar**, **nvarchar**, **text**или **ntext**. Эта директива может использоваться только совместно с **hide**. При использовании этой директивы не следует задавать значение *AttributeName* .  
  
 Комбинирование директив из двух разных групп в большинстве случаев допустимо, однако комбинирование директив одной группы недопустимо.  
  
 Если значения *Directive* и *AttributeName* не заданы, например **Customer!1**, подразумевается директива **element** , то есть **Customer!1!!element**, а данные столбца содержатся в *ElementName*.  
  
 Если задана директива **xmltext** , содержимое столбца упаковывается в один тэг, который интегрируется с оставшейся частью документа. Эта директива полезна при выборке перегруженных, неиспользуемых XML-данных, сохраненных в столбец при помощи OPENXML. Дополнительные сведения см в разделе [OPENXML (SQL Server)](../xml/openxml-sql-server.md).  
  
 Если задано значение *AttributeName* , имя тега заменяется указанным именем. В противном случае атрибут добавляется к текущему списку атрибутов включаемых элементов путем помещения содержимого в начало содержимого без кодирования сущности. Столбец с этой директивой должен быть текстового типа, например **varchar**, **nvarchar**, **char**, **nchar**, **text**или **ntext**. Эта директива может использоваться только совместно с **hide**. Эта директива полезна при выборке перегруженных данных, хранящихся в столбце. Если содержимое не является корректным XML, поведение не определено.  
  
## <a name="in-this-section"></a>в этом разделе  
 В следующем примере демонстрируется применение режима EXPLICIT.  
  
-   [Пример. Получение сведений о сотрудниках](../xml/example-retrieving-employee-information.md)  
  
-   [Пример. Указание директивы ELEMENT](../xml/example-specifying-the-element-directive.md)  
  
-   [Пример. Задание директивы ELEMENTXSINIL](../xml/example-specifying-the-elementxsinil-directive.md)  
  
-   [Пример. Конструирование одноуровневых элементов в режиме EXPLICIT](../xml/example-constructing-siblings-with-explicit-mode.md)  
  
-   [Пример. Указание директив ID и IDREF](../xml/example-specifying-the-id-and-idref-directives.md)  
  
-   [Пример. Указание директив ID и IDREFS](../xml/example-specifying-the-id-and-idrefs-directives.md)  
  
-   [Пример. Указание директивы HIDE](../xml/example-specifying-the-hide-directive.md)  
  
-   [Пример. Указание директивы ELEMENT и кодировка сущности](../xml/example-specifying-the-element-directive-and-entity-encoding.md)  
  
-   [Пример. Задание директивы CDATA](../xml/example-specifying-the-cdata-directive.md)  
  
-   [Пример. Указание директивы XMLTEXT](../xml/example-specifying-the-xmltext-directive.md)  
  
## <a name="see-also"></a>См. также  
 [Использование с RAW Mode для FOR XML](../xml/use-raw-mode-with-for-xml.md)   
 [Использование режима AUTO совместно с FOR XML](../xml/use-auto-mode-with-for-xml.md)   
 [Использование режима PATH совместно с FOR XML](../xml/use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML (SQL Server)](../xml/for-xml-sql-server.md)  
  
  
