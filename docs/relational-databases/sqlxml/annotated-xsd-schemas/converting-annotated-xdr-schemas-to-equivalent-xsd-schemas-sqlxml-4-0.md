---
title: Преобразование схем XDR в эквивалентные схемы XSD (SQLXML 4.0) с заметками | Документация Майкрософт
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XDR schemas, converting schemas
- annotated XSD schemas, converting schemas
- XDR to XSD Converter tool [SQLXML]
- XDR schemas [SQLXML], converting
- converting annotated schemas
- mapping schema [SQLXML], conversions
- XSD schemas [SQLXML], converting schemas
ms.assetid: 151c94a8-66d3-4c46-a5ff-a22df456940a
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 71c2f79ae39ff8617d491d015db7eecb23647d30
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678025"
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>Преобразование схем XDR с заметками в эквивалентные схемы XSD (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Язык определения схем XML (XSD) пришел на смену языку определения схем с сокращенными XML-данными (XDR). После ввода в действие поддержки XSD в [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 предполагается, что новые схемы с заметками должны создаваться при помощи XSD. SQLXML 4.0 включает средство преобразования XDR в XSD, которое создано для предоставления помощи пользователю в преобразовании существующих схем XDR с заметками в равнозначные схемы XSD.  
  
> [!IMPORTANT]  
>  Это средство рекомендуется использовать только для преобразования схем XDR в XSD в целях их применения с SQLXML 4.0. Это не следует считать средством преобразования XDR в XSD общего назначения. Преобразованные схемы XSD могут не действовать в полном соответствии с исходными схемами XDR, будучи используемыми в других средах.  
  
 Если входной XDR-файл задает в XML-декларации кодировку, она становится кодировкой создаваемого выходного XSD-файла.  
  
 Средство преобразования (Cvtschema.exe) установлено в папке Program Files\SQLXML 4.0\bin и исполняется в командной строке.  
  
 Далее представлен общий синтаксис:  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 Где:  
  
 XDRFileName  
 Имя XDR-файла, который необходимо преобразовать в XSD. Это средство читает входной XDR-файл и создает выходной XSD-файл в текущем рабочем каталоге. Если текущий файл имеет расширение XDR или XML, выходной XSD-файл создается с тем же именем, но с расширением XSD. Если расширение имени входного файла кроме .xml или XDR (или если расширение не указано), выходной файл создается с тем же именем, и расширение XSD добавляется к имени входного файла. Например, если именем входного XDR-файла является SampleFile.abc, то полученный XSD-файл сохраняется как SampleFile.abc.xsd.  
  
 -y  
 Перезаписывает существующий XSD-файл XSD-файлом, созданным средством преобразования (необязательно). Если этот флаг не указан, в этом средстве происходит вывод приглашения для пользователя, которое позволяет указать, следует ли переписать существующий XSD-файл и изменить имя выходного файла.  
  
 -w  
 Возвращает некритичные предупреждения, сформированные этим средством в процессе преобразования (необязательно). По умолчанию это средство отображает только сообщения, относящиеся к неустранимым ошибкам.  
  
 -?  
 Возвращает список параметров, которые можно задать с помощью **cvtschema**, вместе с пояснением.  
  
## <a name="see-also"></a>См. также  
 [Сопоставление типов данных XSD с типами данных XPath &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)   
 [Заметки XSD &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  
