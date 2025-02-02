---
title: Изменение возвращенных файлов | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying checked-in files
- checking in files
ms.assetid: 560cd19f-ab22-4273-b00c-149993a630e6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97d6ab997a1ece36919a49243e0f1dc3cc6f3593
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779608"
---
# <a name="edit-checked-in-files"></a>Изменение возвращенных файлов
  Как правило, прежде чем начать изменение файлов в системе управления версиями, их необходимо извлечь. Однако среду [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] можно настроить так, чтобы можно было изменять файлы без их извлечения. При этом изменения хранятся в памяти до тех пор, пока файлы не будут сохранены. Затем поступает запрос извлечь файл из системы управления версиями.  
  
 Если поставщик управления версиями не поддерживает извлечение локальной версии наряду с серверной, при работе в команде разрешать изменение возвращенных файлов не рекомендуется. Большинство поставщиков не поддерживает извлечение локальных версий. Если поставщик не поддерживает извлечение локальных версий, то после изменения возвращенного файла придется вручную выполнить слияние версий, хранящихся в памяти и на сервере, прежде чем файл можно будет вернуть. Автоматическое слияние и слияние под контролем поставщика в этой ситуации не поддерживаются.  
  
### <a name="to-edit-checked-in-files"></a>Изменение возвращенных файлов  
  
1.  В меню **Сервис** выберите команду **Параметры**.  
  
2.  В диалоговом окне **Параметры** раскройте папку **Система управления версиями**, а затем щелкните **Среда**.  
  
3.  Выберите **Разрешить изменение возвращенных элементов**, а затем нажмите кнопку **ОК**.  
  
## <a name="see-also"></a>См. также  
 [Управление возвратами](../../2014/database-engine/manage-checkins.md)   
 [Управление извлечениями](../../2014/database-engine/manage-checkouts.md)  
  
  
