---
title: Шаг 1. Настройка проекта Visual Basic | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b5f6379eb6cfc1d0f9020019d543cda180d9d88b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700611"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Шаг 1. Настройка проекта Visua Basic
В этом сценарии предполагается наличие Microsoft Visual Basic 6.0, ADO 2.5 или более поздней версии и поставщик Microsoft OLE DB для публикаций в Интернете на компьютере. Вы сначала создайте новый проект и затем добавить некоторые элементы управления в форму по умолчанию в проекте.  
  
### <a name="to-create-an-ado-project"></a>Чтобы создать проект ADO:  
  
1.  В Microsoft Visual Basic, создайте новый проект Standard EXE.  
  
2.  Из меню «Проект» выберите команду "ссылки".  
  
3.  Выберите «Microsoft ActiveX данных объектов 2.5 библиотека» и нажмите кнопку ОК.  
  
### <a name="to-insert-controls-on-the-main-form"></a>Чтобы добавить элементы управления в форме:  
  
1.  Добавьте элемент управления ListBox в форму Form1. Значение свойства Name **lstMain**.  
  
2.  Добавьте другой элемент управления ListBox в форму Form1. Значение свойства Name **lstDetails**.  
  
3.  Добавьте элемент управления TextBox в форму Form1. Значение свойства Name **txtDetails**.  
  
## <a name="see-also"></a>См. также  
 [Сценарий публикации в Интернете](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Шаг 2. Инициализация главного списка](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
