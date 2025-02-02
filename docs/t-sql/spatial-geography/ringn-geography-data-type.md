---
title: RingN (тип данных geography) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RingN
- RingN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RingN method
ms.assetid: 30f47275-2727-4d22-bbec-c0c54bcb3ac2
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 14a29f7bfd5d55a634c5ab8be89a1f5e14dd2ccd
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936310"
---
# <a name="ringn-geography-data-type"></a>RingN (тип данных geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Возвращает указанное кольцо экземпляра **geography**: `1 ≤ n ≤ NumRings()`.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
.RingN (expression )  
```  
  
## <a name="arguments"></a>Аргументы  
 *expression*  
 Выражение типа **int** со значением от 1 до количества колец в экземпляре **polygon**.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Тип возвращаемых данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Тип возвращаемого значения CLR: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 Если значение индекса кольца **n** меньше 1, этот метод создает исключение **ArgumentOutOfRangeException.** Значение индекса кольца должно быть больше или равно 1 и меньше или равно значению, возвращенному методом `NumRings()`.  
  
## <a name="examples"></a>Примеры  
 В этом примере создается экземпляр `Polygon` с двумя кольцами и возвращается второе кольцо.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.RingN(2).ToString();  
```  
  
## <a name="see-also"></a>См. также  
 [Расширенные методы в экземплярах Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [NumRings (тип данных geography)](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
  
