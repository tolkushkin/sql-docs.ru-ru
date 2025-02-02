---
title: Детализированные отчеты (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 938a6450-67c1-4eef-80b4-8fdaefeed584
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63119bf6d8ba4e9d907b9c6cdfb6bfe0b7765941
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105934"
---
# <a name="drillthrough-reports-report-builder-and-ssrs"></a>Детализированные отчеты (построитель отчетов и службы SSRS)
  Детализированный отчет — это отчет, открываемый пользователем щелчком по ссылке в другом отчете. Обычно детализированный отчет содержит подробности об элементе, содержащемся в исходном сводном отчете. Например, на этом рисунке в сводном отчете по продажам содержатся заказы на продажу и итоговые данные. Когда пользователь щелкает номер заказа в сводном списке, открывается другой отчет, содержащий подробности о заказе.  
  
 ![rs_DrillThru](../media/rs-drillthru.gif "rs_DrillThru")  
  
 Данные детализированного отчета не извлекаются до тех пор, пока пользователь не щелкнет ссылку в основном отчете, открывающую детализированный отчет. Если данные основного и детализированного отчета необходимо получать одновременно, рассмотрите возможность использования вложенного отчета. Дополнительные сведения см. в разделе [Вложенные отчеты (построитель отчетов и службы SSRS)](subreports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Во время работы в построителе отчетов необходимо подключение к серверу отчетов для просмотра детализированного отчета, открывающегося при щелчке ссылки детализации в основном отчете.  
  
 Чтобы быстро приступить к работе с детализированными отчетами, см. [Учебник. Создание детализированных и главных отчетов (построитель отчетов)](../tutorial-creating-drillthrough-and-main-reports-report-builder.md). Детализированных отчетов также наглядно показано в двух решений бизнес-аналитики, [BI Reporting: Отчеты и скрипты подписки](https://technet.microsoft.com/bi/ff769487.aspx) и [корпоративные панели: Решения для продаж](https://technet.microsoft.com/bi/ff643005.aspx)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="parameters-in-drillthrough-reports"></a>Параметры детализированных отчетов  
 Детализированный отчет обычно содержит параметры, передаваемые ему сводным отчетом. В примере со сводным отчетом по продажам сводка по отчету содержит поле [OrderNumber] в текстовом поле в ячейке таблицы. Детализированный отчет содержит параметр, принимающий в качестве значения номер заказа. При установке ссылки детализированного отчета на это текстовое поле для поля [OrderNumber] также следует установить параметр целевого отчета для поля [OrderNumber]. Если пользователь щелкнет номер заказа в сводном отчете, откроется целевой детализированный отчет, в котором отобразятся сведения об этом номере заказа. Инструкции по созданию детализированных отчетов, изменяемых на основе значений параметров, см. в разделах [Параметры отчета (построитель отчетов и конструктор отчетов)](report-parameters-report-builder-and-report-designer.md) и [Функция InScope (построитель отчетов и службы SSRS)](report-builder-functions-inscope-function.md).  
  
## <a name="designing-the-drillthrough-report"></a>Создание детализированного отчета  
 Чтобы создать детализированный отчет, перед добавлением действия детализации в основном отчете необходимо разработать детализированный отчет.  
  
 Любой отчет может служить детализированным отчетом. Как правило, детализированный отчет принимает один или несколько параметров, которые определяют отображаемые данные, по ссылке из основного отчета. Например, если ссылка из основного отчета была от заказа на продажу, то в детализированный отчет передается номер заказа.  
  
## <a name="creating-a-drillthrough-action-in-the-main-report"></a>Создание действия детализации в основном отчете  
 Ссылки детализации можно добавлять к текстовым полям (включение текста в ячейки таблицы или матрицы), изображениям, диаграммам, датчикам и другим элементам отчета, имеющим страницу свойств «Действие». Дополнительные сведения см. в разделе [Добавление действия детализации в отчет &#40;построитель отчетов и службы SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md).  
  
 Действие детализации в основном отчете может быть создано в виде действия отчета или действия URL-адреса. Для действия отчета детализированный отчет должен существовать на одном с основным отчетом сервере отчетов. Для действия URL-адреса отчет должен существовать по полному URL-адресу. Способ указания отчета может отличаться при работе с сервером отчета или сайтом SharePoint, интегрированном с сервером отчетов. Если сервер отчетов настроен в режиме интеграции с SharePoint, то поддерживаются только действия с URL-адресами.  
  
 Дополнительные сведения см. в разделах [Добавление действия детализации в отчет (построитель отчетов и службы SSRS)](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) и [Указание путей к внешним элементам (построитель отчетов и службы SSRS)](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
## <a name="viewing-a-drillthrough-report"></a>Просмотр детализированного отчета  
 Чтобы просмотреть сводный отчет со ссылками детализации после его опубликования, следует убедиться, что детализированные отчеты находятся на том же сервере отчетов, что и сводный отчет. Во всех случаях для просмотра детализированного отчета пользователь должен обладать разрешениями на доступ к отчету.  
  
## <a name="see-also"></a>См. также  
 [Детализация, углубленная детализация, вложенные отчеты и вложенные области данных (построитель отчетов и службы SSRS)](drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
