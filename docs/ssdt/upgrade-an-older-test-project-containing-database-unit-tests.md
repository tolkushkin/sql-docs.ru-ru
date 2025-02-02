---
title: Обновление старого тестового проекта, содержащего модульные тесты базы данных | Документация Майкрософт
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 42782ff3-e8cf-4c9d-8dac-a95b236edfc4
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d1b91df1ecce9749ebdec3515a339ac31f2507b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65101984"
---
# <a name="upgrade-an-older-test-project-containing-database-unit-tests"></a>Обновление старого проекта тестов, содержащего модульные тесты базы данных
Старый тестовый проект, созданный с помощью Visual Studio 2010 и содержащий модульные тесты базы данных, можно обновить, чтобы использовать новую среду выполнения и средства тестирования SQL Server Data Tools. Сразу после обновления старого проекта вы сможете добавлять модульные тесты в проект SQL Server (дополнительные сведения см. в статье [Создание и определение модульных тестов SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)).  
  
> [!TIP]  
> Если вы используете Visual Studio 2010, то после добавления модульных тестов SQL Server не следует добавлять модульные тесты в тестовый проект, используя шаблон старого модульного теста базы данных. В противном случае потребуется снова преобразовывать проект, чтобы обеспечить правильное выполнение тестов.  
  
Если у вас есть тестовый проект базы данных, который был создан в версии до Visual Studio 2010, можно использовать сведения в разделе [Руководство. Обновление базы данных модульных тестов из предыдущих выпусков Visual Studio](https://msdn.microsoft.com/library/dd193412(VS.100).aspx), чтобы обновить проект базы данных до Visual Studio 2010 перед обновлением проекта до SQL Server Data Tools.  
  
### <a name="initiating-an-upgrade"></a>Запуск обновления  
  
-   Обновление проекта можно запустить из контекстного меню.  
  
    В некоторых случаях SQL Server Data Tools выводит диалоговое окно, в котором вы можете запустить обновление тестового проекта.  
  
-   При обновлении проекта удаляется ссылка на сборку на старую среду тестирования базы данных и добавляется ссылка на новую среду и сборку адаптера. Файл app.config также обновляется.  
  
    > [!NOTE]  
    > Если в тестовом проекте одновременно содержатся файлы с кодом для DatabaseSetup и SQLDatabaseSetup, после обновления проекта до версии SQL Server Data Tools файл DatabaseSetup будет исключен из сборки. Если файл DatabaseSetup исключен из сборки, его можно удалить.  
  
-   После преобразования существующие модульные тесты базы данных, созданные с помощью старого шаблона, будут использовать типы сборки адаптера для доступа к новой среде. Использование сборки адаптера означает, что процесс обновления не изменил скрипты и код тестов. Если добавить в проект модульный тест SQL Server, новый тест будет ссылаться на новую среду напрямую, а не через адаптер. Можно выполнить обновление существующего кода вручную для согласованности с новыми тестами, однако в этом нет необходимости.  
  
## <a name="see-also"></a>См. также:  
[Проверка кода базы данных с помощью модульных тестов SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
  
