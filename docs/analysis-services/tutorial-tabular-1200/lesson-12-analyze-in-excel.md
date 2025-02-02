---
title: Урок 12. Анализ в Excel | Документация Майкрософт
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8a558dafb4619ef9c4d66884f1fea9fd98e0881c
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404106"
---
# <a name="lesson-12-analyze-in-excel"></a>Урок 12. Анализ в Excel
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

На этом занятии будет использовать анализ в Excel функции в SSDT откройте Microsoft Excel, автоматического создания соединения с источником данных для рабочей области модели и автоматически добавить сводную таблицу на лист. Функция анализа в Excel предназначена для обеспечения быстрого и легкого способа проверки эффективности модели до ее развертывания. На этом занятии вы не будете заниматься анализом данных. Цель этого занятия — ознакомить создателя модели со средствами проверки архитектуры разрабатываемых моделей. В отличие от использования анализ в Excel функция, которая предназначена для разработчиков моделей, конечные пользователи будут использовать клиентские приложения, такие как Excel или Power BI для подключения и просмотра данных в развернутых моделях.  
  
Для выполнения этого занятия необходимо установить Excel на том же компьютере, где находится SSDT. Дополнительные сведения см. в разделе [Анализ в Excel](../tabular-models/analyze-in-excel-ssas-tabular.md).  
  
Предполагаемое время для выполнения этого занятия: **20 минут**  
  
## <a name="prerequisites"></a>предварительные требования  
Этот раздел является частью учебника по табличному моделированию, который необходимо изучать по порядку. Перед выполнением задач на этом занятии, необходимо завершить предыдущее занятие: [Занятие 11. Создание ролей](lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Просмотр с помощью перспектив «По умолчанию» и «Продажи через Интернет»  
В этих первых задачах вы просмотрите модель как с помощью перспективы по умолчанию, которая включает все объекты модели, а также с помощью перспективы Internet Sales ранее. Перспектива «Продажи через Интернет» исключает объект таблицы «Заказчик».  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Просмотр с помощью перспективы по умолчанию  
  
1.  Нажмите кнопку **модели** меню > **анализ в Excel**.  
  
2.  В диалоговом окне **Анализ в Excel** нажмите кнопку **ОК**.  
  
    Excel откроет новую книгу. Создается соединение с источником данных, использующее учетную запись текущего пользователя, и перспектива по умолчанию используется для определения доступных для просмотра полей. На лист автоматически добавляется Сводная таблица.  
  
3.  В Excel в **список полей сводной таблицы**, обратите внимание, что **DimDate** и **FactInternetSales** отображаются группы мер, а также **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, и **FactInternetSales** таблицы со всеми соответствующих столбцов отображаются.  
  
4.  Закройте Excel, не сохраняя книгу.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Просмотр с помощью перспективы «Продажи через Интернет»  
  
1.  Нажмите кнопку **модели** меню, а затем щелкните **анализ в Excel**.  
  
2.  В диалоговом окне **Анализ в Excel** оставьте выбранным вариант **Текущий пользователь Windows** , в раскрывающемся списке **Перспектива** выберите **Продажи через Интернет**и нажмите кнопку **ОК**. 
    
    ![как табличных lesson12-перспективы](media/as-tabular-lesson12-perspective.png)
    
3.  В Excel в **поля сводной таблицы**, обратите внимание, что таблица DimCustomer исключена из списка полей.  
    
    ![как табличных lesson12-поля](media/as-tabular-lesson12-fields.png)
    
4.  Закройте Excel, не сохраняя книгу.  
  
## <a name="browse-by-using-roles"></a>Просмотр с помощью ролей  
Роли — неотъемлемая часть любой табличной модели. Без хотя бы одну роль, к которой пользователи добавляются как члены пользователи не смогут получать доступ и анализировать данные при помощи модели. Функция «Анализ в Excel» позволяет проверить создаваемые роли.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Просмотр с помощью роли пользователя Sales Manager  
  
1.  В SSDT откройте **модели** меню, а затем щелкните **анализ в Excel**.  
  
2.  В **анализ в Excel** отображаемое в диалоговом окне **укажите имя пользователя или роль для подключения к модели**выберите **роли**, а затем в раскрывающемся списке выберите **Менеджер по продажам**, а затем нажмите кнопку **ОК**.  
  
    Excel откроет новую книгу. Сводная таблица создается автоматически. Список полей сводной таблицы включает все поля данных, доступные в новой модели.  
      
3.  Закройте Excel, не сохраняя книгу.  
  
## <a name="whats-next"></a>Дальнейшие действия
Перейдите к следующему занятию: [Занятие 13. Развертывание](lesson-13-deploy.md).

  
  
  
