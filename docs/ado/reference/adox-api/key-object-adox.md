---
title: Ключ объекта (ADOX) | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6dbbb81d53755032725ad71ff9bbf49b9beb2f1c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706474"
---
# <a name="key-object-adox"></a>Объект Key (ADOX)
Представляет внешний, первичный или уникальный ключевого поля из таблицы базы данных.  
  
## <a name="remarks"></a>Примечания  
 В следующем коде создается новый **ключ**:  
  
```  
Dim obj As New Key  
```  
  
 С помощью свойств и коллекций **ключ** объекта, вы можете:  
  
-   Определение ключа с [имя](../../../ado/reference/adox-api/name-property-adox.md) свойство.  
  
-   Определить, является ли ключ основной, внешний или уникальными [тип](../../../ado/reference/adox-api/type-property-key-adox.md) свойства.  
  
-   Доступ к базе данных столбцы ключа с [столбцы](../../../ado/reference/adox-api/columns-collection-adox.md) коллекции.  
  
-   Укажите имя связанной таблицы с [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md) свойство.  
  
-   Определить действие, выполняемое для удаления или обновления первичного ключа с [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) и [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) свойства.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Свойства, методы и события объекта Key](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>См. также  
 [Append коллекции Keys метод, тип ключа, RelatedColumn, RelatedTable и UpdateRule свойства (Visual Basic)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Коллекция Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Коллекция Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
