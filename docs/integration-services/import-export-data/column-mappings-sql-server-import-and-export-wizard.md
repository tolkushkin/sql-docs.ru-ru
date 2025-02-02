---
title: Сопоставления столбцов (мастер импорта и экспорта SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5f7b30970020963e83fa101971d6c30d9e76397a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723952"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Сопоставления столбцов (мастер импорта и экспорта SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Если выбрав существующие таблицы и представления, которые нужно скопировать, или просмотрев свой запрос, вы нажмете **Изменить сопоставления**, в мастере импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] откроется диалоговое окно **Сопоставления столбцов** . На этой странице можно указать и настроить конечные столбцы, в которые будут отправляться данные, копируемые из исходных столбцов. Зачастую на этой странице не нужно ничего менять.
  
Если нужно копировать не все столбцы в выбранной таблице, на этой странице можно исключить лишние столбцы. Для столбцов, которые следует пропустить, выберите пункт **игнорировать** в столбце **Назначение** списка **Сопоставления**.
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Снимок экрана: страница "Сопоставления столбцов" 
 На приведенном ниже снимке экрана показан пример диалогового окна **Сопоставления столбцов** в мастере. 
 
 В этом примере демонстрируется создание целевой таблицы, так как выбран параметр **Создать целевую таблицу** . По умолчанию мастер присваивает каждому столбцу в новой конечной таблице то же имя, тип данных и те же свойства, что и у соответствующего столбца в исходной таблице. 
  
 ![Страница "Сопоставления столбцов" в мастере импорта и экспорта](../../integration-services/import-export-data/media/column-mappings.png "Страница \"Сопоставления столбцов\" в мастере импорта и экспорта")  
  
## <a name="review-the-source-and-destination"></a>Просмотр источника и назначения 
![Страница "Сопоставления столбцов", раздел источника и назначения](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Source**  
 Выбранная исходная таблица, представление или запрос.  
  
 **Назначение**  
 Выбранная конечная таблица или представление.  

## <a name="optionally-create-a-new-destination-table"></a>При необходимости создайте конечную таблицу.
![Страница "Сопоставления столбцов", раздел создания таблицы](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **Создать целевую таблицу или файл**  
 Если конечная таблица не существует, создайте ее.    
  
 **Изменить SQL**  
Щелкните **Изменить SQL** , чтобы открыть диалоговое окно **Инструкция SQL Create Table** . Используйте автоматически формируемую инструкцию CREATE TABLE или внесите в нее необходимые изменения. Если вы изменяете инструкцию вручную, убедитесь в том, что внесенные изменения отражаются в списке сопоставлений столбцов. Дополнительные сведения см. в разделе [Инструкция SQL Create Table](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  

### <a name="sometimes-these-options-are-disabled"></a>Иногда эти параметры отключены.
Параметр **Создать целевую таблицу/файл** и кнопка **Изменить SQL** либо автоматически включены, либо автоматически отключены.

-   **Включены.** Если на странице **Выбор исходных таблиц и представлений** указана **новая** целевая таблица, автоматически выбирается параметр **Создать целевую таблицу** и активируется кнопка **Изменить SQL**.

-   **Отключены.** Если на странице **Выбор исходных таблиц и представлений** указана **существующая** целевая таблица, параметр **Создать целевую таблицу** и кнопка **Изменить SQL** автоматически отключаются. Если вы хотите создать конечную таблицу, вернитесь на страницу **Выбор исходных таблиц и представлений** и введите имя **новой** таблицы в столбце **Назначение**.  

## <a name="what-about-existing-data-in-the-destination"></a>Что происходит с существующими данными в месте назначения?
![Страница "Сопоставления столбцов", раздел параметров](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **Удалять строки в целевой таблице или файле**  
 Указывает, необходимо ли очищать данные, содержащиеся в существующей таблице, перед помещением в нее новых данных.  
  
 **Присоединять строки к целевой таблице или файлу**  
 Определяет, нужно ли присоединять новые данные к данным, уже находящимся в существующей таблице.  
  
 **Удалить и создать повторно целевую таблицу**  
 Выберите этот параметр для перезаписи целевой таблицы. Этот параметр доступен, только если вы использовали мастер для создания конечной таблицы. Целевая таблица удаляется и повторно создается только в случае, если созданный мастером пакет был сохранен, а затем запущен снова. Это удобно, если необходимо проверить параметры несколько раз.
  
 **Разрешить вставку в столбец идентификаторов**  
 Установка этого параметра позволяет вставлять значения идентификаторов, существующие в исходных данных, в столбец идентификаторов целевой таблицы. По умолчанию для целевого столбца идентификаторов это не разрешено.  
  
> [!TIP]
> Если существующие первичные ключи находятся в столбце идентификаторов, столбце автоматической нумерации или аналогичном, нужно выбрать этот параметр, чтобы сохранить такие ключи.  В противном случае целевому столбцу идентификаторов обычно присваиваются новые значения.  

## <a name="keep-your-autonumber-or-identity-values"></a>Сохранение значений счетчика или идентификаторов
При экспорте данных, содержащих столбец счетчика или столбец идентификаторов, например при экспорте из Microsoft Access, необходимо установить флажок **Разрешить вставку в столбец идентификаторов**, как описано выше.

## <a name="review-column-mappings"></a>Проверка сопоставлений столбцов
![Страница "Сопоставления столбцов", раздел сопоставлений](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **Сопоставления**  
 Показывает сопоставление каждого столбца источника данных столбцу назначения.
 
Список **Сопоставления** содержит следующие столбцы:  
  
-    **Source**  
     Просмотрите каждый исходный столбец.  
  
-   **Назначение**  
    Просмотрите сопоставленный целевой столбец или выберите другой столбец.
    
    Копировать все столбцы из исходной таблицы необязательно. Щелкните **игнорировать** в этом столбце для столбцов, которые нужно пропустить. Перед сопоставлением столбцов необходимо установить пропуск всех столбцов, которые не будут сопоставляться.  
  
-   **Тип**  
    Просмотрите тип данных для целевого столбца или выберите другой тип данных.
  
-   **Допускает значения NULL**  
    Укажите, допускает ли целевой столбец значение null.  
  
-   **Размер**  
    Укажите количество символов в целевом столбце (если применимо).  
  
-    **Точность**  
    Укажите точность числовых данных в конечном столбце, то есть количество разрядов (если применимо).  
  
 -   **Масштаб**  
    Укажите масштаб числовых данных в конечном столбце, то есть количество знаков после запятой (если применимо).  
  
## <a name="whats-next"></a>Дальнейшие действия  
 После того как вы проверите и настроите конечные столбцы для приема скопированных данных из исходных столбцов и нажмете кнопку **ОК**, диалоговое окно **Сопоставления столбцов** вернет вас на страницу **Выбор исходных таблиц и представлений** или на страницу **Настройка назначения "Неструктурированный файл"**. Дополнительные сведения см. в разделах [Выбор исходных таблиц и представлений](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) или [Настройка назначения "Неструктурированный файл"](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Если заданное сопоставление не добавится в список **Сопоставления** , диалоговое окно **Сопоставления столбцов** переадресует вас на страницу **Просмотр сопоставления типов данных** . На этой странице вы можете просмотреть предупреждения, настроить параметры преобразования и указать способ обработки ошибок. Дополнительные сведения см. в разделе [Просмотр сопоставления типов данных](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>См. также раздел
[Сопоставление типов данных в мастере импорта и экспорта SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[Приступая к работе с простым примером мастера импорта и экспорта](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

