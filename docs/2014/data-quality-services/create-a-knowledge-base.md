---
title: Создание базы знаний | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.selectkb.f1
- sql12.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2402a69f428fe0c9ba2359f100e2baf16e1a1d04
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/09/2019
ms.locfileid: "65480998"
---
# <a name="create-a-knowledge-base"></a>Создание базы знаний
  В этом разделе описано, как создать базу знаний в службах [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) и подготовить ее для управления доменами, обнаружения знаний или добавления политики сопоставления.  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Для создания базы знаний необходимо установить [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] и [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Для создания базы знаний необходимо иметь роль dqs_administrator или dqs_kb_editor в базе данных DQS_MAIN.  
  
##  <a name="Createaknowledgebase"></a> Create a knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запуск клиентского приложения Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] нажмите кнопку **Создать базу знаний**.  
  
3.  Введите имя и описание новой базы знаний.  
  
4.  В поле **Создать базу знаний из**выберите основу для базы знаний:  
  
    -   Выберите **Нет** , если новая база знаний не должна основываться на существующей базе знаний или файле данных.  
  
    -   Выберите **Существующая база знаний** , чтобы создать новую базу знаний на основе базе знаний, которая уже была создана на сервере [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], или на базе знаний по умолчанию. Выберите базу знаний из раскрывающегося списка **Выбор базы знаний** или нажмите кнопку **Обзор** , чтобы отобразить диалоговое окно **Выбор базы знаний** , выберите существующую базу знаний, на которой основывается существующая база знаний, а затем нажмите кнопку **ОК**. При выборе базы знаний из таблицы домены и правила сопоставления в базе знаний будут отображаться в правой части диалогового окна. Вы можете также выбрать базу знаний **Данные служб DQS** , которая является базой знаний по умолчанию, содержащей типовые готовые домены и наборы знаний, относящиеся к американской организации, адрес и данные стороны.  
  
    -   Выберите **Импортировать из файла DQS** , чтобы создать базу знаний на основе DQS-файла, расположенного на сервере [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Нажмите кнопку **Обзор**, выберите файл данных DQS с расширением DQS и нажмите кнопку **ОК**.  
  
5.  В поле **Выбор действия**выберите действие, которое нужно выполнить с новой базой знаний:  
  
    -   Нажмите кнопку **Управление доменами** , чтобы создать базу знаний и перейти на экраны, на которых можно изменить домены в базе знаний.  
  
    -   Нажмите кнопку **Обнаружение знаний** , чтобы создать базу знаний и запустить мастер, который позволяет проанализировать образец данных и заполнить домены базы знаний результатами анализа.  
  
    -   Выберите вариант **Политика сопоставления** , чтобы создать политику сопоставления и добавить ее в базу знаний.  
  
6.  Нажмите кнопку **Создать**.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После создания базы знаний  
 После создания базы знаний откроется мастер, с помощью которого можно выполнить обнаружение знаний, мастер для создания политики сопоставления или страницы для управления доменами. Дополнительные сведения об обнаружении знаний, управлении доменами и политике сопоставления см. в разделах [Обнаружение знаний](../../2014/data-quality-services/perform-knowledge-discovery.md), [Управление доменом](../../2014/data-quality-services/managing-a-domain.md) и [Создание политики сопоставления](../../2014/data-quality-services/create-a-matching-policy.md).  
  
  
