---
title: Создать новую структуру интеллектуального анализа данных OLAP | Документация Майкрософт
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d0a12d7fad2deb138d2dac445492ffce55f1493a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62911310"
---
# <a name="create-a-new-olap-mining-structure"></a>создать новую структуру интеллектуального анализа OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Можно воспользоваться мастером интеллектуального анализа данных в службах [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , чтобы создать структуру интеллектуального анализа данных, в которой будут использоваться данные многомерной модели. Модели интеллектуального анализа данных, основанные на кубах OLAP, способны использовать столбец и его значения в таблицах фактов, измерениях и в группах мер в качестве атрибутов для анализа.  
  
### <a name="to-create-a-new-olap-mining-structure"></a>Создание новой структуры интеллектуального анализа OLAP  
  
1.  В обозревателе решений в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]щелкните правой кнопкой мыши папку **Структуры интеллектуального анализа данных** в проекте служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , а затем выберите пункт **Создать структуру интеллектуального анализа данных** для открытия мастера интеллектуального анализа данных.  
  
2.  На странице **Вас приветствует мастер интеллектуального анализа данных** нажмите кнопку **Далее**.  
  
3.  На странице **Выбор метода определения** установите флажок **На основе существующего куба**, а затем нажмите кнопку **Далее**.  
  
     При получении сообщения об ошибке "Не удается получить список поддерживаемых алгоритмов интеллектуального анализа данных" откройте диалоговое окно **Свойства проекта** и убедитесь, что вы указали имя экземпляра служб Analysis Services, который поддерживает многомерные модели. Создание моделей интеллектуального анализа данных в экземпляре служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] с поддержкой табличного моделирования невозможно.  
  
4.  На странице **Создать структуру интеллектуального анализа данных** примите решение, нужно создавать только структуру интеллектуального анализа данных либо структуру интеллектуального анализа данных вместе со связанной с ней моделью интеллектуального анализа данных. Обычно проще создать модель интеллектуального анализа данных одновременно, поскольку в этом случае вам будет выведено предложение о включении необходимых столбцов.  
  
     Если создается модель интеллектуального анализа данных, выберите нужный алгоритм интеллектуального анализа данных и нажмите кнопку **Далее**. Дополнительные сведения о выборе алгоритма интеллектуального анализа данных см. в разделе [Алгоритмы интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  На странице **Выбор измерения исходного куба** в разделе **Выбрать измерения исходного куба**найдите измерение, содержащее большую часть данных варианта.  
  
     Например, если вам нужно распознать группы заказчиков, можно выбрать измерение "Customer". Если нужно проанализировать приобретения по всем транзакциям, можно выбрать измерение "Sales Order Details". Для пользователя нет ограничений, связанных с использованием только этого измерения, однако запрос должен содержать все важные свойства, необходимые для анализа.  
  
     Нажмите кнопку **Далее**.  
  
6.  На странице **Выбор ключа варианта** в разделе **Атрибуты**выберите атрибут, который будет ключом структуры интеллектуального анализа данных, а затем нажмите кнопку **Далее**.  
  
     Обычно атрибут, который используется в качестве ключа в структуре интеллектуального анализа данных, также является ключом для измерения. Поэтому он будет также предварительно выбран.  
  
7.  На странице **Выбор столбцов уровня вариантов** в разделе **Связанные атрибуты и меры**выберите атрибуты и меры, содержащие значения, которые требуется добавить в качестве данных вариантов в структуру интеллектуального анализа данных. Нажмите кнопку **Далее**.  
  
8.  На странице **Использование столбцов для модели** в разделе **Структура модели интеллектуального анализа**сначала задайте прогнозируемый столбец, а затем выберите столбцы, которые следует использовать в качестве входных.  
  
    -   Установите флажок в самом левом столбце, чтобы включить данные в структуру интеллектуального анализа данных. В структуру можно включать столбцы, которые будут использоваться в качестве справочных, но не будут использоваться при анализе.  
  
    -   Установите флажок в столбце **Входные** , чтобы использовать атрибут как переменную при анализе.  
  
    -   Установите флажок в столбце **Predict** только для прогнозируемых атрибутов.  
  
     Обратите внимание, что столбцы, назначенные в качестве ключей, не могут использоваться для ввода или прогноза.  
  
     Нажмите кнопку **Далее**.  
  
9. На странице **Использование столбцов для модели** можно также добавлять и удалять вложенные таблицы в структуре интеллектуального анализа данных при помощи функций **Добавить вложенные таблицы** и **Вложенные таблицы**.  
  
     В модели интеллектуального анализа данных OLAP вложенная таблица представляет собой еще один набор данных куба, в котором установлена связь «один ко многим» с измерением, представляющим атрибуты варианта. Поэтому при открытии диалогового окна происходит предварительный выбор групп мер, которые уже связаны с измерением, выбранным в качестве таблицы варианта. В это время выполняется выбор другого измерения, которое содержит дополнительные сведения, нужные для выполнения анализа.  
  
     Например, при анализе заказчиков в качестве таблицы вариантов будет использоваться измерение [Customer]. Для вложенной таблицы можно также добавить причину, высказанную заказчиком при приобретении товара, которая содержится в измерении [Sales Reason].  
  
     При добавлении вложенных данных необходимо указать два дополнительных столбца:  
  
    -   Ключ вложенной таблицы: Это должен быть уже выбран на странице **Выбор ключа вложенной таблицы**.  
  
    -   Атрибуты или атрибуты для анализа: Странице **Выбор столбцов вложенной таблицы**содержит список мер и атрибутов выбора вложенной таблицы.  
  
        -   Для каждого атрибута, включаемого в модель, отметьте флажком пункт в левом столбце.  
  
        -   Если атрибут требуется использовать только для анализа, отметьте флажком пункт **Ввод**.  
  
        -   Если столбец требуется включить в качестве одного из прогнозируемых атрибутов для модели, выберите **Прогноз**.  
  
        -   Любой объект, который включается в структуру, но не указывается как вводимые данные или прогнозируемый атрибут, добавляется в структуру с флажком **Ignore**. Это означает, что данные обрабатываются при построении модели, однако не используются при анализе данных и доступны только при детализации. Это может быть удобно, если требуется включить сведения, такие как имена клиентов, но не хотите использовать их в анализ.  
  
     Нажмите кнопку **Завершить** , чтобы закрыть ту часть мастера, которая работает с вложенными таблицами. Если требуется добавить несколько вложенных столбцов, процесс можно повторить.  
  
10. На странице **Задание содержимого и типа данных столбцов** в разделе **Структура модели интеллектуального анализа данных**укажите тип содержимого и тип данных для каждого столбца.  
  
    > [!NOTE]  
    >  Модели интеллектуального анализа OLAP не поддерживают использование функции **Определить** для автоматического определения того, содержит ли столбец непрерывные или дискретные данные.  
  
     Нажмите кнопку **Далее**.  
  
11. На странице **Срез исходного куба** можно отфильтровать данные, используемые для создания структуры интеллектуального анализа данных.  
  
     Создание срезов куба позволяет ограничить данные, использующиеся для построения модели. Например, можно строить отдельные модели для каждого региона, создав срез иерархии Geography и  
  
    -   **Измерение**: Выбор соответствующего измерения из раскрывающегося списка.  
  
    -   **Иерархия**:  Выбор уровня иерархии измерения, по которому необходимо применить фильтр. Например, при создании среза по измерению [Geography] выбирается такой уровень иерархии, как [Region Country Name].  
  
    -   **Оператор**. Выберите оператор из списка.  
  
    -   **Критерий фильтра**: Введите значение или выражение для использования в качестве условия фильтра, или воспользуйтесь раскрывающимся списком, чтобы выбрать значение из списка членов, принадлежащих указанному уровню иерархии.  
  
         Например, при выборе измерения [Geography] и уровня иерархии [Region Country Name] раскрывающийся список будет содержать все допустимые страны, которые можно использовать в качестве условия фильтрации. Можно выбрать несколько элементов. В результате данные в структуре интеллектуального анализа данных будут ограничены данными куба из этих географических областей.  
  
    -   **Параметры**: Пропустите этот флажок. Это диалоговое окно поддерживает несколько сценариев фильтрации куба, однако он не важен при построении структуры интеллектуального анализа данных.  
  
     Нажмите кнопку **Далее**.  
  
12. На странице **Разбиение данных на обучающий и проверочный наборы данных** укажите, какой процент структуры интеллектуального анализа данных следует зарезервировать для проверки, или задайте максимальное количество проверочных вариантов. Нажмите кнопку **Далее**.  
  
     Если указать оба значения, используется наименьшее ограничение.  
  
13. На странице **Завершение работы мастера** введите имя новой структуры интеллектуального анализа данных OLAP и соответствующей первоначальной модели интеллектуального анализа данных.  
  
14. Нажмите кнопку **Готово**.  
  
15. На странице **Завершение работы мастера** появится возможность создания измерения модели интеллектуального анализа данных и/или куба при помощи измерения модели интеллектуального анализа данных. Эти параметры поддерживаются только для моделей, построенных с использованием следующих алгоритмов:  
  
    -   Алгоритм кластеризации (Майкрософт)  
  
    -   Алгоритм дерева принятия решений (Майкрософт)  
  
    -   Алгоритм ассоциативных правил Майкрософт  
  
     **Создать измерение модели интеллектуального анализа данных**: Установите этот флажок и введите имя измерения модели интеллектуального анализа данных. При использовании этого режима будет создано новое измерение в пределах первоначального куба, который использовался для построения структуры интеллектуального анализа данных. Это измерение можно использовать для детализации и проведения дальнейшего анализа. Поскольку измерение располагается в пределах куба, оно автоматически сопоставляется с измерением данных вариантов.  
  
     **Создать куб с использованием измерения модели интеллектуального анализа данных**: Установите этот флажок и введите имя для нового куба. При использовании этого режима будет создан новый куб, который будет содержать как существующие измерения, которые использовались для построения структуры, так и новое измерение интеллектуального анализа данных, содержащее результаты из модели.  
  
## <a name="see-also"></a>См. также  
 [Задачи и инструкции по структуре интеллектуального анализа данных](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
