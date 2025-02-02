---
title: Поддержка параметров сортировки и Юникода | Документация Майкрософт
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- binary collations [SQL Server]
- expression-level collations [SQL Server]
- Windows collations [SQL Server]
- globalization [SQL Server], about globalization
- supplementary character support
- code pages [SQL Server], about code pages
- collations [SQL Server], about collations
- Unicode [SQL Server], collations
- database-level collations [SQL Server]
- reading order
- column-level collations
- locales [SQL Server], about locales
- locales [SQL Server]
- code pages [SQL Server]
- SQL Server collations
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97e66c1c276131876a8a74ab49627f43374cb78f
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775026"
---
# <a name="collation-and-unicode-support"></a>Collation and Unicode Support
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Параметры сортировки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляют свойства, управляющие правилами сортировки, учета регистра и диакритических знаков в данных. Параметры сортировки, используемые с символьными типами данных, такими как **char** и **varchar** , определяют кодовую страницу и соответствующие символы, которые могут использоваться для этого типа данных. Независимо от того, устанавливается ли новый экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], восстанавливается ли база данных из резервной копии или сервер соединяется с клиентскими базами данных, важно понимать требования к языковому стандарту, знать порядок сортировки и необходимость учета регистра или диакритических знаков в данных, с которыми вы работаете. Описание того, как сформировать список доступных параметров сортировки в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], см. в разделе [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md).    
    
При выборе параметров сортировки для сервера, базы данных, столбца или выражения данным присваиваются определенные характеристики, которые влияют на многие операции в базе данных. Например, если строится запрос с предложением `ORDER BY`, порядок результирующего набора может зависеть от параметров сортировки, которые применяются к базе данных, или предложения `COLLATE` на уровне выражения запроса.    
    
Для эффективного использования поддержки параметров сортировки в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]необходимо понимать термины этого раздела и их связь с характеристиками данных.    
    
##  <a name="Terms"></a> Термины, связанные с параметрами сортировки    
    
-   [Параметры сортировки](#Collation_Defn)    
    
-   [Локаль](#Locale_Defn)    
    
-   [Кодовая страница](#Code_Page_Defn)    
    
-   [Порядок сортировки](#Sort_Order_Defn)    
    
###  <a name="Collation_Defn"></a> Параметры сортировки    
Параметры сортировки задают битовые шаблоны, представляющие в наборе данных каждый символ. Параметры сортировки определяют правила, используемые при сортировке и сравнении данных. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает хранение объектов с различными параметрами сортировки в одной базе данных. Для столбцов в кодировке, отличающейся от Юникода, настройка параметров сортировки определяет кодовую страницу данных и соответствующую возможность представления символов. Данные, которые перемещаются между столбцами в форматах, отличных от Юникода, необходимо преобразовывать из исходной кодовой страницы в целевую.    
    
Результат выполнения инструкции[!INCLUDE[tsql](../../includes/tsql-md.md)] может различаться в зависимости от контекста различных баз данных, которые имеют свои параметры сортировки. По возможности используйте стандартные параметры сортировки для всей организации. Тем самым не придется явно указывать параметры сортировки для каждого символа или выражения Юникода. Если необходимо работать с объектами, имеющими различные параметры сортировки и кодовые страницы, создание запросов должно производиться с учетом очередности параметров сортировки. Дополнительные сведения см. в разделе [Очередность параметров сортировки (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md).    
    
Параметры сортировки могут учитывать регистр, диакритические знаки, тип японской азбуки, ширину символов, знаки выбора варианта. В [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] появился дополнительный параметр для кодирования [UTF-8](https://www.wikipedia.org/wiki/UTF-8). Эти параметры задаются путем их добавления к имени параметров сортировки. Например, параметр `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS_UTF8` определяет параметры сортировки с учетом диакритических знаков, регистра, типа японской азбуки, ширины символов и кодировки UTF-8. Еще один пример: параметр `Japanese_Bushu_Kakusu_140_CI_AI_KS_WS_VSS` определяет параметры сортировки без учета регистра, без учета диакритических знаков, с учетом типа японской азбуки, с учетом ширины символов, с учетом знаков выбора варианта и с использованием кодировки не в Юникоде. В следующей таблице описывается режим работы, связанный с этими параметрами.    
    
|Параметр|Описание|    
|------------|-----------------|    
|С учетом регистра (_CS)|Различаются буквы верхнего и нижнего регистров. При выборе этого параметра буквы нижнего регистра при сортировке ставятся перед соответствующими буквами верхнего регистра. Если этот параметр не выбран, параметры сортировки не учитывают регистр. То есть при сортировке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] считает буквы верхнего и нижнего регистров и делает их идентичными друг другу. Можно явно выбрать нечувствительность к регистру, указав параметр _CI.|    
|С учетом диакритических знаков (_AS)|Различаются символы с диакритическими знаками и без них. Например, "a" отлично от "ấ". Если этот параметр не выбран, параметры сортировки не учитывают диакритические знаки. То есть при сортировке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] рассматривает варианты букв с диакритическими знаками и без них как идентичные. Можно явно выбрать нечувствительность к диакритическим знакам, указав параметр _АI.|    
|С учетом типа японской азбуки (_KS)|Различаются два вида японской азбуки: хирагана и катакана. Если данный параметр не выбран, параметр сортировки не чувствителен к типу японской азбуки. То есть при сортировке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] рассматривает символы хирагана и катакана как идентичные. Пропуск этого параметра является единственным способом указания нечувствительности к типу японской азбуки.|    
|С учетом ширины символов (_WS)|Отличия между символами полной ширины и средней ширины. Если данный параметр не выбран, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] принимает отображение одного и того же символа полной ширины и средней ширины для целей сортировки как идентичное. Пропуск этого параметра является единственным способом указания нечувствительности к ширине символов.|    
|С учетом знаков выбора варианта (_VSS) | Различаются различные идеографические знаки выбора варианта в японских параметрах сортировки Japanese_Bushu_Kakusu_140 и Japanese_XJIS_140, впервые представленных в [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]. Последовательность вариантов состоит из базового знака и дополнительного знака выбора вариантов. Если этот параметр _VSS не выбран, параметры сортировки не учитывают знак выбора вариантов, а сам знак выбора вариантов не учитывается при сравнении. То есть при сортировке SQL Server считает символы, основанные на одном базовом символе, но с разными знаками выбора вариантов, равнозначными. См. также статью  [Unicode Ideographic Variation Database](https://www.unicode.org/reports/tr37/)(База данных идеографических вариантов Юникода). <br/><br/> Параметры сортировки с учетом знаков выбора варианта (_VSS) не поддерживаются в полнотекстовых индексах. Полнотекстовые индексы поддерживают только параметры с учетом диакритических знаков (_AS), типа японской азбуки (_KS) и ширины символов (_WS). Подсистемы CLR и XML в SQL Server не поддерживают знаки выбора варианта (_VSS).
|UTF-8 (_UTF8)|Позволяет хранить данные в кодировке UTF-8 в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Если этот параметр не выбран, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] использует формат кодировки по умолчанию (не в Юникоде) для подходящих типов данных.| 
    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает следующие наборы параметров сортировки:    
    
#### <a name="windows-collations"></a>параметры сортировки Windows    
Параметры сортировки Windows определяют правила хранения символьных данных на основе соответствующей локали системы Windows. Для параметров сортировки Windows сравнение данных в формате, отличном от Юникода, реализовано с помощью такого же алгоритма, как и для данных в Юникоде. Базовые правила параметров сортировки Windows задают алфавит или язык, используемый при сортировке по словарю, а также кодовую страницу, используемую для хранения символьных данных не в Юникоде. Сортировка в Юникоде и в других форматах совместима со строковым сравнением в соответствующей версии Windows. Тем самым обеспечивается согласованность обработки различных типов данных в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а разработчики получают возможность сортировать строки в приложениях по тем же правилам, что и в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в разделе [Имя параметров сортировки Windows (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md).    
    
#### <a name="binary-collations"></a>Двоичные параметры сортировки    
При двоичных параметрах сортировки данные сортируются на основе последовательности закодированных значений, определяемых локалью и типом данных. Регистр при этом учитывается. Параметры двоичной сортировки в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] определяют используемый языковой стандарт и кодовую страницу ANSI. При этом принудительно реализуется двоичный порядок сортировки. По причине своей относительной простоты параметры двоичной сортировки помогают повысить производительность приложений. Для типов данных не в Юникоде сравнение данных производится на основе кодовых точек, определенных кодовой страницей ANSI. Типы данных в Юникоде сравниваются на основе элементов кода Юникода. Для двоичных параметров сортировки на основе типов данных Юникода при сортировке данных локаль не учитывается. Например, параметры сортировки Latin_1_General_BIN и Japanese_BIN дают одинаковые результаты сортировки, если используются с данными в Юникоде.    
    
В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]существует два типа двоичной сортировки: старая сортировка **BIN** и новая сортировка **BIN2** . В сортировке **BIN2** все символы сортируются в соответствии с их кодовыми точками. В сортировке **BIN** только первый символ сортируется в соответствии с кодовой точкой, остальные символы сортируются в соответствии с их значениями байта. (Так как платформа Intel не всегда является архитектурой по порядку следования байтов, символы кода Unicode всегда хранятся с перестановкой байт).    
    
#### <a name="sql-server-collations"></a>параметры сортировки SQL Server    
Параметры сортировки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_\*) имеют обратную совместимость с более ранними версиями [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], с точки зрения порядка сортировки. Правила сортировки словаря для данных в формате, отличном от Юникода, не совместимы ни с какими процедурами сортировки операционных систем Windows. Однако сортировка данных в Юникоде совместима с правилами сортировки определенной версии Windows. Так как параметры сортировки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] применяют для данных в Юникоде и других форматах разные правила сравнения, при сравнении одних и тех же данных получаются разные результаты, которые зависят от базового типа данных. Дополнительные сведения см. в разделе [Имя параметров сортировки SQL Server (Transact-SQL)](../../t-sql/statements/sql-server-collation-name-transact-sql.md).    
    
> [!NOTE]    
> При обновлении англоязычной версии экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно задать параметры сортировки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL_\*), чтобы обеспечить совместимость с существующими экземплярами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Поскольку для экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] параметры сортировки по умолчанию определяются во время установки, очень важно правильно настроить параметры сортировки в следующих случаях.    
>     
> -   Код приложения зависит от поведения предыдущих параметров сортировки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .    
> -   Необходимо хранить символьные данные, в которых используется несколько языков.    
    
 Настройка параметров сортировки поддерживается на следующих уровнях экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
#### <a name="server-level-collations"></a>Параметры сортировки уровня сервера   
Параметры сортировки сервера по умолчанию, выбранные в процессе установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , становятся параметрами сортировки по умолчанию для системных баз данных и всех пользовательских баз данных. Обратите внимание, что параметры сортировки исключительно в Юникоде не выбираются во время установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , поскольку они не поддерживаются как параметры сортировки на уровне сервера.    
    
После назначения параметров сортировки серверу, изменить параметры можно будет только с помощью экспорта объектов базы данных, перестроения базы данных **master** и импорта всех объектов и данных базы данных. Вместо изменения параметров сортировки по умолчанию для экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]можно задать желаемые параметры сортировки при создании новой базы данных или столбца базы данных.    
    
#### <a name="database-level-collations"></a>Параметры сортировки уровня базы данных    
При создании или изменении базы данных можно задать параметры ее сортировки по умолчанию с помощью предложения COLLATE в инструкции CREATE DATABASE или ALTER DATABASE. Если параметры сортировки не указаны, базе данных назначаются параметры сортировки сервера.    
    
Невозможно изменить параметры сортировки системных баз данных с помощью изменения параметров сортировки сервера.    
    
Параметры сортировки базы данных используются для всех метаданных в базе данных, а также по умолчанию для всех строковых столбцов, временных объектов, имен переменных и любых других строковых объектов в базе данных. Когда вы изменяете сортировку базы данных пользователя, могут возникнуть конфликты сортировки, кода запросы в базе данных получают доступ к временным таблицам. Временные таблицы всегда хранятся в системной базе данных **tempdb**, которая использует параметры сортировки экземпляра. Запросы, сравнивающие символьные данные в пользовательской базе данных и **tempdb** , могут завершиться ошибкой, если параметры сортировки вызовут конфликт при оценке таких данных. Можно решить эту проблему, указав в запросе предложение COLLATE. Дополнительные сведения см. в разделе [COLLATE (Transact-SQL)](~/t-sql/statements/collations.md).    
    
#### <a name="column-level-collations"></a>Параметры сортировки уровня столбцов    
При создании или изменении таблицы можно указать параметры сортировки для каждого столбца символьной строки с помощью предложения COLLATE. Если параметры сортировки не указаны, то столбцу присваиваются параметры сортировки по умолчанию для базы данных.    
    
#### <a name="expression-level-collations"></a>Параметры сортировки уровня выражений    
Параметры сортировки уровня выражения задаются при выполнении инструкции, и они влияют на способ возврата результирующего набора. Это позволяет определить результаты сортировки предложения ORDER BY в соответствии с конкретным языковым стандартом. Для реализации параметров сортировки уровня выражения предложение COLLATE применяется следующим образом.    
    
```sql    
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;    
```    
    
###  <a name="Locale_Defn"></a> Локаль    
Локаль представляет собой набор сведений, связанных с местоположением или с культурой. В нее может входить имя и идентификатор языка, скрипт, применяемый для записи на нем, а также национальные стандарты. Параметры сортировки могут быть ассоциированы с одним или несколькими локалями. Дополнительные сведения см. в разделе [Номера локалей, назначаемые Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx).    
    
###  <a name="Code_Page_Defn"></a> Code Page    
 Кодовая страница — это упорядоченный набор символов данного скрипта, в котором числовой индекс или значение кодовой точки связано с каждым символом. Кодовую страницу Windows обычно называют *набором символов* или *кодировкой*. Кодовые страницы обеспечивают поддержку кодировок и раскладок клавиатуры, применяемых в различных локалях системы Windows.     
###  <a name="Sort_Order_Defn"></a> Sort Order    
 Порядок сортировки устанавливает способ сортировки значений данных. Это влияет на результаты сравнения данных. Данные сортируются с помощью параметров сортировки, и ее можно оптимизировать с помощью индексов.    
    
##  <a name="Unicode_Defn"></a> Поддержка Юникода    
Юникод — это стандартный способ сопоставления кодовой точки символам. Поскольку он разработан для поддержки всех символов всех языков, различные кодовые страницы для поддержки разных наборов символов больше не требуются. Символьные данные на нескольких языках в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (с [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] по [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) следует всегда хранить в Юникоде (UTF-16; типы данных — **nchar**, **nvarchar** и **ntext**), а не использовать другие типы данных (**char**, **varchar** и **text**). Кроме того, начиная с [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], если используется сортировка UTF-8 (\_UTF8), то предыдущие типы данных, отличные от Юникода, (**char** и **varchar**) становятся типами данных Юникода (UTF-8). 

> [!NOTE]
> В [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] не изменяется поведение ранее существующих типов данных (**nchar**, **nvarchar** и **ntext**) Юникода (UTF-16).   
    
Типы данных, отличные от Юникода, имеют значительные ограничения. Это происходит по той причине, что на компьютере, где не применяется Юникод, можно использовать только одну кодовую страницу. Применение Юникода позволяет повысить производительность, поскольку требуется выполнять меньше преобразований кодовых страниц. Параметры сортировки в Юникоде следует выбирать индивидуально на уровне базы данных, столбца или выражения, так как они не поддерживаются на уровне сервера.    
    
Кодовая страница, используемая клиентом, определяется параметрами операционной системы. Чтобы установить кодовую страницу клиента в операционной системе Windows, используйте раздел **Язык и региональные стандарты** на панели управления.    
    
При переносе данных из сервера на клиент старые клиентские драйверы могут не распознать параметры сортировки сервера. Это может произойти при передаче данных с сервера с поддержкой Юникода на клиент без поддержки Юникода. Лучшим вариантом может быть обновление операционной системы клиента, чтобы обновить параметры сортировки базовой системы. Если на клиенте установлена клиентская программа базы данных, можно попробовать применить обновление службы к клиентской программе базы данных.    
    
Можно также попробовать использовать другие параметры сортировки для данных на сервере. Выберите параметры сортировки, соответствующие кодовой странице в клиенте.    
    
Чтобы воспользоваться доступными в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] параметрами сортировки UTF-16 для оптимизации поиска и сортировки некоторых символов Юникода (только параметры сортировки Windows), можно выбрать один из параметров сортировки поддержки дополнительных символов (\_SC) или один из параметров сортировки версии 140.    
 
Чтобы воспользоваться доступными в [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] параметрами сортировки UTF-8 для оптимизации поиска и сортировки некоторых символов Юникода (только параметры сортировки Windows), необходимо выбрать параметры сортировки для кодировки UTF-8 (\_UTF8).
 
-   Флаг UTF8 может применяться к следующим параметрам сортировки:    
   
    -   Параметры сортировки версии 90 
    
        > [!NOTE]
        > Только когда в этой версии уже существуют дополнительные символы (\_SC) или сортировка с учетом знаков выбора варианта (\_VSS).
    
    -   Параметры сортировки версии 100    
    
    -   Параметры сортировки версии 140   
    
    -   Параметры двоичной сортировки BIN2<sup>1</sup>
    
-   Флаг UTF8 не может применяться к следующим параметрам сортировки:    
    
    -   Параметры сортировки версии 90, которые не поддерживают дополнительные символы (\_SC) или с учетом знаков выбора варианта (\_VSS).    
    
    -   Параметры двоичной сортировки BIN и BIN2<sup>2</sup>    
    
    -   Параметры сортировки SQL\*  
    
<sup>1</sup> Начиная с [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3     
<sup>2</sup> Начиная с [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.3
    
Чтобы получить представление о трудностях, связанных с применением типов данных в Юникоде или не в Юникоде, протестируйте свой сценарий, измерив разницу производительности для этих двух вариантов в вашей среде. Рекомендуется стандартизировать системные параметры сортировки, которые используются в организации, а там, где это возможно, — развертывать серверы и клиенты с поддержкой Юникода.    
    
Во многих случаях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] взаимодействует с другими серверами или клиентами, поэтому в организации может использоваться несколько стандартов доступа к данным для приложений и экземпляров серверов. Клиенты[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] могут быть двух видов:    
    
-   **Клиенты с поддержкой Юникода** , применяющие OLE DB и ODBC версии 3.7 или более поздних версий.    
    
-   **Клиенты без поддержки Юникода** , применяющие библиотеку баз данных и ODBC версий 3.6 или более ранних версий.    
    
В следующей таблице приведены сведения по применению данных на нескольких языках с различными сочетаниями серверов, поддерживающих и не поддерживающих Юникод.    
    
|Сервер|Клиент|Преимущества или ограничения|    
|------------|------------|-----------------------------|    
|Юникод|Юникод|Так как данные в Юникоде широко используются в системе, этот сценарий обеспечивает наилучшую производительность и защиту полученных данных от повреждения. Это случай применения ActiveX (ADO), OLE DB, а также ODBC версий 3.7 или более поздних версий.|    
|Юникод|Не Юникод|В этом случае при перемещении данных на клиентский компьютер возможны ограничения или ошибки, особенно если сервер под управлением новой операционной системы соединяется с клиентом старой версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]и под управлением старой операционной системы. Предпринимается попытка преобразовать находящиеся на сервере данные в Юникоде с помощью соответствующей кодовой страницы в клиенте, кодировка которого отлична от Юникода.|    
|Не Юникод|Юникод|Это не лучшая конфигурация для работы с данными на нескольких языках. Невозможно записать данные в Юникоде на сервер, работающий не в Юникоде. Вероятнее всего, неполадки могут произойти при отправке данных на серверы, которые поддерживают другие кодовые страницы.|    
|Не Юникод|Не Юникод|В этом сценарии очень много ограничений для применения данных на нескольких языках. Можно использовать только одну кодовую страницу.|    
    
##  <a name="Supplementary_Characters"></a> Дополнительные символы    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляет такие типы данных, как **nchar** и **nvarchar**, для хранения данных Юникода (UTF-16) при любом параметре сортировки и типы данных, такие как **char** и **varchar**, для хранения данных Юникода (UTF-8) при параметре сортировки для UTF-8 (\_UTF8). Эти типы данных кодируют текст в формате *UTF-16* и *UTF-8* соответственно. Консорциум Юникода назначает каждому символу уникальную кодовую точку, лежащую в диапазоне от 0x0000 до 0x10FFFF. Наиболее часто используемые символы имеют значения кодовых точек, умещающиеся в 8-разрядное или 16-разрядное слово в памяти и на диске, но символы с кодовыми точками более 0xFFFF требуют для хранения от двух до четырех последовательных 8-разрядных слов (UTF-8) или два последовательных 16-разрядных слова (UTF-16). Они называются *дополнительными символами*, а дополнительные последовательные 8-разрядные или 16-разрядные слова — *суррогатной парой*.    
    
Представленное в [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] новое семейство параметров сортировки дополнительных символов (\_SC) может использоваться с типами данных **nchar**, **nvarchar** и **sql_variant**. Например: `Latin1_General_100_CI_AS_SC`или (при использовании параметров сортировки для японского языка) `Japanese_Bushu_Kakusu_100_CI_AS_SC`. 
 
В [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] расширяется поддержка дополнительных символов для типов данных **char** и **varchar** с новыми параметрами сортировки для UTF-8 (\_UTF8).   

Начиная с [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], все новые параметры сортировки автоматически поддерживают дополнительные символы.

Если используются дополнительные символы:    
    
-   Дополнительные символы могут применяться в операциях сортировки и сравнения только в параметрах сортировки с версией 90 или выше.    
    
-   Все новые параметры сортировки версии 100 поддерживают лингвистическую сортировку с обработкой дополнительных символов.    
    
-   Дополнительные символы не поддерживаются в метаданных (например, в именах объектов баз данных).    
    
-   Для баз данных, в которых используются параметры сортировки с дополнительными символами (\_SC), нельзя включить репликацию [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Это связано с тем, что некоторые из системных таблиц и хранимых процедур, создаваемых для репликации, используют старый тип данных **ntext**, который не поддерживает дополнительные символы.  
    
-   Флаг SC может применяться к следующим параметрам сортировки:    
    
    -   Параметры сортировки версии 90    
    
    -   Параметры сортировки версии 100    
    
-   Флаг SC не может применяться к следующим параметрам сортировки:    
    
    -   Параметры сортировки Windows версии 80 и ниже    
    
    -   Параметры двоичной сортировки BIN и BIN2    
    
    -   Параметры сортировки SQL\*    
    
    -   Параметры сортировки версии 140 (им не требуется флаг SC, так как они уже поддерживают дополнительные символы)    
    
В следующей таблице сравнивается поведение некоторых строковых функций и строковых операторов при использовании дополнительных символов с параметрами сортировки, поддерживающими дополнительные символы (SCA) и без них.    
    
|Строковая функция или оператор|С параметрами сортировки, поддерживающими дополнительные символы (SCA)|Без параметров сортировки, поддерживающих дополнительные символы|    
|---------------------------------|--------------------------|-----------------------------|    
|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)<br /><br /> [LEN](../../t-sql/functions/len-transact-sql.md)<br /><br /> [PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|Суррогатные пары UTF-16 считаются одной кодовой точкой.|Суррогатные пары UTF-16 считаются двумя кодовыми точками.|    
|[LEFT](../../t-sql/functions/left-transact-sql.md)<br /><br /> [REPLACE](../../t-sql/functions/replace-transact-sql.md)<br /><br /> [REVERSE](../../t-sql/functions/reverse-transact-sql.md)<br /><br /> [RIGHT](../../t-sql/functions/right-transact-sql.md)<br /><br /> [SUBSTRING](../../t-sql/functions/substring-transact-sql.md)<br /><br /> [STUFF](../../t-sql/functions/stuff-transact-sql.md)|Эти функции обрабатывают каждую суррогатную пару как одну кодовую точку и работают ожидаемым образом.|Эти функции могут разорвать любые суррогатные пары, что может привести к непредвиденным результатам.|    
|[NCHAR](../../t-sql/functions/nchar-transact-sql.md)|Возвращает символ, соответствующий заданному значению кодовой точки в Юникоде в диапазоне от 0 до 0x10FFFF. Если указанное значение лежит в диапазоне от 0 до 0xFFFF, то возвращается один символ. Для больших значений возвращается соответствующая суррогатная пара.|Если значение превышает 0xFFFF, то вместо соответствующей суррогатной пары возвращается значение NULL.|    
|[UNICODE](../../t-sql/functions/unicode-transact-sql.md)|Возвращает кодовую точку UTF-16 в диапазоне от 0 до 0x10FFFF.|Возвращает кодовую точку UCS-2 в диапазоне от 0 до 0xFFFF.|    
|[Шаблон — совпадение одного символа](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)<br /><br /> [Шаблон — несовпадающие символы](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)|Дополнительные символы поддерживаются для всех операций с символами-шаблонами.|Дополнительные символы не поддерживаются для этих операций с символами-шаблонами. Поддерживаются другие операторы символов-шаблонов.|    
    
##  <a name="GB18030"></a> Поддержка GB18030    
 GB18030 — это отдельный стандарт, который применяется в Китайской Народной Республике для кодирования китайских иероглифов. В кодировке GB18030 введенные данные могут иметь длину 1, 2 или 4 байт. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляет поддержку символов GB18030, распознает их при вводе из клиентского приложения, преобразуя и сохраняя в виде символов Юникода. После сохранения на сервере эти символы при выполнении всех последующих операций рассматриваются как символы Юникода. Можно использовать любые параметры сортировки для китайского языка. Желательно использовать последнюю версию (100). Все параметры сортировки уровня 100 поддерживают лингвистическую сортировку при использовании символов GB18030. Если данные содержат дополнительные символы (суррогатные пары), для оптимизации поиска и сортировки можно использовать параметры сортировки SC, доступные в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .    
    
##  <a name="Complex_script"></a> Поддержка сложных скриптов    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает ввод, хранение, изменение и отображение наборов сложных скриптов. Ниже приведены типы сложных скриптов:    
    
-   Скрипты с языками с различным направлением письма, например сочетание английского и арабского текстов.    
-   Скрипты, в которых форма символов изменяется в зависимости от их положения или где сочетаются разные символы (например, в арабском, хинди, тайском).    
-   Для таких языков как тайский требуются внутренние словари для распознавания слов, поскольку между словами нет пробелов.    
    
Приложения баз данных, взаимодействующие с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , должны применять управляющие элементы, которые поддерживают сложные скрипты. Стандартные средства управления формами Windows, которые создаются в управляемом коде, поддерживают сложные сценарии.    

##  <a name="Japanese_Collations"></a> Параметры сортировки для японского языка, добавленные в  [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]
 
Начиная с версии [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], поддерживаются новые семейства параметров сортировки для японского языка с перестановками различных параметров (\_CS, \_AS, \_KS, \_WS, \_VSS). 

Чтобы получить список этих параметров сортировки, можно выполнить запрос [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:      

```sql 
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name LIKE 'Japanese_Bushu_Kakusu_140%' OR Name LIKE 'Japanese_XJIS_140%'
``` 

Все новые параметры сортировки имеют встроенную поддержку дополнительных символов, поэтому ни у одного нового параметра сортировки нет флага SC.

Эти параметры сортировки поддерживаются в индексах ядра СУБД, оптимизированных для памяти таблицах, индексах columnstore и модулях, скомпилированных в собственном коде.

<a name="ctp23"></a>

## <a name="utf-8-support"></a>Поддержка UTF-8.

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] обеспечивает полную поддержку широко используемой кодировки символов UTF-8 как кодировки импорта или экспорта или как параметров сортировки на уровне столбцов и базы данных для текстовых данных. Кодировка символов UTF-8 допускается в типах данных `CHAR` и `VARCHAR`. Она активируется при создании параметров сортировки с суффиксом `UTF8` или изменении существующих параметров на такие. 

Например, `LATIN1_GENERAL_100_CI_AS_SC` меняется на `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. UTF-8 доступна только для параметров сортировки Windows, которые поддерживают дополнительные символы, представленные в [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. `NCHAR` и `NVARCHAR` допускают только кодирование UTF-16 и остаются неизменными.

Эта функция может обеспечить значительную экономию места в хранилище в зависимости от используемой кодировки. Например, изменение имеющегося типа данных столбца со строками в кодировке ASCII (латинская) с `NCHAR(10)` на `CHAR(10)` с использованием параметров сортировки для UTF-8 на 50 % снижает требования к хранению. Это снижение связано с тем, что `NCHAR(10)` требует для хранения 20 байт, тогда как `CHAR(10)` требует 10 байт для той же строки Юникод.

##  <a name="Related_Tasks"></a> Связанные задачи    
    
|Задача|Раздел|    
|----------|-----------|    
|Описание задания или изменения параметров сортировки экземпляра SQL Server.|[Задание или изменение параметров сортировки сервера](../../relational-databases/collations/set-or-change-the-server-collation.md)|    
|Описание задания или изменения параметров сортировки пользовательской базы данных.|[Установка и изменение параметров сортировки базы данных](../../relational-databases/collations/set-or-change-the-database-collation.md)|    
|Описание задания или изменения параметров сортировки столбца в базе данных.|[Задание или изменение параметров сортировки столбца](../../relational-databases/collations/set-or-change-the-column-collation.md)|    
|Описание способа возврата сведений о параметрах сортировки на уровне сервера, базы данных или столбца.|[Просмотр сведений о параметрах сортировки](../../relational-databases/collations/view-collation-information.md)|    
|Описывается способ написания инструкций Transact-SQL, которые имеют большую степень языковой переносимости или лучше поддерживают несколько языков.|[Написание инструкций Transact-SQL, адаптированных к международному использованию](../../relational-databases/collations/write-international-transact-sql-statements.md)|    
|Описание способа изменения языка сообщений об ошибках и параметров отображения времени и валюты.|[Задание языка сеанса](../../relational-databases/collations/set-a-session-language.md)|    
    
##  <a name="Related_Content"></a> См. также    
[Рекомендованные изменения параметров сортировки SQL Server](https://go.microsoft.com/fwlink/?LinkId=113891)    
[Использование символьного формата Юникод для импорта и экспорта данных (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)        
[Написание инструкций Transact-SQL, адаптированных к международному использованию](../../relational-databases/collations/write-international-transact-sql-statements.md)     
[Рекомендации по миграции SQL Server на Юникод](https://go.microsoft.com/fwlink/?LinkId=113890) — больше не поддерживаются   
[Веб-сайт консорциума Юникод](https://go.microsoft.com/fwlink/?LinkId=48619)    
    
## <a name="see-also"></a>См. также статью    
[Параметры сортировки автономной базы данных](../../relational-databases/databases/contained-database-collations.md)     
[Выбор языка при создании полнотекстового индекса](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)     
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)    
    
 
