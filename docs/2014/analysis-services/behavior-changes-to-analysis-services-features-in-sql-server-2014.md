---
title: Изменения в работе для анализа служб в SQL Server 2014 | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 288f9e0d5a86e34db2fdd81163f229eff5275606
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064339"
---
# <a name="behavior-changes-to-analysis-services-features-in-sql-server-2014"></a>Изменение работы функций служб Analysis Services в SQL Server 2014
  В этом разделе описаны изменения работы функций [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] для табличной модели, многомерной модели, модели анализа данных и развертываний [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] . Изменения в работе касаются того, как функциональные возможности работают или взаимодействуют в текущей версии в сравнении с предыдущими версиями SQL Server.  
  
> [!NOTE]  
>  Напротив, критическое изменение — это изменение, которое препятствует работе модели данных или приложения, интегрированного с [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Дополнительные сведения см. в разделе [Критические изменения функций служб Analysis Services в SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md).  
  
 В этом разделе.  
  
-   [Изменения в поведении в SQL Server 2014](#bkmk_sql2014)  
  
-   [Изменения в SQL Server 2012 с пакетом обновления 1](#bkmk_sql2012sp1)  
  
-   [Изменения в поведении в SQL Server 2012](#bkmk_sql2012)  
  
##  <a name="bkmk_sql2014"></a> Изменения в поведении [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 В этом выпуске не произошло никаких новых изменений работы функций в рамках табличной модели, многомерной модели, модели анализа данных и функциональных возможностей [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] , о которых было объявлено.  Тем не менее, так как версия  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] аналогична версиям [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] и [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] , то для вашего удобства здесь приведены изменения работы функций для обоих предыдущих выпусков на тот случай, если вы осуществили обновление [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="bkmk_sql2012sp1"></a> Изменения в поведении [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]  
 В этом разделе документированы изменения работы функций [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] в [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]. Эти изменения также применяются к [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
|Проблемы|Описание|  
|-----------|-----------------|  
|Книги SQL Server 2008 R2 PowerPivot не обновляются автоматически и не обновляют модели, если используются в SQL Server 2012 PowerPivot с пакетом обновления 1 (SP1) для SharePoint 2013. Поэтому плановые обновления данных не будут действовать для книг SQL Server 2008 R2 PowerPivot.|Книги 2008 R2 открываются в [!INCLUDE[ssGeminiShortvnext](../includes/ssgeminishortvnext-md.md)], однако плановые обновления не выполняются. При просмотре журнала обновления обнаруживается сообщение об ошибке следующего вида:<br /> «Книга содержит неподдерживаемую модель PowerPivot. Модель PowerPivot в книге представлена в формате SQL Server 2008 R2 PowerPivot для Excel 2010. Поддерживаются следующие модели PowerPivot: <br />SQL Server 2012 PowerPivot для Excel 2010,<br />SQL Server 2012 PowerPivot для Excel 2013"<br /><br /> **Как обновление книги:** Плановые обновления не будет работать, пока вы не обновите ее до книги 2012. Для обновления книги и содержащейся в ней модели выполните одно из следующих действий.<br /><br /> Загрузите и откройте книгу в Microsoft Excel 2010 с помощью установленной надстройки SQL Server 2012 PowerPivot для Excel. Затем сохраните книгу и повторно опубликуйте ее на сервере SharePoint.<br /><br /> Загрузите и откройте книгу в Microsoft Excel 2013. Затем сохраните книгу и повторно опубликуйте ее на сервере SharePoint.<br /><br /> <br /><br /> Дополнительные сведения об обновлении книг см. в разделе [обновление книг и запланированное обновление данных &#40;SharePoint 2013&#41;](instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).|  
|Изменения в организации работы DAX [ALL Function](https://msdn.microsoft.com/library/ee634802(v=sql.120).aspx).|До выхода версии [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)], если был задан столбец [Date] в окне «Пометить как таблицу дат» для использования в логике операций со временем и этот столбец [Date] передан в качестве аргумента в функцию ALL для использования в свою очередь в качестве фильтра в функции CALCULATE, пропускаются все фильтры для всех столбцов в таблице независимо от того, имеется ли какой-либо срез в столбце дат.<br /><br /> Например,<br /><br /> `= CALCULATE (<expression>, ALL (DateTable[Date]))`<br /><br /> До выхода версии [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]все фильтры пропускались для всех столбцов DateTable независимо от того, передавался ли столбец [Date] в качестве аргумента в функцию ALL.<br /><br /> Поведение версии [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] и в PowerPivot в Excel 2013 заключается в том, что фильтры пропускаются только для указанного столбца, передаваемого в качестве аргумента функции ALL.<br /><br /> Чтобы отказаться от нового поведения, по существу игнорируя применение всех столбцов в качестве фильтров для всей таблицы, можно исключить столбец [Date] из аргумента, например<br /><br /> `=CALCULATE (<expression>, ALL(DateTable))`<br /><br /> Результат будет такой же, как при организации работы до выхода версии [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)].|  
  
##  <a name="bkmk_sql2012"></a> Изменения в поведении [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 В этом разделе документированы изменения поведения в компонентах служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] в [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Эти изменения также применяются к [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
### <a name="analysis-services-multidimensional-mode"></a>Службы Analysis Services, многомерный режим  
  
#### <a name="nullprocessing-option-set-to-preserve-is-no-longer-supported-for-distinct-count-measures"></a>Параметр NullProcessing со значением «Сохранять» больше не поддерживается для мер числа различных объектов.  
 До версии [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], можно задать было [элемент NullProcessing &#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl) для `Preserve` для мер числа различных объектов.  К сожалению, такой подход часто приводил к недопустимым результатам, а иногда — к сбою задания обработки. Поэтому данная конфигурация более недоступна в [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Попытка использовать вызовет возникает следующая ошибка проверки: «Ошибки в диспетчере метаданных. Preserve не является действительным значением NullProcessing для \<measurename > мера числа различных объектов.»  
  
#### <a name="cube-browser-in-management-studio-and-cube-designer-has-been-removed"></a>Браузер кубов в среде Management Studio и конструктор кубов были удалены  
 Элемент управления браузера кубов, который позволяет перетаскивать поля в структуру сводной таблицы в среде Management Studio или в конструкторе кубов, был удален из продукта. Элемент управления был веб-компонентом Office Web Control (OWC). Веб-компоненты Office работали с устаревшей версией Office, поэтому больше не доступны.  
  
### <a name="powerpivot-for-sharepoint"></a>PowerPivot для SharePoint  
  
#### <a name="higher-permission-requirements-for-using-a-powerpivot-workbook-as-an-external-data-source"></a>Требование разрешений более высокого уровня для использования книги PowerPivot в качестве внешнего источника данных  
 Книга Excel может отображать данные PowerPivot, внедренные в ту же или во внешнюю книгу. В предыдущем выпуске требования к разрешениям были одинаковыми независимо от того, были ли данные PowerPivot внедренными или внешними. Разрешение **Только просмотр** в книге PowerPivot давало полный доступ ко всем данным PowerPivot в книге как для внедренных, так и для внешних соединений.  
  
 В этом выпуске требования к разрешениям были изменены для книг Excel, в которых отображаются данные PowerPivot из внешнего файла. В этом выпуске для подключения к внешней книге PowerPivot из клиентского приложения необходимо иметь разрешения на **Чтение** (а точнее, разрешение **Открытие элементов** ). Дополнительные разрешения определяют, что пользователь имеет права на загрузку для просмотра исходных данных, внедренных в книгу. Дополнительные разрешения отражают тот факт, что данные о модели полностью доступны клиентскому приложению или книге, которые содержат ссылки на них, что в результате лучше выравнивает требования к разрешениям и фактическую работу подключения к данным.  
  
 Чтобы продолжить использование книги PowerPivot в качестве внешнего источника данных, необходимо повысить уровень разрешений SharePoint для пользователей, которые подключаются к внешним данным PowerPivot. Пока вы не измените разрешения, при попытке доступа к книгам PowerPivot по соединению с источником данных пользователи будут получать следующую ошибку: «Веб-служба PowerPivot возвратила ошибку (Отказано в доступе. Запрошенный документ не существует или у вас нет разрешения на открытие файла.)»  
  
> [!WARNING]  
>  Далее описаны действия по прерыванию цепочки наследования разрешений на уровне библиотеки и повышению разрешений пользователя с уровня **Только просмотр** до уровня **Чтение** на определенные документы из этой библиотеки. Перед тем как продолжить, внимательно ознакомьтесь с существующими разрешениями и документами и убедитесь, что эти действия подходят для данного сайта.  
>   
>  В качестве альтернативы можно создать папку в библиотеке, переместить в нее все требуемые документы и задать уникальные разрешения на эту папку.  
  
> [!NOTE]  
>  Если книги хранятся в галерее PowerPivot, разрыв цепочки наследования разрешений для книги приведет к невозможности формирования эскизов для этой книги, если для нее настроено обновление данных. Чтобы одновременно разрешить доступ к книгам и к изображениям предварительного просмотра в галерее, рассмотрите возможность предоставления определенным пользователям разрешений на **Чтение** на уровне библиотеки для всех документов из этой библиотеки.  
  
 Изменять разрешения могут только владельцы сайтов.  
  
 **Как повысить разрешения до уровня для отдельных книг «чтение»**  
  
1.  Щелкните стрелку вниз, чтобы открыть меню для отдельного документа.  
  
2.  Нажмите **Управление разрешениями**.  
  
3.  По умолчанию библиотека наследует разрешения. Чтобы изменить разрешения для отдельных книг в этой библиотеке, нажмите кнопку **Прекратить наследование разрешений**.  
  
4.  Установите флажок около имени пользователя или группы, которым требуются дополнительные разрешения на книги PowerPivot. Дополнительные разрешения позволят этим пользователям получать доступ к внедренным данным PowerPivot и использовать эти данные в качестве внешнего источника данных в других документах.  
  
5.  Нажмите **Изменить разрешения пользователя**.  
  
6.  Выберите разрешения **Чтение** и нажмите кнопку **ОК**.  
  
#### <a name="powerpivot-gallery-new-rules-for-snapshot-generation-for-some-powerpivot-workbooks"></a>Коллекция PowerPivot. Новые правила для создания моментальных снимков для некоторых книг PowerPivot  
 В этом выпуске появились новые требования для создания моментальных снимков в галерее PowerPivot, исключающие потенциальную возможность раскрытия сведений (а именно просмотр моментального снимка данных из источника данных, на просмотр которых у пользователя нет разрешений). Эти требования относятся только к книгам PowerPivot, которые соединяются с внешними источниками данных при каждом просмотре книги. Если используются только книги, отображающие внедренные данные PowerPivot, никаких изменений в механизме формирования моментальных снимков в галерее PowerPivot заметно не будет.  
  
 Далее приведены новые требования к формированию моментальных снимков для книг, данные которых обновляются при каждом их открытии.  
  
-   Книги PowerPivot, которые используются в качестве внешнего источника данных другими книгами или отчетами, должны находиться в той же библиотеке, что и книги, которые эти данные получают. Например, если данные из файла sales-data.xlsx передаются в файл sales-report.xlsx, обе эти книги должны находиться в одной галерее, чтобы моментальные снимки могли отображаться.  
  
-   Книги, которые используются совместно, должны наследовать разрешения от общего родителя (другими словами, от галереи PowerPivot). В нашем примере файлы sales-data.xlsx и sales-report.xlsx должны наследовать разрешения от галереи PowerPivot.  
  
 Если книга не удовлетворяет любому из этих критериев, вместо ожидаемого эскиза будет отображен следующий значок блокировки.  
  
 ![GMNI_PowerPivotGalleryIcon_Locked](media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")  
  
#### <a name="new-default-setting-for-load-balancing-requests-changed-from-round-robin-to-health-based"></a>Новое значение по умолчанию параметра для запросов балансировки нагрузки изменилось с «Циклический перебор» на «По исправности»  
 Приложение службы PowerPivot имеет параметры по умолчанию, определяющие способ распределения запросов к данным PowerPivot между несколькими серверами PowerPivot для SharePoint в ферме. В предыдущем выпуске значением по умолчанию было **Циклический перебор**, при котором запросы распределялись последовательно среди доступных серверов. В этом выпуске значением по умолчанию является **По исправности**. Приложение службы PowerPivot использует статистику работоспособности сервера, такую как доступный объем памяти или ЦП, для определения того, какому экземпляру сервера направить запрос.  
  
 В случае обновления сервера в предыдущем выпуске приложение службы PowerPivot сохранит предыдущее значение по умолчанию (**Циклический перебор**). Чтобы использовать способ распределения **По исправности** , необходимо изменить параметры конфигурации. Дополнительные сведения см. в разделе [Создание и настройка приложения службы PowerPivot](power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="see-also"></a>См. также  
 [Обратная совместимость](../../2014/getting-started/backward-compatibility.md)   
 [Критические изменения служб Analysis Services в SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
  
