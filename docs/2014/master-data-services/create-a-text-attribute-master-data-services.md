---
title: Создание текстового атрибута (службы Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating text attributes
- creating text attributes [Master Data Services]
ms.assetid: cd8b57de-364d-42a3-9273-c1c6b992bb40
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5be296ceca85eb2032f2a409beefaed603c63f98
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483312"
---
# <a name="create-a-text-attribute-master-data-services"></a>Создание текстового атрибута (службы Master Data Services)
  В среде [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]текстовый атрибут создается, если нужно, чтобы пользователи вводили в качестве значения атрибута текстовую строку.  
  
## <a name="prerequisites"></a>предварительные требования  
 Для выполнения этой процедуры:  
  
-   необходимо иметь разрешение на доступ к функциональной области **Администрирование системы** ;  
  
-   необходимо быть администратором модели. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](administrators-master-data-services.md).  
  
-   должна существовать сущность, для которой создается атрибут. Дополнительные сведения см. в разделе [Создание сущности (службы Master Data Services)](../../2014/master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-create-a-text-attribute"></a>Создание текстового атрибута  
  
1.  В [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]щелкните область **Администрирование системы**.  
  
2.  На странице **Представление модели** в строке меню наведите курсор на **Управление** и щелкните **Сущности**.  
  
3.  На странице **Обслуживание сущности** выберите модель из списка **Модель** .  
  
4.  Выберите строку сущности, для которой необходимо создать атрибут.  
  
5.  Щелкните **Изменить выбранную сущность**.  
  
6.  На странице **Изменение сущности** :  
  
    -   если атрибут предназначен для конечных элементов, выберите команду **Добавить конечный атрибут** на панели **Атрибуты конечных элементов**;  
  
    -   если атрибут предназначен для объединенных элементов, выберите команду **Добавить объединенный атрибут** на панели **Атрибуты консолидированных элементов**;  
  
    -   если атрибут предназначен для коллекций, выберите команду **Добавить атрибут коллекции** на панели **Атрибуты коллекций**.  
  
7.  Выберите параметр **В свободной форме** на странице **Добавить атрибут** .  
  
8.  Введите имя атрибута в поле **Имя** . Список слов, которые не должны использоваться как имена атрибутов, см. в разделе [Зарезервированные слова (службы Master Data Services)](../../2014/master-data-services/reserved-words-master-data-services.md).  
  
9. В поле **Ширина отображаемой области (в пикселях)** введите ширину столбца атрибута для отображения в сетке **обозревателя** .  
  
10. В списке **Тип данных** выберите **Текст**.  
  
11. В поле **Длина** введите максимально допустимое количество символов.  
  
12. По желанию установите флажок **Включить отслеживание изменений** , чтобы отслеживать изменения в группах атрибутов. Дополнительные сведения см. в разделе [Добавление атрибутов в группу отслеживания изменений (службы Master Data Services)](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Нажмите кнопку **Сохранить атрибут**.  
  
14. На странице **Обслуживание сущности** нажмите кнопку **Сохранить сущность**.  
  
## <a name="see-also"></a>См. также  
 [Атрибуты (службы Master Data Services)](../../2014/master-data-services/attributes-master-data-services.md)   
 [Изменение имени атрибута &#40;службы Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [Создание атрибута на основе домена (службы Master Data Services)](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Создание файлового атрибута (службы Master Data Services)](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
