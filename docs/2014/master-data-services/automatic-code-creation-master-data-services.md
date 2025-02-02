---
title: Автоматическое создание кодов (службы Master Data Services) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7ee7e06829f72ab44fd036766907be94c95b7d90
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483694"
---
# <a name="automatic-code-creation-master-data-services"></a>Автоматическое создание кодов (службы Master Data Services)
  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]числовые значения могут автоматически формироваться для атрибута Code или другого числового атрибута. При автоматическом формировании кодов есть возможность ввода других значений для кодов вместо исходных, автоматически установленных значений.  
  
## <a name="generating-code-values"></a>Формирование значений кодов  
 Администратор может настроить автоматическое формирование значений для атрибута Code, изменив свойства связанных сущностей. Он может задать исходное значение и предусмотреть увеличение каждого последующего значения на единицу.  
  
 Когда значения атрибута Code вводятся в MDS — либо в одном из программных средств, либо с помощью промежуточного процесса, можно оставить этот атрибут пустым, и тогда значения будут сформированы автоматически. Также можно указать нужное вам значение Code.  
  
## <a name="generating-other-attribute-values"></a>Формирование других значений атрибутов  
 Администратор может автоматически сформировать значения для атрибутов, отличных от Code, создав бизнес-правила. Он может задать исходное значение и определить, насколько будут увеличиваться все последующие значения.  
  
 Когда значения атрибутов вводятся в MDS — либо с помощью одного из программных средств, либо с помощью промежуточного процесса — можно оставить значение атрибута пустым. При использовании бизнес-правил значения будут наращиваться, исходя из наибольшего существующего значения. Например, если правило звучит как "Задать для атрибута формируемое значение по умолчанию начиная с 1, с увеличением последующих значений на 4" и наибольшее значение атрибута равно 700, то следующий добавленный элемент будет равняться 704.  
  
## <a name="deleting-automatically-generated-values"></a>Удаление автоматически сформированных значений  
 После того как администратор включит автоматическое формирование значений для атрибута Code, пользователь может случайно удалить элемент со значением Code, которое необходимо использовать повторно. Отображается сообщение об ошибке «код элемента уже используется элементом, который был удален». Существует два возможных решения:  
  
-   В **управление версиями** функциональной области, администратор может отменить транзакцию, выполненную при удалении элемента. Тем не менее это означает, что все атрибуты и членство в иерархиях и коллекциях являлся членом восстанавливается. Дополнительные сведения см. в разделе [Отмена транзакции &#40;службы Master Data Services&#41;](reverse-a-transaction-master-data-services.md).  
  
-   Администратор может использовать промежуточный процесс для безвозвратного удаления элемента. Дополнительные сведения см. в разделе [деактивировать или удалить членов группы с помощью промежуточного процесса &#40;службы Master Data Services&#41;](add-update-and-delete-data-master-data-services.md).  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Автоматическое формирование значений для атрибута Code.|[Автоматическое формирование значений атрибута Code (службы Master Data Services)](../../2014/master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|Автоматическое формирование значений для других атрибутов.|[Автоматическое формирование значений атрибута, отличного от Code (службы Master Data Services)](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>См. также  
  
-   [Общие сведения о службах Master Data Services](master-data-services-overview-mds.md)  
  
-   [Бизнес-правила (службы Master Data Services)](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [Сущности (службы Master Data Services)](../../2014/master-data-services/entities-master-data-services.md)  
  
  
