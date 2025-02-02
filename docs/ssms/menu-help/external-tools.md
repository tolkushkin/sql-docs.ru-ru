---
title: Внешние инструменты | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- External Tools dialog box
ms.assetid: d7dae88f-0781-4162-96cd-d3a3a4d82035
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 26ff0aa2920072d8c6fd4ef97d9945bf1b365970
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65104841"
---
# <a name="external-tools"></a>Внешние инструменты
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
С помощью этого диалогового окна можно добавить в меню **Сервис** внешние инструменты, такие как диспетчер конфигурации SQL Server или "Блокнот". Добавление внешних средств позволяет легко запускать другие приложения во время работы в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. При запуске средств можно указать аргументы и рабочий каталог. Кроме того, выходные данные некоторых средств могут отображаться в окне «Вывод». Диалоговое окно **Внешние инструменты** доступно в меню **Сервис** .  
  
## <a name="options"></a>Параметры  
**Содержимое меню**  
Перечисляются заголовки элементов, добавляемых в настоящий момент в меню **Сервис** . Для изменения порядка элементов в меню используйте кнопки со стрелками **вверх** и **вниз** . Для удаления элемента из меню используйте кнопку **Удалить** .  
  
**вверх**  
Перемещает выбранный инструмент вверх по списку, отображаемому в меню **Сервис** .  
  
**вниз**  
Перемещает выбранный инструмент вниз по списку, отображаемому в меню **Сервис** .  
  
**Добавить**  
Текстовые поля очищаются, чтобы можно было указать новое средство.  
  
**Удаление**  
Удаляет инструмент или команду из списка **Содержимое меню** , а также из меню **Сервис** .  
  
**Title**  
Имя инструмента или команды, появляющихся во вложенном меню **Внешние инструменты** меню **Сервис** . Поместите символ амперсанд перед буквой в имени средства, чтобы использовать эту букву в качестве клавиши быстрого вызова для этого средства. Например: указание `&Spy++` приводит к отображению пункта **Spy++** в меню **Сервис** .  
  
**Command**  
Указывает путь к файлам с расширениями EXE, COM, PIF, BAT, CMD или к другим файлам, которые планируется запускать. Если установлен флажок `.bat`Использовать окно вывода `.com`, можно просмотреть вывод из файлов типа **,** и других файлов в окне "Вывод".  
  
**Аргументы**  
Указываются переменные, которые передаются средству при выборе соответствующего пункта в меню. Аргументы могут задавать значения, передаваемые средству или команде при их запуске. Например: значение может определять имя файла или каталога. Используйте **кнопку со стрелкой** , чтобы сделать выбор из списка стандартных аргументов. Можно добавить несколько аргументов. Полный список стандартных аргументов и их определений см. в разделе [Arguments for External Tools](../../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md). В зависимости от того, какая команда или средство используется, можно также ввести специальные аргументы, например ключи командной строки.  
  
**Исходный каталог**  
Указывает рабочий каталог средства. Чтобы выбрать каталоги, используйте кнопку со **стрелкой** . Можно выбрать несколько каталогов.  
  
**Use output Window**  
Указывает, отображать ли результаты работы средств в окне «Выход». Этот параметр доступен только для таких файлов, как BAT и COM, которые обычно выводят данные в окно командной строки. Если этот параметр включен, при работе со средством облегчается управление окнами.  
  
**Запрос аргументов**  
Отображается диалоговое окно **Аргументы** , позволяющее пользователю вводить или редактировать значения аргументов при каждом запуске внешнего инструмента.  
  
**Рассматривать вывод как данные в формате Юникод**  
Позволяет отображать данные в формате Юникода в окне «Вывод».  
  
**Закрыть при выходе**  
При закрытии средства закрывается открытое средством окно.  
  
## <a name="example"></a>Пример  
  
#### <a name="to-add-sql-server-configuration-manager-to-the-tools-menu"></a>Добавление диспетчера конфигурации SQL Server в меню "Сервис"  
  
1.  В меню **Сервис** выберите пункт **Внешние инструменты**.  
  
2.  В поле **Заголовок** введите **Диспетчер конфигурации SQL Server**.  
  
3.  В поле **Команда** введите путь к исполняемому файлу консоли управления [!INCLUDE[msCoName](../../includes/msconame_md.md)] , например **C:\WINNT\system32\mmc.exe**.  
  
4.  В поле **Аргументы** введите путь к MSC-файлу, например **"C:\WINNT\system32\SQLServerManager.msc"** .  
  
> [!NOTE]  
> Чтобы проверить расположение соответствующих файлов на компьютере, просмотрите свойства ярлыка среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] в меню **Пуск** .  
