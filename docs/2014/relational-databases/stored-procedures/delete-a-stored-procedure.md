---
title: Удаление хранимой процедуры | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- removing stored procedures
- stored procedures [SQL Server], deleting
- deleting stored procedures
ms.assetid: 232dbf4d-392a-406f-af3a-579518cd8e46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 78b78021f32faed097a4faf29ea139dd85f429e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63015663"
---
# <a name="delete-a-stored-procedure"></a>Удаление хранимой процедуры
    
##  <a name="Top"></a> В этом разделе описывается, как удалить хранимую процедуру [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] при помощи среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Перед началом:**  [Ограничения](#Restrictions), [Безопасность](#Security)  
  
-   **Удаление процедуры, с помощью:**  [среды SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
 Удаление процедуры может вызвать ошибку в зависимых объектах и в скриптах, если эти объекты и скрипты не обновляются для отражения удаления процедуры. Тем не менее, если вместо удаленной создать другую хранимую процедуру с тем же именем и параметрами, хранимые процедуры, которые на нее ссылаются, будут обрабатываться успешно. Дополнительные сведения см. в разделе [Просмотр зависимостей хранимой процедуры](view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Необходимо разрешение ALTER на схему, которой принадлежит процедура, или разрешение CONTROL на процедуру.  
  
##  <a name="Procedures"></a> Удаление хранимой процедуры  
 Можно использовать один из следующих способов:  
  
-   [Среда SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
 **Удаление процедуры в обозревателе объектов**  
  
1.  В обозревателе объектов подключитесь к экземпляру [!INCLUDE[ssDE](../../includes/ssde-md.md)] и разверните его.  
  
2.  Последовательно разверните узел **Базы данных**, базу данных, которой принадлежит процедура, и узел **Программирование**.  
  
3.  Разверните **Хранимые процедуры**, щелкните правой кнопкой мыши удаляемую процедуру, затем нажмите кнопку **Удалить**.  
  
4.  Для просмотра объектов, зависящих от хранимой процедуры, нажмите **Показать зависимости**.  
  
5.  Подтвердите, что выбрана нужная процедура, и нажмите кнопку **ОК**.  
  
6.  Удалите ссылки на процедуру из зависимых объектов и скриптов.  
  
###  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 **Удаление процедуры в редакторе запросов**  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] и разверните его.  
  
2.  Разверните **Базы данных**, разверните базу данных, к которой относится процедура, или с помощью панели инструментов выберите базу данных из списка доступных.  
  
3.  В меню «Файл» выберите команду **Создать запрос**.  
  
4.  Получите имя хранимой процедуры для удаления из текущей базы данных. В обозревателе объектов разверните узел **Программирование** , затем **Хранимые процедуры**. Также можно выполнить следующую инструкцию в редакторе запросов.  
  
    ```sql  
    SELECT name AS procedure_name   
        ,SCHEMA_NAME(schema_id) AS schema_name  
        ,type_desc  
        ,create_date  
        ,modify_date  
    FROM sys.procedures;  
    ```  
  
5.  Скопируйте и вставьте следующий пример в редактор запросов и введите имя хранимой процедуры, которую нужно удалить из текущей базы данных.  
  
    ```sql  
    DROP PROCEDURE <stored procedure name>;  
    GO  
    ```  
  
6.  Удалите ссылки на процедуру из зависимых объектов и скриптов.  
  
## <a name="see-also"></a>См. также  
 [Создание хранимой процедуры](create-a-stored-procedure.md)   
 [Изменение хранимой процедуры](modify-a-stored-procedure.md)   
 [Изменение имени хранимой процедуры](rename-a-stored-procedure.md)   
 [Просмотр определения хранимой процедуры](view-the-definition-of-a-stored-procedure.md)   
 [Просмотр зависимостей хранимой процедуры](view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE (Transact-SQL)](/sql/t-sql/statements/drop-procedure-transact-sql)  
  
  
