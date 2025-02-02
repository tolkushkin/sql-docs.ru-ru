---
title: Замена таблицы или именованного запроса в представлении источника данных (службы Analysis Services) | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a171eafc35446f588d64c74457792912dcebe75a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641117"
---
# <a name="replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services"></a>Замена таблицы или именованного запроса в представлении источника данных (службы Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  В конструкторе представлений источников данных можно заменить таблицу, представление или именованный запрос в представлении источника данных на другую таблицу или представление из того же или из другого источника данных или на именованный запрос, определенный в представлении источника данных. При замене таблицы все другие объекты в базе данных или проекте служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] со ссылками на эту таблицу продолжают ссылаться на таблицу, так как идентификатор объекта для таблицы в представлении источника данных не изменился. Любые связи по-прежнему остаются действительными (на основе соответствия имен и типа столбцов). Если таблица удаляется, а затем добавляется, то ссылки и связи также удаляются, поэтому их необходимо создавать повторно.  
  
 Чтобы заменить таблицу другой таблицей, необходимо активное соединение с источником данных в конструкторе представлений источников данных в режиме проектирования.  
  
 Чаще всего выполняется замена таблицы в представлении источника данных на другую таблицу в источнике данных. На таблицу также можно заменить именованный запрос. Например, ранее таблица была заменена именованным запросом и теперь требуется вернуть таблицу.  
  
> [!IMPORTANT]  
>  При переименовании таблицы в источнике данных выполните шаги по замене таблицы и укажите переименованную таблицу в качестве источника соответствующей таблицы в представлении источника данных до его обновления. Завершение процесса замены и переименования сохраняет в представлении источника данных таблицу, ее ссылки и связи. В противном случае при обновлении представления источников данных переименованная таблица в источнике данных считается удаленной. Дополнительные сведения см. в разделе [Обновление схемы в представлении источника данных (службы Analysis Services)](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md).  
  
##  <a name="bkmk_nq"></a> Замена таблицы именованным запросом  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект или подключитесь к базе данных, содержащей представление источника данных, в котором необходимо заменить таблицу или именованный запрос.  
  
2.  В обозревателе решений откройте папку **Представления источников данных** , а затем дважды щелкните представление источника данных.  
  
3.  Откройте диалоговое окно **Создание именованного запроса** . На панели **Таблицы** либо на панели **Диаграмма** щелкните правой кнопкой мыши таблицу, которую необходимо заменить, укажите **Заменить таблицу** и выберите пункт **Новым именованным запросом**.  
  
4.  В диалоговом окне **Создание именованного запроса** определите именованный запрос и нажмите кнопку **ОК**.  
  
5.  Сохраните измененное представление источника данных.  
  
## <a name="replace-a-table-or-named-query-with-a-table"></a>Замена таблицы или именованного запроса на таблицу  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект или подключитесь к базе данных, содержащей представление источника данных, в котором необходимо заменить таблицу или именованный запрос.  
  
2.  В обозревателе решений откройте папку **Представления источников данных** , а затем дважды щелкните представление источника данных.  
  
3.  Откройте диалоговое окно **Замена таблицы другой таблицей** . На панели **Таблицы** либо на панели **Диаграмма** щелкните правой кнопкой мыши таблицу или именованный запрос, который необходимо заменить, укажите **Заменить таблицу** и выберите пункт **Другой таблицей**.  
  
4.  В диалоговом окне **Замена таблицы другой таблицей** :  
  
    1.  в раскрывающемся списке **Источник данных** выберите необходимый источник данных;  
  
    2.  выберите таблицу, на которую необходимо заменить таблицу или именованный запрос;  
  
5.  Нажмите кнопку **ОК**.  
  
6.  Сохраните измененное представление источника данных.  
  
## <a name="see-also"></a>См. также  
 [Представления источников данных в многомерных моделях](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
