---
title: Сопоставления параметров запросов с переменными в компонентах потока данных | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 92caab2b0631c80403c7367aeb98ae001a5e11eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901637"
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>Сопоставления параметров запросов с переменными в компонентах потока данных
  При настройке конфигурации источника OLE DB для использования параметризованных запросов можно сопоставить параметры с переменными.  
  
 В источнике OLE DB параметризованные запросы используются для фильтрации данных при подключении источника к источнику данных.  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>Сопоставление параметра запроса с переменной  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , содержащий необходимый пакет.  
  
2.  Чтобы открыть пакет, дважды щелкните его в обозревателе решений.  
  
3.  Щелкните вкладку **Поток данных** и перетащите источник OLE DB из **области элементов**в область конструктора.  
  
4.  Щелкните правой кнопкой источник OLE DB и выберите пункт **Правка**.  
  
5.  В окне **Редактор источника OLE DB**выберите диспетчер соединений OLE DB, предназначенный для подключения к источнику данных, или нажмите кнопку **Создать** , чтобы создать новый диспетчер соединений OLE DB.  
  
6.  Выберите параметр **Команда SQL** для режима доступа к данным, а затем введите параметризированный запрос панели **Текст команды SQL** .  
  
7.  Нажмите **Параметры**.  
  
8.  В диалоговом окне **Установка параметров запроса** сопоставьте каждый параметр в списке **Параметры** с переменной в списке **Переменные** или создайте переменную, щелкнув **\<Создать переменную>**. Нажмите кнопку **ОК**.  
  
    > [!NOTE]  
    >  Для сопоставления доступны только системные и пользовательские переменные, находящиеся в области видимости данного пакета, родительского контейнера, такого как «цикл по каждому элементу», или задачи потока данных, содержащей компоненты потока данных, доступные для сопоставления. Переменная должна иметь тип данных, совместимый со столбцом в предложении WHERE, которому назначен параметр.  
  
9. Чтобы просмотреть до 200 строк данных, возвращаемых запросом, нажмите кнопку **Предварительный просмотр** .  
  
10. Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
## <a name="see-also"></a>См. также  
 [Источник OLE DB](ole-db-source.md)   
 [Преобразование «Уточняющий запрос»](transformations/lookup-transformation.md)  
  
  
