---
title: Добавление данных из внешних источников данных (службы SSRS)
ms.prod: reporting-services
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/27/2017
ms.openlocfilehash: c82d8295ec4a8293abc822900e25e654447a492c
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775804"
---
# <a name="add-data-from-external-data-sources-ssrs"></a>Добавление данных из внешних источников данных (службы SSRS)

Чтобы получить данные из внешнего источника данных, используется подключение к данным. Сведения о подключении к данным обычно указываются владельцем внешнего источника данных, ответственным за предоставление разрешений и указывающим тип используемых учетных данных. Сведения о подключении к данным сохраняются в виде источника данных отчета. Тип источника данных определяет модуль обработки данных, который будет использоваться для получения данных.  

##  <a name="DataAccess"></a> Основные сведения о технологии доступа к данным  

Для получения данных набора данных отчета необходимо использование нескольких слоев программного обеспечения доступа к данным. В следующем списке приведено простое описание принципов работы отчетов с технологиями доступа к данным.  

-   **Приложение и пользовательский интерфейс.** Приложение «Построитель отчетов», используемое для создания источников данных, добавления ссылок к общему источнику данных, добавления общих наборов данных и добавления элементов отчетов, содержащих источники данных и наборы данных, от которых они зависят.  

-   **Элементы определения отчетов.** Источники данных и наборы данных являются частью определения отчета. После публикации отчета на сервере отчетов общие источники данных и общие наборы данных управляются независимо от определений отчетов.  

  -   **Источник данных и общий источник данных.** Части определения отчета, содержащие сведения о типе модуля обработки данных, сведения о соединении и данные проверки подлинности.  

  -   **Набор данных и коллекция полей.** Часть определения отчета, содержащая запрос, коллекцию полей и типы данных полей.  

-   **Модули обработки данных служб Reporting Services.** Встроенные модули обработки данных служб, устанавливаемые при установке построителя отчетов. Модуль обработки данных реализует функции выполнения проверки подлинности, доступа к серверным агрегатным значениям и многозначным параметрам.  

-   **Поставщик данных.** Программное обеспечение, управляющее соединениями и получением данных из внешних источников данных. Поставщик данных определяет синтаксис строки соединения. Большая часть модулей обработки данных основана на слое поставщика данных.  

-   **Внешний источник данных.** Источник для получения данных отчета, например, база данных, файл, куб или веб-служба.  

> [!NOTE]  
>  Если соединение с сервером отчетов отсутствует, для выбора доступны установленные совместно с построителем отчетов модули обработки данных. Доступ к данным реализуется от лица одного пользователя с использованием учетных данных компьютера пользователя. При соединении с сервером отчетов можно выбрать модуль обработки данных, установленный на сервере отчетов. Доступ к данным реализуется от лица одного из нескольких пользователей, запускающих отчет, с использованием учетных данных на сервере отчетов. Дополнительные сведения см. в разделе [Указание учетных данных в построителе отчетов](../specify-credentials-in-report-builder.md).  

##  <a name="ReportData"></a> Основные сведения о данных отчета  
Отчет в простейшей форме отображает данные набора данных отчета в области данных на странице отчета, т.е. в одной таблице, диаграмме, матрице или другом типе области данных отчета. Данные в наборе данных отчета получаются от первого результирующего набора, возвращаемого единственной командной запроса, которая выполняется при условии доступа только для чтения к внешнему источнику данных. Все области данных расширяются по мере необходимости, чтобы отобразить все данные из набора данных.  

Данные набора данных, в сущности, имеют табличный формат. Столбцы представляют собой поля запроса набора данных. Строки являются строками результирующего набора. В отчете можно использовать следующие обобщенные типы данных:  

-   Данные прямоугольника. Данные результирующего набора с одинаковым количеством столбцов во всех строках.  

-   Данные с иерархической структурой поддерживаются, как плоский набор строк.  

  -   Неоднородные иерархии, с различным количеством столбцов в строках данных, не поддерживаются. Это необходимо учитывать при работе с некоторыми модулями обработки данных.  

  -   Модули обработки данных, которые работают с многомерными источниками данных, используют протокол XML для аналитики и извлекают данные в виде плоского набора строк, а не в виде набора ячеек.  

  -   Модуль обработки XML-данных автоматически делает XML-данные плоскими для их использования в отчете. Если первый экземпляр XML-элемента не содержит все атрибуты или вложенные элементы, данные могут быть недоступны для использования в качестве данных отчета.  

-   Поддерживается использование рекурсивных данных. Результирующий набор, содержащий иерархию рекурсивных данных, содержит в прямоугольном результирующем наборе все сведения об иерархической структуре. Например, структура подчинения в компании может быть представлена таблицей с двумя столбцами: подчиненный и руководитель. Каждый руководитель также является подчиненным с собственным руководителем. В столбце руководителя у руководителя наивысшего уровня обычно содержится значение NULL или другой идентификатор, указывающий, что у этого сотрудника руководитель отсутствует.  



##  <a name="DataTypes"></a> Работа с типами данных  
При создании набора данных типы данных полей сопоставляются с подмножеством типов данных среды CLR платформы [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Типы данных, которые не удается однозначно сопоставить, возвращаются в виде строк. Дополнительные сведения о работе с типами данных полей см. в разделе [Коллекция полей набора данных (построитель отчетов и службы SSRS)](dataset-fields-collection-report-builder-and-ssrs.md). При создании параметра его тип данных должен поддерживаться определением отчета. Дополнительные сведения о сопоставлении типов данных поставщика данных и параметров отчета см. в разделе [Типы данных в выражениях (построитель отчетов и службы SSRS)](../report-design/expressions-report-builder-and-ssrs.md).  



##  <a name="HowTo"></a> Инструкции  
В этом разделе содержатся пошаговые инструкции по работе с подключениями к данным, источниками данных и наборами данных.  

[Добавление и проверка подключения к данным или источнику данных &#40;построитель отчетов и службы SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  

[Создание общего или внедренного набора данных (построитель отчетов и службы SSRS)](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  

[Добавление фильтра к набору данных (построитель отчетов и службы SSRS)](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  

## <a name="InThisSection"></a> в этом разделе  

В следующих разделах представлены сведения о всех встроенных модулях обработки данных.  

|Раздел|Тип источника данных|  
|-----------|----------------------|  
|[Тип соединения SQL Server (службы SSRS)](sql-server-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|[Тип соединения служб Analysis Services для запросов многомерных выражений (службы SSRS)](analysis-services-connection-type-for-mdx-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[Тип соединения PowerPivot &#40;SSRS&#41;](power-pivot-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[Тип подключения к списку SharePoint](sharepoint-list-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint|  
|[Тип соединения с SQL Azure (службы SSRS)](sql-azure-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|[Тип соединения с SQL Server Parallel Data Warehouse (службы SSRS)](sql-server-parallel-data-warehouse-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|  
|[Тип соединения SAP NetWeaver BI (службы SSRS)](sap-netweaver-bi-connection-type-ssrs.md)|SAP NetWeaver BI|  
|[Тип соединения Hyperion Essbase (службы SSRS)](hyperion-essbase-connection-type-ssrs.md)|Hyperion Essbase|  
|[Тип соединения OLE DB (службы SSRS)](ole-db-connection-type-ssrs.md)|OLE DB|  
|[Тип соединения ODBC (службы SSRS)](odbc-connection-type-ssrs.md)|интерфейс ODBC|  
|[Тип соединения XML (службы SSRS)](xml-connection-type-ssrs.md)|XML|  

## <a name="Related"></a> См. также  

В этих разделах документации содержатся подробные сведения о данных отчетов, а также методические сведения об определении, настройке и использовании элементов отчетов, связанных с данными.  

|Раздел|Описание|  
|-----------|-----------------|  
|[Добавление данных в отчет &#40;построитель отчетов и службы SSRS&#41;](report-datasets-ssrs.md)|Предоставляет общие сведения о доступе к данным отчета.|  
|[Подключения к данным, источники данных и строки подключения в построителе отчетов](../data-connections-data-sources-and-connection-strings-in-report-builder.md)|Предоставляет сведения о подключениях к данным и источникам данных.|  
|[Внедренные и общие наборы данных отчета (построитель отчетов и службы SSRS)](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|Предоставляет сведения об общих и внедренных наборах данных.|  
|[Коллекция полей набора данных (построитель отчетов и службы SSRS)](dataset-fields-collection-report-builder-and-ssrs.md)|Предоставляет сведения о коллекции полей набора данных, создаваемой запросом.|  
|[Источники данных, поддерживаемые службами Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md), см. в документации [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] в [электронной документации](https://go.microsoft.com/fwlink/?linkid=121312) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Предоставляет подробные сведения о поддержке платформ и версий для каждого модуля обработки данных.|  
|[Общие сведения о модулях обработки данных](../extensions/data-processing/data-processing-extensions-overview.md) , см. в документации к [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [по](https://go.microsoft.com/fwlink/?linkid=121312).|Предоставляет подробные сведения о модулях обработки данных для опытных пользователей.|  

## <a name="see-also"></a>См. также  

- [Добавление данных в отчет &#40;построитель отчетов и службы SSRS&#41;](report-datasets-ssrs.md)
- [Конструкторы запросов (построитель отчетов)](../query-designers-report-builder.md)