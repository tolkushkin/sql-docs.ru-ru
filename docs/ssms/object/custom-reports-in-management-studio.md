---
title: Пользовательские отчеты в среде Management Studio | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.summary.new.custom.report.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 1ba3f758-f39b-4f5f-91ca-516cedc78979
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 966cd899d5a3d6019febd4ba939f360c16c9cd78
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095223"
---
# <a name="custom-reports-in-management-studio"></a>Пользовательские отчеты в среде Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Во многих узлах обозревателя объектов в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] отображается набор стандартных отчетов, созданных в [!INCLUDE[msCoName](../../includes/msconame_md.md)]. В этих отчетах сведены все обычно запрашиваемые данные о серверах. Начиная с версии [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] с пакетом обновления 2 (SP2), администраторы могут запускать настраиваемые отчеты, созданные в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] , из среды [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="implementation"></a>Реализация  
Пользовательские отчеты создаются на языке определения отчетов и хранятся в виде файлов определения отчетов (RDL). RDL определяет сведения о получении данных и макете отчета в формате XML. Язык RDL представляет собой открытую схему. Это дает разработчикам возможность расширять его, добавляя дополнительные атрибуты и элементы. Внутри отчета могут выполняться любые допустимые инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
Если обозреватель объектов не подключен к серверу, то пользовательские отчеты могут выполняться в контексте текущего узла, выбранного в обозревателе объектов, если отчеты ссылаются на его параметры отчета. Это позволяет отчету использовать текущий контекст (например, текущую базу данных) либо согласованный контекст (например, указать в пользовательском отчете выбранную базу данных в инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] ).  
  
## <a name="running-a-custom-report"></a>Запуск пользовательского отчета  
В среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] пользовательский отчет может быть запущен одним из следующих способов.  
  
-   Щелкните узел в обозревателе объектов правой кнопкой мыши, наведите указатель на **Отчеты** , а затем выберите пункт **Пользовательские отчеты**. В диалоговом окне **Открытие файла** найдите папку, содержащую RDL-файлы, и откройте нужный файл отчета.  
  
-   Щелкните узел в обозревателе объектов правой кнопкой мыши, наведите указатель на **Отчеты**, а затем выберите пункт **Пользовательские отчеты**. После этого выберите из списка последних использованных файлов нужный пользовательский отчет.  
  
## <a name="limitations"></a>Ограничения  
Во время работы с пользовательскими отчетами необходимо учитывать следующие ограничения.  
  
-   Чтобы предотвратить выполнение вредоносного кода, в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] запрещен автоматический запуск отчетов даже в том случае, если в файловой системе RDL-файлы сопоставлены со средой [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Отчеты не могут выполняться в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] программным способом. Кроме этого, невозможно их выполнение из командной строки среды [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
-   Пользовательские отчеты могут быть запущены в контексте, который не содержит ожидаемых значений. Например, отчет о репликации может быть запущен в контексте базы данных, которая не участвует в репликации, либо от имени пользователя, не имеющего разрешений для доступа к данным, необходимым для его формирования. Автор пользовательского отчета отвечает за правильность его структуры и контекста.  
  
-   Пользовательский отчет не может быть добавлен в список стандартных отчетов.  
  
-   Код, обрабатываемый в отчете, может оказать влияние на производительность сервера.  
  
-   Пользовательские отчеты не поддерживают вложенные отчеты.  
  
-   Текст команды для запросов внутри отчета не должен быть задан через выражение.  
  
-   Любой параметр, используемый в команде (запросе), может ссылаться только на один параметр отчета и не может использовать операторы выражений.  
  
-   Для команд отчетов (запросов) поддерживаются только следующие типы команд: «Только текст» и «Хранимая процедура».  
  
-   Среда обработки отчетов не предусматривает экранирование параметров запросов. Автор запроса должен проверить, что его запрос устойчив к атакам типа «Внедрение SQL».  
  
## <a name="managing-custom-reports"></a>Управление пользовательскими отчетами  
Пользователям, имеющим несколько пользовательских отчетов, рекомендуется упорядочить их по папкам файловой системы, задав соответствующие разрешения файловой системы NTFS.  
  
## <a name="permissions"></a>Разрешения  
Пользовательские отчеты работают с разрешениями текущего пользователя. Чтобы предотвратить изменение выполняемых отчетом запросов злоумышленниками, рекомендуется предоставлять ограниченные разрешения на папки, содержащие файлы отчетов.  
  
И пользователь, и применяемая службой [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] учетная запись должны иметь доступ на чтение системной папки с файлами отчетов.  
  
В отчет может быть внедрена любая допустимая команда [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] , однако она не будет выполнена.  
  
> [!CAUTION]  
> В отчет можно внедрить любую допустимую инструкцию [!INCLUDE[tsql](../../includes/tsql-md.md)] и она будет выполняться из этого отчета. Запуск отчета через учетную запись пользователя, обладающего расширенными правами доступа, делает возможным беспрепятственный запуск любых внедренных инструкций.  
  

  
## <a name="see-also"></a>См. также:  
[Добавление пользовательского отчета в среду Management Studio](../../ssms/object/add-a-custom-report-to-management-studio.md)  
[Отмена подавления предупреждений для пользовательских отчетов](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[Использование пользовательских отчетов для свойств узлов обозревателя объектов](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
  
