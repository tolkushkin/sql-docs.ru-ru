---
title: Выбор источника данных (мастер импорта и экспорта SQL Server) | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b6e399cf6c145f36febd9b32ae7a84c54741bb43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62893599"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Выбор источника данных (мастер импорта и экспорта SQL Server)
  Используйте страницу **Выбор источника данных** , чтобы указать источник данных, который нужно копировать.  
  
 Дополнительные сведения о работе этого мастера см. в разделе [Мастер импорта и экспорта SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Дополнительные сведения о параметрах запуска этого мастера и о разрешениях, необходимых для успешного запуска мастера, см. в разделе [запустить мастер экспорта и импорта SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Мастера импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предназначен для копирования данных из исходного расположения в целевое. Этот мастер может также создать целевую базу данных и целевые таблицы. Однако если нужно скопировать несколько баз данных, таблиц или других объектов базы данных, следует использовать мастер копирования баз данных. Дополнительные сведения см. в статье [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Параметры  
 **Источник данных**  
 Выберите поставщик данных, который соответствует формату хранения данных источника. Для источника данных может существовать несколько поставщиков. Например, в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может использоваться собственный клиент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , поставщик данных платформы .NET Framework для SQL Server или поставщик OLE DB для SQL Server (Майкрософт).  
  
 Свойство **Источник данных** может иметь разное число параметров в зависимости от того, какие поставщики данных установлены на компьютере. В следующих страницах перечислены параметры некоторых часто используемых назначений. В случае использования других поставщиков обращайтесь к поставляемой с ними документации.  
  
## <a name="dynamic-options"></a>Динамические параметры  
 В следующих разделах описаны параметры, доступные для нескольких источников данных. Здесь перечислены не все источники данных из раскрывающегося списка «Источник данных».  
  
### <a name="data-source--sql-server-native-client-and-microsoft-ole-db-provider-for-sql-server"></a>Источник данных = собственный клиент SQL Server и поставщик OLE DB для SQL Server (Майкрософт)  
 **Имя сервера**  
 Введите имя сервера, содержащего данные, или выберите сервер из списка.  
  
 **Использовать проверку подлинности Windows**  
 Укажите, должен ли пакет использовать проверку подлинности [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows для доступа к базе данных. Для лучшей защиты рекомендуется использовать проверку подлинности Windows.  
  
 **Использовать проверку подлинности SQL Server**  
 Укажите, должен ли пакет использовать проверку подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для доступа к базе данных. Если используется проверка подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , необходимо ввести имя пользователя и пароль.  
  
 **Имя пользователя**  
 Укажите имя пользователя для подключения к базе данных, если используется проверка подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Пароль**  
 Укажите пароль для подключения к базе данных, если используется проверка подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **База данных**  
 Выберите базу данных из списка баз данных на указанном экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Обновить**  
 Нажатие кнопки **Обновить** восстанавливает список доступных баз данных.  
  
### <a name="data-source--net-framework-data-provider-for-sql-server"></a>Источник данных = поставщик данных .NET Framework для SQL Server  
 На этой странице представлен алфавитный список параметров поставщика данных [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Важнейшие параметры перечислены в следующей таблице.  
  
 **Источник данных**  
 Введите имя сервера, содержащего данные, или выберите сервер из списка.  
  
 **Исходный каталог**  
 Введите имя базы данных-источника.  
  
 **Встроенные функции безопасности**  
 Выберите `True`, чтобы использовать встроенную проверку подлинности Windows (рекомендуется), или `False` для соединения с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. При выборе `False` необходимо ввести идентификатор пользователя и пароль. Значение по умолчанию — `False`.  
  
 **Идентификатор пользователя**  
 Укажите имя пользователя для подключения к базе данных, если используется проверка подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Пароль**  
 Укажите пароль для подключения к базе данных, если используется проверка подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Другие перечисленные ниже параметры при выборе этого поставщика необязательно указывать для успешного подключения к базе данных-источнику [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Описание этих дополнительных параметров см. в документации по поставщику данных [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в пакете средств разработки программного обеспечения [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
### <a name="data-source--microsoft-excel"></a>Источник данных = Microsoft Excel  
  
> [!NOTE]  
>  Выберите **Microsoft Excel** только в случае, если необходимо соединиться с источником данных, использующим Excel 2003 или более раннюю версию. Чтобы подключиться к источнику данных, использующим Excel 2007, выберите **поставщик Microsoft Office 12.0 Access базы данных ядра OLE DB**, нажмите кнопку **свойства**, а затем на **все** вкладке **Свойства канала передачи данных** диалогового окна введите `Excel 12.0` как значение для **расширенные свойства**.  
  
 **Путь к файлу Excel**  
 Укажите путь и имя файла для рабочего листа, с которого импортируются данные. Например **C:\MyData.xls, \\\Sales\Database\Northwind.xls**. или нажмите **Обзор**.  
  
 **Обзор**  
 Выберите электронную таблицу с помощью диалогового окна **Открыть**.  
  
 **Версия Excel**  
 Выберите версию Excel, в формате которой хранятся исходные данные.  
  
> [!NOTE]  
>  Если данные импортируются из источника [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] , мастер использует компонент служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] «Источник Excel». Сведения о рекомендуемом использовании и известных проблемах см. в разделе [Excel Source](../data-flow/excel-source.md).  
  
### <a name="data-source--microsoft-access"></a>Источник данных = Microsoft Access  
  
> [!NOTE]  
>  Выберите **Microsoft Access** только в случае, если необходимо соединиться с источником данных, использующим Access 2003 или более раннюю версию. Чтобы соединиться с базой данных, использующей Access 2007, выберите **Поставщик OLE DB для ядра СУБД Microsoft Office 12.0 Access** .  
  
 **Имя файла**  
 Укажите путь и имя файла базы данных, их которого импортируются данные. Например, **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**. или нажмите **Обзор**.  
  
 **Обзор**  
 Выберите файл базы данных с помощью диалогового окна **Открыть**.  
  
 **Имя пользователя**  
 Если информационный файл рабочей группы связан с базой данных, укажите допустимое имя пользователя для подключения к базе данных.  
  
 **Пароль**  
 Если информационный файл рабочей группы связан с базой данных, укажите пароль пользователя для подключения к базе данных. Однако если база данных защищена одним и тем же паролем для всех пользователей, его значение необходимо указать в диалоговом окне **Свойства связи данных** , открывающемся при нажатии кнопки **Дополнительно**.  
  
 **Дополнительно**  
 Дополнительные параметры, например пароль базы данных или нестандартный информационный файл рабочей группы, можно указать в диалоговом окне **Свойства связи данных** . Дополнительные сведения о свойствах поставщика OLE DB см. в разделе «Доступ к данным» (Data Access) [библиотеки MSDN по адресу](https://go.microsoft.com/fwlink/?linkid=62553).  
  
### <a name="data-source--flat-file-source"></a>Источник данных = «Неструктурированный файл»  
 См. следующие разделы для получения сведений о параметрах исходного неструктурированного файла.  
  
 [Редактор диспетчера подключений к неструктурированным файлам (страница "Общие")](../general-page-of-integration-services-designers-options.md)  
  
 [Редактор диспетчера подключений к неструктурированным файлам (страница "Столбцы")](../flat-file-connection-manager-editor-columns-page.md)  
  
 [Редактор диспетчера подключений к неструктурированным файлам (страница "Дополнительно")](../flat-file-connection-manager-editor-advanced-page.md)  
  
 [Редактор диспетчера подключений с неструктурированными файлами (страница "Предварительный просмотр")](../flat-file-connection-manager-editor-preview-page.md)  
  
  
