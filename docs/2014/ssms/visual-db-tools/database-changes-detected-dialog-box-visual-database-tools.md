---
title: Диалоговое окно "Обнаружены изменения базы данных" (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.schema.databasechangesdetected
- vdtsql.chm:65543
- vdtsql.chm:65554
ms.assetid: 91f13086-371f-46a2-9f46-804c1415f3ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d5850ce71e483ea33bb99972c243140a63da5f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270537"
---
# <a name="database-changes-detected-dialog-box-visual-database-tools"></a>Диалоговое окно «Обнаружены изменения базы данных» (визуальные инструменты для баз данных)
  Это диалоговое окно появляется при попытке сохранить диаграмму базы данных или выбранных таблиц, но при этом некоторые объекты базы данных, на которых распространяется действие сохранения, являются устаревшими по сравнению с базой данных. Принятие изменений, показанных в диалоговом окне, обновит базу данных до соответствия с диаграммой и перезапишет изменения, сделанные другими пользователями.  
  
> [!NOTE]  
>  Несмотря на то что изменения, произведенные с таблицей или диаграммой базы данных, нельзя отменить, они не будут сохранены в базе данных до тех пор, пока не будет сохранена таблица или диаграмма. Можно отказаться от любых несохраненных изменений, выбрав **Нет** и закрыв все открытые диаграммы без сохранения.  
  
## <a name="options"></a>Параметры  
 **Предупреждать об обнаружении различий**  
 Укажите, выводить ли это диалоговое окно при следующей попытке сохранить диаграмму базы данных или выбранные таблицы. Установленный флажок означает, что диалоговое окно будет появляться каждый раз при попытке сохранить диаграмму, являющуюся устаревшей по отношению к базе данных. Отсутствие флажка означает, что диалоговое окно не будет появляться. По умолчанию этот флажок установлен. Если флажок был снят, его можно установить заново в диалоговом окне **Параметры** .  
  
 **Да**  
 Обновить базу данных, применив все показанное в списке.  
  
 **Нет**  
 Отменить сохранение.  
  
> [!NOTE]  
>  Чтобы обновить диаграмму до соответствия с базой данных, закройте ее без сохранения изменений, щелкните правой кнопкой мыши на обозревателе серверов и выберите «Обновить», затем снова откройте диаграмму.  
  
 **Сохранить текстовый файл**  
 Отображает диалоговое окно **Сохранить как** , которое позволяет указать расположение текстового файла, содержащего список изменений в базе данных.  
  
## <a name="see-also"></a>См. также  
 [Согласование диаграммы базы данных с измененной базой данных &#40;визуальных инструментах баз данных&#41;](visual-database-tools.md)   
 [Многопользовательские среды (визуальные инструменты для баз данных)](multiuser-environments-visual-database-tools.md)  
  
  
