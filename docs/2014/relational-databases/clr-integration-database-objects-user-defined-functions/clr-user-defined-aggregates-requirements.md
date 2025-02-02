---
title: Требования для определяемых пользователем статистических функций CLR | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 31b22b1dce53bb82f85ae946290024408d2facd3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874482"
---
# <a name="requirements-for-clr-user-defined-aggregates"></a>Требования для определяемых пользователем статистических функций CLR
  Тип в сборке CLR можно зарегистрировать как определяемую пользователем агрегатную функцию, если он реализует необходимую статистическую обработку. Такой контракт состоит из атрибута `SqlUserDefinedAggregate` и методов статистического контракта. Статистический контракт включает механизм сохранения промежуточного состояния статистической обработки и механизм накопления новых значений, который состоит из четырех методов: `Init`, `Accumulate`, `Merge`, и `Terminate`. При соблюдении этих требований, появится возможность воспользоваться всеми преимуществами определяемых пользователем статистических функций в [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. В следующих подразделах этого раздела содержатся подробные сведения о создании определяемых пользователем статистических функций и работе с ними. Например, см. в разделе [Invoking CLR User-Defined агрегатные функции](clr-user-defined-aggregate-invoking-functions.md).  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 Дополнительные сведения см. в разделе [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="aggregation-methods"></a>Методы статистической обработки  
 Класс, зарегистрированный как определяемая пользователем статистическая функция, должен поддерживать следующие методы экземпляра. Это методы, которые использует обработчик запросов для выполнения статистической обработки.  
  
|Метод|Синтаксис|Описание|  
|------------|------------|-----------------|  
|`Init`|public void Init();|Обработчик запросов использует данный метод для инициализации вычисления статистической обработки. Этот метод вызывается один раз для каждой группы, которую обработчик запросов подвергает статистической обработке. Обработчик запросов может выбрать повторное использование одного экземпляра класса статистической функции для выполнения статистической обработки нескольких групп. Метод `Init` должен выполнять всю необходимую очистку прежнего использования экземпляра и запускать новые статистические вычисления.|  
|`Accumulate`|открытый void Accumulate (вводом значение [, значение типа входных данных,...]);|Один или несколько параметров, представляющих аргументы функции. *INPUT_TYPE* должен быть управляемым [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] тип данных, эквивалентным собственному [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] тип данных, определенный *input_sqltype* в `CREATE AGGREGATE` инструкции. Дополнительные сведения см. в разделе [сопоставление данных параметров CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).<br /><br /> Для определяемых пользователем типов входной тип аналогичен определяемому пользователем типу. Обработчик запросов использует этот метод для накопления статистических значений. Метод вызывается один раз для каждого значения группы, в которой выполняется статистическая обработка. Обработчик запросов всегда вызывает его только после вызова метода `Init` в данном экземпляре статистического класса. Реализация данного метода должна обновить состояние экземпляра, чтобы отразить накопление передаваемого значения аргумента.|  
|`Merge`|открытый void слияния (udagg_class значение);|Метод используется для слияния еще одного экземпляра этого статистического класса с текущим экземпляром. Обработчик запросов использует этот метод для слияния нескольких частичных вычислений статистической обработки.|  
|`Terminate`|public return_type Terminate();|Этот метод завершает статистическое вычисление и возвращает результат статистической обработки. *Return_type* должен быть управляемым [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] данных типа, который является управляемым эквивалентом *return_sqltype* указано в `CREATE AGGREGATE` инструкции. *Return_type* также может быть определяемым пользователем типом.|  
  
### <a name="table-valued-parameters"></a>Параметры, возвращающие табличные значения  
 Возвращающие табличное значение параметры — это определяемые пользователем табличные типы, которые передаются в процедуру или функцию, предоставляя эффективный способ передачи на сервер нескольких строк данных. Возвращающие табличное значение параметры выполняют функции, аналогичные массивам параметров, но обладают большей гибкостью и лучше интегрируются с [!INCLUDE[tsql](../../includes/tsql-md.md)]. Они также обеспечивают возможность повышения производительности. Кроме того, возвращающие табличное значение параметры способствуют сокращению циклов приема-передачи данных с сервера и на сервер. Вместо того чтобы отправлять на сервер несколько запросов (как в случае списка скалярных параметров), данные можно отправить в виде возвращающего табличное значение параметра. Определяемый пользователем табличный тип нельзя передавать в виде возвращающего табличное значение параметра в управляемую хранимую процедуру или функцию, которая выполняется в процессе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Кроме того, такие процедуры и функции не могут возвращать определяемые пользователем табличные типы. Возвращающие табличное значение параметры также нельзя использовать внутри области контекстного соединения. Однако возвращающий табличное значение параметр можно использовать с SqlClient в управляемых хранимых процедурах или функциях, выполняемых в процессе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], если он используется в соединении, отличном от контекстного соединения. Соединение может быть установлено с тем же сервером, который выполняет управляемую процедуру или функцию. Дополнительные сведения о возвращающие табличное значение параметры, см. в разделе [параметров, возвращающих &#40;СУБД&#41;](../tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="change-history"></a>Журнал изменений  
  
|Обновленное содержимое|  
|---------------------|  
|Обновлено описание метода `Accumulate`, который теперь принимает несколько параметров.|  
  
## <a name="see-also"></a>См. также  
 [Определяемые пользователем типы CLR](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Вызов определяемых пользователем агрегатных функций CLR](clr-user-defined-aggregate-invoking-functions.md)  
  
  
