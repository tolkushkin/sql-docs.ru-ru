---
title: Шаг 1. Создание рабочих папок и переменных среды | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a7f1437346baa2c54801af591a5f23a208d42c2
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723454"
---
# <a name="lesson-1-1---creating-working-folders-and-environment-variables"></a>Занятие 1–1. Создание рабочих папок и переменных среды

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


В этой задаче предстоит создать рабочую папку (C:\DeploymentTutorial) и новые системные переменные среды (`DataTransfer` и `LoadXMLData`), которые будут использоваться в последующих задачах учебника.  
  
Рабочая папка является корневой папкой диска C. Если необходимо, используйте другой диск или расположение. Однако необходимо обратить внимание на это расположение и использовать его в дальнейшем всегда, когда в учебнике встречается ссылка на рабочую папку DeploymentTutorial.  
  
На следующем занятии пакеты, сохраненные в файловой системе, будут развернуты в таблицу sysssispackages базы данных [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb. В идеальном случае предстоит разместить пакеты служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] на другом компьютере. Если это невозможно, можно все-таки многое изучить в этом учебнике, развертывая пакеты в экземпляре [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] на локальном компьютере. Переменные среды, используемые на локальном компьютере и компьютере назначения, имеют одни и те же имена, но в них хранятся разные значения. Например, на локальном компьютере значение переменной среды `DataTransfer` ссылается на папку C:\DeploymentTutorial, в то время как на целевом компьютере переменная среды `DataTransfer` ссылается на папку C:\DeploymentTutorialInstall.  
  
Если планируется разместить пакеты на локальном компьютере, то необходимо создать только один набор переменных среды, однако придется назначить переменным окружения соответствующие значения, перед тем как производить локальное размещение.  
  
Если пакеты планируется разместить на другом компьютере, то необходимо создать два набора переменных сред: один набор для локального компьютера, а другой — для целевого компьютера. Пока можно создать только переменные для компьютера источника, а переменные для целевого компьютера можно создать потом, но на целевом компьютере, прежде чем пакеты будут установлены на него, должны быть доступны как переменные среды, так и папка.  
  
### <a name="to-create-the-local-working-folder"></a>Создание локальной рабочей папки  
  
1.  Щелкните правой кнопкой мыши меню «Пуск» и выберите «Проводник».  
  
2.  Щелкните **Локальный диск (С:)**.  
  
3.  В меню **Файл** наведите указатель на пункт **Создать**, а затем выберите пункт **Папка**.  
  
4.  Переименуйте новую папку в **DeploymentTutorial**.  
  
### <a name="to-create-local-environment-variables"></a>Создание локальных переменных среды  
  
1.  В меню **Пуск** выберите пункт **Панель управления**.  
  
2.  На панели управления дважды щелкните значок **Система**.  
  
3.  В диалоговом окне **Свойства системы** выберите вкладку **Дополнительно** , затем нажмите кнопку **Переменные среды**.  
  
4.  В диалоговом окне **Переменные среды** в области **Системные переменные** нажмите кнопку **Создать**.  
  
5.  В диалоговом окне **Новая системная переменная** введите **DataTransfer** в поле **Имя переменной** и **C:\DeploymentTutorial\datatransferconfig.dtsconfig** в поле **Значение переменной** .  
  
6.  Нажмите кнопку **ОК**.  
  
7.  Снова нажмите кнопку **Создать** и введите **LoadXMLData** в поле **Имя переменной** и **C:\DeploymentTutorial\loadxmldataconfig.dtsconfig** в поле **Значение переменной** .  
  
8.  Нажмите кнопку **ОК** для выхода из диалогового окна **Переменные среды** .  
  
9. Нажмите кнопку **ОК** для выхода из диалогового окна **Свойства системы** .  
  
10. При необходимости перезагрузите компьютер. Если не перезагрузить компьютер, то имя новой переменной не отобразится в мастере настройки пакета, но переменную можно будет использовать.  
  
### <a name="to-create-destination-environment-variables"></a>Создание целевых переменных среды  
  
1.  В меню **Пуск** выберите пункт **Панель управления**.  
  
2.  На панели управления дважды щелкните значок **Система**.  
  
3.  В диалоговом окне **Свойства системы** выберите вкладку **Дополнительно** , затем нажмите кнопку **Переменные среды**.  
  
4.  В диалоговом окне **Переменные среды** в области **Системные переменные** нажмите кнопку **Создать**.  
  
5.  В диалоговом окне **Новая системная переменная** введите **DataTransfer** в поле **Имя переменной** и **C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig** в поле **Значение переменной** .  
  
6.  Нажмите кнопку **ОК**.  
  
7.  Снова нажмите кнопку **Создать** и введите **LoadXMLData** в поле **Имя переменной** и **C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig** в поле **Значение переменной** .  
  
8.  Нажмите кнопку **ОК** для выхода из диалогового окна **Переменные среды** .  
  
9. Нажмите кнопку **ОК** для выхода из диалогового окна **Свойства системы** .  
  
10. При необходимости перезагрузите компьютер.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
[Шаг 2. Создание проекта развертывания](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
  
  
