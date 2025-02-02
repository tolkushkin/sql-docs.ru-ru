---
title: Отчет об оценке (AccessToSQL) | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1278552f1bfe1ccfb7ab250f843e86c62e63440b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62651084"
---
# <a name="assessment-report-accesstosql"></a>Отчет об оценке (AccessToSQL)
Отчет об оценке окна показаны результаты преобразования объектов базы данных, чтобы [!INCLUDE[tsql](../../includes/tsql-md.md)] синтаксис, и может также помочь оценить сложность и стоимость проектов миграции.  
  
Чтобы создать отчет об оценке, выберите объекты для преобразования в обозревателе метаданных исходным кодом, щелкните правой кнопкой мыши **баз данных**, а затем выберите **создать отчет**. Также можно отобразить этот отчет автоматически после преобразования схемы. Тем не менее отчет будет называться отчет о преобразовании. Дополнительные сведения см. в разделе [параметры проекта (GUI) (SSMA распространено)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
## <a name="options"></a>Параметры  
**Панель обозревателя**  
Содержит иерархию объектов в отчет об оценке. Разверните папку для просмотра отдельных объектов и вспомогательных компонентов. Если щелкнуть категорию или объект, в области сведений появится статистика преобразования для этой категории или объект.  
  
**Область сведений**  
Показано преобразование сообщений Статистика "или" Ошибка "и" warning "для выбранного объекта. Например если установлен в папке Tables, в области сведений будет показывать номера внешних ключей, индексов, первичных ключей и таблицы, которые были преобразованы.  
  
**Панель сообщений**  
Показывает ошибки, предупреждения и информационные сообщения, которые были созданы, когда был создан отчет об оценке. Сообщения группируются по номеру.  
  
Чтобы просмотреть сведения о сообщении, щелкните **ошибки**, **предупреждения**, или **сообщений**, а затем разверните сообщение. SSMA будет отображен список объектов, которые содержат эту ошибку. Щелкните объект, чтобы отобразить все сведения о преобразовании для объекта.  
  
## <a name="see-also"></a>См. также  
[Reference(Access) интерфейса пользователя](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
