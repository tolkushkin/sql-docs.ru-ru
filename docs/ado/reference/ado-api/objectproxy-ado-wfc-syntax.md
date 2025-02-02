---
title: ObjectProxy (ADO — синтаксис WFC) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c0b1a69ebbc96197a5bf8fc1cb617e7fde65c731
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707177"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO — синтаксис WFC)
**ObjectProxy** объект представляет сервер и возвращается **createObject** метод [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) объекта. Класс ObjectProxy имеет один метод **вызвать**, который можно вызвать метод на сервере и возвращает объект, полученный в результате этого вызова.  
  
 **com.ms.wfc.data пакета**  
  
## <a name="methods"></a>Методы  
  
### <a name="call-method-adowfc-syntax"></a>Вызовите метод (синтаксис ADO и WFC)  
 Вызывает метод сервера, представленных ObjectProxy. При необходимости аргументы метода может быть передан как массив объектов.  
  
#### <a name="syntax"></a>Синтаксис  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Возвращает  
 Object  
 Объект, полученный в результате вызова метода.  
  
#### <a name="parameters"></a>Параметры  
 *ObjectProxy*  
 **ObjectProxy** объект, представляющий сервер.  
  
 *Метод*  
 Строка, содержащая имя метода для вызова на сервере.  
  
 *аргументы*  
 Необязательный параметр. Массив объектов, которые являются аргументов метода на сервере. Типами данных Java автоматически преобразуются в типы данных, подходящий для использования на сервере.
