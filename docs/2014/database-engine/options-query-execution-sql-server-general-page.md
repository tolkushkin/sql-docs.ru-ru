---
title: Параметры (запроса выполнения SQL Server — "Общие") | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionGeneral
ms.assetid: 3f8d59bc-3f97-4e5d-8b86-5ac670d20780
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 83c0d1ad4d63d361754c5e2183081c30c7c51f2b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089984"
---
# <a name="options-query-execution-sql-server-general-page"></a>Параметры (запроса выполнения SQL Server — "Общие")
  Используйте эту страницу, чтобы задать параметры для запросов служб [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Изменения этих параметров применяются только к новым запросам [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Для изменения параметров текущего запроса выберите пункт **Параметры запроса** в меню **Запрос** или щелкните правой кнопкой мыши в окне запроса [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] и выберите пункт **Параметры запроса**.  
  
## <a name="options"></a>Параметры  
 **SET ROWCOUNT**  
 Значение по умолчанию, равное 0, указывает на то, что [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] будет продолжать ожидание результатов, пока все из них не будут получены. При установке значения больше 0 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] прервет запрос после получения указанного числа строк. Для выключения этого параметра (чтобы возвращались все строки) задайте SET ROWCOUNT 0.  
  
 **SET TEXTSIZE**  
 Значение по умолчанию, равное 2 147 483 647 байт, указывает, что [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] предоставит полный набор данных до ограничения в полях данных `text` и `ntext`. Задав меньшее число, можно ограничить вывод результатов в случае больших значений. Содержимое столбцов большего размера, чем заданное число, будет усекаться.  
  
 **Время ожидания выполнения**  
 Задает значение по умолчанию в диалоговом окне **Создание соединения** . Используйте это поле, чтобы указать [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] количество секунд ожидания перед отменой запроса. Значение, равное 0, указывает на неограниченное время ожидания или отсутствие времени ожидания. При новой установке это значение равно 0.  
  
 **Разделитель пакетов**  
 Введите слово, которое будет использоваться для разделения инструкций языка [!INCLUDE[tsql](../includes/tsql-md.md)] на пакеты. Значение по умолчанию — GO.  
  
 **По умолчанию открывать новые запросы в режиме SQLCMD**  
 При установке этого флажка новые запросы будут открываться в режиме SQLCMD. Дополнительные сведения о режиме SQLCMD см. в разделе [Изменение скриптов SQLCMD при помощи редактора запросов](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md).  
  
 При выборе этого параметра следует учитывать следующие ограничения.  
  
-   Технология IntelliSense в редакторе запросов компонента [!INCLUDE[ssDE](../includes/ssde-md.md)] отключена.  
  
-   Поскольку редактор запросов не запускается из командной строки, невозможно передать ему такие параметры командной строки, как переменные.  
  
-   Поскольку редактор запросов не может ответить на подсказки и приглашения операционной системы, будьте внимательны и не запускайте интерактивные инструкции.  
  
 **Сброс до значений по умолчанию**  
 Выберите этот пункт для сброса всех значений этой страницы и установки значений по умолчанию.  
  
## <a name="see-also"></a>См. также  
 [Служебная программа sqlcmd](../tools/sqlcmd-utility.md)  
  
  
