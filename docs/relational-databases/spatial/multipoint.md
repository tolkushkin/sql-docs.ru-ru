---
title: MultiPoint | Документация Майкрософт
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
author: MladjoA
ms.author: mlandzic
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5eaa5cd9458e6ec5d7f16030c72e64a961a775ec
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936416"
---
# <a name="multipoint"></a>MultiPoint
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Экземпляр **MultiPoint** представляет собой коллекцию точек. Граница у экземпляра **MultiPoint** отсутствует.  
  
## <a name="examples"></a>Примеры  

### <a name="example-a"></a>Пример А.
В следующем примере создается экземпляр `geometry MultiPoint` со значением SRID, равным 23, и двумя точками, с координатами (2, 3) и (7, 8), и значением Z, равным 9,5.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
### <a name="example-b"></a>Пример Б. 
Следующий пример выражает экземпляр `MultiPoint` с помощью `STMPointFromText()`.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
### <a name="example-c"></a>Пример В.
В следующем примере метод `STGeometryN()` используется с целью получения описания первой точки коллекции.  
  
```sql  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>См. также:  
 [Точка](../../relational-databases/spatial/point.md)   
 [Пространственные данные (SQL Server)](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
