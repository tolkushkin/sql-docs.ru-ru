---
title: Функция SQLInstallDriverEx | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5664a4cb745a250aa8db6d98b92a275bb91c7a8d
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536582"
---
# <a name="sqlinstalldriverex-function"></a>Функция SQLInstallDriverEx
**Соответствие стандартам**  
 Представленные версии: ODBC 3.0  
  
 **Сводка**  
 **SQLInstallDriverEx** добавляет сведения о драйвер в Odbcinst.ini запись сведений о системе и увеличивает возможности драйвера *UsageCount* на 1. Тем не менее, если версия драйвер уже существует, но *UsageCount* значение драйвер не существует, новый *UsageCount* имеет значение 2.  
  
 Эта функция фактически не копирует все файлы. Он является обязанностью вызывающей программе для копирования файлов драйвера в целевой каталог должным образом.  
  
 Функциональные возможности **SQLInstallDriverEx** также может осуществляться с помощью [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Аргументы  
 *lpszDriver*  
 [Вход] Описание драйвера (обычно имя связанного СУБД) предоставляемые пользователям вместо имени физического драйвера. *LpszDriver* аргумент должен содержать список пар "ключевое слово значение", описывающий драйвер двумя двоичными нулями. Дополнительные сведения о пары «ключевое слово значение», см. в разделе [подразделы спецификаций драйверов](../../../odbc/reference/install/driver-specification-subkeys.md). Дополнительные сведения о вдвойне заканчивающуюся нулем строку, см. в разделе [функция ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 [Вход] Полный путь к целевой каталог установки, или указатель null. Если *lpszPathIn* является пустым указателем, драйверы, которые будут устанавливаться в системном каталоге.  
  
 *lpszPathOut*  
 [Выход] Путь к целевой каталог, где следует установить драйвер. Если драйвер ранее не были установлены, *lpszPathOut* должно быть таким же, как *lpszPathIn*. Если ранее был установлен драйвер, *lpszPathOut* — путь к предыдущей установки.  
  
 *cbPathOutMax*  
 [Вход] Длина *lpszPathOut*.  
  
 *pcbPathOut*  
 [Выход] Общее число байтов (за исключением знака завершения null) для возврата в *lpszPathOut*. Если количество байтов, доступных для возврата больше или равно *cbPathOutMax*, выходной путь в *lpszPathOut* усекается до *cbPathOutMax* минус символ завершения NULL. *PcbPathOut* аргументом может быть пустым указателем.  
  
 *fRequest*  
 [Вход] Тип запроса. *FRequest* аргумент должен иметь один из следующих значений:  
  
 ODBC_INSTALL_INQUIRY: Запрос установки драйвера.  
  
 ODBC_INSTALL_COMPLETE: Выполните запрос на установку.  
  
 *lpdwUsageCount*  
 [Выход] Счетчик использования драйвера после вызова этой функции.  
  
 Приложения, не задавайте счетчик использования. ODBC будет поддерживать этот счетчик.  
  
## <a name="returns"></a>Возвращает  
 Функция возвращает значение TRUE при успешном выполнении, FALSE в случае неудачи.  
  
## <a name="diagnostics"></a>Диагностика  
 Когда **SQLInstallDriverEx** возвращает значение FALSE, связанным  *\*pfErrorCode* значение можно получить, вызвав **SQLInstallerError**. В следующей таблице перечислены  *\*pfErrorCode* значения, которые могут быть возвращены **SQLInstallerError** и объясняется каждый из них в контексте этой функции.  
  
|*\*pfErrorCode*|Ошибка|Описание|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Ошибки общие установщика|Произошла ошибка для которой нет ошибок определенных установщика.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Недопустимый буфер длины|*LpszPathOut* аргумент не был достаточно велик, чтобы содержать выходной путь. Буфер содержит усеченное путь.<br /><br /> *CbPathOutMax* аргумент было равно 0, и *fRequest* был ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Недопустимый тип запроса|*FRequest* аргумент не является одним из следующих:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Пары "недопустимое ключевое слово значение"|*LpszDriver* аргумент содержит синтаксическую ошибку.|  
|ODBC_ERROR_INVALID_PATH|Путь установки недопустимый|*LpszPathIn* аргумент содержит недопустимый путь.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Не удалось загрузить библиотеку установки драйвера или перевода|Не удалось загрузить библиотеку установки драйвера.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Недопустимый параметр последовательности|*LpszDriver* аргумент не содержит список пар "ключевое слово значение".|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Не удалось увеличить или уменьшить счетчик использования компонента|Установщику не удалось выполнить приращение счетчика использования драйвера.|  
  
## <a name="comments"></a>Комментарии  
 *LpszDriver* аргумент является список атрибутов в виде пар "ключевое слово значение". Каждая пара заканчивается нулевым байтом, а весь список заканчивается нулевым байтом. (То есть две пустые байты обозначения конца списка.) Формат этого списка выглядит следующим образом:  
  
 _драйвер desc_ **\\**0Driver**=**_имя файла DLL драйвера_ **\\**0 [установки**=**_имя файла DLL программы установки_<b>\\</b>0]  
  
 [_драйвер attr ключевое_слово1_**=**_значение1_<b>\\</b>0] [_драйвер attr ключевое_слово2_  **=** _value2_<b>\\</b>0]... <b> \\ </b>0  
  
 где \0 является нулевым байтом и *драйвер attr-keywordn* — любое ключевое слово атрибута драйвера. Ключевые слова должны располагаться в указанном порядке. Например предположим, что драйвер для форматированного текста файлов имеет отдельный драйвер и установки библиотеки DLL и можно использовать файлы с расширениями txt- и CSV-файл. *LpszDriver* аргумент для этого драйвера может выглядеть следующим образом:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Предположим, что драйвер для SQL Server не поддерживает отдельные DLL-файлов установки и не поддерживает любые ключевые слова атрибута драйвера. *LpszDriver* аргумент для этого драйвера может выглядеть следующим образом:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 После **SQLInstallDriverEx** извлекает сведения о драйвере из *lpszDriver* аргумент, он добавляет Описание драйвера в раздел [ODBC Drivers] файла Odbcinst.ini записи в системе сведения. Затем создает раздел с описанием драйвера и добавляет полных путей к DLL-Библиотека драйвера и библиотека DLL программы установки. Наконец возвращает путь к целевой каталог установки, но не копирует файлы драйверов к нему. Фактически, вызывающей программе необходимо скопировать файлы драйверов в целевой каталог.  
  
 **SQLInstallDriverEx** увеличивает счетчик использования компонента, установленного драйвера на 1. Если уже существует версия драйвера, но счетчик использования компонент драйвера не существует, новое значение счетчика использования компонента имеет значение 2.  
  
 Программа установки физически копирование файла драйвера и поддержание счетчик использования файла. Если файл драйвера ранее не были установлены, программа установки необходимо скопировать файл в *lpszPathIn* пути и создать счетчик использования файла. Если файл был ранее установлен, программа установки просто увеличивает счетчик использования файла и возвращает путь перед установкой в *lpszPathOut* аргумент.  
  
> [!NOTE]  
>  Дополнительные сведения о счетчики использования компонента и счетчики использования файла, см. в разделе [подсчет использования](../../../odbc/reference/install/usage-counting.md).  
  
 Если приложение уже установлена более старой версии файла драйвера, драйвер должен удалить и переустановить, таким образом, счетчик использования драйвера компонент допустимым. **SQLConfigDriver** (с *fRequest* из ODBC_REMOVE_DRIVER) сначала должен быть вызван, а затем **SQLRemoveDriver** должен вызываться для уменьшения счетчик использования компонента. **SQLInstallDriverEx** необходимо также вызвать для переустановки драйвера, увеличивая счетчик использования компонента. Программа установки необходимо заменить старый файл с новым файлом. Счетчик использования файла остается неизменным, и любое другое приложение, в который использовать более старой версии файла теперь будет использовать более новой версии.  
  
> [!NOTE]  
>  Если ранее был установлен драйвер и **SQLInstallDriverEx** вызывается для установки драйвера в другом каталоге, то функция возвращает значение TRUE, но *lpszPathOut* будет включать каталог где драйвер уже установлен. Не будут включены в каталоге, введенные в *lpszDriver* аргумент.  
  
 Длина пути в *lpszPathOut* в **SQLInstallDriverEx** позволяет двухфазной установки, поэтому приложение может определить, какие *cbPathOutMax* необходимо определить вызов **SQLInstallDriverEx** с *fRequest* ODBC_INSTALL_INQUIRY режима. Эта команда возвращает общее число байтов, доступных в *pcbPathOut* буфера. **SQLInstallDriverEx** затем может быть вызван с *fRequest* из ODBC_INSTALL_COMPLETE и *cbPathOutMax* аргументу присвоено значение в *pcbPathOut*буфера, а также знак завершения null.  
  
 Если вы решили не использовать двухэтапной модели для **SQLInstallDriverEx**, необходимо задать *cbPathOutMax*, который определяет объем хранилища для пути в целевой каталог, чтобы значение _MAX_PATH, как определен в Stdlib.h, чтобы предотвратить усечение.  
  
 Когда *fRequest* является ODBC_INSTALL_COMPLETE, **SQLInstallDriverEx** не допускает *lpszPathOut* значение NULL (или *cbPathOutMax* быть 0). Если *fRequest* является ODBC_INSTALL_COMPLETE, FALSE возвращается, если количество байтов, доступных для возврата больше или равно *cbPathOutMax*, в результате этого усечение происходит.  
  
 После **SQLInstallDriverEx** был вызван и (при необходимости), программа установки скопировала файл драйвера, необходимо вызвать метод установки драйвера DLL **SQLConfigDriver** задать конфигурацию для драйвер.  
  
## <a name="related-functions"></a>Связанные функции  
  
|Сведения о|См.|  
|---------------------------|---------|  
|Установка диспетчера драйверов|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
