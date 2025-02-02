---
title: Создание измерения с помощью мастера измерений | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ba906ab17169b2e2faf6bef54137fcc4e6210660
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62866894"
---
# <a name="create-a-dimension-using-the-dimension-wizard"></a>Создание измерения с помощью мастера измерений
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Можно создать новое измерение с помощью мастера измерений в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-create-a-new-dimension"></a>Создание нового измерения  
  
1.  В **обозревателе решений**щелкните правой кнопкой мыши узел **Измерения**и выберите команду **Создать измерение**.  
  
2.  На странице **Выбор метода создания** мастера измерений выберите **Использовать существующую таблицу**, а затем нажмите кнопку **Далее**.  
  
    > [!NOTE]  
    >  Иногда приходится создавать измерение, не используя существующую таблицу. Дополнительные сведения см. в разделах [Создание измерения путем формирования в источнике данных таблицы, отличной от таблицы времени](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md) и [Создание измерения времени посредством формирования таблицы времени](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md).  
  
3.  На странице **Определение исходных сведений** выполните следующие действия.  
  
    1.  В списке **Представление источника данных** выберите представление источника данных.  
  
    2.  В списке **Основная таблица** выберите основную таблицу измерения.  
  
    3.  В списке **Ключевые столбцы** просмотрите список ключевых столбцов, автоматически выбранных мастером на основе первичного ключа, заданного в основной таблице измерений. Для изменения настроек по умолчанию задайте ключевые столбцы, связывающие таблицу измерения с таблицей фактов.  
  
    4.  В раскрывающемся списке **Столбец имени** проверьте столбец имен, автоматически выбранный мастером.  
  
         Имя, используемое по умолчанию, подходит, если столбец содержит описательные сведения. Однако при желании можно задать имя, более значимое для конечного пользователя. Например, если атрибут категории продуктов в измерении «Продукты» использует столбец **ProductCategoryKey** в качестве ключевого столбца, то можно в качестве его столбца имени указать столбец **ProductCategoryName** .  
  
         Если список **Ключевые столбцы** содержит несколько ключевых столбцов, следует задать столбец имени, из которого будут взяты значения элементов для ключевого атрибута. Для этого создайте именованное вычисление в представлении источника данных и используйте его как столбец имени.  
  
    5.  Нажмите кнопку **Далее**.  
  
4.  На странице **Выбор связанных таблиц** выберите связанные таблицы, которые нужно включить в измерение, и нажмите **Далее**.  
  
    > [!NOTE]  
    >  Страница **Выбор связанных таблиц** появляется, если заданная основная таблица измерения связана с другими таблицами.  
  
5.  На странице **Выбор атрибутов измерения** выберите атрибуты, которые нужно включить в измерение, а затем нажмите **Далее**.  
  
     При необходимости можно поменять имена атрибутов, разрешить или запретить просмотр и задать тип атрибута.  
  
    > [!NOTE]  
    >  Чтобы поля **Разрешить обзор** и **Тип атрибута** были активны, необходимо выбрать атрибут для включения в измерение.  
  
6.  На странице **Определение логики операций со счетами** в столбце **Встроенные типы счетов** выберите тип счета, а затем нажмите **Далее**.  
  
     Тип счета должен соответствовать типу счета исходной таблицы, указанному в столбце **Типы счетов исходной таблицы** .  
  
    > [!NOTE]  
    >  Страница **Определение логики операций со счетами** появляется, если вы определили атрибут измерения **Тип счета** на странице **Выбор атрибутов измерения** мастера.  
  
7.  На странице **Завершение работы мастера** введите имя для этого нового измерения и просмотрите структуру измерения. Если надо что-либо изменить, нажмите кнопку **Назад**, если нет, нажмите кнопку **Готово**.  
  
    > [!NOTE]  
    >  После добавления, удаления и настройки атрибутов и иерархий в измерении с помощью мастера измерений можно использовать конструктор измерений.  
  
## <a name="see-also"></a>См. также  
 [Создание измерения с помощью существующей таблицы](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
  
  
