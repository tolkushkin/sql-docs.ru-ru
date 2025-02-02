---
title: Табличное моделирование (учебник Adventure Works) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af4d5dfa6d59338fb9640143b387b78421375e05
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067801"
---
# <a name="tabular-modeling-adventure-works-tutorial"></a>Табличное моделирование (учебник по Adventure Works)
  В этом учебнике содержатся уроки по созданию табличной модели служб [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Analysis Services с помощью среды [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="what-you-will-learn"></a>Обзор учебника  
 В ходе работы с этим учебником нам предстоит выполнить следующие действия.  
  
-   Создание нового проекта табличной модели в среде [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Импорт данных из реляционной базы данных SQL Server в проект табличной модели.  
  
-   Создание и управление связями между таблицами в модели.  
  
-   Создание и управление вычислениями, мерами и ключевыми показателями эффективности, которые помогут пользователям анализировать данные модели.  
  
-   Создание и управление перспективами и иерархиями, которые помогут пользователям просматривать данные модели, учитывая особенности предприятия и приложения.  
  
-   Создание секций, разделяющих табличные данные на более мелкие логические части, которые могут быть обработаны независимо от других секций.  
  
-   Обеспечение безопасности объектов моделей и данных за счет создания ролей и присвоения членства пользователям.  
  
-   Развертывание табличной модели в «песочницу» или производственный экземпляр служб Analysis Services, работающий в табличном режиме.  
  
## <a name="tutorial-scenario"></a>Сценарий учебника  
 Этот учебник основывается на вымышленной организации [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] — крупная транснациональная производственная компания, производящая и реализующая металлические и композитные велосипеды на рынках Северной Америки, Европы и Азии. Штаб-квартира компании [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] находится в городе Боселл, штат Вашингтон. В ней работают 500 сотрудников компании. Кроме того, компания [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] имеет в своем составе несколько групп сбыта на региональных рынках.  
  
 Для обеспечения более качественной поддержки потребностей анализа данных отделов продаж и маркетинга и руководства необходимо создать табличную модель для пользователей с целью анализа данных интернет-продаж в образце базы данных AdventureWorksDW.  
  
 Чтобы выполнить этот учебник и создать табличную модель Adventure Works по интернет-продажам, необходимо выполнить ряд занятий. В рамках каждого занятия есть ряд задач. Выполнение каждой задачи в нужном порядке является обязательным для завершения занятия. В определенном занятии может быть несколько задач, которые приводят к схожему результату. Однако способ выполнения задач может немного отличаться. Это необходимо, чтобы показать, что зачастую существует более одного способа решения определенной задачи, а также чтобы стимулировать пользователя использовать навыки, приобретенные при выполнении предыдущих задач.  
  
 Цель занятий — провести пользователя через создание простой табличной модели, запущенной в режиме In-Memory, с использованием разных функций из среды [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Поскольку каждое занятие строится на основе предыдущего занятия, их следует выполнять по порядку. После завершения всех занятий будет создан и развернут образец табличной модели Adventure Works для интернет-продаж на сервере служб Analysis Services.  
  
> [!NOTE]  
>  Этот учебник не содержит занятий или сведений об управлении развернутой базой данных табличной модели с помощью среды SQL Server Management Studio или использовании клиентского приложения для создания отчетов для подключения к развернутой модели для просмотра данных модели.  
  
## <a name="prerequisites"></a>предварительные требования  
 Для прохождения этого учебника необходимо, чтобы на компьютере были установлены следующие компоненты:  
  
-   Экземпляр служб Analysis Services [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], работающий в табличном режиме.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   Образец базы данных AdventureWorksDW. Этот образец базы данных включает данные, необходимые для выполнения заданий учебника. Чтобы загрузить образец базы данных, см. в разделе [ https://go.microsoft.com/fwlink/?LinkID=335807 ](https://go.microsoft.com/fwlink/?LinkID=335807).  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 или более поздняя версия (для использования с функцией анализа в Excel в занятии 11)  
  
## <a name="lessons"></a>Занятия  
 Этот учебник включает следующие занятия.  
  
|Занятие|Предположительное время выполнения|  
|------------|--------------------------------|  
|[Занятие 1. Создание нового проекта табличной модели](lesson-1-create-a-new-tabular-model-project.md)|10 минут.|  
|[Занятие 2. Добавление данных](lesson-2-add-data.md)|20 минут|  
|[Занятие 3. Переименование столбцов](rename-columns.md)|20 минут|  
|[Занятие 4. Пометить как таблицу дат](lesson-3-mark-as-date-table.md)|3 минуты|  
|[Занятие 5. Создание связей](lesson-4-create-relationships.md)|10 минут.|  
|[Занятие 6. Создание вычисляемых столбцов](lesson-5-create-calculated-columns.md)|15 минут|  
|[Занятие 7. Создание мер](lesson-6-create-measures.md)|30 минут|  
|[Занятие 8. Создание ключевых показателей эффективности](lesson-7-create-key-performance-indicators.md)|15 минут|  
|[Занятие 9. Создание перспектив](lesson-8-create-perspectives.md)|5 минут|  
|[Занятие 10. Создание иерархий](lesson-9-create-hierarchies.md)|20 минут|  
|[Занятие 11. Создание секций](lesson-10-create-partitions.md)|15 минут|  
|[Занятие 12. Создание ролей](lesson-11-create-roles.md)|15 минут|  
|[Занятие 13. Анализ в Excel](lesson-12-analyze-in-excel.md)|20 минут|  
|[Занятие 14. Развертывание](lesson-13-deploy.md)|5 минут|  
  
## <a name="supplemental-lessons"></a>Дополнительные занятия  
 Этот учебник также включает в себя [дополнительные занятия](../tutorials/supplemental-lessons.md). Ознакомление с содержащимися здесь разделами не требуется для прохождения этого учебника, но может оказаться полезным для лучшего освоения функций для работы с расширенной табличной моделью.  
  
 Этот учебник содержит следующие дополнительные занятия.  
  
|Занятие|Предположительное время выполнения|  
|------------|--------------------------------|  
|[Реализация динамической безопасности с помощью фильтров строк](../tutorials/implement-dynamic-security-by-using-row-filters.md)|30 минут|  
|[Настройка свойств отчетов для отчетов Power View](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md)Настройка свойств отчетов для отчетов Power View|30 минут|  
  
## <a name="next-step"></a>Следующий шаг  
 Чтобы приступить к изучению учебника, перейдите к первому занятию: [Занятие 1. Создание нового проекта табличной модели](lesson-1-create-a-new-tabular-model-project.md).  
  
  
