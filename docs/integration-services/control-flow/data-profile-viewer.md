---
title: Средство просмотра профиля данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: feacddee000b296e5a0687e63deb1cb75fe1b04c
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727812"
---
# <a name="data-profile-viewer"></a>Средство просмотра профиля данных

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Просмотр и анализ профилей данных — следующий шаг в процессе профилирования данных. Профили можно просмотреть после запуска задачи «Профилирование данных» внутри пакета служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] и расчета профилей данных. Дополнительные сведения о настройке и использовании задач "Профилирование данных" см. в разделе [Установка задачи "Профилирование данных"](../../integration-services/control-flow/setup-of-the-data-profiling-task.md).  
  
> [!IMPORTANT]  
>  В выходном файле могут содержаться конфиденциальные данные о базе данных и о содержащихся в ней данных. Рекомендации по повышению защищенности этого файла см. в разделе [Доступ к файлам, используемым пакетами](../../integration-services/security/security-overview-integration-services.md#files).  
  
## <a name="data-profiles"></a>Профили данных  
 Чтобы просмотреть профили данных, нужно настроить задачу «Профилирование данных» таким образом, чтобы ее выходные данные направлялись в файл, и затем использовать отдельное средство просмотра профиля данных. Чтобы открыть средство просмотра профиля данных, выполните одно из следующих действий.  
  
-   Щелкните правой кнопкой мыши задачу **Профилирование данных[!INCLUDE[ssIS](../../includes/ssis-md.md)] в конструкторе**  и выберите **Изменить**. На странице **Общие** **редактора задачи «Профилирование данных»** нажмите кнопку **Открыть средство просмотра профиля**.  
  
-   В папке *\<диск>*:\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn запустите DataProfileViewer.exe.  
  
 Это средство просмотра отображает запрошенные профили и вычисляемые результаты в нескольких панелях и имеет дополнительную возможность выполнить углубленную детализацию и просмотреть подробные сведения.  
  
 Панель**Профили**   
 На панели **Профили** отображаются профили, запрошенные в задаче "Профилирование данных". Чтобы просмотреть вычисляемые результаты профиля, выделите профиль на панели **Профили** , и результаты отобразятся на других панелях средства просмотра.  
  
 Панель**результатов**   
 На панели **Результаты** сводка вычисляемых результатов профиля отображается в одной строке. Так, при запросе **Профиль распределения длины столбцов**, в этой строке будут указаны минимальная длина и максимальная длина, а также число строк. Для большинства профилей эту строку можно выбрать на панели **Результаты** , чтобы просмотреть дополнительные сведения на дополнительной панели **Сведения** .  
  
 Панель**Сведения**   
 Для большинства типов профилей панель **Сведения** отображает дополнительную информацию о результатах профиля, выбранного на панели **Результаты** . Например, при запросе **Профиль распределения длины столбцов**на панели **Сведения** будет отображена длина каждого найденного столбца. На этой панели отображается также количество и выраженная в процентах доля строк, в которых значением столбца является длина столбца.  
  
 Для трех типов профилей, вычисляемых на основе более чем одного столбца ("Потенциальный ключ", "Функциональная зависимость" и "Включение значений"), на панели **Сведения** отображаются нарушения ожидаемой связи. Например, если пользователь запрашивает «Профиль потенциального ключа», на панели «Сведения» отображаются значения-дубликаты, нарушающие требование уникальности, которому должен удовлетворять потенциальный ключ.  
  
 Если доступен источник данных, используемый для вычисления профиля, можно дважды щелкнуть строку в панели **Сведения** , чтобы вывести соответствующие строки в панели **Углубленная детализация** .  
  
 Панель**Углубленная детализация**   
 На панели **Сведения** можно дважды щелкнуть строку, чтобы увидеть соответствующие строки данных на панели **Углубленная детализация** , если выполняются следующие условия:  
  
-   Доступен источник данных, который используется для вычисления профиля.  
  
-   У пользователя имеется разрешение на просмотр данных.  
  
 Чтобы подключить базу данных-источник к запросу углубленной детализации, средство просмотра профиля данных использует проверку подлинности Windows и учетные данные текущего пользователя. Средство просмотра профиля данных не использует сведения о соединении, хранящиеся в пакете, который запустил задачу «Профилирование данных».  
  
> [!IMPORTANT]  
>  Возможность углубленной детализации, которая доступна в средстве просмотра профиля данных, отправляет активные запросы к исходному источнику данных. Эти запросы могут отрицательно повлиять на производительность сервера.  
>   
>  Если детализация углублением выполняется из выходного файла, созданного некоторое время назад, запросы углубленной детализации могут возвратить набор строк, отличающихся от тех, на основе которых вычислялись первоначальные выходные данные.  
  
 Дополнительные сведения о пользовательском интерфейсе средства просмотра профилей данных см. в разделе [Data Profile Viewer F1 Help](../../integration-services/control-flow/data-profile-viewer-f1-help.md).  
  
## <a name="data-profile-viewer-f1-help"></a>Справка F1 средства просмотра профиля данных
  Используйте средство просмотра профиля данных для просмотра выхода задачи «Профилирование данных».  
  
 Дополнительные сведения об использовании средства просмотра профиля данных см. в разделе [Средство просмотра профиля данных](../../integration-services/control-flow/data-profile-viewer.md). Дополнительные сведения об использовании задачи "Профилирование данных", создающей профиль, который можно проанализировать с помощью средства просмотра профиля данных, см. в разделе [Установка задачи "Профилирование данных"](../../integration-services/control-flow/setup-of-the-data-profiling-task.md).  
  
### <a name="static-options"></a>Статические параметры  
 **Открыть**  
 Нажмите, чтобы просмотреть сохраненный файл, содержащий выход задачи «Профилирование данных»  
  
 Панель**Профили**   
 Раскройте дерево на панели **Профили** , чтобы увидеть, какие профили включены в выход. Выберите профиль, чтобы посмотреть результаты для этого профиля.  
  
 Панель**Сообщения**   
 Отображает сообщения о состоянии.  
  
 Панель**Углубленная детализация**   
 Отображает строки данных, соответствующие значению выхода, если доступен источник данных, который использовался задачей «Профилирование данных».  
  
 Например, при просмотре выхода профиля распределения значений столбцов для столбца US State, панель **Подробное распределение значений** может содержать строку «WA». Дважды щелкните строку на панели **Подробное распределение значений** , чтобы увидеть на панели детализации строки данных, в которых значением столбца штата является "WA".  
  
### <a name="dynamic-options"></a>Динамические параметры  
  
#### <a name="profile-type--column-length-distribution-profile"></a>Тип профиля = Профиль распределения длины столбцов  
  
##### <a name="column-length-distribution-profile---column-pane"></a>Профиль распределения длины столбцов — панель \<столбец>  
 **Минимальная длина**  
 Отображает минимальную длину значений в этом столбце.  
  
 **Максимальная длина**  
 Отображает максимальную длину значений в этом столбце.  
  
 **Без учета начальных пробелов**  
 Показывает, какое значение имело свойство **IgnoreLeadingSpaces** при вычислении этого профиля (True или False). Это свойство задается на странице **Запросы профиля** задачи «Профилирование данных».  
  
 **Без учета конечных пробелов**  
 Показывает, какое значение имело свойство **IgnoreTrailingSpaces** при вычислении этого профиля (True или False). Это свойство задается на странице **Запросы профиля** задачи «Профилирование данных».  
  
 **Количество строк**  
 Отображает число строк в таблице или представлении.  
  
##### <a name="detailed-length-distribution-pane"></a>Панель «Подробное распределение длины»  
 **Длина**  
 Отображает длины столбцов, обнаруженные в профилируемом столбце.  
  
 **Count**  
 Отображает число строк, в которых значение профилируемого столбца имело длину, указанную в столбце **Длина** .  
  
 **Процент**  
 Отображает процент строк, в которых значение профилируемого столбца имело длину, указанную в столбце **Длина** .  
  
#### <a name="profile-type--column-null-ratio-profile"></a>Тип профиля = Профиль соотношения значений NULL в столбцах  
  
##### <a name="column-null-ratio-profile---column-pane"></a>Профиль соотношения значений NULL в столбцах — панель \<столбец>  
 **Количество значений NULL**  
 Отображает число строк, в которых профилируемый столбец содержит значение NULL.  
  
 **Процент значений NULL**  
 Отображает процент строк, в которых профилируемый столбец содержит значение NULL.  
  
 **Количество строк**  
 Отображает число строк в таблице или представлении.  
  
#### <a name="profile-type--column-pattern-profile"></a>Тип профиля = Профиль шаблона столбцов  
  
##### <a name="column-pattern-profile---column-pane"></a>Профиль шаблона столбца — панель \<столбец>  
 **Количество строк**  
 Отображает число строк в таблице или представлении.  
  
##### <a name="pattern-distribution-pane"></a>Панель «Распределение шаблонов»  
 **Шаблон**  
 Отображает шаблоны, вычисляемые для профилируемого столбца.  
  
 **Процент**  
 Отображает процент строк, значения которых соответствуют шаблону, отображаемому в столбце **Шаблон** .  
  
#### <a name="profile-type--column-statistics-profile"></a>Тип профиля = Профиль статистики столбцов  
  
##### <a name="column-statistics-profile---column-pane"></a>Профиль статистики столбцов — панель \<столбец>  
 **Минимальные**  
 Отображает минимальное значение, обнаруженное в профилируемом столбце.  
  
 **Максимум**  
 Отображает максимальное значение, обнаруженное в профилируемом столбце.  
  
 **Среднее**  
 Отображает среднее значение по профилируемому столбцу.  
  
 **Стандартное отклонение**  
 Отображает стандартное отклонение для значений профилируемого столбца.  
  
#### <a name="profile-type--column-value-distribution-profile"></a>Тип профиля = Профиль распределения значений столбцов  
  
##### <a name="column-value-distribution-profile---column-pane"></a>Профиль распределения значений столбцов — панель \<столбец>  
 **Количество различных значений**  
 Отображает число различных значений в профилируемом столбце.  
  
 **Количество строк**  
 Отображает число строк в таблице или представлении.  
  
##### <a name="detailed-value-distribution-pane"></a>Панель «Подробное распределение значений»  
 **Значение**  
 Отображает уникальные значения, обнаруженные в профилируемом столбце.  
  
 **Count**  
 Отображает число строк, в которых профилируемый столбец имеет значение, указанное в столбце **Значение** .  
  
 **Процент**  
 Отображает процент строк, в которых профилируемый столбец имеет значение, указанное в столбце **Значение** .  
  
#### <a name="profile-type--candidate-key-profile"></a>Тип профиля = Профиль потенциальных ключей  
  
##### <a name="candidate-key-profile---table-pane"></a>Профиль потенциальных ключей — панель \<столбец>  
 **Ключевые столбцы**  
 Отображает столбцы, которые были выбраны для профилирования, как потенциальные ключи.  
  
 **Сила ключа**  
 Отображает силу (в процентах) потенциального ключевого столбца или сочетания столбцов. Сила ключа менее 100% означает наличие повторяющихся значений.  
  
##### <a name="key-violations-pane"></a>Панель «Нарушения ключа»  
 **\<Столбец1>, \<Столбец2> и т. д.**  
 Отображает повторяющиеся значения, обнаруженные в профилируемом столбце.  
  
 **Count**  
 Отображает число строк, в которых указанный столбец имеет значение, показанное в первом столбце.  
  
#### <a name="profile-type--functional-dependency-profile"></a>Тип профиля = Профиль функциональной зависимости  
  
##### <a name="functional-dependency-profile-pane"></a>Панель «Профиль функциональной зависимости»  
 **Определяющие столбцы**  
 Отображает столбец или столбцы, выбранные в качестве определяющих. Например, поскольку одному почтовому индексу США всегда соответствует один и тот же штат, поле почтового индекса является определяющим.  
  
 **Зависимые столбцы**  
 Отображает столбец или столбцы, выбранные в качестве зависимых. Например, поскольку одному почтовому индексу США всегда соответствует один и тот же штат, поле штата является зависимым.  
  
 **Степень функциональной зависимости**  
 Отображает силу (в процентах) функциональной зависимости столбцов. Сила ключа менее 100% означает, что в некоторых случаях определяющее значение не определяет зависимое. В приведенном примере, где одному почтовому индексу США должен соответствовать один и тот же штат, это может свидетельствовать о недопустимости одного из значений штата.  
  
##### <a name="functional-dependency-violations-pane"></a>Панель «Нарушения функциональной зависимости»  
  
> [!NOTE]  
>  Высокий процент ошибочных значений данных может привести к непредвиденным результатам в профиле функциональной зависимости. Например, 90% строк могут содержать значение штата «WI» для почтового кода «98052». В профиле в качестве нарушения приведены строки с правильным значением штата «WA».  
  
 **\<имя определяющего столбца>**  
 Отображает значение определяющего столбца или сочетания столбцов для данного случая нарушения функциональной зависимости.  
  
 **\<имя зависимого столбца>**  
 Отображает значение зависимого столбца для данного случая нарушения функциональной зависимости.  
  
 **Число несущего множества**  
 Отображает число строк, в которых определяющий столбец определяет зависимый столбец.  
  
 **Число нарушений**  
 Отображает число строк, в которых определяющий столбец не определяет зависимый столбец. (Это строки, в которых зависимым является значение, показанное в столбце **\<имя зависимого столбца>**.)  
  
 **Процент несущего множества**  
 Отображает процент строк, в которых определяющий столбец определяет зависимый столбец.  
  
#### <a name="profile-type--value-inclusion-profile"></a>Тип профиля = Профиль включения значений  
  
##### <a name="value-inclusion-profile-pane"></a>Панель «Профиль включения значений»  
 **Побочные столбцы подмножества**  
 Отображает столбец или сочетание столбцов, которые были профилированы для определения того, входят ли они в столбцы надмножества.  
  
 **Побочные столбцы надмножества**  
 Отображает столбец или сочетание столбцов, которые были профилированы для определения того, включают ли они значения в столбцах подмножества.  
  
 **Интенсивность включений**  
 Отображает силу (в процентах) перекрытия данных между столбцами. Сила ключа менее 100% означает, что в некоторых случаях значение в подмножестве не обнаружено среди значений в надмножестве.  
  
##### <a name="inclusion-violations-pane"></a>Панель «Нарушения включения»  
 **\<Столбец1>, \<Столбец2> и т. д.**  
 Отображает значения в столбце или столбцах подмножества, не обнаруженные в столбце или столбцах надмножества.  
  
 **Count**  
 Отображает число строк, в которых указанный столбец имеет значение, показанное в первом столбце.  
  
