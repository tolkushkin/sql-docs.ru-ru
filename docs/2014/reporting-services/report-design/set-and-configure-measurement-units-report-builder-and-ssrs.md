---
title: Задание и настройка единиц измерения (построитель отчетов и службы SSRS) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7d29a18d8d194928389ca78fbd854ccb021871c2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105012"
---
# <a name="set-and-configure-measurement-units-report-builder-and-ssrs"></a>Задание и настройка единиц измерения (построитель отчетов и службы SSRS)
  Индикаторы могут иметь два вида единиц измерения: процентные и числовые. По умолчанию в качестве единиц измерения у индикаторов настроены процентные показатели. Таким образом, значения индикаторов, назначаемые для каждого значка в наборе индикаторов, определяются процентным диапазоном. Диапазоны в процентах равномерно разделяются по значкам в наборе индикаторов. Каждый значок отображает состояние индикатора. Процентные показатели для каждого значка в наборе индикаторов можно изменять, задавая различные начальные и конечные процентные значения. Индикаторы могут также автоматически определять минимальное и максимальное значения данных.  
  
 В качестве единицы измерения можно выбрать и числовое значение. В этом случае минимальное и максимальное значения не задаются. Вместо этого задаются только начальные и конечные значения для каждого значка, используемого индикатором.  
  
 Такие параметры, как единицы измерения, можно задать с помощью выражений. Дополнительные сведения см. в разделе [Выражения (построитель отчетов и службы SSRS)](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-use-the-numeric-state-measurement-unit"></a>Использование числовых единиц измерения  
  
1.  Щелкните правой кнопкой мыши индикатор, который необходимо изменить, и выберите **Свойства индикатора**.  
  
2.  Нажмите кнопку **Значения и состояния** на левой панели.  
  
3.  В списке **Единица измерения состояний** щелкните **Числовая**.  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значение параметра.  
  
4.  Для каждого значка в наборе индикаторов обновите значения в текстовых полях **Начало** и **Конец** .  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значение параметров **Начало** и **Конец** .  
  
    > [!NOTE]  
    >  Значения в текстовых полях **Начало** и **Конец** должны быть числовыми.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-percentage-measurement-unit"></a>Использование процентных единиц измерения  
  
1.  Щелкните правой кнопкой мыши индикатор, который необходимо изменить, и выберите **Свойства индикатора**.  
  
2.  Нажмите кнопку **Значения и состояния** на левой панели.  
  
3.  В списке **Единица измерения состояний** щелкните **Процентная**.  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значение параметра.  
  
4.  Измените параметры **Минимум** и **Максимум** , чтобы вместо автоматического обнаружения минимальных и максимальных значений данных, используемых индикатором, применялись конкретные значения (необязательно). Значение **Минимум** должно быть меньше значения **Максимум**.  
  
    > [!NOTE]  
    >  Если минимальное и максимальное значения заданы явно, то индикатором используется заданный диапазон значений независимо от фактического минимального и максимального значения в данных. Таким образом, значения ниже минимума и выше максимума исключаются из оценки, с помощью которой определяется значок индикатора, отображаемый в отчете.  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значения этого параметра.  
  
5.  Для каждого значка в наборе индикаторов обновите значения в текстовых полях **Начало** и **Конец** .  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значение параметров **Начало** и **Конец** .  
  
    > [!NOTE]  
    >  Значения в текстовых полях **Начало** и **Конец** должны быть числовыми.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Индикаторы (построитель отчетов и службы SSRS)](indicators-report-builder-and-ssrs.md)  
  
  
