---
title: STRelate (тип данных geometry) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRelate (geometry Data Type)
- STRelate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRelate (geometry Data Type)
ms.assetid: 9dcb5f58-35ab-4bb3-86ee-2d29eefba6d3
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: bb4c4e589ef3f658cee65812e9263a68a3489d2a
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938310"
---
# <a name="strelate-geometry-data-type"></a>STRelate (тип данных geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Возвращает значение 1, если экземпляр **geometry** связан с другим экземпляром **geometry**, где связь определяется значением шаблона матрицы DE-9IM; в противном случае возвращается 0.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
.STRelate ( other_geometry, intersection_pattern_matrix )  
```  
  
## <a name="arguments"></a>Аргументы  
 *other_geometry*  
 Другой экземпляр **geometry** для сравнения с экземпляром, для которого вызван метод `STRelate()`.  
  
 *intersection_pattern_matrix*  
 Строка типа **nchar(9)** кодирует приемлемые значения для устройства шаблона матрицы DE-9IM между двумя экземплярами **geometry**.  
  
## <a name="remarks"></a>Remarks  
 Этот метод всегда возвращает значение NULL, если у экземпляров **geometry** не совпадают идентификаторы пространственных ссылок (SRID). Этот метод вызывает исключение **ArgumentException**, если формат матрицы неправильный.  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 Тип возвращаемых данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Тип возвращаемого значения CLR: **SqlBoolean**  
  
## <a name="examples"></a>Примеры  
 В приведенном ниже примере используется `STRelate()`, чтобы проверить отсутствие пространственного перекрытия двух экземпляров **geometry** с использованием явного шаблона DE-9IM.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(5 5)', 0);  
SELECT @g.STRelate(@h, 'FF*FF****');  
```  
  
## <a name="see-also"></a>См. также:  
 [Методы OGC в экземплярах Geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
