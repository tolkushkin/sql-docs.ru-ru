---
title: Правильный Affinity Mask и Affinity входов и выходов Mask перекрытие | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3139c864805c7df9220afc9b81d2a242775f4fa7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856697"
---
# <a name="correct-affinity-mask-and-affinity-input-output-mask-overlap"></a>Правильный Affinity Mask и перекрытие маска схожести ввода-вывода
  Это правило проверяет, имеет ли экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] один или несколько процессоров, назначенных для использования как с параметром «affinity mask», так и с параметром «affinity I/O mask». На многопроцессорном компьютере параметры «affinity mask» и «affinity I/O mask» используются для определения процессоров, работающих с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Если для ЦП включены оба параметра, то это может привести к снижению производительности, поскольку вызовет перегрузку процессора.  
  
## <a name="best-practices-recommendations"></a>Рекомендации  
 Необходимо указывать оба параметра, «affinity mask» и «affinity I/O mask», но включать каждый ЦП только для одного параметра.  
  
 Не допускайте, чтобы один и тот же ЦП оказывался задействованным для обоих параметров. Биты, относящиеся к каждому ЦП, должны находиться в одном из следующих состояний:  
  
-   значение 0 для обоих параметров, «affinity mask» и «affinity I/O mask»;  
  
-   значение 0 для параметра «affinity mask» и 1 для параметра «affinity I/O mask»;  
  
-   значение 1 для параметра «affinity mask» и 0 для параметра «affinity I/O mask».  
  
## <a name="for-more-information"></a>Дополнительные сведения см. в разделе  
 [Параметр конфигурации сервера «affinity mask»](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)  
  
 [Параметр конфигурации сервера "affinity Input-Output mask"](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)  
  
 [Параметр конфигурации сервера «affinity64 mask»](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)  
  
 [Параметр конфигурации сервера "affinity64 Input-Output mask"](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)  
  
## <a name="see-also"></a>См. также  
 [Наблюдение с помощью управления на основе политик и принудительное применение рекомендаций с помощью управления на основе политик](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
