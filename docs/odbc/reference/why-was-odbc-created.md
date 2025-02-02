---
title: Зачем создали ODBC? | Документы Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 871919554975f04fae0aeaa1b8e6ec684c6650a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714151"
---
# <a name="why-was-odbc-created"></a>Зачем создали ODBC?
Исторически сложилось так, что компании использовали один СУБД. Через внешний интерфейс этой системы или с помощью приложения, написанные для работы исключительно с этой системой, было сделано все доступа к базе данных. Тем не менее роста использования компьютеров и дополнительные компьютерное оборудование и программное обеспечение стала доступной, для получения разных СУБД работы компании. Причины были множество: Люди, приобрел, какой параметр имел самые дешевые, какой параметр имел самый быстрый, и тем, что им уже знали, какой параметр имел последнюю на рынке, что лучше всего работает для одного приложения. По другим причинам были реорганизации и слияния, где отделов, которые ранее имели единый СУБД теперь серьезные улучшения.  
  
 Проблема даже по мере роста сложности с появлением персональных компьютеров. Эти компьютеры в целый ряд средств для запросов, анализа и отображения данных, а также несколько баз данных, недорогой и простой в использовании. В дальнейшем корпорацией часто настраивали данные разбиты на множество ПК, серверы и миникомпьютеры, сохраненные в разнообразных несовместимые баз данных и осуществляется очень большое количество различных средств, некоторые из которых может получить все данные.  
  
 Последний запрос поступил с появлением клиент серверная, который стремится облегчить наиболее эффективного использования ресурсов компьютера. Недорогое персональные компьютеры (клиенты) располагаются на рабочем столе и укажите оба это графический интерфейс для данных и ряд недорогих средствах, таких как электронные таблицы, диаграммы, программы и создателям отчетов. Разместить СУБД, где они могут использовать свои вычислительную мощность и центрального расположения для предоставления доступа к данным, быстрый, хорошо скоординированную, миникомпьютеры и компьютеры, называвшиеся мэйнфреймами (серверов). Как было переднего плана программного обеспечения должен быть подключен к серверным базам данных?  
  
 Подобная проблема чаще сталкиваются независимых поставщиков программного обеспечения (ISV). Написание программного обеспечения базы данных для миникомпьютеры и мэйнфреймами поставщиков обычно приходилось писать одну версию приложения для каждого СУБД или написание кода для конкретных СУБД для каждого СУБД, они хотели получить доступ к. Поставщики, написание программного обеспечения для персональных компьютеров приходилось писать процедуры доступа данных для каждого разных СУБД, с которым они хотели бы работать. Часто это означало, написание и поддержку доступа к данным, подпрограммы, а не приложений и приложений часто были проданы не на их качество, но на ли они доступ данные в заданной СУБД затрачено огромное количество ресурсов.  
  
 То, что оба вида разработчикам требовалось был способ доступа к данным в различных СУБД. Группы компьютеров с миникомпьютер необходим способ слияния данных из разных СУБД в одном приложении, хотя группе персонального компьютера требуется эта возможность, а также способ написать одно приложение, независимо от любой один СУБД. Короче говоря обе группы требуется совместимый способ доступа к данным; они требуется открыть подключение к базе данных.
