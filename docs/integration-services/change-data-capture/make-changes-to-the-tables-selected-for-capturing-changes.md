---
title: Внесение изменений в выбранные для отслеживания изменений таблицы | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- makChanToTab
ms.assetid: a309f82a-c6ef-464d-a6ef-df555bfb609a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3ccaf1145b4d1c2b1f0c0c72adb67e6eecc4f1b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728686"
---
# <a name="make-changes-to-the-tables-selected-for-capturing-changes"></a>Внесение изменений в выбранные для отслеживания изменений таблицы

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  В этом диалоговом окне можно выбрать столбцы из выбранной таблицы, изменения данных в которых будут отслеживаться. Можно также изменить **Роль безопасности** и **Экземпляр отслеживания** .  
  
 В этом диалоговом окне можно выбрать столбцы из выбранной таблицы, изменения данных в которых будут отслеживаться.  
  
 **Изменение списка столбцов, включенных в экземпляр CDC**  
  
 Выполните одно из следующих действий (или оба).  
  
-   Установите флажки для всех дополнительных столбцов, которые необходимо включить.  
  
-   Снимите флажки для тех столбцов, которые необходимо исключить.  
  
 **Изменить тип данных для определенного столбца**.  
  
 Для столбца можно выбрать другой тип данных. В качестве нового типа данных можно выбрать только тип, совместимый с исходным.  
  
 Чтобы изменить тип данных, щелкните столбец **Тип данных** и выберите другой тип данных. Доступны только те типы данных, которые совместимы с исходным.  
  
> [!NOTE]  
>  Если нельзя выбрать ни одного типа данных, то раскрывающийся список будет недоступен.  
  
 **Изменение роли безопасности**  
  
 Введите новое имя или измените имя роли безопасности в поле **Роль безопасности** .  
  
 **Изменение или добавление экземпляра отслеживания**  
  
 В поле **Экземпляр отслеживания** введите имя экземпляра отслеживания.  
  
## <a name="see-also"></a>См. также:  
 [Как создать экземпляр изменения базы данных SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Выберите столбцы и таблицы Oracle](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
