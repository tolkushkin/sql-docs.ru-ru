---
title: 'Занятие 5.: Проектирование родительского отчета с помощью мастера отчетов | Документация Майкрософт'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 661b4f3cc63eb0c19fddb53f872e940d1f9976e2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108442"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>Занятие 5.: Проектирование дочернего отчета с использованием мастера отчетов
  После создания подключения к данным и таблицы данных для дочернего отчета следующий шаг состоит в проектировании дочернего отчета в конструкторе отчетов с помощью мастера отчетов. Дополнительные сведения о конструкторе отчетов см. в разделе [Разработка отчетов с использованием конструктора отчетов (SSRS)](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>Проектирование дочернего отчета с использованием мастера отчетов  
  
1.  Обязательно выберите в **обозревателе решений**веб-сайт верхнего уровня.  
  
2.  Щелкните правой кнопкой мыши веб-сайт и выберите пункт **Добавить новый элемент**.  
  
3.  В **Добавление нового элемента** диалоговом окне щелкните **мастер отчетов**, введите имя файла отчета и нажмите кнопку **добавить**.  
  
     Запустится мастер отчетов.  
  
4.  В **свойства набора данных** странице **источника данных** выберите **DataSet2**.  
  
     Значение, указанное в поле **Доступные наборы данных** , автоматически изменится. В нем будет указана созданная ранее таблица данных.  
  
5.  Нажмите кнопку **Далее**.  
  
6.  На странице **Размещение полей** выполните указанные ниже действия.  
  
    1.  Перетащите элементы **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**и **StockedQty** из области **Доступные поля** в поле **Значения** .  
  
    2.  Щелкните стрелку рядом с полем **Sum(ProductID)**, **Sum(PurchaseOrderID)**, **Sum(PurchaseOrderDetailID)**, **Sum(OrderQty)**,  **SUM(ReceivedQty)**, **Sum(RejectedQty)**, и **Sum(StockedQty)** и очистить **Sum** выбора.  
  
7.  Нажмите кнопку **Далее** , затем щелкнуть **Готово** закрыть **мастер отчетов**.  
  
     В результате создается RDLC-файл. Файл откроется в конструкторе отчетов. Спроектированный вами табликс появится в области конструктора.  
  
8.  Добавьте в открытый RDLC-файл параметр, выполнив следующие действия.  
  
    1.  Нажмите кнопку **параметры** в **данные отчета** области, а затем щелкните **добавить параметры**.  
  
    2.  Введите **productid** в поле **Имя** .  
  
    3.  В списке **Тип данных** должно быть выбрано значение **Integer** .  
  
    4.  Нажмите кнопку **ОК**.  
  
9. Сохраните RDLC-файл.  
  
## <a name="next-task"></a>Следующая задача  
 Тем самым с помощью мастера отчетов был успешно спроектирован дочерний отчет. Затем в приложение для веб-сайта необходимо добавить элемент управления ReportViewer.  
  
  
