---
title: Публикация выполнения хранимой процедуры в публикации транзакций (SQL Server Management Studio) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07bab8c30c138139dee50b349ac797e5c86fa5c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238727"
---
# <a name="publish-the-execution-of-a-stored-procedure-in-a-transactional-publication-sql-server-management-studio"></a>опубликовать выполнение хранимой процедуры в публикации транзакций (среда SQL Server Management Studio)
  В диалоговом окне **Свойства статьи — \<статья>** можно указать, что публикуется не только определение, но и выполнение хранимой процедуры. Это диалоговое окно доступно в мастере создания публикаций, а также в диалоговом окне **Свойства публикации — \<публикация>**. Дополнительные сведения об использовании мастера и доступе к этому диалоговому окну см. в статьях [Создание публикации](create-a-publication.md) и [Просмотр и изменение свойств публикации](view-and-modify-publication-properties.md).  
  
 Определение процедуры (инструкция CREATE PROCEDURE) реплицируется на подписчик при инициализации подписки. Когда процедура выполняется на издателе, репликация выполняет соответствующую процедуру на подписчике.  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>Публикация выполнения хранимой процедуры  
  
1.  Выберите хранимую процедуру на странице **Статьи** мастера создания публикаций или в диалоговом окне **Свойства публикации — \<публикация>**.  
  
2.  Щелкните **Свойства статьи**, а затем щелкните **Задать свойства выделенной хранимой процедуры**.  
  
3.  В диалоговом окне **Свойства статьи — \<статья>** укажите одно из следующих значений для параметра **Репликация**.  
  
    -   **Выполнение хранимой процедуры**  
  
    -   **Выполнение в сериализованной транзакции хранимой процедуры**  
  
         Это рекомендуемый параметр, поскольку он реплицирует выполнение процедуры только в случае ее выполнения в контексте сериализуемой транзакции. При выполнении хранимой процедуры вне сериализуемой транзакции изменения, вносимые в данные опубликованных таблиц, реплицируются как ряды инструкций языка обработки данных.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Если вы находитесь в диалоговом окне **Свойства публикации — \<публикация>**, нажмите кнопку **ОК**, чтобы сохранить изменения и закрыть диалоговое окно.  
  
## <a name="see-also"></a>См. также  
 [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
