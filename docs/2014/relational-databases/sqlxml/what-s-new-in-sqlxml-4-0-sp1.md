---
title: Что&#39;возможности в SQLXML 4.0 с пакетом обновления 1 | Документация Майкрософт
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- SQLNCLI, SQLXML
- what's new [SQLXML]
- SQLXML, what's new
- migrating SQLXML applications
- redistributing SQLXML
- SQL Server Native Client, SQLXML
- side-by-side installations [SQLXML]
ms.assetid: 48f7720b-1705-402d-93ce-097ff1737877
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ca2bc726b0bf017ec4b3dd0451313d60ef57696
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012140"
---
# <a name="what39s-new-in-sqlxml-40-sp1"></a>Что&#39;возможности в SQLXML 4.0 с пакетом обновления 1
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 с пакетом обновления 1 (SP1) содержит различные обновления и улучшения. В этом разделе содержится описание всех обновлений и предоставляются ссылки на более подробные сведения (если они доступны). SQLXML 4.0 с пакетом обновления 1 (SP1) предоставляет улучшения для поддержки новых типов данных, появившихся в [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. В этом разделе рассматриваются следующие вопросы.  
  
-   Установка SQLXML 4.0 с пакетом обновления 1 (SP1)  
  
-   Проблемы параллельной установки  
  
-   SQLXML 4.0 и MSXML  
  
-   Распространение SQLXML 4.0  
  
-   Поддержка [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Поддержка новых типов данных [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
-   Изменения в SQLXML 4.0, относящиеся к массовой загрузке XML  
  
-   Изменения в SQLXML 4.0, относящиеся к разделам реестра  
  
-   Проблемы переноса  
  
## <a name="installing-sqlxml-40-sp1"></a>Установка SQLXML 4.0 с пакетом обновления 1 (SP1)  
 До версии [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] компонент SQLXML 4.0 распространялся с SQL Server и входил в состав установки по умолчанию всех версий SQL Server, за исключением SQL Server Express. Начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], последняя версия SQLXML (SQLXML 4.0 с пакетом обновления 1 (SP1)) больше не включается в состав SQL Server. Чтобы установить SQLXML 4.0 с пакетом обновления 1, загрузите ее из [места установки для SQLXML 4.0 с пакетом обновления 1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 Файлы SQLXML 4.0 с пакетом обновления 1 (SP1) устанавливаются в следующий каталог:  
  
 `%PROGRAMFILES%\SQLXML 4.0\`  
  
> [!NOTE]  
>  Все необходимые настройки реестра для SQLXML 4.0 вносятся в процессе установки.  
  
 Чтобы обеспечить эксплуатацию 32-разрядных приложений SQLXML под управлением WOW64 в 64-разрядных операционных системах Windows, запустите 64-разрядный пакет SQLXML 4.0 с пакетом обновления 1 (SP1), имеющий имя sqlxml4.msi, который можно найти в центре загрузки.  
  
#### <a name="uninstalling-sqlxml-40-sp1"></a>Удаление SQLXML 4.0 с пакетом обновления 1 (SP1)  
 Для SQLXML 3.0 с пакетом обновления 3 (SP3), SQLXML 4.0 и SQLXML 4.0 с пакетом обновления 1 (SP1) применяются общие разделы реестра. При удалении более поздних версий SQLXML на том же компьютере, где установлен SQLXML 3.0 с пакетом обновления 3 (SP3), может потребоваться повторная установка SQLXML 3.0 с пакетом обновления 3 (SP3).  
  
## <a name="side-by-side-installation-issues"></a>Проблемы параллельной установки  
 Процесс установки SQLXML 4.0 не удаляет файлы, установленные для прежних версий SQLXML. Поэтому возможно существование DLL-библиотек для нескольких различающихся версиями установок SQLXML на компьютере. Можно запускать установленные экземпляры параллельно. SQLXML 4.0 содержит как независимые от версии, так и зависимые от версии идентификаторы PROGID. Во всех рабочих приложениях должны использоваться зависимые от версии идентификаторы PROGID.  
  
## <a name="sqlxml-40-sp1-and-msxml"></a>SQLXML 4.0 с пакетом обновления 1 (SP1) и MSXML  
 SQLXML 4.0 не устанавливает MSXML. SQLXML 4.0 использует службы MSXML 6.0, которые устанавливаются в составе установки [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] или более поздней установки.  
  
## <a name="redistributing-sqlxml-40-sp1"></a>Распространение SQLXML 4.0 с пакетом обновления 1 (SP1)  
 Предусмотрена возможность распространять SQLXML 4.0 с пакетом обновления 1 (SP1) с помощью распространяемого пакета установщика. Один из способов установки нескольких пакетов в одном (с точки зрения пользователя) сеансе установки состоит в применении технологии построителей цепочек и загрузчиков. Дополнительные сведения см. в статьях Разработка пользовательского пакета загрузчика для Visual Studio 2005 и Добавление настраиваемых необходимых компонентов.  
  
 Если приложение планируется использовать на платформе, отличной от той, на которой оно разрабатывалось, можно скачать из центра загрузки Майкрософт версии sqlncli.msi for x64, Itanium и x86.  
  
 Существуют также отдельно распространяемые программы установки для MSXML 6.0 (msxml6.msi). Они находятся на установочном компакт-диске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в следующем каталоге:  
  
 `%CD%\Setup\`  
  
 Эти установочные файлы можно использовать для установки MSXML 6.0 непосредственно с компакт-диска. Их можно также использовать для свободного распространения MSXML 6.0 и SQLXML 4.0 с пакетом обновления 1 (SP1) вместе с собственными приложениями.  
  
 Нужно также распространить собственный клиент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], если он используется с приложением как поставщик данных. Дополнительные сведения см. в статье [Установка SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="support-for-sql-server-native-client"></a>Поддержка собственного клиента SQL Server  
 SQLXML 4.0 поддерживает как поставщика SQLOLEDB и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поставщики Native Client. Рекомендуется использовать ту же версию [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поставщик для собственного клиента и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поскольку [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client разработано для поддержки все новые типы данных, которые предусматриваются сервером, таких как `Date, Time`, `DateTime2`, и `dateTimeOffset` типы данных в [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] и поддерживается [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client.  
  
 Собственный клиент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] — это технология доступа к данным, которая введена в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Она объединяет поставщика SQLOLEDB и драйвер SQLODBC в одну собственную динамическую библиотеку (DLL), а также предоставляет новую уникальную функциональность, независимую от компонентов доступа к данным MDAC и отличную от них.  
  
 Технология собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может применяться для создания новых или усовершенствования существующих приложений, которым требуется доступ к новым функциям [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], которые не поддерживаются SQLOLEDB и SQLODBC в компонентах MDAC и [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Например, собственный клиент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] необходим для клиентских функций SQLXML, таких как FOR XML, чтобы использовать тип данных `xml`. Дополнительные сведения см. в разделе [форматирование XML на стороне клиента &#40;SQLXML 4.0&#41;](formatting/client-side-xml-formatting-sqlxml-4-0.md), [использование объектов ADO для выполнения запросов SQLXML 4.0](using-ado-to-execute-sqlxml-4-0-queries.md), и [программирование SQL Server Native Client](../native-client/sql-server-native-client-programming.md).  
  
> [!NOTE]  
>  Между SQLXML 4.0 и SQLXML 3.0 нет полной обратной совместимости. В результате устранения некоторых ошибок и других функциональных изменений, особенно прекращения поддержки SQLXML ISAPI, нельзя использовать виртуальные каталоги IIS с SQLXML 4.0. Большинство приложений будут работать с небольшими изменениями, но их необходимо проверить перед запуском в рабочей среде с SQLXML 4.0.  
  
## <a name="support-for-data-types-introduced-in-sql-server-2005-and-sql-server-2008"></a>Поддержка типов данных, появившихся в SQL Server 2005 и SQL Server 2008  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] представленные `xml` тип данных и SQLXML 4.0 поддерживает `xml` тип данных. Дополнительные сведения см. в разделе [поддержка типов данных в SQLXML 4.0 xml](xml-data-type-support-in-sqlxml-4-0.md).  
  
 Примеры использования типа данных `xml` в SQLXML при сопоставлении XML-представлений, массовой загрузке XML и выполнении диаграмм обновления XML приведены в следующих разделах.  
  
-   [По умолчанию осуществляется сопоставление элементов и атрибутов с таблицами и столбцами XSD](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
-   [Вставка данных с помощью диаграмм обновления XML](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
-   [Примеры массовой загрузки XML-документов](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] представленные `Date, Time`, `DateTime2`, и **DateTimeOffset** типов данных. SQLXML 4.0 с пакетом обновления 1 (SP1) позволяет использовать эти четыре новых типа данных в качестве встроенных скалярных типов в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client OLE DB Provider (SQLNCLI10), который поставляется вместе с [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="xml-bulk-load-changes-for-sqlxml-40-sp1"></a>Изменения в SQLXML 4.0 с пакетом обновления 1 (SP1), относящиеся к массовой загрузке XML  
  
-   Для SQLXML 4.0 поле переполнения SchemaGen создается с помощью `xml` тип данных. Дополнительные сведения см. в разделе [модель объектов массовой загрузки SQL Server XML](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md).  
  
-   Если ранее были созданы приложения [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic и нужно использовать SQLXML 4.0, необходимо перекомпилировать приложения со ссылкой на Xblkld4.dll.  
  
-   Для приложений Visual Basic Scripting Edition необходимо зарегистрировать используемую DLL-библиотеку. В следующем примере, если указаны независимые от версий идентификаторы PROGID, приложение зависит от последней зарегистрированной DLL-библиотеки:  
  
    ```  
    set objBulkLoad = CreateObject("SQLXMLBulkLoad.SQLXMLBulkLoad")   
    ```  
  
    > [!NOTE]  
    >  Зависимый от версии идентификатор PROGID — SQLXMLBulkLoad.SQLXMLBulkLoad.4.0.  
  
## <a name="registry-key-changes-for-sqlxml-40"></a>Изменения в SQLXML 4.0, относящиеся к разделам реестра  
 В SQLXML 4.0 разделы реестра изменились по сравнению с предшествующими выпусками на следующие:  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\SchemaCacheSize  
  
 Необходимо изменить настройки, чтобы эти разделы были действительны в SQLXML 4.0.  
  
 Кроме того, в SQLXML 4.0 появились следующие разделы реестра:  
  
-   `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\ReportErrorsWithSQLInfo`  
  
     По умолчанию SQLXML 4.0 возвращает собственные сведения об ошибке, предоставленные OLE DB и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], вместо высокоуровневой ошибки (как в случае с прежними версиями SQLXML). Если такое поведение нежелательно, значение типа DWORD этого раздела реестра должно быть установлено в 0 (значение по умолчанию — 1).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\FORXML_GenerateGUIDBraces  
  
     По умолчанию SQLXML возвращает значения идентификатора SQL Server GUID без заключения в фигурные скобки. Если идентификатор GUID значение должно возвращаться с фигурными скобками (например, {*некоторые GUID*}), этот раздел реестра должен иметь значение 1 (по умолчанию — 0).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\SQL2000CompatMode  
  
     По умолчанию, когда средство синтаксического анализа XML загружает данные, пробелы нормализуются в соответствии с правилами XML 1.0. Это приводит к потере некоторых пробельных символов в данных. Таким образом, текстовое представление данных может измениться после синтаксического анализа, хотя семантически данные остаются прежними.  
  
     Раздел представлен таким образом, что можно оставить пробельные символы в данных. Если добавить этот раздел реестра и установить его значение равным 0, пробельные символы (возврат каретки, переноса строки и табуляция) в XML-документе возвращаются закодированными для значений атрибутов. Для значений элементов возвращается закодированным только символ возврата каретки.  
  
     Пример:  
  
    ```  
    CREATE TABLE T( Col1 int, Col2 nvarchar(100));  
    GO  
    -- Insert data with tab, line feed and carriage return).  
    INSERT INTO T VALUES (1, 'This is a tab    . This is a line feed and CR   
     more text');  
    GO  
    -- Test this query (without the registry key).  
    SELECT * FROM T   
    FOR XML AUTO;  
    -- This is the result (no encoding of special characters).  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
    -- Now add registry key with value 0 and execute the query again.  
    -- Note the encoding for carriage return, line-feed and tab in the attribute value.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
  
    -- Update the query and specify ELEMENTS directive  
    SELECT * FROM T  
    FOR XML AUTO, ELEMENTS  
    -- Only the carriage return is returned encoded.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
       <T>  
          <Col1>1</Col1>  
          <Col2>This is a tab    . This is a line feed and CR   
     more text</Col2>  
       </T>  
    </r>  
    ```  
  
## <a name="migration-issues"></a>Проблемы переноса  
 Ниже перечислены проблемы, которые могут повлиять на перенос прежних приложений SQLXML на SQLXML 4.0.  
  
### <a name="ado-and-sqlxml-40-queries"></a>Запросы ADO и SQLXML 4.0  
 В предыдущих версиях SQLXML выполнение запросов на основе URL-адресов поддерживалось с помощью виртуальных каталогов IIS и ISAPI-фильтра SQLXML. Для приложений, использующих SQLXML 4.0, эта функция больше не поддерживается.  
  
 Вместо этого запросы, шаблоны и диаграммы обновления SQLXML могут выполняться с помощью расширений SQLXML для объектов данных ActiveX (ADO), появившихся в компонентах доступа к данным MDAC 2.6 и более поздних.  
  
 Дополнительные сведения см. в разделе [использование объектов ADO для выполнения запросов SQLXML 4.0](using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="supportability-for-sqlxml-30-isapi-and-data-types-introduced-in-sql-server-2005"></a>Поддержка SQLXML 3.0 ISAPI и новых типов данных в SQL Server 2005  
 Поскольку ISAPI удалена поддержка SQLXML 4.0, если вашему решению требуется определить типы данных функций, представленных в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] например [тип данных xml](/sql/t-sql/xml/xml-transact-sql) или [-определяемые пользователем типы данных (UDT)](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)и веб-доступ, необходимо будет использовать другое решение, например [управляемые классы SQLXML](../sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md) или другой тип обработчика HTTP, таких как собственные веб-службы XML для SQL Server 2005.  
  
 Кроме того, если эти расширения типов не требуется, можно продолжать применять SQLXML 3.0 для подключения к [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] установок. Средства поддержки ISAPI, реализованные в SQLXML 3.0, будут работать с более поздними версиями, но не поддерживают и не распознают тип данных `xml` и определяемые пользователем типы данных, поддержка которых появилась в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
### <a name="xml-bulk-load-security-changes-for-temporary-files"></a>Изменения в массовой загрузке XML для временных файлов  
 Для SQLXML 4.0 и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] разрешения на файл массовой загрузки XML предоставляются пользователю, выполняющему операцию массовой загрузки. Разрешения на чтение и запись наследуются из файловой системы. В прежних выпусках SQLXML и SQL Server, массовая загрузка XML на основе SQLXML создавала временные файлы, которые не были защищены и могли быть считаны любым пользователем.  
  
### <a name="migration-issues-for-client-side-for-xml"></a>Проблемы миграции для FOR XML на клиентской стороне  
 Из-за изменений в механизме выполнения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может возвращать разные значения в метаданных для базовой таблицы, от возвращаемых при выполнении запроса FOR XML в [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Если это происходит, форматирование результатов запроса FOR XML на стороне клиента будут иными, в зависимости о версии, на которой работал запрос.  
  
 Если запрос FOR XML выполняется на клиентской стороне с помощью SQLXML 3.0 над столбцом данных типа `xml`, данные в результатах будут возвращены как строка с полным преобразованием в сущность. В SQLXML 4.0, если собственный клиент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLNCLI11) указан как поставщик, данные возвращаются как XML.  
  
  
