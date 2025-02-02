---
title: Настройка параметров регулирования количества запросов подключений ODBC | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15a3efd678d7b1f055daebc31d71d4044ad19eef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198542"
---
# <a name="setting-odbc-connection-pooling-options"></a>Настройка параметров регулирования количества запросов подключений ODBC
Организация пулов соединений позволяет приложению использовать соединение из пула подключений, которые не обязательно должны быть повторно при каждом обращении. Можно использовать **организация пулов соединений** вкладке **администратор источников данных ODBC** диалоговое окно для включения и отключения наблюдения за производительностью. Дважды щелкните имя драйвера, чтобы задать период ожидания соединения.  
  
 В параметре реестра CPTimeout пул подключений включен на уровне драйвера. Включение этого выборочной драйвер позволяет системному администратору для включения пула подключений для драйверов, которые может поддерживать его. Он выполняется путем задания значения по умолчанию CPTimeout во время программы установки драйвера. Дважды щелкните имя драйвера, чтобы задать период ожидания соединения.  
  
 Дополнительные сведения о пуле соединений см. в разделе [организация пулов соединений ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Мониторинг производительности  
 Наблюдение за производительностью отслеживает производительность подключения, записывать широкий набор статистики. Эти статистические данные можно настроить разработчиком, включают следующие элементы:  
  
|Счетчик|Определение|  
|-------------|----------------|  
|Счетчик жестких соединения ODBC в секунду|Количество фактических подключений в секунду, которые выполняются на сервере. При первом среды выполняет интенсивной нагрузке, этот счетчик поднимутся очень быстро. Через несколько секунд она будет удалена до нуля. Это обычную ситуацию возникновения при работе организация пулов соединений. После установления соединения с сервером они будут использовать и помещен в пул для повторного использования.|  
|ODBC жестких отключить счетчик в секунду|Количество жестких разрывов соединений в секунду, выданных на сервер. Это фактических подключений к серверу, которые выпускаются при организации пула соединений. Это значение будет увеличен с нуля, при остановке всех клиентов в системе и подключения начинают истечения времени ожидания.|  
|Счетчик мягкое подключение ODBC в секунду|Число подключений удовлетворены пулом за секунду в другие слова, подключения, из пула, которые были переданы пользователей. Этот счетчик показывает, работает ли пул. В зависимости от нагрузки на сервере нередко это Показать соединения с небольшим потоком 40 – 60 в секунду.|  
|Счетчик Мягкое отключение ODBC в секунду|Количество разрывов соединений в секунду, выданный службой приложений. Когда приложение освобождает или отключается, соединения помещается обратно в пул.|  
|Текущий счетчик активного подключения ODBC|Число подключений в пуле, которые в настоящее время используются.|  
|Текущий счетчик свободное подключение ODBC|Текущее количество свободных подключений в пуле. Это динамических подключений, которые доступны для использования.|  
|Пулы активной|Количество активных пулов. Этот счетчик был добавлен в Windows 8, драйверов, которые управляют соединений в пуле соединений. Дополнительные сведения см. в разделе [Driver-Aware Connection Pooling](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Пулы, созданные|Количество пулов, active, включая активные и удален пулов. Этот счетчик был добавлен в Windows 8, драйверов, которые управляют соединений в пуле соединений. Дополнительные сведения см. в разделе [Driver-Aware Connection Pooling](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Необходимо указать собственные параметры мониторинга. Примеры для наблюдения за производительностью, должны быть добавлены с помощью этой версии ODBC.
