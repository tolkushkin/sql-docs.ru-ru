---
title: Программирование ADO JScript | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e53f1d6e30497282cce8e895f458d81660240d9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701301"
---
# <a name="jscript-ado-programming"></a>Программирование объектов ADO с использованием JScript
## <a name="creating-an-ado-project"></a>Создание проекта ADO  
 Microsoft JScript не поддерживает библиотеки типов, вам не нужен для ссылки ADO в проекте. Следовательно не связанные функции, такие как завершение командной строки, поддерживаются. Кроме того по умолчанию ADO перечисления константы не определены в JScript.  
  
 Тем не менее ADO предоставляет с двумя включить файлы, содержащие следующие определения для использования с JScript:  
  
-   Для использования сценариев на стороне сервера Adojavas.inc, который устанавливается в папках библиотеки ADO.  
  
-   Для использования сценариев на стороне клиента Adcjavas.inc установленный в папках библиотеки ADO.  
  
 Можно скопировать и вставить определения констант из этих файлов в ASP-страниц или, при выполнении сценариев на стороне сервера, скопируйте файл Adojavas.inc в папку на веб-сайт и ссылается на нее из страницы ASP со следующим образом:  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Создание объектов ADO в JScript  
 Вместо этого необходимо использовать **CreateObject** вызов функции:  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>Пример JScript  
 Ниже приведен общий пример программирования на стороне сервера JScript в файле Active Server Page (ASP), который открывает **записей** объекта:  
  
```javascript
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```
