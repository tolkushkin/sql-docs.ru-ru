---
title: Руководство. Подключение к базе данных и просмотр существующих объектов | Документация Майкрософт
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.connectionpicker.f1
ms.assetid: 9b331800-3806-4459-ac58-88cdc98124d3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 21096819ebd7a54ab8f4505ad980c0e6a5266d6f
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2019
ms.locfileid: "65098107"
---
# <a name="how-to-connect-to-a-database-and-browse-existing-objects"></a>Руководство. Подключение к базе данных и просмотр существующих объектов
Очень часто администраторам баз данных и разработчикам приходится подключаться к действующей базе данных, проектировать или просматривать ее схему, а также выполнять запросы к ее объектам. Теперь обозреватель объектов SQL Server в Visual Studio содержит специальный узел **SQL Server**, в котором все подключенные экземпляры SQL Server и их базы данных сгруппированы так, как это делается в SSMS. Подключенные экземпляры SQL Server могут быть локальными (выполняющийся экземпляр SQL Server 2008) или удаленными (экземпляр SQL Azure).  
  
Приведенная ниже процедура предполагает, что образец базы данных AdventureWorks уже установлен. На сайте [CodePlex](https://msftdbprodsamples.codeplex.com/) можно найти и установить образцы баз данных для различных версий SQL Server. При желании можно выполнить приведенные ниже инструкции и указать существующую базу данных на вашем сервере.  
  
### <a name="to-connect-to-a-database-instance"></a>Подключение к экземпляру базы данных  
  
1.  Проверьте, открыт ли в Visual Studio **обозреватель объектов SQL Server**. Если нет, в меню **Вид** выберите **Обозреватель объектов**.  
  
2.  Щелкните правой кнопкой мыши узел **SQL Server** в **обозревателе объектов SQL Server** и выберите **Добавить SQL Server**.  
  
3.  В диалоговом окне **Соединение с сервером** введите в поле **Имя сервера** имя экземпляра, к которому нужно подключиться, учетные данные и нажмите кнопку **Подключить**.  
  
4.  В **обозревателе объектов SQL Server** разверните узел **Базы данных** под экземпляром сервера. Все базы данных, размещаемые на этом экземпляре сервера, появятся в узле **Базы данных** .  
  
5.  Разверните узел **AdventureWorks** (или другую базу данных). Обратите внимание, что сущности базы данных организованы иерархически, как это делается в среде SQL Server Management Studio.  
  
