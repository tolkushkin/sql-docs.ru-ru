---
title: Матрица совместимости с | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d0fc510c7c45dab8fbc79cc8e74001ff1855b6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026567"
---
# <a name="compatibility-matrix"></a>Матрица совместимости
В следующей таблице описаны совместимости типов приложений и драйверов, заданные ранее в этом разделе.  
  
|Тип приложения<br /><br /> и версии|32-разрядная версия ODBC<br /><br /> 2.*x* драйвера|ODBC 3.*x*<br /><br /> Драйвер|Драйвер ODBC 3.8|Драйвер ISO и откройте группу совместимым|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16-разрядное приложение, любая версия|Совместимость|Совместимость|Совместимость|Совместимость|  
|Чистые 2. *x* приложения|Совместимость|Совместимость|Совместимость|Не совместимые [3]|  
|Чистые 2. *x* повторной компиляции приложения|Совместимость|Совместимость [1]|Совместимость [1]|Не совместимые [3]|  
|Чистые 2. *x* приложения Юникода|Совместимость|Совместимость [1]|Совместимость [1]|Не совместимые [3]|  
|Чистые Open Group и соответствует требованиям стандарта ISO приложения|Не совместимо|Совместимость [2]|Совместимость [2]|Совместимость [2]|  
|Чистые 3.0 приложения|Не совместимо|Совместимость|Совместимость|Не совместимые [4]|  
|Чистые 3,5 приложения|Не совместимо|Совместимость|Совместимость|Не совместимые [4]|  
|Чистые приложения 3,8 (или более поздней версии)|Не совместимые [5]|Не совместимые [5]|Совместимость|Не совместимые [4]|  
|Замененное приложение|Совместимость|Совместимость|Совместимость|Не совместимые [3]|  
  
 [1] приложение необходимо перекомпилировать с использованием заголовков ODBC 3.5 (или более поздней версии) с параметром ЮНИКОДА (если это приложение на основе Юникода) и значение аргумент ODBCVER 0x0250.  
  
 [2] приложение необходимо скомпилировать с помощью заголовков ODBC 3.5 (или более поздней версии) и связать с диспетчером драйверов ODBC. Его также необходимо установить флаг заголовка ODBC_STD.  
  
 [3] в этой конфигурации потенциально могут не работать, так как нет компонентов в ODBC 2. *x* не входящие в стандарты, такие как закладки.  
  
 [4] в этой конфигурации могут завершиться сбоем для работы, поскольку нет компонентов в ODBC 3 *.x* не входящие в стандарты, такие как закладки.  
  
 [5] Эта конфигурация может привести к сбою, так как функции ODBC 3.8, не входящие в 2.x или 3.x драйверы ODBC, такие как относящиеся к драйверу [типы данных C в ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Диспетчер драйверов совместимости  
 Приложения ODBC 3.0, должны работать со всеми версиями диспетчера драйверов должны выполните следующие действия при запуске.  
  
-   Выделите дескриптор среды.  
  
-   Значение атрибута среды SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3_80. Если диспетчер драйверов возвращает значение SQL_ERROR, диспетчер драйверов старше, чем 3.8. Сброс SQL_ATTR_ODBC_VERSION значение SQL_OV_ODBC3 или SQL_OV_ODBC2, соответствующим образом, в соответствии с диспетчера драйверов.  
  
-   Выделите дескриптор соединения.  
  
-   Установите подключение.  
  
-   Вызовите SQLGetInfo для SQL_DRIVER_ODBC_VER определить номер версии драйвера. Если драйвер является драйвером ODBC 3.8, можно использовать типы C специфические для драйвера. В противном случае не используйте типы данных C специфические для драйвера.  
  
 Обратите внимание на то, что перекомпилированным приложением ODBC 3.x можно использовать функций ODBC 3.8, отличных от драйвера C типы без указания SQL_OV_ODBC3_80 для SQL_ATTR_ODBC_VERSION. Это похоже на перекомпилированным приложением ODBC 2.x с помощью функций ODBC 3.x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>С помощью SQLCancelHandle в приложения совместимы с всех диспетчеров драйверов  
 Так как [функция SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) не поддерживается в диспетчерах драйверов, выпущенных до Windows 7, приложение не удается загрузить в более старых версиях Windows, если он вызывает **SQLCancelHandle** напрямую. Для работы со всеми версиями диспетчеров драйверов и использовать **SQLCancelHandle** в новых версиях Windows, приложение должно вызывать **SQLCancelHandle** косвенно с помощью **LoadLibrary** и **GetProcAddress.**  
  
## <a name="see-also"></a>См. также  
 [Новые возможности ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
