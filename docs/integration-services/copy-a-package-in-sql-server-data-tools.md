---
title: Копирование пакета с помощью SQL Server Data Tools | Документы Майкрософт
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 147452998a4ad9501d0a8cf50791d8e12c533a26
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727270"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>Копирование пакета с помощью SQL Server Data Tools

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  В этом разделе описывается, как создать новый пакет служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] копированием существующего пакета и как обновить свойства **Name** и **GUID** нового пакета.  
  
### <a name="to-copy-a-package"></a>Копирование пакета  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , содержащий пакет, который нужно скопировать.  
  
2.  Дважды щелкните пакет в обозревателе решений.  
  
3.  Убедитесь, что копируемый пакет выбран в обозревателе решений либо в конструкторе служб SSIS выбрана вкладка, содержащая пакет  
  
4.  В меню **Файл** выберите команду **Сохранить \<имя пакета> как**.  
  
    > [!NOTE]  
    >  Чтобы команда **Сохранить как** появилась в меню **Файл** , пакет нужно открыть в конструкторе служб SSIS.  
  
5.  При необходимости перейдите в другую папку.  
  
6.  Обновите имя файла пакета. Убедитесь, что файл сохраняется с расширением DTSX.  
  
7.  Нажмите кнопку **Сохранить**.  
  
8.  Выберите, обновлять ли имя объекта пакета, чтобы оно соответствовало имени файла. Если нажать кнопку **Да**, то свойство пакета **Name** обновится. Новый пакет будет добавлен к проекту служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] и открыт в конструкторе служб [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
9. При необходимости перейдите на вкладку **Поток управления** и выберите **Свойства**.  
  
10. В окне "Свойства" щелкните значение свойства идентификатора (ID), а затем выберите **\<Сформировать новый идентификатор>** в раскрывающемся списке.  
  
11. В меню **Файл** выберите команду **Сохранить выбранные элементы** , чтобы сохранить новый пакет.  
  
## <a name="see-also"></a>См. также:  
 [Сохранение одной копии пакета](https://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [Создание пакетов в SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Пакеты служб Integration Services (SSIS)](../integration-services/integration-services-ssis-packages.md)  
  
  
