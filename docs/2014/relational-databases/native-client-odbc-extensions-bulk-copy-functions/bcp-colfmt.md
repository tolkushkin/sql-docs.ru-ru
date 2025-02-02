---
title: bcp_colfmt | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c583ffad2267a82c39d4ab6c7cd71a1852c7cb2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065472"
---
# <a name="bcpcolfmt"></a>bcp_colfmt
  Указывает исходный или целевой формат данных в пользовательском файле. При использовании с форматом источника **bcp_colfmt** указывает формат существующего файла данных, используемого в качестве источника данных в массовом копировании [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] таблицы. При использовании с целевым форматом, файл данных создается с использованием форматов столбцов, указанных с помощью **bcp_colfmt**.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
RETCODE bcp_colfmt (  
HDBC   
hdbc  
,  
INT  
idxUserDataCol  
,  
BYTE   
eUserDataType  
,  
INT   
cbIndicator  
,  
DBINT   
cbUserData  
,  
LPCBYTE   
pUserDataTerm  
,  
INT   
cbUserDataTerm  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Аргументы  
 *HDBC*  
 Дескриптор соединения ODBC с поддержкой массового копирования.  
  
 *idxUserDataCol*  
 Порядковый номер столбца в пользовательском файле данных, для которого указывается формат. Первый столбец имеет номер 1.  
  
 *eUserDataType*  
 Тип данных этого столбца в файле пользователя. Если он отличается от типа данных соответствующего столбца в таблице базы данных (*idxServerColumn*), массовое копирование преобразует данные, если это возможно.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] появилась поддержка SQLXML и SQLUDT токенами типов данных в *eUserDataType* параметра.  
  
 *EUserDataType* перечисляется [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] токенами типов данных в файле sqlncli.h, не перечислителях типов данных ODBC C. Например, можно указать символьную строку SQL_C_CHAR типа ODBC с помощью специфического для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] типа SQLCHARACTER.  
  
 Чтобы задать представление данных по умолчанию для типа данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , установите этот параметр в значение 0.  
  
 Для массового копирования из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в файл, когда *eUserDataType* равном SQLDECIMAL или SQLNUMERIC:  
  
-   Если исходный столбец не **десятичное** или **числовых**, используются по умолчанию точности и масштаба.  
  
-   Если исходный столбец **десятичное** или **числовых**, используются точность и масштаб исходного столбца.  
  
 *cbIndicator*  
 Длина в байтах признака длины и допустимости значений NULL в данных столбца. Допускаются следующие значения длины признака: 0 (если признак не используется), 1, 2, 4 или 8.  
  
 Чтобы задать для признака массового копирования использование по умолчанию, установите этот параметр в значение SQL_VARLEN_DATA.  
  
 Признаки располагаются в памяти непосредственно перед данными, а в файле данных — непосредственно перед данными, к которым они применяются.  
  
 Если для столбца файла данных используется несколько способов задания длины (например, признак и максимальная длина столбца или признак и последовательность-признак конца), то для массового копирования выбирается способ, применение которого вызовет копирование данных наименьшего объема.  
  
 Если пользователь не изменяет формат данных, то создаваемые при массовом копировании файлы данных содержат признаки, которые определяют, когда столбец может принимать значение NULL или его данные имеют переменную длину.  
  
 *cbUserData*  
 Максимальная длина в байтах данных в столбце пользовательского файла, не включая длину признака длины или признака конца.  
  
 Установка *cbUserData* значения sql_null_data показывает, что все значения в столбце файла данных, или должно быть присвоено значение NULL.  
  
 Установка *cbUserData* значения SQL_VARLEN_DATA указывает, что система должна определить длину данных в каждом столбце. Для некоторых столбцов это может означать, что создаваемые признаки длины и допустимости значений NULL предваряют данные при копировании из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], или ожидается их наличие в данных, копируемых в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] символьных и двоичных типов данных *cbUserData* может иметь значение SQL_VARLEN_DATA, SQL_NULL_DATA, 0 или любое положительное значение. Если *cbUserData* имеет значение SQL_VARLEN_DATA, система использует либо признак длины при его наличии, либо последовательность с признаком конца для определения длины данных. Если задан и признак длины, и последовательность признака конца, то при массовом копировании используется значение, применение которого вызывает копирование данных наименьшего объема. Если *cbUserData* имеет значение SQL_VARLEN_DATA, данные измеряется [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] указан символ или двоичного типа и ни признак длины, ни последовательность с признаком конца, система возвращает сообщение об ошибке.  
  
 Если значение *cbUserData* больше или равно 0, то система рассматривает значение *cbUserData* как максимальную длину данных. Но если в дополнение к положительному значению для *cbUserData*указан признак длины или последовательность признака конца, то система определяет объем данных методом, который приведет к копированию наименьшего объема данных.  
  
 Значение *cbUserData* представляет объем данных в байтах. Если символьные данные представлены строкой знаков в Юникоде, то положительное значение параметра *cbUserData* представляет количество символов, умноженное на размер символа в байтах.  
  
 *pUserDataTerm*  
 Последовательность-признак конца, используемая для этого столбца. Этот параметр предназначен главным образом для символьных типов данных, поскольку все другие типы имеют фиксированную длину или, как в случае с двоичными данными, требуют наличия признака длины, в котором записано точное число присутствующих байтов.  
  
 Чтобы исключить обработку признака конца в извлекаемых данных или указать, что данные в файле пользователя не имеют признака конца, установите этот параметр в значение NULL.  
  
 Если для столбца файла пользователя используется несколько способов задания длины (например, признак конца и признак длины или признак конца и максимальная длина столбца), то для массового копирования выбирается способ, применение которого вызывает копирование данных наименьшего объема.  
  
 При необходимости API-интерфейс массового копирования выполнит преобразование символов из Юникода в многобайтовую кодировку (MBCS). Обратите особое внимание, правильно ли задана строка байтов, служащая признаком конца, а также ее длина.  
  
 *cbUserDataTerm*  
 Длина в байтах последовательности-признака конца, используемой для этого столбца. Если в данных признак конца отсутствует или нежелателен, то установите это значение в 0.  
  
 *idxServerCol*  
 Порядковый номер столбца в таблице базы данных. Первый столбец имеет номер 1. Порядковый номер столбца возвращается функцией [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
 Если это значение равно 0, операция массового копирования пропускает столбец в файле данных.  
  
## <a name="returns"></a>Возвращает  
 SUCCEED или FAIL.  
  
## <a name="remarks"></a>Примечания  
 **Bcp_colfmt** функция позволяет указать формат пользовательского файла для массового копирования. Формат для массового копирования состоит из следующих частей:  
  
-   сопоставление столбцов файла пользователя со столбцами базы данных;  
  
-   тип данных каждого столбца в файле пользователя;  
  
-   длина дополнительного признака для каждого столбца;  
  
-   максимальная длина данных в каждом столбце файла пользователя;  
  
-   дополнительная последовательность байт, служащая признаком конца для каждого столбца;  
  
-   длина дополнительной последовательности байт, служащей признаком конца.  
  
 Каждый вызов **bcp_colfmt** указывает формат для одного столбца пользовательского файла. Например, чтобы изменить параметры по умолчанию для трех столбцов в файле данных пользователя с пятью столбцами, сначала вызовите [bcp_columns](bcp-columns.md)**(5)**, а затем вызвать **bcp_colfmt** пять раз в три из этих вызовов задайте нужный формат. Для оставшихся двух вызовов необходимо установить *eUserDataType* 0, а также набор *cbIndicator*, *cbUserData*, и *cbUserDataTerm* 0, SQL_VARLEN _DATA и 0 соответственно. Эта процедура копирует все пять столбцов. Для трех применяется заданный измененный формат, а для двух оставшихся — формат по умолчанию.  
  
 Для *cbIndicator*, значение 8, чтобы указать тип больших значений теперь является допустимым. Если для поля, которому соответствует столбец с новым типом max, указан префикс, его значение можно установить только в 8. Дополнительные сведения см. в разделе [bcp_bind](bcp-bind.md).  
  
 **Bcp_columns** функция должна вызываться перед любыми вызовами **bcp_colfmt**.  
  
 Необходимо вызвать **bcp_colfmt** один раз для каждого столбца в файле пользователя.  
  
 Вызов **bcp_colfmt** более одного раза для любого пользовательского файла столбца возникает ошибка.  
  
 Нет необходимости копировать все данные из пользовательского файла в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Чтобы пропустить столбец, укажите формат данных для этого столбца, задав *idxServerCol* параметра значение 0. Если требуется пропустить столбец, необходимо указать его тип.  
  
 Для сохранения спецификации формата можно воспользоваться функцией [bcp_writefmt](bcp-writefmt.md) .  
  
## <a name="bcpcolfmt-support-for-enhanced-date-and-time-features"></a>Поддержка функцией bcp_colfmt улучшенных возможностей даты и времени  
 Для сведения данных он вводит использовании *eUserDataType* параметров для типов даты и времени, см. в разделе [изменения массового копирования для типов усиленной даты и времени &#40;OLE DB и ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Дополнительные сведения см. в разделе [время улучшения функций даты и &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>См. также  
 [Функции массового копирования](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
