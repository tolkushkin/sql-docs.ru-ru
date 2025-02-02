---
title: Регистрация сборки базы данных-диалоговое окно (службы Analysis Services — многомерные данные) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidevstudio.assembly.registerassembly.f1
ms.assetid: 0c07cc87-fc94-456f-b878-7b23e39772b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06647219ca5768495620bb1db60cf34910844f25
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070473"
---
# <a name="register-database-assembly-dialog-box-analysis-services---multidimensional-data"></a>Диалоговое окно «Регистрация сборки базы данных» (службы Analysis Services — многомерные данные)
  Используйте диалоговое окно **Регистрация серверной сборки**в среде [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] для установки свойств ссылки на сборку в базе данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Диалоговое окно **Регистрация серверной сборки** вызывается, если щелкнуть правой кнопкой мыши папку "Сборки" экземпляра или базы данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] в **обозревателе объектов** и выбрать пункт **Создать сборку**.  
  
## <a name="options"></a>Параметры  
  
|Термин|Определение|  
|----------|----------------|  
|**Тип**|Выбирает тип ссылки на сборку. Доступны следующие значения:<br /><br /> **Сборка .NET** <br />                      Ссылка указывает на сборку [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework.<br /><br /> **COM DLL** <br />                      Ссылка на сборку указывает на библиотеку COM.<br /><br /> <br /><br /> **\*\* Примечание по безопасности \* \***  сборки COM могут представлять угрозу безопасности. По этой причине, а также по ряду других сборки COM в службах [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)]являются устаревшими. Поддержка сборок COM в последующих версиях может быть прекращена.|  
|**Имя файла**|Введите полный путь и имя файла сборки .NET или библиотеки COM.|  
|**...**|Щелкните, чтобы открыть диалоговое окно **Открыть** , и выберите полный путь и имя файла для сборки .NET или библиотеки COM.|  
|**Имя сборки**|Введите имя для ссылки на сборку.<br /><br /> Примечание. Изменение этого значения не изменяет имя сборки, на который ссылается ссылки на сборку, но зато измените имя, используемое с [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] экземпляра или базы данных, при ссылке на сборку.|  
|**Включить отладочные данные**|Выберите этот параметр для включения отладочных данных (если есть) для сборки .NET или библиотеки СОМ.|  
|**Отметка времени создания**|Отображает дату и время создания ссылки на сборку.|  
|**Последнее обновление схемы**|Отображается дата и время последнего обновления метаданных для ссылки на сборку.|  
|**Source**|Отображается источник ссылки на сборку. Обычно это свойство содержит полный путь и имя файла сборки, на которую указывает ссылка.|  
|**Безопасный**|Выберите этот параметр для использования этого набора разрешений для ссылки сборки. При выборе этого параметра сборке разрешаются только внутренние расчеты и доступ к локальным базам данных. Код, выполняемый сборкой в таком режиме, не может получать доступ к внешним системным ресурсам — файлам, сети, переменным среды и реестру.<br /><br /> **\*\* Примечание по безопасности \* \***  этот параметр является рекомендованной установкой разрешений для сборок, которые выполняют задачи вычисления и данных управления без доступа к ресурсам за пределами [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Он представляет собой наиболее ограниченный набор разрешений.|  
|**Внешний доступ**|Выберите этот параметр для использования этого набора разрешений для ссылки сборки. При выборе этого параметра сборке разрешаются только внутренние расчеты и доступ к локальным базам данных. Код, выполняемый сборкой в таком режиме, может получать доступ к внешним системным ресурсам — файлам, сети, переменным среды и реестру.<br /><br /> **\*\* Примечание по безопасности \* \***  этот вариант рекомендуется для сборок, которые обращаются к ресурсам за пределами [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. По умолчанию сборки в таком режиме выполняются от имени учетной записи данной службы. Это код в такой сборке может явно олицетворять вызывающего [!INCLUDE[msCoName](../includes/msconame-md.md)] контекст безопасности проверки подлинности Windows. Так как по умолчанию сборка выполняется как учетная запись службы, разрешение на выполнение сборок в таком режиме нужно предоставлять только ролям, которым доверено выполняться как учетным записям службы. Этот параметр представляет менее строгие разрешения, чем **Безопасный**, но более строгие, чем **Не ограничено**.|  
|**Неограниченный**|Выберите этот параметр для использования этого набора разрешений для ссылки сборки. Если выбран этот параметр, сборка имеет неограниченный доступ к ресурсам как внутренним, так и внешним. Код, выполняемый из сборки в таком режиме, может вызывать неуправляемый код.<br /><br /> **\*\* Примечание по безопасности \* \***  этот параметр не рекомендуется, если сборки требуется неограниченный доступ. С точки зрения безопасности этот параметр идентичен параметру **Внешний доступ**. Однако сборки в режиме **Внешний доступ** обеспечивают различные надежные и устойчивые средства защиты, которых нет у сборок в данном режиме. Задание этого режима позволяет коду в сборке выполнять запрещенные операции в пространстве процессов и таким образом можно нарушать устойчивость и масштабируемость служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Этот режим представляет собой наименее ограничивающий набор разрешений и должен использоваться с осторожностью.|  
|**Использовать указанные имя пользователя и пароль**|Выберите этот режим, чтобы объект служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] использовал учетные данные для безопасного доступа определенной пользовательской учетной записи.|  
|**Имя пользователя**|Введите домен и имя учетной записи пользователя для использования выбранным объектом служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Домен и имя пользовательской учетной записи используют следующий формат:<br /><br /> *\<Имя домена >* **\\**  *\<учетную запись пользователя >*<br /><br /> Примечание. Этот параметр будет включен только в случае выбора параметра **Использовать указанные имя пользователя и пароль** .|  
|**Пароль**|Введите домен и имя учетной записи пользователя для использования выбранным объектом служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Использовать учетную запись службы**|Выберите этот параметр, чтобы объект служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] использовал учетные данные безопасности, связанные со службой [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , управляющей объектом.|  
|**Использовать учетные данные текущего пользователя**|Выберите этот параметр, чтобы объект служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] использовал учетные данные для безопасного доступа учетной записи текущего пользователя.|  
|**Default**|Выберите этот режим, чтобы использовать пользовательскую учетную запись по умолчанию для служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Этот режим равноценен установке параметра **Использовать учетные данные текущего пользователя** .|  
|**Описание**|Введите описание для ссылки на сборку.|  
  
## <a name="see-also"></a>См. также  
 [Конструкторы и диалоговые окна служб Analysis Services &#40;многомерных данных&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Управление сборками многомерной модели](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
