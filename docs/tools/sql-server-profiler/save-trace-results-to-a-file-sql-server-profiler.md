---
title: Сохранение результатов трассировки в файл (приложение SQL Server Profiler) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b130d29fa98abd107a540b7acccc4bebd4e93ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62712641"
---
# <a name="save-trace-results-to-a-file-sql-server-profiler"></a>сохранить результаты трассировки в файл (приложение SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  В данном разделе описано сохранение результатов трассировки в файл с помощью [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-save-trace-results-to-a-file"></a>Сохранение результатов трассировки в файл  
  
1.  В меню **Файл** выберите пункт **Создать трассировку**, а затем подключитесь к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Отображается диалоговое окно **Свойства трассировки**.  
  
    > [!NOTE]  
    >  Если установлен параметр **Начать трассировку немедленно после установления соединения**, диалоговое окно **Свойства трассировки**не отображается, а вместо этого начинается трассировка. Чтобы отключить этот параметр, в меню **Сервис**выберите пункт **Параметры**и снимите флажок **Начать трассировку немедленно после установления соединения** .  
  
2.  В поле **Имя трассировки** введите имя трассировки.  
  
3.  Установите флажок **Сохранять в файл** .  
  
     Отображается диалоговое окно **Сохранить как**.  
  
4.  Укажите путь и имя файла в диалоговом окне **Сохранить как**. Нажмите кнопку **Сохранить.**  
  
    > [!NOTE]  
    >  Убедитесь, что служба SQL Server обладает достаточными разрешениями для записи в файл в указанном каталоге.  
  
5.  В диалоговом окне **Свойства трассировки** введите максимальный размер файла в поле **Максимальный размер файла (МБ)** . Значение по умолчанию — 5 мегабайт.  
  
6.  При необходимости укажите следующие необязательные параметры:  
  
    -   Установите флажок **Включить операцию переключения на файл продолжения** , чтобы [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] создавал новые файлы данных трассировки при достижении максимального размера файла. Этот параметр выбран по умолчанию.  
  
    -   Установите флажок **Данные трассировки серверных процессов** , чтобы гарантировать, что сервер сохранит данные обо всех событиях трассировки.  
  
        > [!NOTE]  
        >  Когда флажок **Данные трассировки серверных процессов**снят, сервер не записывает события, если запись событий привела бы к существенному понижению производительности.  
  
## <a name="see-also"></a>См. также:  
 [Приложение SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
