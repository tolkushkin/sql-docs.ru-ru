---
title: Импорт базы знаний из файла DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: d1dbd724cca4025d34b673e3181ff7be3fdb9c89
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66776609"
---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>Импорт базы знаний из файла .dqs

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  В этом разделе описывается, как импортировать всю базу знаний из файла данных DQS в службах [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Этот файл данных создан путем экспорта существующей базы знаний из приложения [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] (см. раздел [Экспорт базы знаний в файл .dqs](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)).  
  
 Использование файла DQS для экспорта содержания базы знаний и последующего импорта содержимого в другую базу знаний на том же [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] или на другом [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] упрощает процесс создания набора знаний, экономя время и усилия. Это позволяет совместно использовать базу знаний и ее знания, экономя время. Файл DQS будет содержать все сведения базы знаний, включая домены и политику сопоставления, кроме присоединенных ссылочных данных. Будут импортированы опубликованные и неопубликованные данные.  
  
 Файл данных .dqs зашифрован, поэтому его нельзя просмотреть.  
  
 При импорте базы знаний вы можете использовать то же самое имя, если только это имя базы знаний уже не существует в клиентском приложении; в этом случае базу знаний следует переименовать.  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Чтобы импортировать базу знаний из файла данных DQS, необходимо предварительно экспортировать базу знаний в файл DQS.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Для импорта базы знаний из файла DQS необходимо иметь роль dqs_kb_editor или dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="Import"></a> Импорт базы знаний из файла DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запуск клиентского приложения Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] нажмите кнопку **Создать базу знаний**.  
  
3.  Введите имя для базы знаний.  
  
4.  Нажмите стрелку вниз **Создать базу знаний из**и выберите **Импорт из файла DQS**.  
  
5.  Чтобы **Выбрать файл данных**, нажмите кнопку **Обзор**.  
  
6.  В диалоговом окне **Импорт из файла данных** перейдите к папке, содержащей файл DQS, который надо импортировать, и щелкните имя этого файла. Нажмите кнопку **Открыть**.  
  
7.  Убедитесь, что база знаний и домены правильно отображаются в списке **Домен** .  
  
8.  Выберите действия, которые требуется выполнить, и нажмите кнопку **Создать**.  
  
9. В диалоговом окне **Импорт базы знаний** убедитесь, что строка состояния указывает, что импорт завершен. Нажмите кнопку **ОК**.  
  
10. Завершите задачи обнаружения знаний, управления доменами или политики сопоставления, которые необходимо выполнить, и нажмите кнопку **Готово**.  
  
11. Нажмите кнопку **Опубликовать** , чтобы опубликовать знания в базе знаний, или кнопку **Нет** , чтобы не публиковать.  
  
12. Если вы опубликовали базу знаний, нажмите кнопку **ОК**.  
  
13. На домашней странице служб Data Quality Services убедитесь, что база знаний содержится в списке **Недавние базы знаний**.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После импорта базы знаний из файла DQS  
 После импорта базы знаний из файла DQS можно добавить набор знаний в базу знаний или использовать базу знаний в проекте очистки или сопоставления данных в зависимости от содержимого базы знаний. Дополнительные сведения см. в разделах [Обнаружение знаний](../data-quality-services/perform-knowledge-discovery.md), [Управление доменом](../data-quality-services/managing-a-domain.md), [Управление составным доменом](../data-quality-services/managing-a-composite-domain.md), [Создание политики сопоставления](../data-quality-services/create-a-matching-policy.md), [Очистка данных](../data-quality-services/data-cleansing.md) и [Сопоставление данных](../data-quality-services/data-matching.md).  
  
  
