---
title: Элемент DatabaseToConnect (DTA) | Документация Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6c06339b7e38272e1a6923183f79869cbdd871c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62857496"
---
# <a name="databasetoconnect-element-dta"></a>Элемент DatabaseToConnect (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Позволяет задать первую базу данных, к которой подключается помощник по настройке ядра СУБД при настройке рабочей нагрузки.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|**Тип данных и длина**|**string**, неограниченная длина|  
|**Значение по умолчанию**|Нет.|  
|**Наличие**|Необязательный параметр. Может использоваться один раз для каждого элемента **TuningOptions** .|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элементы|  
|------------------|--------------|  
|**Родительский элемент**|[Элемент TuningOptions (DTA)](../../tools/dta/tuningoptions-element-dta.md)|  
|**Дочерние элементы**|None|  
  
## <a name="remarks"></a>Remarks  
 Используйте **DatabaseToConnect** для указания имени первой базы данных, к которой должен подключиться помощник по настройке ядра СУБД при запуске сеанса настройки. Этот элемент позволяет задать только одну базу данных. Если задано несколько имен баз данных, помощник по настройке ядра СУБД вернет ошибку.  
  
## <a name="example"></a>Пример  
 Пример использования см. в разделе [Образец входного XML-файла с описанием встроенной рабочей нагрузки (DTA)](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>См. также:  
 [Справочник по входным XML-файлам (помощник по настройке ядра СУБД)](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
