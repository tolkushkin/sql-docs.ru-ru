---
title: Обновление книг и запланированное обновление данных (SharePoint 2013) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a49c4af4-e243-4926-be97-74da1f9d54eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57fe740bdd02c96eb21994f5996c734620793616
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079843"
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>Обновление книг и запланированное обновление данных (SharePoint 2013)
  В этом разделе описываются способы использования книг, созданных в предыдущих средах PowerPivot, и способы обновления книг PowerPivot с целью получения преимуществ от новых функций этого выпуска. Дополнительные сведения о новых возможностях см. в разделе [новые возможности PowerPivot](https://go.microsoft.com/fwlink/?LinkID=203917).  
  
> [!WARNING]  
>  Невозможно выполнить откат обновления для книг, автоматически обновленных на сервере. После обновления книги она остается обновленной. Для использования предыдущей версии можно повторно опубликовать предыдущую книгу в SharePoint, восстановить предыдущую версию или повторно использовать книгу. Дополнительные сведения о восстановлении и повторном использовании документа в SharePoint см. в разделе [Планирование защиты содержимого с использованием корзин и управления версиями](https://go.microsoft.com/fwlink/?LinkId=238669).  
  
 Этот раздел состоит из следующих подразделов.  
  
-   [Общие сведения об обновлении книг](#bkmk_overview)  
  
-   [Выполните обновление до книг версии SQL Server 2012 с пакетом обновления 1 (SP1) от книг 2008 R2](#bkmk_to_2012sp1_from_2008r2)  
  
-   [Обновление до книг Office 2013 из версий, созданных с помощью 2012 надстройки PowerPivot для Excel](#bkmk_to_2012sp1_from_2012)  
  
-   [Обновление до книг SQL Server 2012 из версий, созданных с помощью надстройки 2008 R2 PowerPivot для Excel 2010](#bkmk_to_2012_from_2008R2)  
  
-   [Запуск нескольких версий книги на сервере более новых версий](#bkmk_runold)  
  
##  <a name="bkmk_overview"></a> Общие сведения об обновлении книг  
 Книга PowerPivot — это книга Excel с внедренными данными PowerPivot. Обновление книги обеспечивает два преимущества.  
  
-   Используйте новые возможности [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)].  
  
-   Становится возможным плановое обновление данных для книг, которые работают с сервером служб [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] Analysis Services в режиме интеграции с SharePoint.  
  
> [!IMPORTANT]  
>  Нельзя выполнить откат обновленной книги, поэтому обязательно создайте копию файла, если предполагается его использование в предыдущих версиях [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]или [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 В следующей таблице перечислены поддержка и поведение книг PowerPivot в зависимости от среды, в которой была создана книга. Описанное поведение включает общие методы работы пользователя, поддерживаемые варианты обновления книги в определенной среде и плановое обновление данных книги, которая еще не была обновлена.  
  
### <a name="workbook-behavior-and-upgrade-options"></a>Поведение и варианты обновления книги  
  
|Создано в|\<|Поддержка и поведение|>|  
|----------------|--------|--------------------------|--------|  
||**2008 R2 PowerPivot для SharePoint 2010**|**2012 PowerPivot для SharePoint 2010**|**2012 PowerPivot с пакетом обновления 1 для SharePoint 2013**|  
|**2008 R2 PowerPivot для Excel 2010**|Все компоненты|**Возможности:** Пользователи могут взаимодействовать с книгой в браузере и использовать ее в качестве источника данных для других решений.<br /><br /> **Обновление:** Автоматическое обновление книг в библиотеке документов, если автоматическое обновление включено для системной службы PowerPivot в ферме SharePoint<br /><br /> **Расписание обновления данных.** НЕ поддерживается. Книгу необходимо обновить.|**Возможности:** Пользователи могут взаимодействовать с книгой и использовать ее в качестве источника данных для других решений.<br /><br /> **Обновление:** Автоматическое обновление недоступно. Необходимо вручную обновить книги 2008 R2 до версии 2012 или до версии Office 2013.<br /><br /> **Расписание обновления данных.** НЕ поддерживается. Книгу необходимо обновить.|  
|**2012 PowerPivot для Excel**|Не поддерживается|Все компоненты|**Возможности:** Пользователи могут взаимодействовать с книгой в браузере и использовать ее в качестве источника данных для других решений. Расписание обновления данных доступно.<br /><br /> **Обновление:** Автоматическое обновление не поддерживается. Пользователи могут вручную обновить книги до версии Office 2013.<br /><br /> **Расписание обновления данных:** поддерживается.|  
|**Excel 2013**|Не поддерживается|Не поддерживается|Все компоненты|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a> Выполните обновление до книг версии SQL Server 2012 с пакетом обновления 1 (SP1) от книг 2008 R2  
 В этом разделе описывается обновление книг SQL Server 2012 PowerPivot с пакетом обновления 1 (SP1) для Excel 2013 от книг SQL Server 2008 R2 PowerPivot для Excel 2010.  
  
 **Изменение поведения:** Книги SQL Server 2008 R2 PowerPivot не обновляются автоматически при их использовании в SQL Server 2012 с пакетом обновления 1 PowerPivot для SharePoint 2013. Поэтому плановые обновления данных не будут действовать для книг SQL Server 2008 R2 PowerPivot.  
  
 Книги 2008 R2 открываются в PowerPivot для SharePoint 2013, однако плановые обновления данных не выполняются. При просмотре журнала обновления обнаруживается сообщение об ошибке следующего вида:  
  
 «Книга содержит неподдерживаемую модель PowerPivot. Модель PowerPivot в книге представлена в формате SQL Server 2008 R2 PowerPivot для Excel 2010. Поддерживаются следующие модели PowerPivot:  
  
-   SQL Server 2012 PowerPivot для Excel 2010.  
  
-   SQL Server 2012 PowerPivot для Excel 2013.  
  
 **Как обновление книги:** Плановое обновление данных не будет работать, пока вы не обновите ее до книги 2012. Для обновления книги и содержащейся в ней модели выполните одно из следующих действий.  
  
-   Загрузите и откройте книгу в Microsoft Excel 2010 с помощью установленной надстройки SQL Server 2012 PowerPivot для Excel.  
  
     Откройте окно PowerPivot и обновите модель PowerPivot.  
  
     Сохраните книгу и повторно опубликуйте ее в SharePoint.  
  
-   Загрузите и откройте книгу в Microsoft Excel 2013.  
  
     Откройте окно PowerPivot и обновите модель PowerPivot.  
  
     Затем сохраните книгу и повторно опубликуйте ее на сервере SharePoint.  
  
 Дополнительные сведения об изменениях функций служб Analysis Services, см. в разделе [изменения в работе функций служб Analysis Services в SQL Server 2014](../../behavior-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
 Дополнительные сведения о журнале обновления см. в разделе [Просмотр журнала обновления данных &#40;PowerPivot для SharePoint&#41;](../../power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a> Обновление до книг Office 2013 из версий, созданных с помощью 2012 надстройки PowerPivot для Excel  
 В этом разделе описывается обновление **до** SQL Server 2012 PowerPivot с пакетом обновления 1 (SP1) в Excel 2013 **от** книг SQL Server 2012 PowerPivot для Excel 2010.  
  
 Обновление книги устраняет следующие ошибки, которые возникают при попытке обновления данных книги предшествующей версии по расписанию:  
  
 «Операция обновления для книг, созданных в ранних версиях PowerPivot не доступны.»  
  
 **Обновление книги**  
  
1.  Обновите каждую книгу вручную, открыв ее в Microsoft Excel 2013.  
  
2.  Для обновления книги и содержащейся в ней модели загрузите и откройте книгу в приложении Microsoft Excel 2013.  
  
3.  Откройте окно PowerPivot и обновите модель PowerPivot.  
  
4.  Затем сохраните книгу и повторно опубликуйте ее на сервере SharePoint 2013.  
  
##  <a name="bkmk_to_2012_from_2008R2"></a> Обновление до книг SQL Server 2012 из версий, созданных с помощью надстройки 2008 R2 PowerPivot для Excel 2010  
 В этом разделе описывается обновление **до** SQL Server 2012 PowerPivot для Excel 2010 **от** книг SQL Server 2008 R2 PowerPivot для Excel 2010.  
  
 Обновление книги устраняет следующие ошибки, которые возникают при попытке обновления данных книги предшествующей версии по расписанию:  
  
 «Операция обновления для книг, созданных в ранних версиях PowerPivot не доступны.»  
  
 **Обновление книги**  
  
 Существует два способа обновления.  
  
1.  Обновить версию каждой книги вручную путем ее открытия в Excel на компьютере, где установлена версия [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] PowerPivot для Excel с последующей повторной публикацией на сервере. При открытии книги в последней версии надстройки выполняются следующие внутренние операции. Поставщик данных в строке подключения к данным книги обновляется до MSOLAP.5, обновляются также метаданные, и выполняется воссоздание связей для соответствия более новой реализации.  
  
2.  Иначе администратор SharePoint может включить функцию автоматического обновления для службы PowerPivot в ферме SharePoint, чтобы автоматически обновить книгу [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] PowerPivot при выполнении обновления данных по расписанию (обновлены только книги, для которых настроено обновление данных по расписанию).  
  
    > [!NOTE]  
    >  Автоматическое обновление — это функция настройки сервера; его нельзя включить или отключить для конкретной книги, библиотеки или семейства веб-сайтов.  
  
 **Настройка автоматического обновления во время обновления данных**  
  
 Чтобы включить автоматическое обновление, необходимо установить флажок **Автоматически обновлять книги PowerPivot для обновления данных с сервера** в программе настройки PowerPivot. Флажок находится на странице **Обновление системной службы PowerPivot** этой программы либо на странице **Создание приложения службы PowerPivot** при настройке новой установки.  
  
 Запустив следующий командлет, можно проверить, включена ли функция автоматического обновления.  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 Результатом вызова Get-PowerPivotSystemService будет список свойств вместе с соответствующими значениями. В списке свойств нужно найти `WorkbookUpgradeOnDataRefresh`. Оно будет иметь значение **true** , если автоматическое обновление включено. Если же это свойство имеет значение **false**, перейдите на следующий шаг и включите автоматическое обновление книги.  
  
 Чтобы включить автоматическое обновление книги, выполните следующую команду:  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true -Confirm:$false  
```  
  
 После обновления книги можно пользоваться обновлением данных по расписанию и новыми возможностями надстройки PowerPivot для Excel.  
  
##  <a name="bkmk_runold"></a> Запуск нескольких версий книги на сервере более новых версий  
 Книги PowerPivot более старых и новых версий можно использовать одновременно на экземпляре [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 В зависимости от метода установки сервера **может потребоваться** установить предыдущую версию поставщика OLE DB служб Analysis Services, чтобы на одном сервере можно было открывать книги как старых, так и новых версий.  
  
 Обратите внимание, что не поддерживается публикация книг новой версии на предшествующих экземплярах SQL Server [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] . Экземпляр [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] не загружает книги, созданные в версии [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)], а экземпляр SQL Server 2012 не будет загружать книги Office 2013 с расширенными моделями данных, созданные с использованием PowerPivot версии [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] в Excel.  
  
###  <a name="bkmk_msolapxslx"></a> Как проверить сведения о поставщике данных MSOLAP в книге PowerPivot  
 Для определения текущей версии поставщика OLE DB для книги PowerPivot выполните следующие действия. Для проверки сведений подключения к данным не требуется установка надстройки [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] .  
  
1.  Нажмите кнопку **Соединения**на вкладке «Данные» в Excel. Нажмите кнопку **Свойства**.  
  
2.  На вкладке **Определение** в начале строки подключения отображается версия поставщика.  
  
     **Provider=MSOLAP.5** указывает, что книга версии [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
     **Provider=MSOLAP.4** указывает на версию [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)].  
  
     **Источник данных = $Embedded$** указывает, что книга является книгой PowerPivot, используя внедренную базу данных.  
  
###  <a name="bkmk_msolappc"></a> Проверка текущей версии поставщика данных MSOLAP на локальном компьютере  
 Для определения текущей версии поставщика OLE DB на сервере или рабочей станции, на которой запускаются книги PowerPivot, используйте инструкции, приведенные ниже. Сведения о текущей версии позволят выполнять диагностику ошибок подключений к данным после обновления.  
  
1.  В редакторе реестра перейдите в раздел HKEY_CLASSES_ROOT  
  
2.  С помощью прокрутки перейдите в раздел MSOLAP. Убедитесь, что в списке поставщиков OLAP, установленных в системе, указан MSOLAP.5. Убедитесь, что для параметра MSOLAP | CurVer задано значение MSOLAP.5  
  
## <a name="see-also"></a>См. также  
 [Перенос PowerPivot в SharePoint 2013](migrate-power-pivot-to-sharepoint-2013.md)   
 [Обновление PowerPivot для SharePoint](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Новые возможности служб Analysis Services и бизнес-аналитики](../../what-s-new-in-analysis-services.md)   
 [Просмотр журнала обновления данных &#40;PowerPivot для SharePoint&#41;](../../power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
