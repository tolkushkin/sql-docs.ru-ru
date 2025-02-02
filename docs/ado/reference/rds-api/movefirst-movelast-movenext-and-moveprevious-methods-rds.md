---
title: Примеры MoveFirst, MoveLast, MoveNext и MovePrevious методы (RDS) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7d3a46791d81557b3e93da4a0d330d118e5b00b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712541"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>Методы MoveFirst, MoveLast, MoveNext и MovePrevious (служба удаленных рабочих столов)
Переходит к первой, последней, следующей или предыдущей записи в указанном [записей](../../../ado/reference/ado-api/recordset-object-ado.md) объекта.  
  
> [!IMPORTANT]
>  Начиная с Windows 8 и Windows Server 2012, серверные компоненты служб удаленных рабочих СТОЛОВ, больше не включаются в операционной системе Windows (см. в разделе Windows 8 и [настольная книга по совместимости Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) для получения дополнительных сведений). Клиентские компоненты служб удаленных рабочих СТОЛОВ будет поддерживаться в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Приложения, использующие служб удаленных рабочих СТОЛОВ, следует перевести [WCF-сервиса данных](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Параметры  
 *DataControl*  
 Объектную переменную, которая представляет [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) объекта.  
  
## <a name="remarks"></a>Примечания  
 Можно использовать **переместить** методы с **RDS. DataControl** объект для перемещения по записям данных в элементах управления с привязкой к данным на веб-странице. Предположим, например, можно отобразить **записей** в сетке путем привязки к **RDS. DataControl** объекта. Вы можете включить первый, Last, Next и назад кнопок, которые пользователь может щелкнуть для перехода к первой, последней, далее, или предыдущей записи отображаемых **записей**. Это делается путем вызова **MoveFirst**, **MoveLast**, **MoveNext**, и **MovePrevious** методы **RDS. DataControl** объекта в процедурах onClick для кнопки первой, последней, Далее и назад соответственно. [Пример адресной книги](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) показано, как это сделать.  
  
## <a name="applies-to"></a>Объект применения  
 [Объект DataControl (служба удаленных рабочих столов)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>См. также  
 [Метод Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Примеры MoveFirst, MoveLast, MoveNext и MovePrevious методы (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Метод MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


