---
title: Формирование веб-каналов данных из отчета (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e68baae2-9f2a-4f13-9179-9ac7f29111c5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ceca9ef914afeab3420bbd35c46c582c112644dc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107851"
---
# <a name="generate-data-feeds-from-a-report-report-builder-and-ssrs"></a>Формирование веб-каналов данных из отчета (построитель отчетов и службы SSRS)
  Можно формировать Atom-совместимые потоки данных из отчетов, а затем использовать эти потоки данных в приложениях, например в клиенте [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , который может использовать потоки данных.  
  
 Модуль Atom подготовки отчетов служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] формирует сервисный документ канала Atom, в котором перечислены потоки данных, доступные в отчете. Этот документ содержит сведения по меньшей мере об одном потоке данных для каждой области данных отчета. В зависимости от типа области данных и самих данных, которые отображает эта область, службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] могут сформировать из нее несколько потоков данных.  
  
 Сервисный документ Atom содержит для каждого потока данных уникальный идентификатор, который упоминается в URL-адресе для доступа к содержимому потока данных.  
  
 Дополнительные сведения см. в разделе [формирование потоков данных из отчетов &#40;построитель отчетов и службы SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-generate-an-atom-service-document"></a>Формирование сервисного документа Atom  
  
1.  Перейдите с **домашней** страницы диспетчера отчетов к отчету, из которого требуется сформировать потоки данных.  
  
2.  Щелкните отчет.  
  
     Отчет выполняется.  
  
3.  На панели инструментов нажмите кнопку «Экспорт в поток данных».  
  
     Появится запрос, что нужно сделать с файлом: сохранить или открыть документ Atom, содержащий поток данных.  
  
4.  Щелкните **Сохранить** , чтобы сохранить документ в файловой системе, или **Открыть** , чтобы просмотреть содержимое документа перед сохранением. **По умолчанию документ открывается в браузере.**  
  
5.  Укажите расположение для сохранения документа.  
  
6.  При необходимости имя файла можно изменить.  
  
    > [!NOTE]  
    >  По умолчанию имя документа совпадает с именем отчета.  
  
7.  Убедитесь, что документ имеет тип **ATOMSVC**, затем нажмите кнопку **Сохранить**.  
  
8.  При необходимости откройте файл ATOMSVC в браузере либо в текстовом или XML-редакторе.  
  
### <a name="to-view-an-atom-compliant-data-feed"></a>Просмотр Atom-совместимого потока данных  
  
1.  Если сервисный документ Atom еще не открыт, найдите и откройте его в браузере, например в Internet Explorer.  
  
2.  Скопируйте в браузер URL-адрес потока данных, который требуется просмотреть из сервисного документа Atom.  
  
     Формат URL-адреса будет следующим:  
  
 `http://<server name>/ReportServer?%2f<ReportName>rs%3aCommand=Render&rs%3aFormat=ATOM&rc%3aDataFeed=<Identifier>`  
  
1.  Нажмите клавишу ВВОД.  
  
     Появится запрос, что нужно сделать с файлом: сохранить или открыть документ Atom, содержащий поток данных.  
  
2.  Щелкните **Сохранить** , чтобы сохранить документ в файловой системе, или **Открыть** , чтобы просмотреть поток данных перед сохранением.  
  
3.  Укажите расположение для сохранения документа.  
  
4.  При необходимости имя файла можно изменить.  
  
    > [!NOTE]  
    >  По умолчанию имя документа совпадает с именем отчета. Если в сервисном документе Atom есть несколько потоков, все они используют по умолчанию одно и то же имя — имя отчета. Чтобы различать их, дайте им значимые имена.  
  
5.  Убедитесь, что документ имеет тип **ATOM**, затем нажмите кнопку **Сохранить**.  
  
6.  При необходимости откройте файл ATOM в браузере либо в текстовом или XML-редакторе.  
  
## <a name="see-also"></a>См. также  
 [Экспорт отчетов &#40;построитель отчетов и службы SSRS&#41;](export-reports-report-builder-and-ssrs.md)  
  
  
