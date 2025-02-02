---
title: Создание прокси веб-службы | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: b1217843-8d3d-49f3-a0d2-d35b0db5b2df
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: decf503b7da6fb4e3f3a3846a714b1062255f1a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62520385"
---
# <a name="creating-the-web-service-proxy"></a>Создание учетной записи-посредника веб-службы
  Клиент и веб-служба могут обмениваться данными с помощью сообщений SOAP, в который входные и выходные параметры инкапсулируются в формате XML. Класс-посредник сопоставляет параметры с XML-элементами, а затем отправляет сообщения SOAP по сети. Таким образом класс-посредник устраняет необходимость связываться с веб-службой на уровне SOAP и позволяет вызывать методы веб-службы в любой среде разработки, которая поддерживает протокол SOAP и прокси для веб-служб.  
  
 Добавить прокси-класс-в проект разработки, использующий платформу [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], можно двумя способами: с помощью средства WSDL в [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] и путем добавления веб-ссылки в среде [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. В следующих подразделах эта тема описана более подробно.  
  
## <a name="adding-the-proxy-using-the-wsdl-tool"></a>Добавление класса-посредника с помощью программы WSDL  
 Пакет SDK для [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] включает программу Wsdl.exe для работы с языком WSDL, которая позволяет создать прокси-класс веб-службы для использования в среде разработки [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Средство WSDL — это самый распространенный способ создания прокси-класса клиента на языках, поддерживающих веб-службы (в настоящее время это C# и [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]).  
  
 **Добавление прокси-класса в проект с помощью Wsdl.exe**  
  
1.  Запустите программу Wsdl.exe из командной строки, чтобы создать класс-посредник, указав (по крайней мере) URL-адрес для веб-службы сервера отчетов.  
  
     Например, следующая инструкция командной строки указывает URL-адрес для конечной точки управления в веб-службе сервера отчетов:  
  
    ```  
    wsdl /language:CS /n:"Microsoft.SqlServer.ReportingServices2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     Программа WSDL принимает ряд аргументов командной строки для создания прокси-класса. В предыдущем примере для использования в классе-посреднике указывается язык C# и рекомендуемое пространство имен (чтобы предотвратить конфликт имен в случае использования нескольких конечных точек веб-службы), а затем создается файл кода C# с именем ReportingService2010.cs. Если в примере указать язык [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], будет создан прокси-файл с именем ReportingService2010.vb. Этот файл создается в каталоге, из которого запущена команда.  
  
2.  Скомпилируйте класс-посредник в файл сборки (с расширением DLL) и создайте в проекте ссылку на сборку или добавьте класс в качестве элемента проекта.  
  
    > [!NOTE]  
    >  Если класс-посредник добавляется в проект вручную, необходимо добавить ссылку на библиотеку System.Web.Services.dll. Если прокси-класс добавляется с помощью веб-ссылки в Visual Studio .NET, то ссылка создается автоматически. Дополнительные сведения см. в подразделе «Добавление класса-посредника с помощью веб-ссылки в Visual Studio» далее в этом разделе.  
  
     После добавления класса-посредника в качестве элемента проекта в обозревателе решений появляется соответствующий файл.  
  
3.  Чтобы вызвать службу программным образом, создайте экземпляр класса-посредника.  
  
     В следующем примере кода показан синтаксис для создания в проекте экземпляра класса-посредника <xref:ReportService2010.ReportingService2010>.  
  
```vb  
Dim service As New ReportingService2010()  
```  
  
```csharp  
ReportingService2010 service = new ReportingService2010();  
  
```  
  
 Дополнительные сведения о программе Wsdl.exe, включая полный синтаксис, см. в разделе «Программа WSDL» документации по пакету SDK для [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Полное описание прокси для веб-служб см. в разделе «Создание прокси для веб-служб с поддержкой XML» документации по пакету SDK для [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="adding-the-proxy-using-a-web-reference-in-visual-studio"></a>Добавление учетной записи-посредника с помощью веб-ссылки в Visual Studio  
 Веб-ссылка позволяет проекту использовать одну или несколько веб-служб. Среда [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] позволяет пользователям добавлять в проекты ссылки на веб-службы с помощью нескольких простых действий.  
  
 **Добавление веб-ссылки в проект**  
  
1.  В **обозревателе решений** выберите проект, который будет использовать веб-службу.  
  
2.  В меню **Проект** выберите пункт **Добавить веб-ссылку**.  
  
     Откроется диалоговое окно **Добавление веб-ссылки**.  
  
3.  В поле **URL-адрес** введите полный путь к веб-службе сервера отчетов.  
  
     Упрощенный URL-адрес конечной точки выполнения отчета для веб-службы сервера отчетов может иметь следующий вид:  
  
    ```  
    http://<Server Name>/reportserver/reportexecution2005.asmx  
    ```  
  
     URL-адрес содержит домен, в котором развернута веб-служба сервера отчетов, имя папки, содержащей службу, и имя файла обнаружения для службы. Полное описание различных элементов URL-адреса см. в разделе [Доступ к API-интерфейсу SOAP](../accessing-the-soap-api.md).  
  
     Описание методов и свойств, предоставляемых веб-службой, появляется слева в панели браузера.  
  
    > [!NOTE]  
    >  Дополнительные сведения об элементах, связанных с веб-службой сервера отчетов, см. в разделе [Методы веб-службы сервера отчетов](../methods/report-server-web-service-methods.md).  
  
4.  Убедитесь, что проект может использовать веб-службу сервера отчетов, а также в наличии необходимых разрешений для доступа к серверу отчетов.  
  
5.  В поле **Имя веб-ссылки** введите имя, которое будет использоваться в коде для программного доступа к веб-службе сервера отчетов.  
  
6.  Нажмите кнопку **Добавить ссылку**, чтобы создать в приложении ссылку на веб-службу.  
  
     Новая ссылка появится в **обозревателе решений** в узле "Веб-ссылки" для активного проекта и будет иметь имя, указанное в поле **Имя веб-ссылки**.  
  
7.  В **обозревателе решений** разверните папку "Веб-ссылки", чтобы показать пространство имен для классов веб-ссылки, которые доступны элементам проекта.  
  
     После добавления веб-ссылки в проект соответствующие файлы отображаются в папке, входящей в папку "Веб-ссылки" **обозревателя решений**.  
  
 После добавления веб-ссылки используйте следующий код для создания экземпляра класса-посредника:  
  
```vb  
Dim rs As New myNamespace.myReferenceName.ReportExecutionService()  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
myNamespace.myReferenceName.ReportExecutionService rs = new myNamespace.myReferenceName.ReportExecutionService();  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
```  
  
 Также можно добавить директиву **using** (**Import** в [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) в ссылку на веб-службу сервера отчетов. Если применить эту директиву, нет необходимости полностью уточнять типы пространства имен. Для этого добавьте в файл следующий код:  
  
```vb  
Import myNamespace.myReferenceName  
```  
  
```csharp  
using myNamespace.myReferenceName;  
```  
  
## <a name="see-also"></a>См. также  
 [Веб-служба сервера отчетов](../report-server-web-service.md)   
 [Создание приложений с помощью веб-службы и .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Технический справочник (службы SSRS)](../../technical-reference-ssrs.md)  
  
  
