---
title: Метод setSelectMethod (SQLServerDataSource) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c48aabcb618ba16c0769210903318b0d386d941d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767848"
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>Метод setSelectMethod (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Задает тип курсора по умолчанию, используемый для всех результирующих наборов, созданных при помощи данного объекта [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>Параметры  
 *selectMethod*  
  
 Значение **String**, содержащее тип курсора по умолчанию.  
  
## <a name="remarks"></a>Remarks  
 Свойство selectMethod содержит тип курсора по умолчанию, который используется для результирующего набора. Это свойство полезно при работе с крупными результирующими наборами, когда не нужно сохранять результирующий набор целиком в памяти клиента. Если установить это свойство в значение cursor, то можно создать серверный курсор, который будет получать данные меньшими фрагментами. Если свойство selectMethod не задано, метод [getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md) возвращает значение по умолчанию — direct.  
  
## <a name="see-also"></a>См. также:  
 [Элементы SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Класс SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
