---
title: Задача 4. Задание правил домена | Документация Майкрософт
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ea4397bddf9ab1c08c099df4c473a5e43c54c9ec
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489069"
---
# <a name="task-4-setting-domain-rules"></a>Задача 4. Задание правил домена
  В этой задаче вы создаете правило для **контактный адрес электронной почты** домена, чтобы проверить, заканчивается ли адрес электронной почты **@adventure-works.com**. См. в разделе [создания правила домена](https://msdn.microsoft.com/library/hh510397.aspx) Дополнительные сведения на странице.  
  
1.  Нажмите кнопку **контактный адрес электронной почты** в **список доменов**.  
  
2.  Переключиться в режим **правил домена** вкладку на правой панели.  
  
     ![Добавить новую кнопку панели инструментов правило домена](../../2014/tutorials/media/et-settingdomainrules-01.jpg "добавьте новую кнопку панели инструментов правила домена")  
  
3.  В области справа щелкните **добавить новое правило домена** на панели инструментов (см. рисунок) чтобы добавить правило.  
  
4.  Тип **проверки по электронной почте** для **имя_правила** и нажмите клавишу **ввод**. **Active** флажок должен быть установлен по умолчанию. Этот элемент управления позволяет временно отключить правило.  
  
5.  В **построить правило** панели щелкните **стрелка вниз**и выберите **значение заканчивается**.  
  
6.  Тип **@adventure-works.com** в текстовое поле и нажмите клавишу **ВКЛАДКЕ**. Можно добавить дополнительные условия, нажав кнопку **добавить новое условие в выбранное предложение** кнопку панели инструментов в **построить правило** области.  
  
     ![Отправить по электронной почте правило проверки](../../2014/tutorials/media/et-settingdomainrules-02.jpg "по электронной почте правила проверки")  
  
7.  Нажмите кнопку **запустить выбранное правило домена к тестовым данным** на панели инструментов в правой панели, чтобы проверить правило на основе образца данных.  
  
     ![Запустить правило домена на кнопку панели инструментов данных теста](../../2014/tutorials/media/et-settingdomainrules-03.jpg "запустить правило домена на кнопку панели инструментов данных теста")  
  
8.  В **проверка доменного правила** диалоговом окне щелкните **добавляет новый проверочный термин для правила домена** на панели инструментов.  
  
     ![Проверить правило домена-диалоговое окно](../../2014/tutorials/media/et-settingdomainrules-04.jpg "проверить диалоговое окно правила домена")  
  
9. Тип **frank7@adventure-works.com** (допустимое значение) в **контактный адрес электронной почты** столбца.  
  
10. Повторите два предыдущих шага, чтобы добавить **joe2@adventure-work.com** (недопустимое значение с нет на ").  
  
11. Нажмите последнюю кнопку (**проверить правило домена на всех терминах**) на панели инструментов, чтобы проверить входные данные посредством правила.  
  
     ![Проверить правило домена на панели инструментов кнопку все условия](../../2014/tutorials/media/et-settingdomainrules-05.jpg "проверить правило домена на панели инструментов кнопку все условия")  
  
12. Обратите внимание, что первая запись отображается как допустимый элемент, а вторая — как недопустимый элемент.  
  
     ![Результаты проверки правила домена](../../2014/tutorials/media/et-settingdomainrules-06.jpg "результаты проверки правила домена")  
  
13. Нажмите кнопку **закрыть** закрыть **проверка доменного правила** диалоговое окно.  
  
## <a name="next-step"></a>Следующий шаг  
 [Задача 5. Задание связей на основе](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
