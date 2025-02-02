---
title: Назначение потоковой передачи данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 504c05882d1e7c690b8ddbd46c331073f63bbb7c
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727001"
---
# <a name="data-streaming-destination"></a>Назначение потоковой передачи данных

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


   **Назначение потоковой передачи данных** — это компонент назначения служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS), который позволяет **поставщику OLE DB для служб SSIS** использовать выходные данные пакета служб SSIS в качестве табличного результирующего набора. Можно создать связанный сервер, использующий поставщик OLE DB для служб SSIS, а затем выполнить SQL-запрос к связанному серверу, чтобы просмотреть данные, возвращаемые пакетом служб SSIS.  
  
 В приведенном ниже примере следующий запрос возвращает выходные данные из пакета Package.dtsx в проекте SSISPackagePublishing в папке Power BI каталога служб SSIS. Этот запрос использует связанный сервер с именем [Default Linked Server for Integration Services], который, в свою очередь, использует новый поставщик OLE DB для служб SSIS. Запрос содержит имя папки, имя проекта и имя пакета в каталоге служб SSIS. Поставщик OLE DB для служб SSIS запускает пакет, указанный в запросе, и возвращает табличный результирующий набор.  
  
```sql
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>Компоненты публикации веб-канала данных  
 Компоненты публикации веб-канала данных включают следующие компоненты: поставщик OLE DB для SSIS, назначение потоковой передачи данных и мастер публикации пакетов служб SSIS. С помощью мастера можно опубликовать пакет служб SSIS в экземпляре базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в виде представления SQL. Мастер помогает создать связанный сервер, использующий поставщик OLE DB для служб SSIS, и представление SQL, представляющее запрос на связанном сервере. Представление для результатов запроса запускается из пакета служб SSIS в качестве табличного набора данных.  
  
 Чтобы убедиться, что поставщик SSISOLEDB установлен, в SQL Server Management Studio разверните узлы **Объекты сервера**, **Связанные серверы**, **Поставщики**и проверьте, отображается ли поставщик **SSISOLEDB** . Дважды щелкните **SSISOLEDB**, установите параметр **Допускать в ходе процесса** , если он не установлен, а затем нажмите кнопку **ОК**.  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>Публикация пакета служб SSIS в качестве представления SQL  
 Ниже описаны действия по публикации пакета служб SSIS в качестве представления SQL.  
  
1.  Создайте пакет служб SSIS с помощью компонента **назначения потоковой передачи данных** и разверните пакет в каталоге служб SSIS.  
  
2.  Откройте **мастер публикации пакетов служб SSIS** , запустив файл ISDataFeedPublishingWizard.exe из расположения C:\Program Files\Microsoft SQL Server\130\DTS\Binn или мастер публикации веб-каналов данных в меню "Пуск".  
  
     Мастер создает связанный сервер с помощью поставщика OLE DB для служб SSIS (SSISOLEDB), а затем — представление SQL, состоящее из запроса на связанном сервере. Этот запрос содержит имя папки, имя проекта и имя пакета в каталоге служб SSIS.  
  
3.  Выполните представление SQL в SQL Server Management Studio и просмотрите результаты из пакета служб SSIS. Представление отправляет запрос поставщику OLE DB для служб SSIS через созданный связанный сервер. Поставщик OLE DB для служб SSIS выполняет пакет, указанный в запросе, и возвращает табличный результирующий набор.  
  
> [!IMPORTANT]  
>  Подробные инструкции см. в статье [Пошаговое руководство. Публикация пакета служб SSIS в представлении SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md).  

## <a name="configure-data-streaming-destination"></a>Настройка назначения потоковой передачи данных
  Настроить назначение потоковой передачи данных можно с помощью диалогового окна **Advanced Editor for Data Streaming Destination** (Расширенный редактор для назначения потоковой передачи данных). Чтобы открыть это диалоговое окно, дважды щелкните компонент или щелкните правой кнопкой мыши компонент в конструкторе потоков данных и выберите пункт **Изменить**.  
  
 Это диалоговое окно содержит три вкладки: **Свойства компонента**, **Входные столбцы**и **Свойства входов и выходов**.  
  
## <a name="component-properties-tab"></a>Вкладка "Свойства компонента"  
 Эта вкладка содержит следующие изменяемые поля:  
  
|Поле|Описание|  
|-----------|-----------------|  
|Имя|Имя компонента назначения потоковой передачи данных в пакете.|  
|ValidateExternalMetadata|Указывает, проверяется ли компонент во время разработки с использованием внешних источников данных. Если задано значение False, проверка с использованием внешних источников данных откладывается до времени выполнения.|  
|IDColumnName|В представлении, созданном в мастере публикации веб-каналов данных, есть дополнительный столбец идентификатора. Столбец идентификатора выступает в качестве EntityKey для выходных данных из потока данных, если данные используются в качестве канала OData в других приложениях.<br /><br /> Имя по умолчанию для этого столбца — _ID. Однако можно указать и другое имя.|  
  
## <a name="input-columns-tab"></a>Вкладка "Входные столбцы"  
 В верхней области этой вкладки отображаются все доступные входные столбцы. Выберите столбцы, которые требуется включить в выходные данные этого компонента. Выбранные столбцы отображаются в списке в нижней области. Имя выходного столбца можно изменить, введя новое имя в поле **Выходной псевдоним** в списке.  
  
## <a name="input-output-properties-tab"></a>Вкладка "Свойства входов и выходов"  
 Как и на вкладке "Входные столбцы", на этой вкладке можно изменить имена выходных столбцов. В древовидном представлении слева разверните узел **Data Streaming Destination Input** (Входные данные назначения потоковой передачи данных), а затем — **Входные столбцы**. Щелкните имя входного столбца и измените имя выходного столбца в области справа.
