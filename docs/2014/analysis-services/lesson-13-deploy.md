---
title: Урок 14. Развертывание | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96ffa6445d46f1e68efa907330d0945a499bf3b2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079141"
---
# <a name="lesson-14-deploy"></a>Урок 14. Развертывание
  На этом занятии мы выполним настройку свойства развертывания, указав экземпляр сервера развертывания служб Analysis Services в табличном режиме и имя развертываемой модели. Затем мы выполним развертывание модели на указанном экземпляре. После развертывания пользователи смогут подключаться к модели с помощью клиентского приложения создания отчетов. Дополнительные сведения см. в разделе [Развертывание решений табличной модели (табличные службы SSAS)](tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
 Предполагаемое время для выполнения этого занятия: **5 минут**  
  
## <a name="prerequisites"></a>предварительные требования  
 Этот раздел является частью учебника по табличному моделированию, который необходимо изучать по порядку. Перед выполнением задач на этом занятии, необходимо завершить предыдущее занятие: [Занятие 13. Анализ в Excel](lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Развертывание модели  
  
#### <a name="to-configure-deployment-properties"></a>Настройка свойств развертывания  
  
1.  В среде [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] в **обозревателе решений** щелкните правой кнопкой мыши проект **Табличная модель интернет-продаж Adventure Works** и выберите в контекстном меню пункт **Свойства**.  
  
2.  В диалоговом окне **Страницы свойств табличной модели интернет-продаж AW** на вкладке **Сервер развертывания**в свойстве **Сервер** введите имя экземпляра служб Analysis Services, запущенном в табличном режиме. Это будет экземпляр, на котором будет развернута модель.  
  
    > [!IMPORTANT]  
    >  Для развертывания модели необходимо разрешение администратора на удаленном экземпляре служб Analysis Services.  
  
3.  Проверьте **режим запроса** свойству **In-Memory**.  
  
    > [!NOTE]  
    >  Модель, созданная с помощью этого учебника, не будет поддерживаться в режиме DirectQuery.  
  
4.  В **базы данных** введите `Adventure Works Internet Sales Model`.  
  
5.  В **куба** свойство имени, типа `Adventure Works Internet Sales Model`.  
  
6.  Убедитесь в том, что все выбрано правильно, и нажмите кнопку **ОК**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Развертывание табличной модели интернет-продаж Adventure Works  
  
1.  В среде [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] щелкните меню **Сборка** и выберите команду **Развернуть табличную модель интернет-продаж AW**.  
  
     Появится диалоговое окно «Развертывание», в котором будет отображено состояние развертывания метаданных, а также каждая таблица, включенная в модель.  
  
## <a name="conclusion"></a>Заключение  
 Поздравляем! На этом заканчивается создание и развертывание табличной модели служб Analysis Services. Этот учебник помог вам выполнить одну из самых распространенных задач в создании табличной модели. Теперь, когда модель интернет-продаж Adventure Works развернута, можно использовать среду SQL Server Management Studio для управления ею, создания скриптов обработки и плана резервного копирования. Пользователи могут подключаться к модели с помощью клиентского приложения для создания отчетов, например Microsoft Excel или [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
## <a name="additional-resources"></a>Дополнительные ресурсы  
 Дополнительные сведения о свойствах табличной модели, поддерживающих отчеты [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], см. в разделе [Свойства отчетов Power View (табличные службы SSAS)](tabular-models/properties-ssas-tabular.md).  
  
## <a name="see-also"></a>См. также  
 [Режим DirectQuery (табличные службы SSAS)](tabular-models/directquery-mode-ssas-tabular.md)   
 [Настройка моделирования данных по умолчанию и свойств развертывания (табличные службы SSAS)](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Базы данных табличной модели (табличные службы SSAS)](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
