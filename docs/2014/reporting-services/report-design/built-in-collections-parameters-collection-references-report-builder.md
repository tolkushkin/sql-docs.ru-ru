---
title: Ссылки на коллекцию параметров (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c3c9452a9be55c71431a0ed3012769b1f5f6d8eb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106404"
---
# <a name="parameters-collection-references-report-builder-and-ssrs"></a>Ссылки на коллекцию параметров (построитель отчетов и службы SSRS)
  Параметры отчета являются одной из встроенных коллекций, на которые можно ссылаться из выражения. Включая в выражение параметры, можно настраивать внешний вид и данные отчета в соответствии с выбором пользователя. Выражения могут использоваться в любом свойстве элемента отчета или текстового поля, имеющего параметр (*Fx*) или \<**Expression**>. Кроме того, выражения применяются для дополнительного управления содержимым отчета и его внешним видом. Дополнительные сведения см. в разделе [Примеры выражений (построитель отчетов и службы SSRS)](expression-examples-report-builder-and-ssrs.md).  
  
 При сравнении значений параметра со значениями полей набора данных во время выполнения типы данных сравниваемых элементов должны совпадать. Параметры отчета может принимать одно из следующих типов: Значение типа Boolean, DateTime, Integer, Float или Text, представляющий базовый тип данных String. При необходимости может понадобиться преобразовать тип данных параметра, чтобы он соответствовал значению набора данных. Дополнительные сведения см. в разделе [Типы данных в выражениях (построитель отчетов и службы SSRS)](expressions-report-builder-and-ssrs.md).  
  
 Чтобы включить в выражение ссылку на параметр, следует понимать, как правильно указать ее синтаксис, который зависит от того, однозначный или многозначный параметр использован.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> Использование в выражении однозначного параметра  
 В следующей таблице показаны примеры синтаксиса, применяемого при включении в выражение ссылки на однозначный параметр произвольного типа данных.  
  
|Пример|Описание|  
|-------------|-----------------|  
|`=Parameters!` *\<Имя_параметра>* `.IsMultiValue`|Возвращает значение `False`.<br /><br /> Проверяет, является ли параметр многозначным. Если возвращено значение `True`, то параметр является многозначным и представляет собой коллекцию объектов. Если возвращено значение `False`, значит, параметр является однозначным и представляет собой один объект.|  
|`=Parameters!` *\<Имя_параметра>* `.Count`|Возвращает целочисленное значение 1. Для однозначного параметра счетчик всегда равен 1.|  
|`=Parameters!` *\<Имя_параметра>* `.Label`|Возвращает метку параметра, часто используемую в качестве отображаемого имени в раскрывающемся списке допустимых значений.|  
|`=Parameters!` *\<Имя_параметра>* `.Value`|Возвращает значение параметра. Если свойство Label не было задано, это значение появляется в раскрывающемся списке допустимых значений.|  
|`=CStr(Parameters!`  *\<Имя_параметра>* `.Value)`|Возвращает значение параметра в виде строки.|  
|`=Fields(Parameters!` *\<Имя_параметра>* `.Value).Value`|Возвращает значение поля с таким же именем, как и у параметра.|  
  
 Дополнительные сведения о добавлении параметров в фильтр см. в разделе [Добавление фильтров набора данных, фильтров области данных и групповых фильтров (построитель отчетов и службы SSRS)](add-dataset-filters-data-region-filters-and-group-filters.md).  
  
##  <a name="Multi"></a> Использование многозначного параметра в выражении  
 В следующей таблице показаны примеры синтаксиса, применяемого при включении в выражение ссылки на многозначный параметр произвольного типа данных.  
  
|Пример|Описание|  
|-------------|-----------------|  
|`=Parameters!` *\<Имя_параметра_с_несколькими_значениями>* `.IsMultiValue`|Возвращает значение `True` или `False`.<br /><br /> Проверяет, является ли параметр многозначным. Если возвращено значение `True`, то параметр является многозначным и представляет собой коллекцию объектов. Если возвращено значение `False`, то параметр является однозначным и представляет собой один объект.|  
|`=Parameters!` *\<Имя_параметра_с_несколькими_значениями>* `.Count`|Возвращает целочисленное значение.<br /><br /> Относится к количеству значений. Для однозначного параметра счетчик всегда равен 1. Для многозначного параметра счетчик имеет значение 0 или больше.|  
|`=Parameters!` *\<Имя_параметра_с_несколькими_значениями>* `.Value(0)`|Возвращает первое значение многозначного параметра.|  
|`=Parameters!` *\<Имя_параметра_с_несколькими_значениями>* `.Value(Parameters!` *\<Имя_параметра_с_несколькими_значениями>* `.Count-1)`|Возвращает последнее значение многозначного параметра.|  
|`=Split("Value1,Value2,Value3",",")`|Возвращает массив значений.<br /><br /> Создает массив значений для многозначного параметра типа `String`. Во втором параметре можно использовать любой разделитель для разбиения. Это выражение можно использовать для задания значений по умолчанию для многозначного параметра или для создания такого многозначного параметра, который надо отослать во вложенный или детализированный отчет.|  
|`=Join(Parameters!` *\<Имя_параметра_с_несколькими_значениями>* `.Value,", ")`|Возвращает значение типа `String`, содержащее значения многозначного параметра, разделенные точкой с запятой. Во втором параметре можно использовать любой разделитель для соединения.|  
  
 Дополнительные сведения об использовании параметров в фильтре см. в разделе [Параметры отчета (построитель отчетов и конструктор отчетов)](report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>См. также  
 [Выражения (построитель отчетов и службы SSRS)](expressions-report-builder-and-ssrs.md)   
 [Часто используемые фильтры (построитель отчетов и службы SSRS)](commonly-used-filters-report-builder-and-ssrs.md)   
 [Добавление, изменение или удаление параметра отчета (построитель отчетов и службы SSRS)](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Учебник. Добавление параметра к отчету (построитель отчетов)](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Учебники по &#40;построитель отчетов&#41;](../report-builder-tutorials.md)   
 [Встроенные коллекции в выражениях (построитель отчетов и службы SSRS)](built-in-collections-in-expressions-report-builder.md)  
  
  
