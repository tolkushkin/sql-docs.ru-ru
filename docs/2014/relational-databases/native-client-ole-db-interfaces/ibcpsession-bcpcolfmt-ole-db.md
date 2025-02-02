---
title: IBCPSession::BCPColFmt (OLE DB) | Документация Майкрософт
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPColFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColFmt method
ms.assetid: 2852f4ba-f1c6-4c4c-86b2-b77e4abe70de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e896f3e04d24becf136b7abefcff9dbe97fa0970
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240263"
---
# <a name="ibcpsessionbcpcolfmt-ole-db"></a>IBCPSession::BCPColFmt (OLE DB)
  Создает привязку между переменными программы и столбцами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
HRESULT BCPColFmt(   
DBORDINALidxUserDataCol,  
inteUserDataType,  
intcbIndicator,  
intcbUserData,  
BYTE *pbUserDataTerm,  
intcbUserDataTerm,  
DBORDINALidxServerCol);  
```  
  
## <a name="remarks"></a>Примечания  
 Метод **BCPColFmt** используется для создания привязки между полями файла данных BCP и столбцами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. В качестве параметров он принимает длину, тип, признак конца и длину префикса столбца, а также задает каждое из этих свойств для отдельных полей.  
  
 Если пользователь работает в интерактивном режиме, этот метод вызывается дважды для каждого столбца: один раз, чтобы задать формат столбца согласно значениям по умолчанию (которые соответствуют типу столбца на сервере), а второй раз, чтобы задать формат согласно типу столбца, выбранному клиентом в интерактивном режиме.  
  
 В неинтерактивном режиме этот метод вызывается только один раз для каждого столбца, чтобы задать ему символьный или собственный тип, а также задать признаки конца столбца и строк.  
  
 При помощи метода **BCPColFmt** можно указывать формат файла пользователя для операций массового копирования. Формат для массового копирования состоит из следующих частей:  
  
-   Сопоставление полей файла пользователя со столбцами базы данных.  
  
-   Тип данных каждого поля в файле пользователя.  
  
-   Длина дополнительного признака для каждого поля.  
  
-   Максимальная длина данных в каждом поле файла пользователя.  
  
-   Дополнительная последовательность байтов, служащая признаком конца для каждого поля.  
  
-   длина дополнительной последовательности байт, служащей признаком конца.  
  
 При каждом вызове метода **BCPColFmt** задается формат для одного поля в файле пользователя. Например, чтобы изменить значения по умолчанию трех полей в файле данных пользователя, состоящем из пяти полей, сначала вызовите метод `BCPColumns(5)`, а затем метод **BCPColFmt** пять раз и в трех из этих вызовов задайте нужный формат. При оставшихся двух вызовах для параметра *eUserDataType* установите значение BCP_TYPE_DEFAULT, а параметрам *cbIndicator*, *cbUserData*и *cbUserDataTerm* присвойте значения 0, BCP_VARIABLE_LENGTH и 0 соответственно. Эта процедура копирует все пять столбцов. Для трех применяется заданный измененный формат, а для двух оставшихся — формат по умолчанию.  
  
> [!NOTE]  
>  Необходимо вызывать метод [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) перед любым вызовом метода **BCPColFmt**. Метод **BCPColFmt** необходимо вызывать по одному разу для каждого столбца из файла пользователя. При вызове метода **BCPColFmt** более одного раза для любого столбца из файла пользователя возникает ошибка.  
  
 Копировать все данные из файла пользователя в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не обязательно. Чтобы пропустить столбец, укажите формат данных для этого столбца, установив параметр idxServerCol в значение 0. Чтобы поле было пропущено, по-прежнему необходимо добавить все необходимые данные для метода, чтобы он работал правильно.  
  
 **Примечание.** При помощи функции [IBCPSession::BCPWriteFmt](ibcpsession-bcpwritefmt-ole-db.md) можно сохранить спецификацию формата, предоставленную с помощью метода **BCPColFmt**.  
  
## <a name="arguments"></a>Аргументы  
 *idxUserDataCol*[in]  
 Индекс поля из файла данных пользователя.  
  
 *eUserDataType*[in]  
 Тип данных поля из файла данных пользователя. Допустимые типы данных приведены в файле заголовка собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (sqlncli.h) в формате BCP_TYPE_XXX, например BCP_TYPE_SQLINT4. Если задано значение BCP_TYPE_DEFAULT, поставщик попытается использовать тот же тип, к которому принадлежит столбец таблицы или представления. Массовое копирование из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в файл при `eUserDataType` аргумента задано значение BCP_TYPE_SQLDECIMAL или BCP_TYPE_SQLNUMERIC:  
  
-   Если тип исходного столбца отличается от decimal и numeric, то используются точность и масштаб по умолчанию.  
  
-   Если исходный столбец имеет тип decimal или numeric, то используются точность и масштаб исходного столбца.  
  
 *cbIndicator*[in]  
 Длина префикса поля. По умолчанию — BCP_PREFIX_DEFAULT. Допустимая длина префикса — 0, 1, 2, 4 или 8. Размер префикса 8 чаще всего используется для указания на то, что поле является фрагментированным. Фрагментация используется для повышения эффективности массового копирования столбцов типов с большими значениями.  
  
 *cbUserData*[in]  
 Максимальная длина в байтах данных этого поля в файле пользователя без учета длины любого признака длины или признака конца.  
  
 Параметр `cbUserData` присвоено значение bcp_length_null, это указывает, что все значения в данных полях файла, или должны быть установлены в значение NULL. Параметр `cbUserData` присвоено значение bcp_length_variable, это указывает, что система должна определить длину данных для каждого поля. Для некоторых полей это может означать, что создаваемые признаки длины и допустимости значений NULL предваряют данные при копировании из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]или ожидается наличие этих признаков в данных, копируемых в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] символьных и двоичных типов данных `cbUserData` может иметь значение BCP_LENGTH_VARIABLE, BCP_LENGTH_NULL, 0 или любое положительное значение. Если `cbUserData` присвоено значение BCP_LENGTH_VARIABLE, система использует либо признак длины при его наличии, либо последовательность с признаком конца для определения длины данных. Если задан и признак длины, и последовательность признака конца, то при массовом копировании используется значение, применение которого вызывает копирование данных наименьшего объема. Если `cbUserData` присвоено значение BCP_LENGTH_VARIABLE, данные измеряется [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] символьному или двоичному типу, а если указан признак длины, ни последовательность с признаком конца, система возвращает сообщение об ошибке.  
  
 Если `cbUserData` равно 0 или положительное значение, система использует `cbUserData` как максимальную длину данных. Тем не менее если в дополнение к положительному `cbUserData`, длины или признака конца последовательность, система определяет объем данных с помощью метода, который вычисляет наименьший размер копируемых данных.  
  
 `cbUserData` Значение представляет число байтов данных. Если символьные данные представлены строкой знаков в Юникоде, то положительное `cbUserData` значение параметра представляет число символов, умноженное на размер в байтах каждого символа.  
  
 *pbUserDataTerm*[size_is][in]  
 Последовательность с признаком конца, которая должна использоваться для поля. Этот параметр предназначен главным образом для символьных типов данных, поскольку все другие типы имеют фиксированную длину или, как в случае с двоичными данными, требуют наличия признака длины, в котором записано точное число присутствующих байтов.  
  
 Чтобы исключить обработку признака конца в извлекаемых данных или указать, что данные в файле пользователя не имеют признака конца, установите этот параметр в значение NULL.  
  
 Если для столбца файла пользователя используется несколько способов задания длины (например, признак конца и признак длины или признак конца и максимальная длина столбца), то для массового копирования выбирается способ, применение которого вызывает копирование данных наименьшего объема.  
  
 При необходимости API-интерфейс массового копирования выполнит преобразование символов из Юникода в многобайтовую кодировку (MBCS). Обратите особое внимание, правильно ли задана строка байтов, служащая признаком конца, а также ее длина.  
  
 *cbUserDataTerm*[in]  
 Длина в байтах последовательности с признаком конца, которая должна использоваться для столбца. Если в данных признак конца отсутствует или нежелателен, то установите это значение в 0.  
  
 *idxServerCol*[in]  
 Порядковый номер столбца в таблице базы данных. Первый столбец имеет номер 1. Порядковый номер столбца сообщается методом **IColumnsInfo::GetColumnInfo** либо подобными методами. Если это значение равно 0, то при массовом копировании это поле в файле данных будет пропущено.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 S_OK  
 Метод выполнен успешно.  
  
 E_FAIL  
 Произошла ошибка, связанная с поставщиком. Подробные сведения можно получить при помощи интерфейса [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) .  
  
 E_UNEXPECTED  
 Непредвиденный вызов метода. Например, перед вызовом этого метода не был вызван метод [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md).  
  
 E_INVALIDARG  
 Недопустимое значение аргумента.  
  
 E_OUTOFMEMORY  
 Ошибка, связанная с нехваткой памяти.  
  
## <a name="see-also"></a>См. также  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Выполнение операций массового копирования](../native-client/features/performing-bulk-copy-operations.md)  
  
  
