---
title: Введите свойства (столбец) (ADOX) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::Type
- _Column::GetType
- _Column::get_Type
- _Column::put_Type
- _Column::PutType
helpviewer_keywords:
- Type property [ADOX]
ms.assetid: 5c6718b6-f728-478a-8afb-5d17b0a91d1f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3a4a249b6a710e097ae98d75555e65cb1533700c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705721"
---
# <a name="type-property-column-adox"></a>Свойство Type (Column) (ADOX)
Указывает тип данных столбца.  
  
## <a name="settings-and-return-values"></a>Параметры и возвращаемые значения  
 Возвращает или задает **Long** значение, которое может принимать одно из [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) константы. Значение по умолчанию — **adVarWChar**.  
  
## <a name="remarks"></a>Примечания  
 Это свойство доступно для чтения/записи, до [столбец](../../../ado/reference/adox-api/column-object-adox.md) объект добавляется в коллекцию или к другому объекту, после чего она доступна только для чтения.  
  
## <a name="applies-to"></a>Объект применения  
 [Объект Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>См. также  
 [Пример свойства ParentCatalog (Visual Basic)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Свойство Type (ключ) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)   
 [Свойство Type (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
