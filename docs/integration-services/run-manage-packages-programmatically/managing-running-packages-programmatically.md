---
title: Программное управление запуском пакетов | Документы Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 56e09491833cf96c83651b4e6a8038c1ad7a3bc6
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65719042"
---
# <a name="managing-running-packages-programmatically"></a>Программное управление запуском пакетов

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  При программном способе работы с пакетами служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] может потребоваться определить, какие пакеты уже запущены в настоящее время. Класс <xref:Microsoft.SqlServer.Dts.Runtime.Application> пространства имен <xref:Microsoft.SqlServer.Dts.Runtime> предоставляет необходимые для этого методы и классы.  
  
 Дополнительные сведения о мониторинге пакетов см. в разделе [Управление пакетами (службы SSIS)](../../integration-services/service/package-management-ssis-service.md).  
  
 Все методы, используемые в данном разделе, требуют наличия ссылки на сборку **Microsoft.SqlServer.ManagedDTS**. После добавления ссылки в новый проект импортируйте пространство имен <xref:Microsoft.SqlServer.Dts.Runtime> с помощью инструкции **using** или **Imports**.  
  
> [!IMPORTANT]  
>  Методы класса <xref:Microsoft.SqlServer.Dts.Runtime.Application> для работы с хранилищем пакетов служб SSIS поддерживают только имена «.», localhost и имя сервера для локального сервера. Нельзя использовать имя «(local)».  
  
## <a name="determining-which-packages-are-currently-running"></a>Определение, какие пакеты запущены в настоящее время  
 Чтобы определить, какие пакеты запущены в настоящее время на указанном сервере, вызовите метод <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A>. Этот метод возвращает коллекцию <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> объектов <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage>.  
  
> [!NOTE]  
>  Администраторы могут видеть все пакеты, выполняющиеся в настоящее время на компьютере, а другие пользователи видят только те пакеты, которые запустили они сами.  
  
## <a name="working-with-running-packages"></a>Работа с запущенными пакетами  
 Определив, какие пакеты запущены в настоящее время, можно получить сведения об этих пакетах и запросить остановку выполнения пакета.  
  
### <a name="getting-information-about-a-running-package"></a>Получение сведений о запущенном пакете  
 При просмотре коллекции <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> можно с помощью свойств объекта <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> найти пакет или получить дополнительные сведения о запущенных пакетах.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>Остановка выполнения пакета  
 Можно вызвать метод <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> объекта <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage>, чтобы остановить выполнение пакета. Между созданием запроса на остановку пакета и действительной остановкой пакета может пройти некоторое время.  
  
## <a name="see-also"></a>См. также:  
 [Управление пакетами (службы SSIS)](../../integration-services/service/package-management-ssis-service.md)   
 [Программное перечисление доступных пакетов](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
