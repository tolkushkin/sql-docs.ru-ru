---
title: Remote Blob Store (RBS) и группы доступности AlwaysOn (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 32b2ab48c3406c9820ca264a1cef236a041a5924
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62814555"
---
# <a name="remote-blob-store-rbs-and-alwayson-availability-groups-sql-server"></a>Удаленное хранилище больших двоичных объектов (RBS) и группы доступности AlwaysOn (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] может обеспечить решение высокой доступности и аварийного восстановления для BLOB-объектов [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][удаленного хранилища больших двоичных объектов (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) . [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] защищает все метаданные и схемы удаленного хранилища больших двоичных объектов, хранящиеся в базе данных доступности, копируя их на вторичные реплики. Эта база данных содержимого SharePoint. В целом [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] хранит метаданные этого удаленного хранилища больших двоичных объектов независимо от больших двоичных объектов.  
  
 Защита BLOB-данных в RBD зависит от расположения больших двоичных объектов следующим образом.  
  
|Место хранения большого двоичного объекта|Могут ли группы доступности защищать данные этого большого двоичного объекта?|  
|-------------------------|-----------------------------------------------------|  
|Та же база данных, содержащая метаданные удаленного хранилища больших двоичных объектов (хранимая с помощью удаленного поставщика FILESTREAM хранилища RBS)|Да|  
|Другая база данных в том же экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (хранимая с помощью удаленного поставщика FILESTREAM хранилища RBS)|Да<br /><br /> Рекомендуется поместить эту базу данных в ту же группу доступности, что и базу данных, содержащую метаданные удаленного хранилища больших двоичных объектов.|  
|Другая база данных находится на другом экземпляре [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (хранимая с помощью удаленного поставщика FILESTREAM хранилища RBS)|Да<br /><br /> Эта база данных должна находиться в отдельной группе доступности.|  
|Стороннее хранилище больших двоичных объектов|Нет<br /><br /> Чтобы защитить эти BLOB-данные, воспользуйтесь механизмами высокого уровня доступности поставщика хранилища больших двоичных объектов.|  
  
##  <a name="Limitations"></a> Ограничения  
  
-   Программы обслуживания хранилища RBS должны быть нацелены на первичную реплику.  
  
##  <a name="Recommendations"></a> Рекомендации  
  
-   Используйте прослушивателя группы доступности. Дополнительные сведения см. в разделе [Прослушиватели групп доступности, возможность подключения клиентов и отработка отказа приложений (SQL Server)](../../listeners-client-connectivity-application-failover.md).  
  
##  <a name="RelatedContent"></a> См. также  
  
-   [Обслуживание удаленного хранилища больших двоичных объектов](https://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) (в электронной документации [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] )  
  
-   [Запуск программы обслуживания удаленного хранилища больших двоичных объектов](https://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) (блог)  
  
-   [Настройка удаленного хранилища больших двоичных объектов (RBS) с поставщиком FILESTREAM (SharePoint 2010)](https://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) (блог)  
  
## <a name="see-also"></a>См. также  
 [Подключение клиента AlwaysOn &#40;SQL Server&#41;](always-on-client-connectivity-sql-server.md)   
 [Удаленное хранилище больших двоичных объектов (RBS) (SQL Server)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  
