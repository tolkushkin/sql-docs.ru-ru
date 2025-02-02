---
title: Добавление вложенного отчета и параметров (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10093"
- sql12.rtp.rptdesigner.subreportproperties.general.f1
ms.assetid: 94f960f8-a629-4f1e-8277-c3b8f0680d98
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 906f4527bdca38f4571a2e1686f885a2857e47c3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106784"
---
# <a name="add-a-subreport-and-parameters-report-builder-and-ssrs"></a>Добавление вложенного отчета и параметров (построитель отчетов и службы SSRS)
  Вложенные отчеты следует использовать в том случае, если необходимо создать основной отчет, являющийся контейнером для нескольких связанных отчетов. Вложенный отчет — это ссылка на другой отчет. Чтобы связать отчеты посредством значений данных (например, для отображения данных из нескольких отчетов одному клиенту), необходимо разработать параметризованный отчет (например отчет, показывающий сведения об определенном клиенте), который будет служить в качестве вложенного отчета. При добавлении вложенного отчета в основной отчет можно указать параметры, которые будут переданы вложенному отчету.  
  
 Вложенные отчеты также можно добавить к динамическим строкам или столбцам в таблице или матрице. При обработке основного отчета будет выполнена обработка вложенного отчета для каждой строки. В данном случае следует оценить, можно ли получить необходимый результат с помощью областей данных или вложенных областей данных.  
  
 Чтобы добавить вложенный отчет к отчету, сначала необходимо создать отчет, который будет использоваться в качестве вложенного. Дополнительные сведения о создании вложенного отчета см. в разделе [Вложенные отчеты (построитель отчетов и службы SSRS)](subreports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-subreport"></a>Добавление вложенного отчета  
  
1.  На вкладке **Вставка** щелкните **Вложенный отчет**.  
  
2.  В области конструктора щелкните поверхность отчета и перетащите его поле до желаемого размера вложенного отчета. Либо щелкните область конструктора, чтобы создать вложенный отчет с размером по умолчанию.  
  
3.  Щелкните правой кнопкой мыши вложенный отчет, а затем выберите пункт **Свойства вложенного отчета**.  
  
4.  В диалоговом окне **Свойства вложенного отчета** введите имя в текстовое поле **Имя** или примите имя по умолчанию. В пределах отчета имя должно быть уникальным. По умолчанию присваивается стандартное имя, такое как Subreport1 или Subreport2.  
  
5.  В списке **Использовать этот отчет в качестве вложенного отчета** нажмите кнопку **Обзор**или введите имя отчета. Рекомендуется нажать кнопку **Обзор** , поскольку путь к вложенному отчету будет указан автоматически. Указать отчет можно несколькими способами. Дополнительные сведения см. в разделе [Указание путей к внешним элементам (построитель отчетов и службы SSRS)](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
6.  Щелкните **Да** в области **Пропустить границу на разрыве страницы** , чтобы предотвратить вывод границы в середине вложенного отчета, если он занимает более одной страницы (необязательно).  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-specify-parameters-to-pass-to-a-subreport"></a>Указание параметров, передаваемых вложенному отчету  
  
1.  В режиме конструктора щелкните правой кнопкой мыши вложенный отчет и выберите **Свойства вложенного отчета**.  
  
2.  В диалоговом окне **Свойства вложенного отчета** щелкните **Параметры**.  
  
3.  Нажмите кнопку **Добавить**. В сетку параметров добавится новая строка.  
  
4.  Введите имя параметра во вложенном отчете в текстовое поле **Имя** или выберите его из списка. Это имя должно совпадать с именем параметра вложенного отчета, а не с именем параметра запроса.  
  
5.  В списке **Значение** введите или выберите значение для передачи вложенному отчету. Это значение может быть статическим текстом или выражением, ссылающимся на какое-либо поле или иной объект в основном отчете.  
  
    > [!NOTE]  
    >  Если в списке **Параметры** построителя отчетов пропущен параметр, а вложенный отчет имеет определенное значение по умолчанию, вложенный отчет будет обработан правильно.  
    >   
    >  В конструкторе отчетов все параметры, которые требуются вложенному отчету, должны быть включены в список **Параметры** . Если не хватает какого-либо требуемого параметра, вложенный отчет не будет правильно отображен в основном отчете.  
  
6.  Повторите шаги с 3 по 5, чтобы указать имена и значения для всех параметров вложенного отчета.  
  
7.  Для удаления параметра вложенного отчета щелкните этот параметр в сетке параметров и выберите **Удалить**.  
  
8.  Чтобы изменить порядок параметров вложенного отчета, щелкните параметр и нажмите кнопку со стрелкой вверх или вниз.  
  
     Изменение порядка параметров вложенного отчета не скажется на обработке вложенного отчета.  
  
## <a name="see-also"></a>См. также  
 [Вложенные отчеты (построитель отчетов и службы SSRS)](subreports-report-builder-and-ssrs.md)   
 [Поведение при подготовке к просмотру (построитель отчетов и службы SSRS)](rendering-behaviors-report-builder-and-ssrs.md)  
  
  
