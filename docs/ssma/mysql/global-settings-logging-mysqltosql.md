---
title: Глобальные параметры (Ведение журнала) (MySQLToSQL) | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0d033492-5ec3-473a-8de1-821894ec9518
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 225d0cd15aa170edc146eda0615a708ab0fe3ce2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63195155"
---
# <a name="global-settings-logging--mysqltosql"></a>Глобальные параметры (ведение журнала) (MySQLToSQL)
Используйте **глобальные параметры** диалоговое окно, чтобы указать параметры ведения журнала для SSMA. Как правило можно изменить эти параметры только в том случае, при взаимодействии со службой поддержки продукта.  
  
Чтобы открыть это диалоговое окно, в **средства** меню, выберите **глобальные параметры** и нажмите кнопку **ведение журнала** кнопки в нижней части левой панели.  
  
## <a name="options"></a>Параметры  
**Уровень сообщений**  
Следующие параметры доступны в разделе **уровень сообщений**:  
  
|Параметр|Описание|  
|----------|---------------|  
|**[все категории]**|Используется для задания уровня ведения журнала для всех следующих параметров.|  
|**Сборщик**|Собирает метаданные о исходной схемы и сохраняет его в проект.|  
|**Преобразователь**|Преобразует структуры объектов базы данных источника, таких как таблицы и хранимые процедуры в соответствующий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] структуры.|  
|**Migrator данных**|Перенос данных из базы данных-источника в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Модуль форматирования**|Подкомпонента преобразователя, который формирует скрипты для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] схемы.|  
|**Графический пользовательский интерфейс**|Сообщения, которые отображаются при использовании средства SSMA.|  
|**Компоновщик**|Разрешает SQL-идентификаторов и предоставляет сведения о других компонентов.|  
|**Другое**|Все сообщения, не входящие в другие категории.|  
|**Средство синтаксического анализа**|Выполняет синтаксический анализ исходной схеме.|  
|**Синхронизатор**|Загружает источник объектов базы данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**TreeConverter**|Преобразует объекты в исходных метаданных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] метаданных.|  
  
Для каждого параметра в разделе **уровень сообщений**, настройте один из следующих уровней ведения журнала для SSMA:  
  
|||  
|-|-|  
|**Неустранимая ошибка**|Запись в журнал сообщения о неустранимых ошибках.|  
|**Ошибка**|Запись в журнал ошибок и сообщения о неустранимых ошибках.|  
|**Предупреждение**|Запись в журнал предупреждение, ошибка и сообщения о неустранимых ошибках.|  
|**Info**|Запись в журнал ошибки информационное, предупреждение и сообщения, Неустранимая ошибка.|  
|**Отладка**|Записи всех сообщений, включая отладку сообщения в журнал.|  
  
**Путь к файлу журнала**  
Путь к файлу и имя файлов журнала SSMA. Чтобы указать другое имя, щелкните по текущему пути и нажмите кнопку обзора (**...** ) кнопку.  
  
**Размер файла журнала**  
Максимальный размер файла журнала в КБ. Минимальный размер — 10 КБ. Размер по умолчанию — 10 240 КБ.  
  
**Общее число файлов журнала**  
После заполнения один файл журнала, SSMA переименовать файл журнала и создана новая транзакция. При использовании этого параметра, укажите максимальное количество сохраняемых файлов журнала. Минимальное значение — 2.  
  
