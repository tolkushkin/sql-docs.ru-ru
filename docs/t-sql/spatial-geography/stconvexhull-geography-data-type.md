---
title: STConvexHull (тип данных geography) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: c823f686909be54890b3c1686da615233c3e9da2
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937126"
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (тип данных geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Возвращает объект, представляющий выпуклую оболочку экземпляра **geography**.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
.STConvexHull ( )  
```  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 Тип возвращаемых данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Тип возвращаемого значения CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Возвращает объект `FullGlobe` для экземпляра **geography**, угол конверта которого больше 90 градусов.  
  
 Возвращает пустую коллекцию **geography** для пустого экземпляра **geography**.  
  
 Возвращает значение **null** для неинициализированного экземпляра **geography**.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. Использование функции STConvexHull() в неинициализированном экземпляре географического объекта  
 В приведенном ниже примере используется `STConvexHull()` для неинициализированного экземпляра **geography**.  
  
```
 DECLARE @g geography;  
 SELECT @g.STConvexHull();
 ```  
  
### <a name="b-using-stconvexhull-on-an-empty-geography-instance"></a>Б. Использование функции STConvexHull() в пустом экземпляре географического объекта  
 В следующем примере используется `STConvexHull()` в пустом экземпляре `Polygon`.  
  
```
 DECLARE @g geography = 'POLYGON EMPTY';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
### <a name="c-finding-the-convex-hull-of-a-non-convex-polygon-instance"></a>В. Обнаружение выпуклой оболочки невыпуклого экземпляра объекта Polygon  
 В следующем примере метод `STConvexHull()` используется для поиска выпуклой оболочки невыпуклого экземпляра `Polygon`.  
  
```  
 DECLARE @g geography;  
 SET @g = geography::Parse('POLYGON((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
 SELECT @g.STConvexHull().ToString();  
```  
  
### <a name="d-finding-the-convex-hull-on-a-geography-instance-with-an-envelope-angle-larger-than-90-degrees"></a>Г. Обнаружение выпуклой оболочки экземпляра географического объекта с углом пакета больше 90 градусов  
 В приведенном ниже примере `STConvexHull()` используется для экземпляра **geography**, угол конверта которого больше 90 градусов.  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  
