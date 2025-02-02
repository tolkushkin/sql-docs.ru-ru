---
title: Сериализация XML из объектов базы данных CLR | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- serialization
- XML serialization [CLR integration]
- common language runtime [SQL Server], XML serialization
- XmlSerializer class
ms.assetid: ac84339b-9384-4710-bebc-01607864a344
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 646d15dc3091323e6e7db2af757640122fb2f0fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779783"
---
# <a name="xml-serialization-from-clr-database-objects"></a>Сериализация XML из объектов базы данных CLR
  XML-сериализация используется в двух случаях:  
  
-   при вызове веб-служб из объектов среды CLR;  
  
-   для преобразования определяемого пользователем типа данных в XML.  
  
 Выполнение XML-сериализации с помощью вызова класса `XmlSerializer` обычно создает дополнительную сборку сериализации, перегружаемую в проект, содержащий исходную сборку.  Однако в целях безопасности в CLR эта перегрузка отключена. Таким образом для вызова веб-службы или преобразования определяемого пользователем ТИПА в XML внутри [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], следует создать сборку вручную с помощью инструмента **Sgen.exe** поставляемого вместе с .NET Framework, которое создает необходимые сборки сериализации. При вызове класса `XmlSerializer` следует создать сборку сериализации вручную, проделав следующие шаги:  
  
1.  Запустите **Sgen.exe** средство, которое входит в состав пакета SDK для .NET Framework для создания сборки, содержащей сериализаторы XML для исходной сборки.  
  
2.  Зарегистрируйте созданную сборку в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью инструкции `CREATE ASSEMBLY`.  
  
 Сведения об ошибках, возникающих при выполнении XML-сериализации см. в следующей статье технической поддержки Майкрософт: [«Не удается загрузить динамически созданную сборку сериализации»](https://support.microsoft.com/kb/913668).  
  
 Сведения о типах данных, не поддерживаемых классом XMLSerializer, см. в разделе о поддержке привязки к схеме XML на платформе .NET Framework в документации по платформе .NET Framework.  
  
## <a name="see-also"></a>См. также  
 [Доступ к данным из объектов базы данных CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
