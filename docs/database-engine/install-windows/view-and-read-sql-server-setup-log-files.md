---
title: Просмотр и чтение файлов журналов программы установки SQL Server | Документы Майкрософт
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: eaa665f77bf549cbe956c2bf658585f12a8be0fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794693"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>Просмотр и чтение файлов журналов программы установки SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Программа установки SQL Server по умолчанию создает файлы журналов в папке с датой и меткой времени в **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log**, где *nnn* — это число, соответствующее устанавливаемой версии SQL. Формат папки журналов с меткой времени — ГГГГММДД_ччммсс. При запуске программы установки в автоматическом режиме журналы создаются по пути %temp%\sqlsetup*.log. Все файлы в папке журналов архивируются в файле Log\*.cab в соответствующей папке журналов.  

   | Файл           | Путь |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<имя_компьютера>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\ГГГГММДД_ччммсс |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\ГГГГММДД_ччммсс|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\ГГГГММДД_ччммсс\Datastore
   | **Файлы журнала MSI** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\ГГГГММДД_ччммсс\\\<имя>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\ГГГГММДД_ччммсс |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\ГГГГММДД_ччммсс |
   | **Для автоматической установки** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > Число *nnn* в пути соответствует устанавливаемой версии SQL. На приведенном выше рисунке установлена версия SQL 2017, поэтому в пути используется число 140. Для SQL 2016 использовалась бы папка с числом 130, а для SQL 2014 — с числом 120.
  
 Работа программы установки SQL Server состоит из трех основных этапов: 
  
1.  проверка глобальных правил: проверяются основные требования к системе;
2.  обновление компонентов: проверяется наличие обновлений для устанавливаемой версии;
3.  запрошенное пользователем действие: позволяет пользователю выбрать и настроить компоненты.
  

В результате этого процесса создается один сводный журнал, а также один подробный журнал для базовой установки SQL Server или два подробных журнала в случае установки обновления, например пакета обновления, одновременно с базовой установкой. 
  
Кроме того, имеются файлы хранилища данных, в которых содержится моментальный снимок состояния всех объектов конфигурации, отслеживаемых процессом установки; эти файлы могут пригодиться при диагностике ошибок конфигурации. Для каждого этапа выполнения создаются XML-файлы дампа, которые сохраняются во вложенной папке в папке журнала с меткой времени в хранилище данных. 

В следующих разделах описываются файлы журналов установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="summarytxt-file"></a>Файл Summary.txt. 
  
### <a name="overview"></a>Обзор  
 В этом файле отображаются компоненты [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , обнаруженные на этапе установки, среда операционной системы, значения параметров командной строки (если указаны) и общее состояние всех выполненных MSI/MSP.
  
 Журнал структурирован с использованием следующих разделов:
  
-   Общая сводка выполнения  
-   Свойства и конфигурация компьютера, на котором была запущена программа установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ранее установленного на компьютере  
-   Описание версии установки и свойства пакета установки
-   Входные параметры среды выполнения, указанные при установке  
-   Местоположение файла конфигурации  
-   Данные о результатах выполнения  
-   Глобальные правила  
-   Правила, связанные с определенным сценарием установки  
-   Правила, при выполнении которых произошла ошибка  
-   Местоположение файла отчета о выполнении правил


  >[!NOTE]
  > Обратите внимание на то, что при применении исправлений может быть несколько вложенных папок (по одной для каждого экземпляра, к которому применяются исправления, и еще одна для общих компонентов). Они содержат одинаковые наборы файлов (например, %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<ГГГГММДД_ЧЧММ>\MSSQLSERVER). 
  
### <a name="location"></a>Местоположение  
 Файл summary.txt находится в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 Чтобы найти ошибки в текстовом файле сводки, воспользуйтесь поиском с ключевыми словами «error» или «failed».
  
## <a name="summarymachinenameyyyymmddhhmmsstxt-file"></a>Файл Summary_\<ИмяКомпьютера>_ГГГГММДД_ЧЧММсс.txt
  
### <a name="overview"></a>Обзор  
 Базовый файл summary_engine схож с файлом справки и создается при выполнении основного рабочего процесса.
  
### <a name="location"></a>Местоположение  
 Файл Summary_\<ИмяКомпьютера>_ГГГГММДД_ЧЧММсс.txt находится в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.
  
  
## <a name="detailtxt-file"></a>Файл Detail.txt
  
### <a name="overview"></a>Обзор
 Detail.txt создается при выполнении рабочего процесса основных процедур, таких как установка или обновление, и обеспечивает сведения о выполнении. Журналы в файле создаются с учетом времени инициации всех действий, связанных с установкой. В текстовом файле указывается порядок выполнения действий и их зависимости.  
  
### <a name="location"></a>Местоположение  
 Файл detail.txt находится в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\Detail.txt.  
  
 При возникновении ошибки во время процесса установки исключение или ошибка регистрируются в конце этого файла. Чтобы найти ошибки в этом файле, сначала проверьте его конец, а затем воспользуйтесь поиском по файлу с ключевыми словами "ошибка" и "исключение".
    
## <a name="msi-log-files"></a>Файлы журнала MSI.
  
### <a name="overview"></a>Обзор  
 В файлах журнала MSI указаны сведения о установке пакетов. Они создаются MSIEXEC при установке определенных пакетов.  
  
 Типы файлов журналов MSI:
  
-   \<компонент>_\<архитектура>\_\<взаимодействие>.log   
-   \<компонент>_\<архитектура>\_\<язык>\_\<взаимодействие>.log   
-   \<компонент>_\<архитектура>\_\<взаимодействие>\_\<рабочий процесс>.log  
  
### <a name="location"></a>Местоположение  
 Файлы журналов MSI расположены в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\<имя\>.log.  
  
 В конце файла приведена сводка выполнения, в которой указываются общее состояние (успешное или ошибка) и свойства. Для поиска ошибок в файле MSI воспользуйтесь поиском по запросу "value 3" и просмотрите текст рядом с этой строкой.  
  
## <a name="configurationfileini-file"></a>Файл ConfigurationFile.ini
  
### <a name="overview"></a>Обзор  
 В файле конфигурации содержатся входные параметры, указанные при установке. Их можно использовать для повторной установки, что избавит от необходимости их ввода вручную. Однако пароли учетных записей, PID и некоторые параметры не сохраняются в файле конфигурации. Параметры могут либо быть добавлены к файлу или указаны с помощью командной строки или пользовательского интерфейса программы установки. Дополнительные сведения см. в разделе [Установка SQL Server 2016 с помощью файла конфигурации](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### <a name="location"></a>Местоположение  
 Файл ConfigurationFile.ini находится в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.  
  
## <a name="systemconfigurationcheckreporthtm-file"></a>Файл SystemConfigurationCheck_Report.htm
  
### <a name="overview"></a>Обзор  
 В отчете о проверке конфигурации системы содержится краткое описание всех выполняемых правил и состояния выполнения.
  
### <a name="location"></a>Местоположение  
Файл SystemConfigurationCheck_Report.htm находится в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## <a name="see-also"></a>См. также раздел  
 [Установка SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)
