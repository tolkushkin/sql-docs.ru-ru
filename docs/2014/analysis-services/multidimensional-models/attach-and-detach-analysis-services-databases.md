---
title: Присоединение и отсоединение баз данных служб Analysis Services | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssms.detachdatabase.f1
- sql12.asvs.ssms.attachdatabase.f1
- sql12.asvs.ssmsimbi.AttachDatabase.f1
- sql12.asvs.ssmsimbi.DetachDatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4447f58baaa5ea88a48c67a9a32fcda77681d8d4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077487"
---
# <a name="attach-and-detach-analysis-services-databases"></a>Подключение и отключение баз данных служб Analysis Services
  Часто администратору базы данных (dba) служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] необходимо на некоторое время перевести базу данных в режим "вне сети", а затем перевести ее в режим "в сети" на том же или на другом экземпляре сервера. Такие ситуации часто обусловлены потребностями предприятия, например необходимостью переместить базу данных на другой диск для повышения производительности, освободить место для увеличения размера базы данных или при обновлении какого-либо продукта. Для всех этих и других случаях `Attach` и `Detach` команды включают [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] переводить базу данных перевести в автономный режим и его обратно через Интернет с минимальными усилиями.  
  
## <a name="attach-and-detach-commands"></a>Команды Attach и Detach  
 Команда `Attach` позволяет перевести базу данных из режима «вне сети» в режим «в сети». База данных может быть присоединена как к исходному, так и к любому другому экземпляру сервера. При присоединении базы данных пользователь может указать для нее значение свойства **ReadWriteMode** . Команда `Detach` позволяет перевести базу данных на сервере в режим «вне сети».  
  
## <a name="attach-and-detach-usage"></a>Использование команд Attach и Detach  
 Команда `Attach` позволяет перевести в режим «в сети» существующую структуру базы данных. Если база данных присоединена в режиме `ReadWrite`, она может быть присоединена к экземпляру сервера только один раз. Если же база данных присоединена в режиме `ReadOnly`, она может быть присоединена к нескольким экземплярам сервера. Это, однако, не означает, что база данных может быть присоединена к одному экземпляру сервера более одного раза. Если попытаться сделать это (даже после копирования данных в другую папку), будет выдана ошибка.  
  
> [!IMPORTANT]  
>  Если для отсоединения базы данных потребовался пароль, для ее присоединения необходим тот же пароль.  
  
 Команда `Detach` позволяет перевести в режим «вне сети» существующую структуру базы данных. При отсоединении базы данных можно указать пароль для защиты конфиденциальных метаданных.  
  
> [!IMPORTANT]  
>  Чтобы обеспечить защиту содержимого файлов данных, необходимо защитить папку, вложенные папки и файлы данных с помощью списков управления доступом.  
  
 При отсоединении базы данных сервер выполняет следующие шаги.  
  
|Отсоединение базы данных в режиме чтения и записи|Отсоединение базы данных в режиме только для чтения|  
|--------------------------------------|-------------------------------------|  
|1. Сервер выполняет запрос блокировки CommitExclusive для базы данных.<br />2. Сервер ожидает, пока все входящие транзакции завершатся фиксацией или откатом.<br />3. Сервер формирует все метаданные, необходимые для отключения базы данных.<br />4. База данных помечается как удаленная.<br />5. Сервер фиксирует транзакцию.|1. База данных помечается как удаленная.<br />2. Сервер фиксирует транзакцию.<br /><br /> <br /><br /> Примечание. Нельзя сменить пароль для базы данных только для чтения. Если указать пароль для присоединяемой базы данных, уже защищенной паролем, возникнет ошибка.|  
  
 Команды `Attach` и `Detach` должны выполняться в пределах одной операции. Они не могут сочетаться в одной транзакции с другими операциями. Кроме того `Attach` и `Detach` команды являются атомарными транзакционными командами. Это означает, что только вся операция целиком может завершиться либо успешно, либо неуспешно. База данных не может остаться в незавершенном состоянии.  
  
> [!IMPORTANT]  
>  Чтобы выполнить команду `Detach`, необходимы права администратора сервера или базы данных.  
  
> [!IMPORTANT]  
>  Чтобы выполнить команду `Attach`, необходимы права администратора сервера.  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Перемещение базы данных служб Analysis Services](move-an-analysis-services-database.md)   
 [Режимы ReadWriteModes базы данных](database-readwritemodes.md)   
 [Переключение базы данных служб Analysis Services между режимами ReadOnly и ReadWrite](switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Элемент Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Элемент Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  
