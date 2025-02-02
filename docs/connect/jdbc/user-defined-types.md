---
title: Определяемые пользователем типы | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 90d887e93ca2de0214f53f9a7383854183e492c3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782440"
---
# <a name="user-defined-types"></a>Определяемые пользователем типы

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Определяемые пользователем типы появились в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], чтобы дать разработчику возможность расширить серверную систему скалярных типов путем хранения объектов среды CLR в базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Определяемые пользователем типы могут содержать несколько элементов, и их поведение может отличаться от традиционных псевдонимов типов данных, которые состоят из одного системного типа данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ранее размер определяемых пользователем типов был ограничен 8 килобайтами. В [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] добавлена поддержка определяемых пользователем типов, размер которых превышает 64 килобайта. Начиная с версии 3.0 драйвер JDBC также поддерживает определяемые пользователем типы с размером более 64 килобайт при указании формата UserDefined.

Поведение определяемых пользователем типов с размером, не превышающим 8000 байт, не изменилось, но теперь поддерживаются более крупные, определяемые пользователем типы, для которых сообщается размер unlimited.

## <a name="see-also"></a>См. также:

[Основные сведения о типах данных драйвера JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
