---
title: Средство просмотра данных | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataviewer.f1
helpviewer_keywords:
- Data Viewer dialog box
ms.assetid: 6351309a-688f-4e82-9697-1712130f10a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 100dbd947b8b5b8de340bfd45a4d2705a4b0d475
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726983"
---
# <a name="data-viewer"></a>Средство просмотра данных

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Если настроен путь для применения средства просмотра данных, то это средство отображает данные буфер за буфером по мере перемещения данных между двумя компонентами потока данных.  
  
## <a name="options"></a>Параметры  
 **Зеленая стрелка**  
 Переход к данным в следующем буфере. Если данные можно переместить в одиночный буфер, то этот параметр недоступен.  
  
 **Отсоединить**  
 Отсоединить средство просмотра данных.  
  
 **Примечание.** Отсоединение средства просмотра данных не приводит к удалению самого средства. При отсоединении средства просмотра данных данные продолжают следовать по пути, однако данные в средстве просмотра не обновляются для поддержания соответствия с данными в каждом буфере.  
  
 **Присоединить**  
 Присоединить средство просмотра данных.  
  
 **Примечание.** Когда средство просмотра данных присоединяется, оно отображает информация из каждого буфера потока данных, а затем приостанавливает свою работу. Можно перемещаться от буфера к буферу с помощью зеленой стрелки.  
  
 **Скопировать данные**  
 Копирование данных текущего буфера в буфер обмена.  
  
## <a name="see-also"></a>См. также:  
 [Отладка потока данных](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
  
