---
title: Обзор интеграции (CLR) среды CLR | Документация Майкрософт
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- managed code [SQL Server]
- common language runtime [SQL Server], about CLR integration
- cross-language integration
- integrating CLR [SQL Server]
- .NET Framework [SQL Server], common language runtime
- code access security [CLR integration]
- managed code [SQL Server], CLR integration
ms.assetid: 7be9e644-36a2-48fc-9206-faf59fdff4d7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 69903654faf21a7649ec8b54a269e71a99d559c3
ms.sourcegitcommit: 36c5f28d9fc8d2ddd02deb237937c9968d971926
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354539"
---
# <a name="common-language-runtime-integration"></a>Интеграция среды CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и [Azure базы данных SQL управляемого экземпляра](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index) позволяют реализовать некоторые функции, с помощью языков .net с помощью собственного интеграция среды CLR (CLR) как модули на сервере SQL Server (процедуры, функции и триггеры). Среда CLR предоставляет управляемому коду такие услуги, как межъязыковая интеграция, управление доступом для кода, управление временем существования объекта, а также поддержку отладки и профилирования. Для пользователей и разработчиков [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] интеграция со средой CLR означает, что теперь можно писать хранимые процедуры, триггеры, определяемые пользователем типы и функции (скалярные и возвращающие табличное значение), а также определяемые пользователем агрегатные функции на любом языке среды .NET, включая [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic и [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] включает в себя предварительно установленную платформу .NET Framework (версия 4).  

> [!WARNING]
>  Среда CLR использует управление доступом для кода (CAS) в .NET Framework, которое больше не поддерживается в качестве границы безопасности. Сборки среды CLR, созданные с помощью `PERMISSION_SET = SAFE`, могут получать доступ к внешним системным ресурсам, вызывать неуправляемый код и получать права системного администратора. Начиная с [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)], появился параметр `sp_configure`, называемый `clr strict security`, для повышения безопасности сборок среды CLR. `clr strict security` включен по умолчанию и рассматривает сборки `SAFE` и `EXTERNAL_ACCESS`, как если бы они были помечены `UNSAFE`. Параметр `clr strict security` можно отключить для обеспечения обратной совместимости, но это делать не рекомендуется. Корпорация Майкрософт рекомендует подписывать все сборки с помощью сертификата или асимметричного ключа с соответствующим именем входа, которому предоставлено разрешение `UNSAFE ASSEMBLY` в базе данных master. Дополнительные сведения см. в статье о параметре [clr strict security](../../database-engine/configure-windows/clr-strict-security.md). Администраторы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] также могут добавлять сборки в список сборок, которым должно доверять ядро СУБД. Дополнительные сведения см. в разделе [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md).

## <a name="when-to-use-clr-modules"></a>Когда следует использовать модули среды CLR?

Интеграция со средой CLR позволяет реализовать сложные функции, доступные в .net Framework, такие как регулярные выражения, код для доступа к внешним ресурсам (серверы, веб-служб, баз данных), пользовательское шифрование, и т.д. Ниже приведены некоторые из преимуществ использования интеграции со средой CLR на стороне сервера.
  
-   **Улучшенная модель программирования.** Языки платформы .NET Framework во многих отношениях богаче языка Transact-SQL. Они предлагают конструкции и возможности, ранее не доступные разработчикам программ для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Разработчики могут также использовать всю мощь библиотеки платформы .NET Framework (.NET Framework Library), предоставляющей обширный набор классов, которые позволяют быстро и эффективно решать возникающие при разработке проблемы.   
  
-   **Улучшенная надежность и безопасность.** Управляемый код выполняется в среде CLR, размещаемой в компоненте Database Engine. В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] таким образом обеспечивается более безопасная и надежная альтернатива расширенным хранимым процедурам, доступным в предыдущих версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Возможность определять типы данных и агрегатные функции.** Определяемые пользователем типы данных и статистические функции — два новых вида объектов в базе данных, расширяющие возможности запросов и хранения данных СУБД [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Упрощение процесса разработки в результате стандартизации среды.** Разработка базы данных интегрирована в будущие версии среды разработки [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio .NET. Для разработки и отладки объектов и скриптов баз данных разработчики используют те же инструментальные средства, что и для разработки компонентов и служб платформы .NET Framework клиентского и среднего уровня.  
  
-   **Возможность повышения производительности и масштабируемости.** Во многих случаях средства компиляции и модели выполнения платформы .NET Framework предоставляют выигрыш в производительности по сравнению с Transact-SQL.  
  
 В следующей таблице перечислены подразделы этого раздела.  
  
 [Общие сведения об интеграции со средой CLR](../../relational-databases/clr-integration/clr-integration-overview.md)  
 Описание видов объектов, которые можно построить с помощью интеграции со средой CLR, и обзор требований к построению объектов баз данных с помощью интеграции со средой CLR.  
  
 [Новые возможности в интеграции со средой CLR](../../relational-databases/clr-integration/clr-integration-what-s-new.md)  
 Описывает новые возможности в данном выпуске.  
  
 [Архитектура интеграции со средой CLR](https://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)  
 Описание целей разработки интеграции со средой CLR.  
  
 [Включение интеграции со средой CLR](../../relational-databases/clr-integration/clr-integration-enabling.md)  
 Описание включения интеграции со средой CLR.  
  
## <a name="see-also"></a>См. также  
 [Установка .NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx) ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] только)   
 [Производительность интеграции со средой CLR](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  
