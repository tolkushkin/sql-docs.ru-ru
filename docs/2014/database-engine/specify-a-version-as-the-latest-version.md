---
title: Указание версии в качестве последней версии | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], latest version
- latest file version specified
- file versions [SQL Server]
ms.assetid: 407dffb1-3ecf-461e-835d-124781f26ee7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f34631e979ded7a329939c23a758ccc0c9aea959
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773480"
---
# <a name="specify-a-version-as-the-latest-version"></a>Указание версии в качестве последней
  При регистрации файла в системе управления версиями версия этого файла становится последней. Пользователи, извлекающие последнюю версию, получают локальные копии возвращенного до этого элемента.  
  
 Однако в некоторых ситуациях в качестве последней необходимо назначить более раннюю версию элемента. Например, было выполнено извлечение файла, его изменение и последующая регистрация. После этого возникла необходимость отмены изменений. Так как элемент был возвращен, непосредственная отмена соответствующего исходного извлечения невозможна. В этой ситуации можно назначить исходную извлеченную версию в качестве последней версии элемента.  
  
 Существует несколько способов назначения последней версии.  
  
-   **Закрепление версии**. При закреплении версии файла более поздние версии, чем закрепленная, не удаляются. Кроме того, можно снять закрепление ранее закрепленного файла. При этом версия файла, возвращенная позже всех, становится последней. Однако извлечь закрепленный файл невозможно.  
  
-   **Откат до указанной версии**. При откате до какой-либо версии все более поздние версии удаляются из системы управления версиями. Затем можно извлечь последнюю из оставшихся версий.  
  
### <a name="to-pin-a-version"></a>Закрепление версии  
  
1.  Откройте решение в среде [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  В обозревателе решений выберите файл, который необходимо назначить в качестве последней версии.  
  
3.  На **файл** последовательно выберите пункты **системы управления версиями** и нажмите кнопку **ViewHistory**.  
  
4.  В **журнал** \<файл > диалоговом окне выберите версию, необходимо задать в качестве последней и нажмите кнопку **ПИН-код**.  
  
     Возле выбранной версии появится символ закрепления, указывающий, что теперь это текущая версия файла. Если в среде [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] загружена другая версия, программа предложит перезагрузить файл.  
  
### <a name="to-roll-back-to-a-version"></a>Выполнение отката до определенной версии  
  
1.  Откройте решение в среде [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  В обозревателе решений выберите элемент, который необходимо задать в качестве последней версии.  
  
3.  На **файл** последовательно выберите пункты **системы управления версиями** и нажмите кнопку **журнал**.  
  
4.  В **параметры журнала** диалоговом окне щелкните **ОК** для отображения **журнал файла** диалоговое окно.  
  
5.  В **журнал файла** выберите версию, необходимо указать в качестве последней версии и нажмите кнопку **отката**.  
  
     Появится сообщение, уведомляющее о том, что все версии после выбранной будут удалены.  
  
6.  Нажмите кнопку **Да** выполнить откат до выбранной версии.  
  
## <a name="see-also"></a>См. также  
 [Управление возвратами](../../2014/database-engine/manage-checkins.md)   
 [Возврат файлов](../../2014/database-engine/check-in-files.md)  
  
  
