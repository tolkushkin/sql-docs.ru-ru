---
title: Альтернативные способы подключения к данным (построитель отчетов) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: aebc5f3d-97d5-4d54-b525-753fed073a9a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 36f489f25adc9746f844a6289ca8a2849ad83870
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109985"
---
# <a name="alternative-ways-to-get-a-data-connection-report-builder"></a>Альтернативные способы создания подключения к данным (построитель отчетов)
  Подключение к данным содержит сведения, необходимые для подключения к внешнему источнику данных, например к базе данных [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Обычно сведения о соединении и учетные данные, которые будут использоваться при соединении с источником данных, можно получить у владельца источника данных.  
  
 Чтобы указать подключение к данным, можно воспользоваться общим источником данных с сервера отчетов или создать внедренный источник данных, используемый только в отдельном отчете.  
  
 В большинстве учебников используются внедренные источники данных, но при наличии доступа к общим источникам данных можно воспользоваться и ими.  
  
## <a name="getting-a-data-connection-from-a-shared-data-source"></a>Создание подключения к данным из общего источника данных  
 Если на сервере отчетов имеется доступный общий источник данных, для использования которого достаточно прав, можно использовать его вместо внедренного источника данных. В следующей процедуре описан поиск общих источников данных и ввод учетных данных, необходимых для их использования.  
  
 Чтобы воспользоваться общим источником данных, необходимо перейти к серверу отчетов и выбрать источник. Обычно URL-адрес сервера отчетов можно получить у администратора сервера отчетов.  
  
#### <a name="to-specify-a-data-connection-from-a-list-of-shared-data-sources"></a>Выбор подключения к данным из списка общих источников данных  
  
1.  На странице **Выбор набора данных** выберите команду **Создать набор данных**, а затем нажмите кнопку **Далее**. Откроется страница **Выберите соединение с источником данных** .  
  
2.  В списке источников данных выберите источник, на доступ к которому имеется разрешение.  
  
3.  Нажмите кнопку **Проверить соединение**, чтобы проверить соединение с источником данных. Отобразится сообщение «Соединение установлено успешно». [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Нажмите кнопку **Далее**.  
  
     При необходимости введите учетные данные. Чтобы сохранить учетные данные локально, установите флажок **Сохранить пароль с соединением**. Если этот параметр не выбран, ввод учетных данных будет требоваться каждый раз при запуске отчета.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-specify-a-data-connection-by-browsing-to-a-shared-data-source-on-a-report-server"></a>Указание подключения к данным путем выбора общего источника данных на сервере отчетов  
  
1.  На странице **Выбор набора данных** выберите команду **Создать набор данных**, а затем нажмите кнопку **Далее**. Откроется страница **Выберите соединение с источником данных** .  
  
2.  Нажмите кнопку **Обзор**. Откроется диалоговое окно **Выбор источника данных** .  
  
3.  В раскрывающемся списке **Папка** выберите пункт **Последние сайты и серверы**. На панели источника данных щелкните URL-адрес сервера и нажмите кнопку **Открыть**.  
  
     Отобразится список источников данных или моделей.  
  
4.  Либо в поле **Имя**введите URL-адрес сервера отчетов. Нажмите кнопку **Открыть**.  
  
     Построитель отчетов подключится к серверу отчетов и загрузит источники данных, доступные в корневой папке.  
  
5.  Перейдите к папке, содержащей источник данных, на подключение к которому имеются разрешения, выберите источник данных и нажмите кнопку **Открыть**.  
  
     Снова откроется страница **Выбор соединения с источником данных** .  
  
6.  Нажмите кнопку **Проверить соединение**, чтобы проверить соединение с источником данных.  
  
     Отобразится сообщение «Соединение установлено успешно». [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Нажмите кнопку **Далее**.  
  
8.  При запросе имени пользователя и пароля введите учетные данные. Чтобы сохранить учетные данные локально, установите флажок **Сохранить пароль с соединением**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Добавление данных в отчет &#40;построитель отчетов и службы SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Учебники по &#40;построитель отчетов&#41;](report-builder-tutorials.md)  
  
  
