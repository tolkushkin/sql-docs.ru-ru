---
title: Шаг 3. Добавление и настройка диспетчера подключений OLE DB | Документация Майкрософт
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e55427c2249a93d2a97bbc13b7385dd56fac5d01
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723503"
---
# <a name="lesson-1-3-add-and-configure-an-ole-db-connection-manager"></a>Занятие 1-3. Добавление и настройка диспетчера подключений OLE DB

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



После добавления диспетчера подключений к неструктурированным файлам с целью подключения к источнику данных необходимо добавить диспетчер подключений OLE DB для соединения с назначением. Диспетчер соединений OLE DB позволяет пакету получать данные из любого источника данных, совместимого с OLE DB, а также загружать данные в такой источник данных. Используя диспетчер подключений OLE DB, можно указать для соединения сервер, метод проверки подлинности и базу данных по умолчанию.  
  
В этой задаче будет создан диспетчер подключений OLE DB, использующий проверку подлинности Windows для подключения к локальному экземпляру **AdventureWorksDW2012**. На этот диспетчер подключений OLE DB также станут ссылаться другие компоненты, которые будут созданы позже в ходе работы с этим учебником, такие как преобразование "Уточняющий запрос" и назначение OLE DB.  
  
## <a name="add-and-configure-an-ole-db-connection-manager"></a>Добавление и настройка диспетчера подключений OLE DB

1. В области **Обозреватель решений** щелкните правой кнопкой мыши папку **Диспетчеры подключений** и выберите команду **Создать диспетчер подключений**.

1. В диалоговом окне **Добавление диспетчера соединений со службами SSIS** выберите **OLEDB**, а затем **Добавить**.
    
2. В диалоговом окне **Настройка диспетчера соединений OLE DB** нажмите кнопку **Создать**.  
  
3. Введите **localhost**в поле **Имя сервера**.  
  
    Если в качестве имени сервера указано значение localhost, диспетчер соединений соединяется с экземпляром [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , расположенном по умолчанию на локальном компьютере. Чтобы использовать удаленный экземпляр [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], замените localhost именем сервера, с которым нужно соединиться.  
  
4. Убедитесь, что в группе **Вход на сервер** выбран вариант **Использовать проверку подлинности Windows** .  
  
5. В группе **Соединение с базой данных** в окне **Выберите или введите имя базы данных** введите или выберите имя **AdventureWorksDW2012**.  
  
6. Нажмите **Проверить соединение**, чтобы убедиться в том, что параметры соединения указаны правильно.  
  
7. Нажмите кнопку **ОК**.  
  
8. Нажмите кнопку **ОК**.  
  
9. Убедитесь в том, что в области **Диспетчеры подключений** выбрано **localhost.AdventureWorksDW2012**.  
  

## <a name="go-to-next-task"></a>Перейти к следующему шагу
[Шаг 4. Добавление задачи потока данных к пакету](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>См. также раздел  
[Диспетчер соединений OLE DB](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
