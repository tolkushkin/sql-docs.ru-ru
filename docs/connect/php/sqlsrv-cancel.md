---
title: sqlsrv_cancel | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_cancel
apitype: NA
helpviewer_keywords:
- sqlsrv_cancel
- API Reference, sqlsrv_cancel
ms.assetid: 75798c9b-f711-445d-9b8f-ba4d405ca50a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6c5b4c9120eca9ed37dd1e7824c630c72ee91313
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797019"
---
# <a name="sqlsrvcancel"></a>sqlsrv_cancel
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Отменяет инструкцию. Это означает, что удаляются все ожидающие результаты для инструкции. После вызова этой функции инструкцию можно выполнить повторно, если она была подготовлена с помощью [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md). Вызов этой функции не требуется, если были использованы все результаты, связанные с инструкцией.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sqlsrv_cancel( resource $stmt)  
```  
  
#### <a name="parameters"></a>Параметры  
*$stmt*: отменяемая инструкция.  
  
## <a name="return-value"></a>Возвращаемое значение  
Логическое значение: **true** , если операция была выполнена успешно. В противном случае — **false**.  
  
## <a name="example"></a>Пример  
Следующий пример ориентируется на базу данных [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) для выполнения запроса, а затем использует и подсчитывает результаты, пока переменная *$salesTotal* не достигнет заданного значения. Оставшиеся после этого результаты запроса удаляются. В примере предполагается, что SQL Server и базы данных AdventureWorks установлены на локальном компьютере. При выполнении примера из командной строки все выходные данные выводятся в консоль.  
  
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
  
/* Prepare and execute the query. */  
$tsql = "SELECT OrderQty, UnitPrice FROM Sales.SalesOrderDetail";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
if( sqlsrv_execute( $stmt ) === false)  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Initialize tracking variables. */  
$salesTotal = 0;  
$count = 0;  
  
/* Count and display the number of sales that produce revenue  
of $100,000. */  
while( ($row = sqlsrv_fetch_array( $stmt)) && $salesTotal <=100000)  
{  
     $qty = $row[0];  
     $price = $row[1];  
     $salesTotal += ( $price * $qty);  
     $count++;  
}  
echo "$count sales accounted for the first $$salesTotal in revenue.\n";  
  
/* Cancel the pending results. The statement can be reused. */  
sqlsrv_cancel( $stmt);  
?>  
```  
  
## <a name="comments"></a>Комментарии  
Инструкцию, подготовленную и выполненную с помощью сочетания [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) и [sqlsrv_execute](../../connect/php/sqlsrv-execute.md), можно выполнить повторно с помощью **sqlsrv_execute** после вызова **sqlsrv_cancel**. Инструкцию, выполненную с помощью [sqlsrv_query](../../connect/php/sqlsrv-query.md), нельзя выполнить повторно после вызова **sqlsrv_cancel**.  
  
## <a name="see-also"></a>См. также:  
[Справочник по API для драйвера SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Подключение к серверу](../../connect/php/connecting-to-the-server.md)

[Извлечение данных](../../connect/php/retrieving-data.md)

[Информация о примерах кода в документации](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)

  
