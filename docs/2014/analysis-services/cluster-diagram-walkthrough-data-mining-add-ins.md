---
title: Кластер Пошаговое руководство по диаграмме (надстройки интеллектуального анализа данных) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc2df250b0728934f258c8217d29adfb91e66ff5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66087905"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>Пошаговое руководство по диаграмме кластеров (надстройки интеллектуального анализа данных)
  После создания модели кластеризации, можно импортировать его в Visio с помощью **кластера** фигуры, а затем продолжить настройку и Улучшение макета. **Фигуры интеллектуального анализа данных для Visio** включают следующие пользовательские элементы управления для работы с диаграммами интеллектуального анализа данных:  
  
-   создание элементов управления для диаграммы кластеров.  
  
     Эти параметры являются частью **мастера кластера** , запускается, когда форма перемещается в рабочее пространство Visio.  
  
-   **Data Mining Layout** панели инструментов  
  
     Эти параметры добавляется в рабочую область Visio для последующей работы с фигурами интеллектуального анализа данных. Параметры различаются в зависимости от используемого типа модели интеллектуального анализа данных.  
  
## <a name="build-a-cluster-diagram"></a>Создание диаграммы кластеров  
 Это пошаговое руководство демонстрирует, как можно создать и настроить диаграмму кластеризации в Visio.  
  
 Чтобы следовать описанным шагам, следует иметь готовую модель кластеризации. Если у вас нет модели, используйте [мастера кластера &#40;интеллектуального анализа данных надстройки для Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) мастера и создать модель с помощью набора данных для обучения в образце книги, используя параметры по умолчанию.  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>Используйте мастер фигур Visio в кластере  
  
1.  Если вы не видите **фигур интеллектуального анализа данных Microsoft** в **фигур** выберите **Дополнительные фигуры**выберите **открыть набор элементов**и откройте шаблон из места установки по умолчанию.  
  
     \<диск >: \Program files\Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Перетащите **кластера** фигуры на страницу.  
  
3.  На странице приветствия **мастера фигур Visio в кластере**, нажмите кнопку **Далее**.  
  
4.  На **выбрать источник данных** странице **мастера кластера**, Выбор соединения с [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] сервер, содержащий модели интеллектуального анализа данных, которую требуется визуализировать.  
  
5.  Выберите модель соответствующие интеллектуального анализа данных и нажмите кнопку **Далее**.  
  
     Чтобы убедиться, что вы выбираете модель кластеризации, изучите описание на **свойства** области.  
  
6.  Если подключение установлено успешно, на странице **параметры диаграммы кластеров**, выберите тип диаграммы кластеров для включения в презентацию Visio:  
  
     **Отображать только фигуры кластеров**  
     Данный параметр создает простую диаграмму кластеров, при этом каждый кластер может отображаться в виде прямоугольника или любой другой формы, которую вы можете выбрать.  
  
     **Отображать кластеры с диаграммой характеристик**  
     Этот параметр позволяет создать диаграмму, аналогичную предыдущей, однако внутри ее форм представлены гистограммы, описывающие характеристики кластера.  
  
     ![Пример диаграммы характеристик кластера в Visio](media/dm13-visio-cluster-samplecharshape.gif "пример диаграммы характеристик кластера в Visio")  
  
     **Отображать кластеры с диаграммой сравнения**  
     Этот параметр создает точно такую же схему, что и диаграмма кластеров, однако в ней приводится список характеристик текущего кластера, которыми он наиболее сильно отличается от других кластеров.  
  
     Можно переключиться на другой тип диаграммы после того, как мастер создаст диаграмму. Для этого щелкните кластер правой кнопкой мыши и выберите новый тип диаграммы. Теперь выберите вариант, **Показывать кластеры с диаграммой характеристик**.  
  
7.  Оставьте для параметра **количество строк в диаграмме**, 5.  
  
     Этот параметр не изменяет количество кластеров в модели; он просто ограничивает количество атрибутов, которые могут отображаться в виде функции каждого кластера.  
  
     Однако параметр действует в качестве фильтра данных диаграммы, поэтому невозможно увеличить количество элементов в более поздней версии.  
  
8.  Щелкните **Дополнительно**.  
  
     **Варианты создания кластера** диалоговое окно также настраивается внешний вид форм, используемых в диаграмме. Можно изменить цвета, используемые на диаграмме, и фигуру, используемую для кластеров.  
  
     **Переменная заливки** управления не работает в Office 2013.  
  
     ![Нажмите кнопку Дополнительно, чтобы выбрать цвета фигуры](media/dm13-visio-clusteroptions-advanced.gif "нажмите кнопку Дополнительно, чтобы выбрать цвета фигуры")  
  
     **Совет.** Некоторые цвета могут быть изменены позже с помощью тем Visio и элементов управления редактированием фигур. Однако темы Visio также переопределяют некоторые из выбранных цветов, поэтому рекомендуется начать с цветами по умолчанию и применять изменения постепенно.  
  
9. Нажмите кнопку **Готово** для создания диаграммы.  
  
     Мастер извлекает сведения из модели интеллектуального анализа данных, отображает фигуры и заполняет каждый кластер атрибутами и значениями.  
  
     ![Сеть зависимостей](media/dm13-visiodepnet-defaultgraph.gif "сеть зависимостей")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Просмотр и изменение законченной диаграммы  
 После завершения создания диаграммы можно продолжить настройку внешнего вида с помощью элементов управления Visio, как показано в следующем примере.  
  
 ![Диаграмма кластеров, настроенная с помощью Visio](media/dm13-visio-clustercomplete1.gif "Диаграмма кластеров, настроенная с помощью Visio")  
  
 Все основные формы кластеров формируются мастером. Используйте следующие средства для обновления и персонализации диаграммы.  
  
1.  Перетащите ползунок в **варианты создания кластера** элемента управления, чтобы отфильтровать слабые связи и упростить диаграмму.  
  
2.  Используйте Visio **страница повторного макета** параметр, чтобы поэкспериментировать с различными макетами кластера.  
  
3.  Используйте **соединители** параметр **разработки** tab для изменения стиля соединителя таким образом чтобы линии не пересекали кластеры.  
  
4.  Нажмите кнопку **Add-Ins** ленты, а затем укажите одну из панелей, используемых для работы с диаграммами интеллектуального анализа данных:  
  
     **Макет**  
     Оптимизирует расположение кластеров для улучшения их размещения на текущей странице.  
  
     **Изменение размера страницы**  
     Этот элемент управления был предназначен для предыдущих версий HTML. Используйте элементы управления изменением размера страницы Visio.  
  
     **Описание**  
     Если выбран кластер, щелкните этот параметр, чтобы отобразить сведения о кластере.  
  
     ![Щелкните описание для получения сведений о кластере](media/dm13-visio-cluster-description-control.gif "щелкните описание для получения сведений о кластере")  
  
     **Интенсивность ребра**  
     Указывает степень достоверности для линий, соединяющих кластеры.  
  
     Однако, если вы примените любое особое форматирование, отличное от форматирования по умолчанию мастера, в том числе с использованием некоторых фонов, возможно, эти цифры будут невидимы.  
  
     **Slider**  
     Фильтрует строки между кластерами. Перемещение ползунка вверх удаляет все, кроме наиболее важных взаимосвязей.  
  
     **Заливка**  
     Этот элемент управления не работает в Office 2013.  
  
5.  Используйте **сдвига и масштабирования** управления, в **область задач** области Visio **представление** ленты, чтобы сосредоточиться на наборе кластеров и перемещать диаграмму.  
  
6.  Щелкните правой кнопкой мыши любой кластер, чтобы увидеть параметры, характерные для формы кластера.  
  
    -   Изменение стиля диаграммы.  
  
    -   Добавление диаграммы характеристик кластера.  
  
    -   Добавление диаграммы сравнения кластеров.  
  
## <a name="see-also"></a>См. также  
 [Устранение неполадок с диаграммами интеллектуального анализа данных Visio &#40;надстройки интеллектуального анализа данных SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
