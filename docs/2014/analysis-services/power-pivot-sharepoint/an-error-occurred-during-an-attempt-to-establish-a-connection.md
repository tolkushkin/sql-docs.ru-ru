---
title: 'При попытке установить соединение с внешним источником данных произошла ошибка. Следующие соединения не удалось обновить: Данные PowerPivot | Документация Майкрософт'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c09c8984e964b4bdfa93b0fcebae2e613d484892
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071944"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection-to-the-external-data-source-the-following-connections-failed-to-refresh-powerpivot-data"></a>При попытке установить соединение с внешним источником данных произошла ошибка. Следующие соединения не удалось обновить: данные PowerPivot
  Эта ошибка возникает во время запроса данных PowerPivot на сервере, где не установлен PowerPivot для SharePoint. Она также возникает в случае, если службы SQL Server Analysis Services (PowerPivot) остановлены, или при попытке просмотра данных PowerPivot предыдущей версии.  
  
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Применение|PowerPivot для SharePoint|  
|Номер версии продукта|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Причина|Ошибка подключения к данным.|  
|Текст сообщения|При попытке установить соединение с внешним источником данных произошла ошибка. Следующие соединения не удалось обновить: данные PowerPivot|  
  
## <a name="explanation"></a>Объяснение  
 Службы Excel возвращают эту ошибку во время запроса данных PowerPivot в книге Excel, которая опубликована на сайте SharePoint, при этом в среде SharePoint не установлен сервер PowerPivot для SharePoint, либо служба SQL Server Analysis Services (PowerPivot) остановлена.  
  
 Эта ошибка возникает при срезе или фильтрации данных PowerPivot, когда ядро запросов недоступно.  
  
## <a name="user-action"></a>Действие пользователя  
 Установите PowerPivot для SharePoint или переместите книгу PowerPivot в среду SharePoint, где установлен экземпляр PowerPivot для SharePoint. Дополнительные сведения см. в разделе [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 Если установлено программное обеспечение, убедитесь, что экземпляр служб SQL Server Analysis Services (PowerPivot) запущен. Установите флажок **Управление службами на сервере** в центре администрирования. Кроме того, проверьте консольное приложение «Службы» в разделе «Администрирование».  
  
 Для книг PowerPivot, созданных в версии PowerPivot для Excel SQL Server 2008 R2, необходимо установить поставщик OLE DB служб Analysis Services версии SQL Server 2008 R2. Эта ошибка возникает, если поставщик установлен, но файл Microsoft.AnalysisServices.ChannelTransport.dll не зарегистрирован. Дополнительные сведения о регистрации файла см. в статье [Установка поставщика OLE DB служб Analysis Services на серверах SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
## <a name="see-also"></a>См. также  
 [Подключение к данным использует проверку подлинности Windows, а учетные данные невозможно делегировать. Следующие соединения не удалось обновить: Данные PowerPivot](the-data-connection-user-could-not-be-delegated.md)  
  
  
