---
title: Задание максимального размера для таблицы трассировки (приложение SQL Server Profiler) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- size [SQL Server], trace tables
- maximum table size for traces
ms.assetid: d0ae83e5-1c88-4a2e-be05-2c341280b978
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 15ef5e8621a5edd216b300a8a96f3a9656b55b12
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267150"
---
# <a name="set-a-maximum-table-size-for-a-trace-table-sql-server-profiler"></a>установить максимальный размер для таблицы трассировки (приложение SQL Server Profiler)
  В этом подразделе рассказывается о том, как задать максимальный размер таблицы трассировки при помощи приложения [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-set-a-maximum-table-size-for-a-trace-table"></a>Установка максимального размера таблицы трассировки  
  
1.  В меню **Файл** выберите пункт **Создать трассировку**, а затем подключитесь к экземпляру SQL Server.  
  
     Отображается диалоговое окно **Свойства трассировки**.  
  
    > [!NOTE]  
    >  Если установлен параметр **Начать трассировку немедленно после установления соединения**, диалоговое окно **Свойства трассировки**не отображается, а вместо этого начинается трассировка. Чтобы отключить этот параметр, в меню **Сервис**выберите пункт **Параметры**и снимите флажок **Начать трассировку немедленно после установления соединения** .  
  
2.  В поле **Имя трассировки** введите имя трассировки.  
  
3.  В списке **Имя шаблона**выберите шаблон трассировки.  
  
4.  Установите флажок **Сохранить в таблицу**.  
  
5.  Подключитесь к серверу, на который будет записываться трассировка.  
  
     Откроется диалоговое окно **Целевая таблица** .  
  
6.  Выберите базу данных для трассировки из списка **База данных** .  
  
7.  В поле **Таблица** введите или выберите имя таблицы.  
  
8.  Установите флажок **Установить максимальное число строк** и укажите максимальное число строк для таблицы трассировки.  
  
    > [!NOTE]  
    >  Когда количество строк в таблице превысит указанный максимум, регистрация событий трассировки прекратится. Однако трассировка продолжится.  
  
## <a name="see-also"></a>См. также  
 [Приложение SQL Server Profiler](sql-server-profiler.md)   
 [Приложение SQL Server Profiler](sql-server-profiler.md)  
  
  
