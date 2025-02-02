---
title: sqlsrv_client_info | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_client_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_client_info
- sqlsrv_client_info
ms.assetid: 3e2d3679-436a-45d8-8bdc-7c633b65a720
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5cf0c29f6d095361cb3fd8a1d1cb316beb646433
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797009"
---
# <a name="sqlsrvclientinfo"></a>sqlsrv_client_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Возвращает сведения о подключении и стеке клиента.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sqlsrv_client_info( resource $conn)  
```  
  
#### <a name="parameters"></a>Параметры  
*$conn*: ресурс подключения, посредством которого осуществляется подключение клиента.  
  
## <a name="return-value"></a>Возвращаемое значение  
Ассоциативный массив с ключами, описанными в следующей таблице, или значение **false** , если ресурс подключения имеет значение NULL.  
  
**Для PHP для SQL Server версии 3.2 и 3.1**:  
  
|Key|Описание|  
|-------|---------------|  
|DriverDllName|MSODBCSQL11.DLL (драйвер ODBC 11 для SQL Server)|  
|DriverODBCVer|Версия ODBC (xx.yy)|  
|DriverVer|Версия DLL-библиотеки драйвера ODBC 11 для SQL Server:<br /><br />xx.yy.zzzz ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] версии 3.2 или 3.1)|  
|ExtensionVer|Версия php_sqlsrv.dll:<br /><br />3.2.xxxx.x (для [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] версии 3.2)<br /><br />3.1.xxxx.x (для [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] версии 3.1)|  
  
**Для PHP для SQL Server версии 3.0 и 2.0**:  
  
|Key|Описание|  
|-------|---------------|  
|DriverDllName|SQLNCLI10.DLL ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] версии 2.0)|  
|DriverODBCVer|Версия ODBC (xx.yy)|  
|DriverVer|Версия DLL-библиотеки собственного клиента SQL Server<br /><br />10.50.xxx ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] версии 2.0)|  
|ExtensionVer|Версия php_sqlsrv.dll:<br /><br />2.0.xxxx.x ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] версии 2.0)|  
  
## <a name="example"></a>Пример  
Следующий пример записывает сведения о клиенте в консоль при выполнении из командной строки. В примере предполагается, что SQL Server установлен на локальном компьютере. При выполнении примера из командной строки все выходные данные выводятся в консоль.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
if( $client_info = sqlsrv_client_info( $conn))  
{  
       foreach( $client_info as $key => $value)  
      {  
              echo $key.": ".$value."\n";  
      }  
}  
else  
{  
       echo "Client info error.\n";  
}  
  
/* Close connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>См. также:  
[Справочник по API для драйвера SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Информация о примерах кода в документации](../../connect/php/about-code-examples-in-the-documentation.md)  
  
