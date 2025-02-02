---
title: Создание почтовых наклеек в Microsoft Word с использованием данных Visual FoxPro | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data [ODBC], mailing labels
- Visual FoxPro data [ODBC], Word
- mailing labels [ODBC]
- Visual FoxPro ODBC driver [ODBC], Word
- FoxPro ODBC driver [ODBC], word
ms.assetid: c901b60c-9f84-407a-b3d1-b4d301a71370
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c759e530baf792de7e015eac87337f35cf9f5a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312537"
---
# <a name="creating-mailing-labels-in-microsoft-word-using-visual-foxpro-data"></a>Создание почтовых наклеек в Microsoft Word с использованием данных Visual FoxPro
Можно использовать данных Visual FoxPro в Microsoft Word для Windows 95 или Windows 98 документа. Например может потребоваться создание почтовых наклеек с сведения о клиенте, хранятся в таблице Visual FoxPro.  
  
### <a name="to-create-mailing-labels"></a>Создание почтовых наклеек  
  
1.  В Microsoft Word создайте новый документ.  
  
2.  В меню "Сервис" выберите слияния.  
  
3.  Во вспомогательном методе слияния выберите команду Создать, а затем выберите метки рассылки.  
  
4.  В области основного документа выберите активного окна.  
  
5.  В источнике данных выберите получение данных, а затем выберите тип источника данных.  
  
6.  В диалоговом окне Открыть источник данных выберите MS Query.  
  
7.  В диалоговом окне Выбор источника данных выберите источник данных Visual FoxPro и нажмите кнопку использования.  
  
8.  Если база данных, поддерживаемого источника данных содержит таблицы, выберите таблицу, в диалоговом окне Добавить таблицы. Microsoft Query Отображает добавлена таблица в верхней части конструктора запросов.  
  
9. Выберите поля для запроса, перетащив их из таблицы в нижней части конструктора.  
  
10. В меню «Файл» выберите возврат данных в Microsoft Word. Закрывает Microsoft Query, и выбранные данные доступна для использования в документ слияния.  
  
11. В области основного документа выберите программу установки.  
  
12. В диалоговом окне Параметры меток выберите принтера и метка сведений и затем щелкните ОК.  
  
13. В диалоговом окне создания метки выберите поля, которые вы хотите напечатать на почтовых наклеек, а затем нажмите кнопку ОК.  
  
14. Во вспомогательном методе слияния слияния данных с документом, установите для слияния.  
  
15. В диалоговом окне слияния выберите параметры и нажмите кнопку объединить.
