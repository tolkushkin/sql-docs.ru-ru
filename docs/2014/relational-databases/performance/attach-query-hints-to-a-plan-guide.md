---
title: Присоединение указаний запросов к структуре плана | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 2131f796-6359-4f9e-9047-da0b3d4dedaf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 89af21c2c591db2dff678be7aaf8c064e728b9ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151075"
---
# <a name="attach-query-hints-to-a-plan-guide"></a>Присоединение указаний запросов к структуре плана
  Любые сочетания действительных указаний запроса могут быть использованы в руководстве плана. Когда структура плана совпадает с запросом, предложение OPTION, указанное в предложении указания структуры плана, добавляется к запросу, прежде чем запрос подвергается компиляции и оптимизации. Если в запросе, совпавшем со структурой плана, уже присутствует предложение OPTION, указания запроса, заданные в структуре плана, заменяют рекомендации в запросе. Чтобы структура плана совпала с запросом, уже содержащим предложение OPTION, предложение OPTION запроса необходимо включить при указании текста запроса для сопоставления в инструкции sp_create_plan_guide. Если необходимо, чтобы подсказки, указанные в руководстве плана, были добавлены к подсказкам, которые уже существуют в запросе, вместо того, чтобы заменить их, следует указать и исходные, и дополнительные подсказки в предложении OPTION структуры плана.  
  
> [!CAUTION]  
>  Структуры планов с неправильным использованием указаний запросов могут привести к проблемам при компиляции во время выполнения и ухудшению производительности. Структуры планов должны применяться только опытными разработчиками и администраторами баз данных.  
  
## <a name="common-query-hints-used-in-plan-guides"></a>Общие указания запросов, используемые в структурах планов  
 Запросы, получающие преимущества от структур планов, обычно используют параметры и могут выполняться неэффективно, так как при их выполнении кэшируются планы запросов со значениями параметров, не соответствующими сценарию худшего случая или типичному сценарию. Для решения этой проблемы можно использовать указания запросов OPTIMIZE FOR и RECOMPILE. Подсказка OPTIMIZE FOR сообщает [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , что нужно использовать конкретное значение параметра при оптимизации запроса. Указание RECOMPILE сообщает серверу, что после выполнения план запроса нужно удалить и что оптимизатору запросов нужно будет перекомпилировать план при следующем выполнении запроса. См. пример в статье [Руководства планов](plan-guides.md).  
  
 Кроме того, можно задать указания таблицы INDEX, FORCESCAN и FORCESEEK как указания запроса. При использовании в качестве указаний запроса они ведут себя так же, как и встроенные табличные указания или указания представлений. Указание INDEX вынуждает оптимизатор запросов использовать только заданные индексы при получении доступа к данным ссылочной таблицы или ссылочного представления. Указание FORCESEEK вынуждает оптимизатор запросов использовать только операцию поиска по индексу для доступа к данным ссылочной таблицы или ссылочного представления в запросе. Эти указания предоставляют дополнительные функциональные возможности структуре плана и позволяют оказывать большее влияние на процесс оптимизации запросов, использующих структуру плана.  
  
  
