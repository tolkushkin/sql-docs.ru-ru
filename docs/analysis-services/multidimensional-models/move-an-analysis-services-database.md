---
title: Перемещение базы данных служб аналитики | Документация Майкрософт
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3247bf2ca459f013131b21a25278bcc6e5d10b9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62930902"
---
# <a name="move-an-analysis-services-database"></a>Перемещение базы данных служб Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Часто возникают ситуации, когда администратору баз данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] необходимо переместить базу данных для многомерной или табличной модели в другое место. Такие ситуации часто обусловлены потребностями предприятия, например необходимостью переместить базу данных на другой диск для повышения производительности, освободить место для увеличения размера базы данных или при обновлении какого-либо продукта.  
  
 Существует много способов перенести базу данных в другое место. В этом документе описаны следующие распространенные сценарии:  
  
-   интерактивно с помощью среды SSMS;  
  
-   программным способом с помощью объектов AMO;  
  
-   с помощью скриптов, используя XML для аналитики  
  
 При выполнении любого сценария необходимо, чтобы пользователь получил доступ к папке базы данных и применил один из методов перемещения файлов в конечное место назначения.  
  
> [!NOTE]  
>  При отсоединении базы данных без назначения ей пароля эта база данных оказывается в незащищенном состоянии. Рекомендуется назначить базе данных пароль для защиты конфиденциальных данных. Кроме того, к папке базы данных, к вложенным папкам и к файлам следует применять соответствующие меры защиты доступа, чтобы исключить несанкционированный доступ к этим объектам.  
  
## <a name="procedures"></a>Процедуры  
  
#### <a name="moving-a-database-interactively-using-ssms"></a>Перемещение базы данных в интерактивном режиме с помощью среды SSMS  
  
1.  Найдите перемещаемую базу данных на левой или правой панели среды SSMS.  
  
2.  Щелкните правой кнопкой мыши базу данных и выберите **отсоединить...**  
  
3.  Назначьте пароль отсоединяемой базе данных и нажмите кнопку **ОК** , чтобы выполнить команду отсоединения.  
  
4.  При помощи любого механизма, поддерживаемого операционной системой, или стандартным для вас образом выполните перемещение папки базы данных в новое расположение.  
  
5.  Найдите папку **Базы данных** на левой или правой панели среды SSMS.  
  
6.  Щелкните правой кнопкой мыши **баз данных** папку и выберите **присоединить...**  
  
7.  В текстовое поле **папка** впечатайте новое местоположение папки базы данных. Кроме того, можно использовать кнопку обзора (**...** ) найдите папку базы данных.  
  
8.  Выберите режим **ReadWrite** для базы данных.  
  
9. Введите пароль, который использовался в шаге 3, и нажмите кнопку **ОК** , чтобы выполнить команду присоединения.  
  
#### <a name="moving-a-database-programmatically-using-amo"></a>Перемещение базы данных программным путем с помощью объектов AMO  
  
1.  В приложении на C# проведите адаптацию следующего образца кода и выполните указанные задачи.  
  
 `private void MoveDb(Server server, string dbName,`  
  
 `string dbInitialLocation, string dbFinalLocation,`  
  
 `string dbPassword, ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `//Verify dbInitialLocation exists before continuing`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `//Save current cursor and change cursor to Cursors.WaitCursor`  
  
 `db = server.Databases[dbName];`  
  
 `db.Detach(dbPassword);`  
  
 `//Add your own code to copy the database files to the destination where you intend to attach the database`  
  
 `//Verify dbFinalLocation exists before continuing`  
  
 `server.Attach(dbFinalLocation, dbReadWriteMode, dbPassword);`  
  
 `//Restore cursor to its original`  
  
 `}`  
  
 `}`  
  
1.  В приложении на C# вызовите метод `MoveDb()` , указав необходимые параметры.  
  
2.  Скомпилируйте и выполните код для перемещения базы данных.  
  
#### <a name="moving-a-database-by-script-using-xmla"></a>Перемещение базы данных с помощью скрипта XML для аналитики  
  
1.  Откройте новую вкладку XML для аналитики в среде SSMS.  
  
2.  Скопируйте следующий шаблон скрипта XML для аналитики.  
  
 `<Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  Замените шаблон `%dbName%` именем базы данных, а шаблон `%password%` — соответствующим паролем. Символы «%» являются частью шаблона, и поэтому их необходимо удалить.  
  
2.  Выполните команду XML для аналитики.  
  
3.  При помощи любого механизма, поддерживаемого операционной системой, или стандартным для вас образом выполните перемещение папки базы данных в новое расположение.  
  
4.  Скопируйте следующий шаблон скрипта XML для аналитики в новую вкладку XML для аналитики.  
  
 `<Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  Замените шаблон `%dbFolder%` полным путем к папке базы данных в формате UNC, шаблон `%ReadOnlyMode%` — соответствующим значением ( **ReadOnly** или **ReadWrite**), а шаблон `%password%` — паролем. Символы «%» являются частью шаблона, и поэтому их необходимо удалить.  
  
2.  Выполните команду XML для аналитики.  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.AnalysisServices.Core.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Подключение и отключение баз данных служб Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Место хранения базы данных](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [Режимы ReadWriteModes базы данных](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Элемент Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Элемент Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Элемент ReadWriteMode](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [Элемент DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
