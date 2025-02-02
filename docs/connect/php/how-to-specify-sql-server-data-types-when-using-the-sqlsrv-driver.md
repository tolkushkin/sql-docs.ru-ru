---
title: Практическое руководство. Указание типов данных SQL Server при использовании драйвера SQLSRV | Документы Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: 1fcf73cb-5634-4d89-948f-9326f1dbd030
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5d4727029dbb1ba4fbfdbdd10abf6b1cd0812790
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799654"
---
# <a name="how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver"></a>Практическое руководство. Указание типов данных SQL Server при использовании драйвера SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Эта статья показывает, как использовать драйвер SQLSRV, чтобы указать тип данных SQL Server для данных, отправляемых на сервер. Сведения, содержащиеся в этой статье, не распространяются на использование драйвера PDO_SQLSRV.  
  
Чтобы указать тип данных SQL Server, необходимо использовать дополнительный массив *$params* при подготовке и выполнении запроса, который вставляет или обновляет данные. Дополнительные сведения о структуре и синтаксисе массива *$params* см. в статье [sqlsrv_query](../../connect/php/sqlsrv-query.md) или [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
Ниже представлена обобщенная процедура указания типа данных SQL Server при отправке данных на сервер:  
  
> [!NOTE]  
> Если тип данных SQL Server не указан, используются типы по умолчанию. Дополнительные сведения о типах данных SQL Server по умолчанию см. в статье [Default SQL Server Data Types](../../connect/php/default-sql-server-data-types.md).  
  
1.  Определите запрос Transact-SQL, который вставляет или обновляет данные. Используйте вопросительные знаки (?) в качестве заполнителей для значений параметров в запросе.  
  
2.  Инициализируйте или обновите переменные PHP, которые соответствуют заполнителям в запросе Transact-SQL.  
  
3.  Создайте массив *$params* , используемый при подготовке или выполнении запроса. Обратите внимание, что при указании типа данных SQL Server каждый элемент массива *$params* также должен быть массивом.  
  
4.  Укажите требуемый тип данных SQL Server, используя соответствующую константу **SQLSRV_SQLTYPE_*** в качестве четвертого параметра в каждом подмассиве массива *$params*. Полный список констант **SQLSRV_SQLTYPE_*** см. в разделе SQLTYPEs статьи [Константы (драйверы Майкрософт для PHP для SQL Server)](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). Например, в следующем коде *$changeDate*, *$rate*и *$payFrequency* соответственно указаны как типы SQL Server **datetime**, **money**и **tinyint** в массиве *$params* . Так как для параметра *$employeeId* тип SQL Server не указан и параметр инициализируется целым числом, используется тип SQL Server по умолчанию **integer** .  
  
    ```  
    $employeeId = 5;  
    $changeDate = "2005-06-07";  
    $rate = 30;  
    $payFrequency = 2;  
    $params = array(  
                array($employeeId, null),  
                array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
                array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
                array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
              );  
    ```  
  
## <a name="example"></a>Пример  
В следующем примере данные вставляются в таблицу *HumanResources.EmployeePayHistory* базы данных AdventureWorks. Типы SQL Server указаны для параметров *$changeDate*, *$rate*и *$payFrequency* . Тип SQL Server по умолчанию используется для параметра *$employeeId* . Чтобы убедиться, что данные были успешно вставлены, выполняется извлечение и отображение тех же данных.  
  
В примере предполагается, что SQL Server и база данных [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) установлены на локальном компьютере. При выполнении примера из командной строки все выходные данные выводятся в консоль.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define the query. */  
$tsql1 = "INSERT INTO HumanResources.EmployeePayHistory (EmployeeID,  
                                                        RateChangeDate,  
                                                        Rate,  
                                                        PayFrequency)  
           VALUES (?, ?, ?, ?)";  
  
/* Construct the parameter array. */  
$employeeId = 5;  
$changeDate = "2005-06-07";  
$rate = 30;  
$payFrequency = 2;  
$params1 = array(  
               array($employeeId, null),  
               array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
               array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
               array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
           );  
  
/* Execute the INSERT query. */  
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
if( $stmt1 === false )  
{  
     echo "Error in execution of INSERT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the newly inserted data. */  
/* Define the query. */  
$tsql2 = "SELECT EmployeeID, RateChangeDate, Rate, PayFrequency  
          FROM HumanResources.EmployeePayHistory  
          WHERE EmployeeID = ? AND RateChangeDate = ?";  
  
/* Construct the parameter array. */  
$params2 = array($employeeId, $changeDate);  
  
/*Execute the SELECT query. */  
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if( $stmt2 === false )  
{  
     echo "Error in execution of SELECT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results. */  
$row = sqlsrv_fetch_array( $stmt2 );  
if( $row === false )  
{  
     echo "Error in fetching data.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
echo "EmployeeID: ".$row['EmployeeID']."\n";  
echo "Change Date: ".date_format($row['RateChangeDate'], "Y-m-d")."\n";  
echo "Rate: ".$row['Rate']."\n";  
echo "PayFrequency: ".$row['PayFrequency']."\n";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt1);  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="see-also"></a>См. также:  
[Извлечение данных](../../connect/php/retrieving-data.md)

[Информация о примерах кода в документации](../../connect/php/about-code-examples-in-the-documentation.md)

[Практическое руководство. Указание типов данных PHP](../../connect/php/how-to-specify-php-data-types.md)

[Преобразование типов данных](../../connect/php/converting-data-types.md)

[Практическое руководство. Отправка и извлечение данных UTF-8 с помощью встроенной поддержки UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)  
  
