---
title: Задание столбцов данных и событий для файла трассировки (приложение SQL Server Profiler) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- adding events
- traces [SQL Server], data columns
- deleting events
- removing events
- traces [SQL Server], events
ms.assetid: 7da715a3-2f03-4063-b6a4-20fd7b44e675
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33e11dde29a9f2b016f5f70fa3c12bd728928f93
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267419"
---
# <a name="specify-events-and-data-columns-for-a-trace-file-sql-server-profiler"></a>указать столбцы событий и данных для файла трассировки (приложение SQL Server Profiler)
  Данный раздел содержит информацию об указании классов событий и столбцов данных для трассировок при помощи [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-specify-events-and-data-columns-for-a-trace"></a>Указание событий и столбцов данных для трассировки  
  
1.  В диалоговом окне **Свойства трассировки** или **Свойства шаблона трассировки** выберите вкладку **Выбор событий** .  
  
     Вкладка **Выбор событий** содержит сетку. Сетка — это таблица, которая содержит каждый из классов событий, доступных для трассировки. На каждый класс событий в таблице приходится по одной строке. Классы событий могут незначительно различаться в зависимости от типа и версии сервера, к которому они подключены. Классы событий идентифицируются в столбце **События**сетки и группируются по категориям событий. В оставшихся столбцах перечислены столбцы данных, которые могут быть возвращены для каждого класса событий.  
  
2.  В диалоговом окне **Выбор событий**.  
  
3.  Чтобы переместить события из трассировки, снимите флажок в столбце **События** для каждого класса событий.  
  
4.  Чтобы включить события в трассировку, установите флажок в столбце **События** для каждого класса событий или проверьте столбец данных, который соответствует событию.  
  
> [!IMPORTANT]  
>  Если трассировка будет коррелировать с данными системного монитора или монитора производительности, то столбцы данных **Время начала** и **Время окончания** должны быть включены в трассировку.  
  
 Если произведена проверка окна, соответствующего событию, то при внесении класса событий каждый связанный столбец данных также включается в трассировку. Если проверялось окно для определенного столбца, то в трассировку включается только этот столбец.  
  
1.  Чтобы удалить столбцы данных из класса событий, снимите флажки со столбца данных в строке класса событий либо щелкните правой кнопкой мыши заголовок столбца и выберите **Снять выделение столбца** .  
  
2.  При необходимости примените фильтры к трассировке. Дополнительные сведения см. в статье [Создание трассировки(приложение SQL Server Profiler)](filter-events-in-a-trace-sql-server-profiler.md).  
  
## <a name="see-also"></a>См. также  
 [Приложение SQL Server Profiler](sql-server-profiler.md)  
  
  
