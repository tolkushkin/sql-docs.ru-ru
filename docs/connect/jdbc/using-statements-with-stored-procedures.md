---
title: Использование инструкций с помощью хранимых процедур | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2dd4ead601700baefaf356840fba4184ab427ef2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798544"
---
# <a name="using-statements-with-stored-procedures"></a>Использование инструкций с хранимыми процедурами

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Хранимая процедура является процедурой базы данных, схожей с процедурой на других языках программирования, которая хранится в самой базе данных. В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно создавать хранимые процедуры с помощью [!INCLUDE[tsql](../../includes/tsql-md.md)] или общеязыковой среды выполнения (CLR) и одного из поддерживаемых Visual Studio языков программирования, например Visual Basic или C#. Как правило, хранимые процедуры [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] могут выполнять следующие операции:  
  
- принимать входные параметры и возвращать вызывающей процедуре или пакету ряд значений в виде выходных параметров;  
  
- содержать программные инструкции, которые выполняют операции в базе данных, в том числе вызывающие другие процедуры;  
  
- возвращать значение состояния вызывающей процедуре или пакету, таким образом передавая сведения об успешном или неуспешном завершении (и причины последнего).  
  
> [!NOTE]  
> Дополнительные сведения о хранимых процедурах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] см. в статье "Основные сведения о хранимых процедурах" электронной документации по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Для работы с данными в базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с использованием хранимых процедур драйвер [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] содержит классы [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) и [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Выбор класса для использования зависит от того, какие IN (входные) или OUT (выходные) параметры требуются хранимой процедуре. Если хранимая процедура не требует параметров IN или OUT, можно использовать класс SQLServerStatement; если хранимая процедура будет вызываться несколько раз или требует только параметры IN, можно использовать класс SQLServerPreparedStatement. Если хранимая процедура требует IN и параметров OUT, следует использовать класс SQLServerCallableStatement. Необходимо использовать класс SQLServerCallableStatement только в том случае, когда хранимая процедура требует использования параметров OUT.  
  
> [!NOTE]  
> Хранимые процедуры могут также возвращать счетчики обновлений и несколько результирующих наборов. Дополнительные сведения см. в разделе [с помощью хранимых процедур со счетчиком обновлений](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) и [с помощью нескольких результирующих наборов](../../connect/jdbc/using-multiple-result-sets.md).  
  
При использовании драйвера JDBC для вызова хранимой процедуры с параметрами следует использовать escape-последовательность SQL `call` вместе с методом [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) класса [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Ниже приводится полный синтаксис escape-последовательности`call`:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
> Дополнительные сведения о `call` и другие SQL escape-последовательности, см. в разделе [с помощью escape-последовательностей SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
В этом разделе описываются способы вызова хранимых процедур [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью драйвера JDBC и escape-последовательности SQL `call`.  
  
## <a name="in-this-section"></a>в этом разделе  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Использование хранимых процедур без параметров](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|Описывает способы использования драйвера JDBC для запуска хранимых процедур, не содержащих входных или выходных параметров.|  
|[Использование хранимых процедур с входными параметрами](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|Описывает способы использования драйвера JDBC для запуска хранимых процедур, содержащих входные параметры.|  
|[Использование хранимых процедур с выходными параметрами](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|Описывает способы использования драйвера JDBC для запуска хранимых процедур, содержащих выходные параметры.|  
|[Использование хранимых процедур с состояниями возврата](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|Описывает способы использования драйвера JDBC для запуска хранимых процедур, содержащих возвращаемые значения состояния.|  
|[Использование хранимых процедур со счетчиком обновлений](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|Описывает способы использования драйвера JDBC для запуска хранимых процедур, содержащих счетчики обновления.|  
  
## <a name="see-also"></a>См. также:

[Использование инструкций с драйвером JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
