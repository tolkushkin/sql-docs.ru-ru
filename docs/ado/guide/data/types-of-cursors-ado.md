---
title: Типы курсоров (ADO) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 717229c9645384477b89e67b569c15179e9f3bc5
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704907"
---
# <a name="types-of-cursors-ado"></a>Типы курсоров (ADO)
Как правило приложение должно использовать самый простой курсор, который предоставляет доступ, необходимые данные. Дополнительные курсора характеристик некоторые особенности (однопроходный, только для чтения, статический прокрутки, без буферизации) имеет цену - в клиентской памяти, сетевой нагрузки или производительности. Во многих случаях параметры курсора по умолчанию создаются более сложные курсора, чем действительно требуется приложению.  
  
 Выбор типа курсора зависит от того, в том, как приложение использует результирующий набор, а также на несколько аспектов, включая размер результирующего набора, процент часто используемых данных, чувствительность к изменения данных и производительности приложений требования.  
  
 Самое простое Выбор курсора зависит от того, нужно ли изменить или просто просмотреть данные:  
  
-   Если нужно прокручивать набор результатов, но не изменения данных, используйте [последовательного](../../../ado/guide/data/forward-only-cursors.md) или [статический](../../../ado/guide/data/static-cursors.md) курсора.  
  
-   Если у вас есть большой результирующий набор и вам необходимо выбрать несколько строк, используйте [keyset](../../../ado/guide/data/keyset-cursors.md) курсора.  
  
-   Если вы хотите синхронизировать результирующий набор с последних добавляет, изменяет и удаляет все одновременно работающие пользователи, используйте [динамическое](../../../ado/guide/data/dynamic-cursors.md) курсора.  
  
 Несмотря на то, что каждый тип курсора кажется distinct, имейте в виду, что эти типы курсоров не так много разных видов просто в результате перекрывающиеся характеристики и параметры.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Курсоры последовательного доступа](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [Статические курсоры](../../../ado/guide/data/static-cursors.md)  
  
-   [Курсоры ключевого набора](../../../ado/guide/data/keyset-cursors.md)  
  
-   [Динамические курсоры](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>См. также  
 [Однопроходные курсоры](../../../ado/guide/data/forward-only-cursors.md)   
 [Статические курсоры](../../../ado/guide/data/static-cursors.md)   
 [Управляемые набором ключей курсоры](../../../ado/guide/data/keyset-cursors.md)   
 [Динамические курсоры](../../../ado/guide/data/dynamic-cursors.md)
