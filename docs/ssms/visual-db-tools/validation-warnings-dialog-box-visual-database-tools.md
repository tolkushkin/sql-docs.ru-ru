---
title: Диалоговое окно "Предупреждения проверки" (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 77a20360718563f101b44e68bf287e59876d8d38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098561"
---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>Диалоговое окно «Предупреждения проверки» (визуальные инструменты для баз данных)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Это диалоговое окно появляется при попытке сохранить изменения с потенциально опасными побочными эффектами или в случае вероятной неудачи операции фиксации базы данных. Это диалоговое окно указывает возможные побочные эффекты или возможные причины неудачи операции фиксации. Диалоговое окно предоставляет возможность продолжить действие или отменить его.  
  
> [!NOTE]  
> Это диалоговое окно выводится при попытке передачи изменений в базу данных или при сохранении скрипта изменения.  
  
Появление диалогового окна может быть вызвано любой из следующих причин:  
  
-   Возможно, отсутствуют разрешения базы данных на фиксацию всех изменений.  
  
-   Внесение изменений может привести к неправильному формированию производных столбцов, ограничений по умолчанию или проверочных ограничений.  
  
-   Изменение типа данных столбца может привести к потере данных.  
  
-   Изменение может привести к тому, что размер индекса будет более 900 байт.  
  
-   Изменение может изменить таблицу или столбец, являющиеся источниками для связанного со схемой представления или определяемой пользователем функции.  
  
-   Изменение приведет к воссозданию таблицы, которая имеет один или более зашифрованных триггеров; триггеры будут удалены.  
  
-   Изменения приведут к установке особых параметров настройки ANSI_NULLS или ANSI_PADDING (или обоих) для столбцов одной таблицы.  
  
## <a name="options"></a>Параметры  
**Да**  
Продолжите операцию и создайте скрипт изменения или передайте изменения в базу данных. Операции фиксации могут быть неудачными, если отсутствуют права на изменение базы данных, если изменения приведут к тому, что размер индекса будет более 900 байт; или если изменения приведут к неправильному формированию вычисляемого столбца, ограничения по умолчанию или проверочных ограничений.  
  
**Нет**  
Отменить сохранение.  
  
**Сохранить текстовый файл**  
Отображает диалоговое окно **Сохранить как** , которое позволит указать местоположение текстового файла, содержащего список предупреждений.  
  
## <a name="see-also"></a>См. также:  
[Проектирование таблиц (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[Разделы по конструированию запросов и представлений (визуальные инструменты для баз данных)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
