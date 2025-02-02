---
title: Диспетчер HTTP-соединений | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.httpconnection.server.f1
- sql13.dts.designer.httpconnection.proxy.f1
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6076c2e0cf877a150a2b66a5b9f4728e2cdd25c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728233"
---
# <a name="http-connection-manager"></a>диспетчер HTTP-соединений

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  HTTP-соединение позволяет пакету получить доступ к веб-серверу через протокол HTTP, чтобы передавать или принимать файлы. Задача «Веб-служба» из состава служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] использует этот диспетчер соединений.  
  
 При добавлении к пакету диспетчера HTTP-соединений [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] создает диспетчер соединений, который будет решать задачи HTTP-соединений во время работы, устанавливает свойства диспетчера соединений и добавляет его к коллекции **Connections** пакета.  
  
 Свойство диспетчера соединений **ConnectionManagerType** имеет значение **HTTP.**  
  
 Произвести настройку диспетчера HTTP-соединений можно следующими способами:  
  
-   Используйте учетные данные. Если диспетчер соединений использует учетные данные, то необходимо указать имя пользователя, пароль и домен.  
  
    > [!IMPORTANT]  
    >  Диспетчер HTTP-соединений поддерживает только анонимную проверку подлинности и обычную проверку подлинности. Проверка подлинности Windows не поддерживается.  
  
-   Используйте сертификат клиента. Если диспетчер соединений использует сертификат клиента, то среди его свойств есть имя сертификата.  
  
-   Введите время ожидания при подключении к серверу и размер фрагмента данных для записи данных.  
  
-   Используйте прокси-сервер. Прокси-сервер также может быть настроен для использования учетных данных, а также для обхода прокси-сервера и использования локальных адресов.  
  
## <a name="configuration-of-the-http-connection-manager"></a>Настройка диспетчера HTTP-соединений  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о программной настройке диспетчера соединений см. в разделе <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## <a name="http-connection-manager-editor-server-page"></a>Редактор диспетчера HTTP-сеансов (страница «Сервер»)
  Используйте вкладку **Сервер** диалогового окна **Редактор диспетчера HTTP-соединений** , чтобы настроить диспетчер HTTP-соединений, указав такие свойства, как URL-адрес и учетные данные безопасности. HTTP-соединение позволяет пакету получить доступ к веб-серверу через протокол HTTP, чтобы передавать или принимать файлы. После настройки диспетчера HTTP-соединений можно проверить соединение.  
  
> [!IMPORTANT]  
>  Диспетчер HTTP-соединений поддерживает только анонимную проверку подлинности и обычную проверку подлинности. Проверка подлинности Windows не поддерживается.  
  
 Дополнительные сведения о диспетчере HTTP-соединений см. в разделе [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Дополнительные сведения о распространенном сценарии использования диспетчера HTTP-соединений см. в разделе [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
### <a name="options"></a>Параметры  
 **URL-адрес сервера**  
 Введите URL-адрес для сервера.  
  
 Если планируется загрузить WSDL-файл с помощью кнопки **Загрузить язык WSDL** на странице **Общие** в окне **Редактор задачи «Веб-служба»** , введите URL-адрес для WSDL-файла. Этот URL-адрес заканчивается строкой «?wsdl».  
  
 **Использовать учетные данные**  
 Укажите, должен ли диспетчер HTTP-соединений использовать для проверки подлинности учетные данные безопасности пользователя.  
  
 **User name**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Пароль**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Домен**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Использовать сертификат клиента**  
 Укажите, должен ли диспетчер HTTP-соединений использовать для проверки подлинности сертификат клиента.  
  
 **Сертификат**  
 Выберите сертификат из списка, воспользовавшись диалоговым окном **Выбор сертификата** . Текстовое поле отображает имя, связанное с этим сертификатом.  
  
 **Время ожидания (сек)**  
 Укажите время ожидания при установке соединения с веб-сервером. По умолчанию для этого свойства устанавливается значение 30 секунд.  
  
 **Размер фрагмента данных (КБ)**  
 Укажите размер фрагмента для записи данных.  
  
 **Проверка соединения**  
 После настройки диспетчера HTTP-подключений проверьте работоспособность соединения, нажав кнопку **Проверить соединение**.  
  
## <a name="http-connection-manager-editor-proxy-page"></a>Редактор диспетчера HTTP-соединений (страница «Прокси-сервер»)
  Используйте вкладку **Прокси-сервер** диалогового окна **Редактор диспетчера HTTP-соединений** , чтобы настроить диспетчер HTTP-соединений для работы с прокси-сервером. HTTP-соединение позволяет пакету получить доступ к веб-серверу через протокол HTTP, чтобы передавать или принимать файлы.  
  
 Дополнительные сведения о диспетчере HTTP-соединений см. в разделе [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Дополнительные сведения о распространенном сценарии использования диспетчера HTTP-соединений см. в разделе [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
### <a name="options"></a>Параметры  
 **Использовать прокси-сервер**  
 Укажите, должен ли диспетчер HTTP-сеансов подключаться через прокси-сервер.  
  
 **URL-адрес прокси-сервера**  
 Введите URL-адрес прокси-сервера.  
  
 **Не использовать прокси-сервер при локальном подключении**  
 Укажите, должен ли диспетчер HTTP-соединений исключать прокси-сервер для локальных адресов.  
  
 **Использовать учетные данные**  
 Укажите, должен ли диспетчер HTTP-соединений использовать учетные данные для прокси-сервера.  
  
 **User name**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Пароль**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Домен**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Список адресов, не требующих прокси-сервера**  
 Список адресов, для которых прокси-сервер использоваться не должен.  
  
 **Добавить**  
 Введите адрес, для которого прокси-сервер использоваться не должен.  
  
 **Удалить**  
 Выберите адрес и затем удалите его, нажав кнопку **Удалить**.  
  
## <a name="see-also"></a>См. также:  
 [Задача «Веб-служба»](../../integration-services/control-flow/web-service-task.md)   
 [Соединения в службах Integration Services (SSIS)](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
