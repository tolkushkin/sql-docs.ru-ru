---
title: Элементов модели страница «безопасность» (диспетчер отчетов) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.modelitemsecurity.f1
ms.assetid: 8c5b29ae-1f17-41f2-ab59-97899b8fb4fc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f45169a2fdc8fdc4d56cb27a8bf6348a3c3c1a29
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108231"
---
# <a name="model-item-security-page-report-manager"></a>Страница «Безопасность элементов модели» (диспетчер отчетов)
  На этой странице можно защитить элементы модели, предоставляя или отменяя разрешения «только для чтения» в отношении определенных элементов. Безопасность элементов модели определяет порядок нерегламентированного просмотра данных во время выполнения и возможность использования элементов опубликованной модели при создании отчетов в построителе отчетов. Для использования этой функции необходимы разрешения диспетчера содержимого.  
  
 Безопасность элементов модели применяется к модели, которая обрабатывается на сервере отчетов, и не влияет на SMDL-файлы, изменяемые в конструкторе моделей или используемые в конструкторе отчетов. Более того, она не применяется к пользователям, имеющим разрешения на изменение определения модели. Любому пользователю, имеющему для модели разрешения &#0171;</ph>Диспетчер содержимого&#0187;</ph> или &#0171;</ph>Издатель&#0187;</ph>, доступны все ее части независимо от того, применяется ли безопасность элементов модели.  
  
> [!NOTE]  
>  Элементы модели могут иметь дополнительную защиту благодаря использованию фильтров безопасности.  
  
 Безопасность элементов модели можно определить для сущностей, папок и отдельных полей в рамках модели. Поскольку модель содержит большое количество защищаемых элементов, наследование разрешений встроено в модель, что позволяет обеспечить защиту большого количества элементов с помощью относительно небольшого количества назначений ролей. Наследование разрешений основано на следующем.  
  
-   Модель  
  
-   Корневой узел  
  
-   Папки или сущности  
  
-   Поля  
  
 Изначально разрешения на доступ к элементам модели наследуется через назначения ролей, задаваемые для самой модели. Пользователь, имеющий разрешение просматривать модель в папке диспетчера отчетов, может просмотреть все элементы этой модели.  
  
 После включения защиты элементов модели необходимо создать, по крайней мере, одно назначение ролей для корневого узла. Это исходное назначение ролей на корневом узле становится новым источником наследуемых разрешений. Оно автоматически наследуется всеми элементами в иерархии модели.  
  
 Чтобы выполнить дальнейшую настройку разрешений на просмотр данных, можно изменять разрешения для папок и сущностей. И наконец, можно установить разрешения для отдельных полей.  
  
 Чтобы упростить обслуживание, связанное с назначениями ролей, вместо отдельных полей разрешения следует создавать для папок и сущностей. Поиск созданных назначений ролей не поддерживается. Если для конкретных полей установлены настройки безопасности и в дальнейшем необходимо обновить эти настройки, нужно будет прощелкать все пространство имен модели для поиска полей с примененными настройками безопасности.  
  
 Для начала создайте назначение роли на корневом узле, после чего создайте дополнительные назначения ролей для сущностей и папок. Чтобы отменить защиту элементов модели, снимите флажок **Обеспечивать индивидуальную безопасность отдельных элементов этой модели**. Снятие этого флажка восстанавливает исходные разрешения, унаследованные от модели.  
  
## <a name="navigation"></a>Навигация  
 Чтобы перейти к этому местоположению в пользовательском интерфейсе, используйте следующую процедуру.  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>Открытие страницы свойств отчета «Общие»  
  
1.  Откройте диспетчер отчетов и найдите модель, для которой необходимо настроить защиту элементов модели.  
  
2.  Подведите курсор к модели и щелкните стрелку раскрывающегося списка.  
  
3.  В раскрывающемся меню выберите **Управление**. Откроется страница свойств модели «Общие».  
  
4.  Перейдите на вкладку **Безопасность элементов модели** .  
  
## <a name="options"></a>Параметры  
 **Обеспечивать безопасность отдельных элементов этой модели**  
 Щелкните этот флажок, чтобы включить безопасность элемента модели.  
  
 **Задать настройки безопасности для отдельных элементов модели в режиме**  
 Показывает все элементы модели. Можно осуществлять навигацию по пространству имен модели для выбора элемента, безопасность которого требуется настроить. Одновременно можно выбрать только один элемент. Прежде чем переходить к другим сущностям и папкам, убедитесь в создании назначения ролей для корневого элемента.  
  
 **Наследовать разрешения от родительского элемента**  
 Выберите этот параметр, чтобы унаследовать настройки безопасности родительского элемента.  
  
 **Назначить разрешения следующим пользователям и группам (разделенных точкой с запятой)**  
 Выберите этот параметр, чтобы указать учетную запись пользователя или группы, для которой определяется доступ. Если используются настройки безопасности по умолчанию, учетные записи пользователей и групп представляют собой учетные записи домена Windows. Укажите учетные записи в следующем формате:  *\<домена >\\< учетная запись\>*.  
  
## <a name="see-also"></a>См. также  
 [Справка F1 по использованию сервера отчетов среде Management Studio](tools/report-server-in-management-studio-f1-help.md)  
  
  
