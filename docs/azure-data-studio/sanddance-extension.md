---
title: SandDance для Studio данных Azure
titleSuffix: Azure Data Studio
description: Как использовать SandDance студии данных Azure
ms.custom: seodec18
ms.date: 04/18/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 683aea4066c0b27db295cc07db31ecd07fb33245
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798081"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>SandDance для Studio данных Azure (Предварительная версия)
Azure Data Studio предлагает способ создания быстрого визуализации для файлов CSV и .tsv, вы работаете. Сюда входят локальные файлы или файлы в HDFS в ваш кластер SQL Server 2019 больших данных. Это расширение полезно в тех случаях, когда вы пытаетесь имеют быстрого просмотра данных и понять, что происходит. Мы используем технологию, которая называется SandDance от Microsoft Research, которые можно создавать визуализации данных на месте.

![анимация sanddance](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

С помощью простой для понимания представлений, SandDance помогает получить ценные сведения о данных, и это в справке свою очередь, вы указываете истории, поддерживаемых данными, построение случаев на основе свидетельства, проверки гипотез, более глубокого анализа в поверхности объяснения, поддержки принятия решений для покупок, или связывание данных в контексте шире, практические примеры.

SandDance использует единицы визуализации, применимые взаимно-однозначное сопоставление между строками в базе данных и метки на экране.
Smooth анимированные переходы между представлениями помогает поддерживать контекст, как взаимодействовать с данными.

## <a name="usage"></a>Использование

Начиная с меню "файл" Открыть папку открыть помощью или [Ctrl + K, Ctrl + O] каталог, содержащий. CSV-файл.  Затем из панели обозревателя правой кнопкой мыши файл CSV-файла или .tsv, а выберите *представления в SandDance*.

Щелкните правой кнопкой мыши на CSV-файл или TSV-файл в HDFS, если вы подключены к кластеру больших данных SQL Server 2019 г. и выберите *представления в SandDance*.

## <a name="known-issues"></a>Известные проблемы

В настоящее время данные должны иметь первый столбец как уникальный идентификатор.

В настоящее время мы не ограничение на число строк, которые визуализируются. Тем не менее потребление памяти возрастает пропорционально количеству строк, поэтому рекомендуется только около 100 тыс. строк в наборе данных или представлении.

См. в разделе [известные проблемы](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>Заметки о выпуске

### <a name="100"></a>1.0.0

Первоначальный выпуск azdata sanddance

## <a name="next-steps"></a>Следующие шаги
Дополнительные сведения, [посетите репозиторий GitHub.](https://github.com/Microsoft/SandDance)
