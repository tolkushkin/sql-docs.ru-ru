---
title: Определение источника данных | Документация Майкрософт
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e52d6b6ef2a98089f17fe83a55d50b7693dbbc1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404016"
---
# <a name="lesson-1-2---defining-a-data-source"></a>Занятие 1 – 2-Определение источника данных
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

После создания проекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] работа с проектом обычно начинается с определения одного или нескольких источников данных, которые будут использоваться в этом проекте. Для определения источника данных нужно задать строку соединения, которая будет использована для подключения к этому источнику данных. Дополнительные сведения см. в разделе [Создание источника данных (многомерные службы SSAS)](../multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
В следующей задаче предстоит определить образец базы данных AdventureWorksDWSQLServer2012 в качестве источника данных для проекта учебника по службам [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Хотя эта база данных в данном случае расположена на локальном компьютере, часто исходные базы данных размещаются на одном или нескольких удаленных компьютерах.  
  
### <a name="to-define-a-new-data-source"></a>Определение нового источника данных  
  
1.  В обозревателе решений (справа от окна Microsoft Visual Studio) щелкните правой кнопкой мыши папку **Источники данных**и выберите пункт **Создать источник данных**.  
  
2.  На странице **Мастер источников данных** в **мастере источников данных**нажмите кнопку **Далее** , чтобы открыть страницу **Выбор метода определения соединения** .  
  
3.  На странице **Выбор метода определения соединения** можно определить источник данных на основе нового соединения, существующего соединения или предварительно определенного объекта источника данных. В этом учебнике будет определен источник данных на основе нового соединения. Убедитесь в том, что выбран параметр **Создать источник данных, основанный на существующем или на новом соединении** , а затем нажмите кнопку **Создать**.  
  
4.  В диалоговом окне **Диспетчер соединений** определяются свойства соединения для источника данных. Убедитесь в том, что в списке **Поставщик** выбран **Собственный поставщик данных OLE DB\Собственный клиент SQL Server 11.0** .  
  
    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] также поддерживают других поставщиков, которые доступны в списке **Поставщик** .  
  
5.  В текстовом поле **Имя сервера** введите **localhost**.  
  
    Чтобы подключиться к именованному экземпляру на локальном компьютере, введите **localhost\\<instance name>** . Чтобы подключиться к конкретному компьютеру вместо локального, введите имя компьютера или его IP-адрес.  
  
6.  Убедитесь в том, что выбран параметр **Использовать проверку подлинности Windows** . В поле списка **Выберите или введите имя базы данных** выберите **AdventureWorksDW2012**.  
  
7.  Нажмите кнопку **Проверить соединение** , чтобы проверить соединение с базой данных.  
  
8.  Нажмите кнопку **ОК**, а затем нажмите кнопку **Далее**.  
  
9. На странице мастера **Сведения об олицетворении** определяются учетные данные безопасности, которые будут использованы в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] для подключения к источнику данных. Олицетворение влияет на учетную запись Windows, которая используется для подключения к источнику данных при выборе проверки подлинности Windows. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] не поддерживает олицетворение для обработки объектов OLAP. Выберите параметр **Использовать учетную запись службы**и нажмите кнопку **Далее**.  
  
10. На странице **Завершение работы мастера** примите имя по умолчанию **Adventure Works DW 2012**, а затем нажмите кнопку **Готово** , чтобы создать источник данных.  
  
> [!NOTE]  
> Чтобы изменить свойства существующего источника данных, дважды щелкните этот источник в папке **Источники данных** , чтобы показать свойства источника данных в **конструкторе источников данных**.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
[Определение представления источников данных](lesson-1-3-defining-a-data-source-view.md)  
  
## <a name="see-also"></a>См. также  
[Создание источника данных (многомерные службы SSAS)](../multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
