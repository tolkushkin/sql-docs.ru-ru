---
title: Оптимизированная для памяти файловая группа | Документация Майкрософт
ms.custom: ''
ms.date: 11/19/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 64402f73fdf43c0ebcbeff338ed72d56d55227be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155574"
---
# <a name="the-memory-optimized-filegroup"></a>Оптимизированная для памяти файловая группа
  Для создания оптимизированных для памяти таблиц необходимо сначала создать оптимизированную для памяти файловую группу. Оптимизированная для памяти файловая группа содержит один или несколько контейнеров. В каждом контейнере содержатся файлы данных или разностных файлы (или и те и другие).  
  
 Даже если строки данных из таблиц `SCHEMA_ONLY` не сохраняются, а метаданные оптимизированных для памяти таблиц и компилированных в собственном коде хранимых процедур хранятся в традиционных каталогах, модулю [!INCLUDE[hek_2](../../includes/hek-2-md.md)] все равно требуется оптимизированная для памяти файловая группа для оптимизированных для памяти таблиц `SCHEMA_ONLY`, чтобы обеспечить согласованную работу баз данных, в которых есть оптимизированные для памяти таблицы.  
  
 В основе оптимизированной для памяти файловой группы лежит файловая группа FILESTREAM, но при этом имеются следующие отличия.  
  
-   Можно создать только одну оптимизированную для памяти файловую группу для одной базы данных. Необходимо явно пометить файловую группу как содержащую данные memory_optimized_data. Файловую группу можно создать при создании базы данных или же добавить ее позднее.  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   В файловую группу MEMORY_OPTIMIZED_DATA необходимо добавить один или несколько контейнеров. Пример:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   Для создания оптимизированной для памяти файловой группы не требуется включать файловый поток ([Включение и настройка FILESTREAM](../blob/enable-and-configure-filestream.md)). Сопоставление с файловым потоком выполняется модулем [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
-   В оптимизированную для памяти файловую группу можно добавлять новые контейнеры. Может потребоваться новый контейнер для расширения пространства, необходимого для устойчивых таблиц, оптимизированных для памяти и также распределять по нескольким контейнерам ввода-вывода.  
  
-   Перемещение данных в оптимизированной для памяти файловой группе оптимизировано в конфигурации группы доступности AlwaysOn. В отличие от файлов FILESTREAM, которые отправляются во вторичные реплики, файлы контрольных точек (файлы данных и разностные файлы) из оптимизированной для памяти файловой группы не отправляются во вторичные реплики. Файлы данных и разностные файлы формируются на вторичной реплике с помощью журнала транзакций.  
  
Далее приведены ограничения оптимизированной для памяти файловой группы.  
  
-   После создания оптимизированной для памяти файловой группы удалить ее можно только после удаления базы данных. В рабочей среде возникновение необходимости в удалении оптимизированной для памяти файловой группы маловероятно.  
  
-   Невозможно удалить контейнер, который не является пустым, или перемещать пары, состоящие из файла данных и разностного файла, в другой контейнер в оптимизированной для памяти файловой группе.  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Настройка оптимизированной для памяти файловой группы  
Рекомендуется создать несколько контейнеров в оптимизированной для памяти файловой группе и разместить их на разных дисках, чтобы получить большую пропускную способность по потоковой передаче данных в память.  
  
При настройке хранилища необходимо обеспечить наличие свободного места на диске, которое будет в четыре раза больше размера надежных, оптимизированных для памяти таблиц. Убедитесь, что подсистема ввода-вывода поддерживает необходимое значение IOPS для рабочей нагрузки. Если пары файлов данных и разностных файлов заполняются при данном IOPS, необходимо в три раза увеличить IOPS с учетом операций сортировки и объединения. Можно увеличить объем хранилища и IOPS путем добавления в оптимизированную для памяти файловую группу одного или нескольких контейнеров.  
  
При использовании нескольких контейнеров, размещенных на нескольких дисках, файлы данных и разностные файлы распределяются по контейнерам путем циклического перебора. Первый файл данных выделяется из первого контейнера, разностный файл — из следующего контейнера, после чего дальнейшее выделение производится таким же образом. Эта схема выделения позволяет равномерно распределять файлы данных и разностные файлы по контейнерам при наличии нечетного числа дисков, каждый из которых сопоставлен с одним контейнером. Однако при наличии четного числа дисков, каждый из которых сопоставлен с одним контейнером, хранилище может получиться несбалансированным, когда файлы данных будут сопоставляться с нечетными дисками, а разностные файлы — с четными. Для получения сбалансированного потока ввода-вывода по восстановлению, рекомендуется размещать пары файлов данных и разностных на том же шпинделе/хранилище, как описано в следующем примере.  

> [!CAUTION]
> Если значение `MAXSIZE` задается для оптимизированной для памяти файловой группы и файлы контрольных точек превышают максимальный размер контейнера, база данных будет помечена как подозрительная (SUSPECT).   
> В этом случае не пытайтесь задать для базы данных режим OFFLINE и ONLINE, так как это приведет к переходу базы данных в состояние RECOVERY_PENDING.
  
### <a name="example"></a>Пример 
Рассмотрим оптимизированную для памяти файловую группу с двумя контейнерами: контейнер 1 на диске X и контейнер 2 на диске Y.  
Поскольку размещение файлов данных и разностных файлов осуществляется путем циклического перебора, в контейнере 1 будут находиться только файлы данных, а в контейнере 2 — только разностные файлы, что ведет к дисбалансу операций сохранения и ввода-вывода в секунду, поскольку файлы данных значительно больше, чем разностные файлы.    
Чтобы равномерно распределить файлы данных и разностные файлы по дискам X и Y, создайте четыре, а не два контейнера и сопоставить первые два контейнера с диском X, а следующие два контейнера с диском Y.  
С помощью циклического распределения файл данных и первой разностный файл выделяется из контейнера-1 и 2 соответственно, которой сопоставлены с диском X.   
Аналогичным образом следующий файл данных и разностных выделяется из контейнера-3 и 4, которые сопоставлены с диском Y. Благодаря этому распределение данных и разностных файлов по двум дискам равномерно.  
 
  
## <a name="see-also"></a>См. также  
[Создание и управление хранилищем для оптимизированных для памяти объектов](creating-and-managing-storage-for-memory-optimized-objects.md)     
[Файлы и файловые группы базы данных](../../relational-databases/databases/database-files-and-filegroups.md)    
  
