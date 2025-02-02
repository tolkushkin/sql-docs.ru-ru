---
title: Редактор диспетчера HTTP-сеансов (страница «сервер») | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 197a2668beb60acf2473a1f53786d7b553e08cf6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058245"
---
# <a name="http-connection-manager-editor-server-page"></a>Редактор диспетчера HTTP-сеансов (страница «Сервер»)
  Используйте вкладку **Сервер** диалогового окна **Редактор диспетчера HTTP-соединений** , чтобы настроить диспетчер HTTP-соединений, указав такие свойства, как URL-адрес и учетные данные безопасности. HTTP-соединение позволяет пакету получить доступ к веб-серверу через протокол HTTP, чтобы передавать или принимать файлы. После настройки диспетчера HTTP-соединений можно проверить соединение.  
  
> [!IMPORTANT]  
>  Диспетчер HTTP-соединений поддерживает только анонимную проверку подлинности и обычную проверку подлинности. Проверка подлинности Windows не поддерживается.  
  
 Дополнительные сведения о диспетчере HTTP-соединений см. в разделе [HTTP Connection Manager](connection-manager/http-connection-manager.md). Дополнительные сведения о распространенном сценарии использования диспетчера HTTP-соединений см. в разделе [Web Service Task](control-flow/web-service-task.md).  
  
## <a name="options"></a>Параметры  
 **URL-адрес сервера**  
 Введите URL-адрес для сервера.  
  
 Если планируется загрузить WSDL-файл с помощью кнопки **Загрузить язык WSDL** на странице **Общие** в окне **Редактор задачи «Веб-служба»** , введите URL-адрес для WSDL-файла. Этот URL-адрес заканчивается строкой «?wsdl».  
  
 **Использовать учетные данные**  
 Укажите, должен ли диспетчер HTTP-соединений использовать для проверки подлинности учетные данные безопасности пользователя.  
  
 **Имя пользователя**  
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
  
## <a name="see-also"></a>См. также  
 [Справочник по сообщениям об ошибках служб Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Редактор диспетчера HTTP-сеансов (страница "Прокси-сервер")](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  
