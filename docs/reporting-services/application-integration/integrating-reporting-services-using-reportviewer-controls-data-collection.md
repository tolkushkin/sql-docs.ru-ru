---
title: Сбор данных в элементе управления ReportViewer 2016
uthor: markingmyname
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.custom: ''
ms.date: 09/18/2018
ms.openlocfilehash: 69d37c54e49943807c35102362f161e2dbf23068
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/10/2019
ms.locfileid: "66823004"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Интеграция служб Reporting Services с помощью элементов управления ReportViewer — сбор данных

Элемент управления собирает анонимные данные, которые позволяют лучше понять, как клиенты используют продукт. Данные об использовании позволяют улучшать продукт в будущем.

Описание методик сбора и использования данных Microsoft SQL Server и средства просмотра отчетов приведено в [заявлении о конфиденциальности](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a name="opting-out-of-data-collection"></a>Отказ от сбора данных

Сбор данных об использовании можно отключить с помощью свойства ```EnableTelemetry```.

```xml
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

Кроме того, это можно сделать программным способом перед настройкой элемента управления.
    
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>См. также раздел

[Using the WebForms ReportViewer Control](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md) (Использование элемента управления средства просмотра отчетов WebForms)  
[Интеграция служб Reporting Services с помощью элементов управления средства просмотра отчетов](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



