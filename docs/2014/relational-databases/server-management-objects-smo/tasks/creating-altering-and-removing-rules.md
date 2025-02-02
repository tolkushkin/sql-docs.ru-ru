---
title: Создание, изменение и удаление правил | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d201b20e0bdfd213c62c060250b5674589ab91cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62519328"
---
# <a name="creating-altering-and-removing-rules"></a>Создание, изменение и удаление правил
  В SMO правила представлены объектом <xref:Microsoft.SqlServer.Management.Smo.Rule>. Правило определяется свойством <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A>, которое является текстовой строкой, содержащей выражение условия, использующее операторы или предикаты, например IN, LIKE или BETWEEN. Правило не может ссылаться на столбцы или другие объекты базы данных. В правило могут входить встроенные функции, не ссылающиеся на объекты базы данных.  
  
 Определение в свойстве <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> должно содержать переменную, ссылающуюся на введенное значение данных. Для представления значения при создании правила можно использовать любое имя или символ, но первым символом должна быть \@ символов.  
  
## <a name="example"></a>Пример  
 Чтобы использовать какой-либо из представленных примеров кода, нужно выбрать среду, шаблон и язык программирования, с помощью которых будет создаваться приложение. Дополнительные сведения см. в разделе [Создание проекта SMO на Visual Basic в Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) или [Visual C создайте&#35; проекта SMO в Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Создание, изменение и удаление правила на языке Visual Basic  
 Данный образец кода показывает, как создать правило, добавить его в столбец, изменить свойства объекта <xref:Microsoft.SqlServer.Management.Smo.Rule>, отсоединить его от столбца и удалить его.  
  
 Инструкция `Dim` для объекта <xref:Microsoft.SqlServer.Management.Smo.Rule> указывается с полным путем к сборке, чтобы избежать неоднозначности с объектом <xref:Microsoft.SqlServer.Management.Smo.Rule> в сборке System.Data.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBRules1](SMO How to#SMO_VBRules1)]  -->  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Создание, изменение и удаление правила на языке Visual C#  
 Данный образец кода показывает, как создать правило, добавить его в столбец, изменить свойства объекта <xref:Microsoft.SqlServer.Management.Smo.Rule>, отсоединить его от столбца и удалить его.  
  
 Инструкция `Dim` для объекта <xref:Microsoft.SqlServer.Management.Smo.Rule> указывается с полным путем к сборке, чтобы избежать неоднозначности с объектом <xref:Microsoft.SqlServer.Management.Smo.Rule> в сборке System.Data.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>Создание, изменение и удаление правила в PowerShell  
 Данный образец кода показывает, как создать правило, добавить его в столбец, изменить свойства объекта <xref:Microsoft.SqlServer.Management.Smo.Rule>, отсоединить его от столбца и удалить его.  
  
 Инструкция `Dim` для объекта <xref:Microsoft.SqlServer.Management.Smo.Rule> указывается с полным путем к сборке, чтобы избежать неоднозначности с объектом <xref:Microsoft.SqlServer.Management.Smo.Rule> в сборке System.Data.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule `  
-argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.   
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.   
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and   
# column as arguments in the BindToColumn method.   
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.   
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
