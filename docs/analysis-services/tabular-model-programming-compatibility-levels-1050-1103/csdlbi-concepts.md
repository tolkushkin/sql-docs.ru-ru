---
title: Основные понятия CSDLBI | Документация Майкрософт
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 486bbe240656bb2719ad4ce8f1ec51b226bec30b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62466913"
---
# <a name="csdlbi-concepts"></a>Основные понятия CSDLBI
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Язык определения концептуальной схемы с заметками бизнес-аналитики (CSDLBI) основан на среде Entity Data Framework, которая является абстракцией, представляющей данные способом, который позволяет программно оценивать, опрашивать или экспортировать разрозненные наборы данных. CSDLBI используется для представления моделей данных, созданных с помощью [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], поскольку поддерживает широкий выбор отчетов, управляемых данными, и приложений.  
  
 В этом разделе описывается процесс сопоставления представления CSDLBI с моделями данных [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (и табличными и многомерными) с примерами каждого вида модели.  
  
 Примеры, которые используются для иллюстрации этих основных понятий, взяты из образца базы данных AdventureWorks, доступном на узле Codeplex. Дополнительные сведения об образцах см. в разделе [образцы Adventure Works для SQL Server](http://go.microsoft.com/fwlink/?linkID=220093).  
  
## <a name="structure-of-a-tabular-model-in-csdlbi"></a>Структура табличной модели в CSDLBI  
 Документ языка CSDLBI, в котором описана модель отчета и данные в нем, начинается с XSD-инструкции, за которой следует определение модели.  
  
 Эта модель обладает пространством имен, которое содержит следующие основные сущности, взаимосвязи и свойства.  
  
-   **EntityContainer** перечислены таблицы в модели.  
  
-   Каждая таблица отображается с **EntityContainer** как **EntitySet**.  
  
-   Каждая связь между двумя таблицами описан как **AssociationSet** , определяющий конечные точки и роли связи.  
  
-   **EntityType** элемент расширен для BISM предоставлять дополнительные сведения о таблицах и столбцах в них, включая свойства для сортировки и отображения.  
  
-   **Мер** элемент определяет вычисления, которые могут использоваться в модели. Меру можно превратить в путем добавления набора особых атрибутов отображения, с помощью нового **ключевого показателя Эффективности** элемент.  
  
-   Отдельного представления перспектив не существует. В языке CSDL, однако они отмечены присутствуют столбцы и таблицы, не включенные в перспективу **Hidden** атрибута.  
  
### <a name="entities-entitysets-and-entitytypes"></a>Сущности, EntitySets и EntityTypes  
 Упоминание сущности в Entity Data Framework расширено на представление столбцов и таблиц из модели данных. В следующем фрагменте представлен список **EntitySet** элементов в простой модели, содержащей только три таблицы.  
  
```  
<EntityContainer Name="SimpleModel">  
<EntitySet Name="DimCustomer"EntityType="SimpleModel.DimCustomer">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimDate" EntityType="SimpleModel.DimDate">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimGeography" EntityType="SimpleModel.DimGeography">  
     <bi:EntitySet />  
   </EntitySet> />  
  
```  
  
 **EntitySet** не содержит сведений о столбцах или данных в таблице. Детальное описание столбцов и их свойств предоставляется элементом EntityType.  
  
 **EntitySet** элемент для каждой сущности (таблицы) включает коллекцию свойств, которые определяют ключевой столбец, тип данных, длину столбца, допустимость значений NULL, поведение при сортировке и т. д. Например, в следующем фрагменте языка CSDL описываются три столбца в таблице «Клиент». Первым столбцом является особый скрытый столбец, который используется моделью для внутренних целей.  
  
```  
<EntityType Name="Customer">  
  <Key>  
     <PropertyRef Name="RowNumber" />  
  </Key>  
    <Property Name="RowNumber" Type="Int64" Nullable="false">  
     <bi:Property Hidden="true" Contents="RowNumber"  
       Stability="RowNumber" />  
    </Property>  
    <Property Name="CustomerKey" Type="Int64" Nullable="false">  
      <bi:Property />  
    </Property>  
     <Property Name="FirstName" Type="String" MaxLength="Max" FixedLength="false">  
       <bi:Property />  
      </Property>  
  
```  
  
 Чтобы ограничить размер создаваемого документа языка CSDLBI, свойства, которые появляются более одного раза в сущности указываются путем ссылки на существующее свойство, таким образом, чтобы свойство помещалось в список только однажды для **EntityType**. Клиентское приложение может получить значение свойства путем нахождения **EntityType** , соответствующий **OriginEntityType**.  
  
### <a name="relationships"></a>Связи  
 В Entity Data Framework связи определяются как *ассоциации* между сущностями.  
  
 У ассоциации всегда имеется две конечные точки, каждая из которых указывает на поле или столбец в таблице. Поэтому между двумя таблицами могут существовать множественные связи, если у этих связей имеются разные конечные точки. Имя роли назначается конечным точкам ассоциации и указывает на то, как используется ассоциация в контексте модели данных. Примером имени роли может быть **ShipTo**при применении к Идентификатору клиента, который связан с Идентификатором клиента в таблице Orders.  
  
 Представление языка CSDLBI модели также содержит атрибуты ассоциации, которые определяют, как сущности сопоставляются друг с другом в контексте *кратность* ассоциации. Кратность указывает, находится атрибут или столбец в конечной точке связи между таблицами с одной стороны связи или с нескольких сторон. Для связи «один к одному» отсутствует отдельное значение. Заметки CSDLBI поддерживают значение кратности 0 (что означает, что сущность не связана ни с чем) или 0–1, что означает существование связи «один к одному» или «один ко многим».  
  
 На следующем образце представлено определение выхода CSDLBI для связи между таблицами с названием Date и ProductInventory, где две таблицы соединяются в столбец DateAlternateKey. Обратите внимание, что по умолчанию имя **AssociationSet** полное доменное имя из столбцов, участвующих в связи. Однако вы можете изменить это поведение при разработке модели так, чтобы в ней использовался другой формат имен.  
  
```  
<AssociationSet Name="ProductInventory_Date_DateKey" Association="Model.ProductInventory_Date_DateKey">  
              <End EntitySet="ProductInventory" />  
              <End EntitySet="Date" />  
              <bi:AssociationSet />  
            </AssociationSet>  
  
```  
  
### <a name="visualization-and-navigation-properties"></a>Свойства визуализации и навигации  
 Важной частью заметок CSDLBI являются свойства для определения представления, на уровне отчета и для перемещения по связям между сущностями. Обычно при создании модели данных не придается особого значения тому, как данные упорядочены, сгруппированы или каково их значение по умолчанию, исходя из того, что клиентское приложение укажет порядок и другие данные представления. Однако табличные модели службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] разработаны для интеграции с клиентом отчетов [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Они содержат свойства и атрибуты, которые поддерживают представление сущностей из модели данных в область конструктора отчета.  
  
 Расширения для преставления включают атрибуты для указания значений сбора данных по умолчанию, которые будут использоваться с цифровыми данными для индикации того, что текстовое поле указывает на URL-адрес изображения, либо для назначения поля, используемого для сортировки текущего поля.  
  
### <a name="name-properties-and-naming-conventions"></a>Свойства имени и контекст именования  
 Схема CSDLBI предоставляет каждой сущности уникальное имя и идентификатор, которые могут использоваться как ключ. Кроме того, некоторые сущности могут иметь заголовки, используемые для отображения, а также контекстные имена, которые изменяются в зависимости от места использования конкретной сущности.  
  
 **Документации** элемент позволяет конструкторам отчетов задавать описания сущности, помогающий бизнес-пользователям понимать значение данных. Некоторые сущности также позволяют использовать один или несколько **заметки** атрибутов, которые предоставляют дополнительные метаданные приложения и клиентами.  
  
 При создании модели при помощи средств [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] создаваемые имена объектов назначаются в соответствии с соглашением об именах объектов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и обеспечивают уникальность имен. Но поскольку язык CSDLBI основан на среде Entity Data Framework (EDF), для которой необходимо, чтобы имена отвечали требованиям соглашения об именах идентификаторов C#, когда сервер создает выход CSDLBI для модели, он берет имена, используемые в схеме [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], и автоматически создает новые имена объектов, соответствующие требованиям EDF. В следующей таблице описаны действия, необходимые для создания новых имен.  
  
|Правило|Действие|  
|----------|------------|  
|Отсутствуют запрещенные символы|Запрещенные символы заменяются на символ подчеркивания.|  
|Имена должны быть уникальными|Если две строки одинаковы, одна из них становится уникальной путем добавления символа подчеркивания и номера|  
  
> [!WARNING]  
>  Заголовки и квалификаторы обладают переводами, и для каждого конкретного языка может присутствовать либо заголовок, либо квалификатор. Это означает, что, когда квалификатор с именем или квалификатор с заголовком слиты, строки могут быть на разных языках.  
  
## <a name="additions-to-support-multidimensional-models"></a>Добавления для поддержки многомерных моделей  
 Заметки CSDLBI версии 1.0 поддерживали только табличные модели. В версии 1.1 была добавлена поддержка многомерных моделей (кубов OLAP), созданных обычными средствами разработки бизнес-аналитики. Таким образом, теперь можно отправить XML-запрос к многомерной модели и получить CSDLBI-определение модели для использования в отчетах.  
  
 **Кубы:** SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] табличной базы данных может содержать только один режим. В отличие от нее каждая многомерная база данных может содержать несколько кубов, при этом каждая база данных связывается с кубом по умолчанию. Поэтому при отправке XML-запроса к многомерному серверу необходимо указать куб, в противном случае будет возвращено XML для куба по умолчанию.  
  
 В остальном представление куба похоже на представление базы данных табличной модели. Имя куба и куб соответствуют имени и идентификатору табличной базы данных.  
  
 **Размеры:** Измерение в CSDLBI представляется как со столбцами и свойствами сущности (таблицы). Обратите внимание, что даже не входящее в перспективу, измерения, включенного в модель будет представлено в выходе языка CSDL, отмеченное как **Hidden**.  
  
 **Перспективы:** Клиент может запрашивать язык CSDL для отдельных перспектив. Дополнительные сведения см. в разделе [строк DISCOVER_CSDL_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset).  
  
 **Иерархии:** Иерархии поддерживаются и представлены в CSDLBI как набор слоев.  
  
 **Члены:** Добавлена поддержка для элемента по умолчанию и значения по умолчанию автоматически добавляются к выходу CSDLBI.  
  
 **Вычисляемые элементы:** Многомерные модели поддерживают вычисляемые элементы для дочернего элемента **все** с единственным действительным элементом.  
  
 **Атрибуты измерения:** В выходе CSDLBI атрибуты измерения поддерживаются и автоматически помечаются как необрабатываемые статистически.  
  
 **Ключевые показатели эффективности:** Ключевые показатели эффективности поддерживались в CSDLBI версии 1.1, но представление изменилось. Ранее ключевой показатель эффективности являлся свойством меры. В версии 1.1 элемент KPI можно добавить в меру  
  
 **Новые свойства:** Были добавлены дополнительные атрибуты для поддержки моделей DirectQuery.  
  
 **Ограничения:** Безопасность ячеек не поддерживается.  
  
## <a name="see-also"></a>См. также  
 [Заметки языка CSDL для бизнес-аналитики (CSDLBI)](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
  
