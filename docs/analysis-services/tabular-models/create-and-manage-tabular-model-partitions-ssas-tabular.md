---
title: Создание и управление секциями для табличных моделей | Документация Майкрософт
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7067449c0de9958e98a7a9dc5cc09c7f89f33fa9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472296"
---
# <a name="create-and-manage-tabular-model-partitions"></a>Создание и управление секциями табличной модели
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Секции разделяют таблицу на логические части. Каждая секция затем может обрабатываться (обновляться) независимо от других секций. Секции, определенные для модели во время разработки модели, дублируются в модели развертывания. После развертывания можно настроить управление секциями с помощью диалогового окна **Секции** в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или с помощью скрипта. В задачах этого раздела описывается создание и управление секциями в развернутой модели.  
  
  > [!NOTE]  
>  Секции в табличных моделях, созданных на уровне совместимости 1400 определяются с помощью инструкции запроса M. Дополнительные сведения см. в разделе [ссылку M](https://msdn.microsoft.com/library/mt211003.aspx). 
>
  
## <a name="tasks"></a>Задания  
 Создание секций и управление ими в развернутой базе данных с табличной моделью выполняются в диалоговом окне **Секции** среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Чтобы открыть диалоговое окно **Секции** в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], щелкните таблицу правой кнопкой мыши и выберите команду **Секции**.  
  
###  <a name="bkmk_create_new"></a> Создание новой секции  
  
1.  В диалоговом окне **Секции** нажмите кнопку **Создать** .  
  
2.  В поле **Имя секции**введите имя секции. По умолчанию к имени секции, заданной по умолчанию, будет добавляться номер, постепенно увеличивающийся для каждой новой секции.  
  
3.  В **инструкцию запроса**введите или вставьте инструкцию запроса SQL или M, определяющую столбцы и любые предложения, вы хотите включить в секцию в окно запроса.  
  
4.  Чтобы проверить инструкцию, нажмите кнопку **Проверить синтаксис**.  
  
###  <a name="bkmk_copy"></a> Копирование секции  
  
1.  В диалоговом окне **Секции** в списке **Секции** выберите секцию, которую необходимо скопировать, и нажмите кнопку **Копировать** .  
  
2.  В поле **Имя секции**введите новое имя секции.  
  
3.  В **инструкцию запроса**, изменить инструкцию запроса.  
  
###  <a name="bkmk_merge"></a> Объединение двух или более разделов  
  
-   В диалоговом окне **Секции** в списке **Секции** выберите щелчками мыши при нажатой клавише CTRL секции, которые необходимо объединить, и нажмите кнопку **Объединить** .  
  
> [!IMPORTANT]  
>  Слияние секций не обновляет их метаданные. Необходимо изменить инструкцию SQL или M для получающейся в результате секции, чтобы убедиться в том, что все операции обработки обрабатывают все данные в объединенной секции.  
  
###  <a name="bkmk_delete"></a> Удаление секции  
  
-   В диалоговом окне **Секции** в списке **Секции** выберите секцию, которую необходимо удалить, и нажмите кнопку **Удалить** .  
  
## <a name="see-also"></a>См. также  
 [Секции табличных моделей](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Секции табличных моделей, обработка](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  
