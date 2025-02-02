---
title: Элементы SQLServerNClob | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8386d896391405777648ee3ec27b188b313c737c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788954"
---
# <a name="sqlservernclob-members"></a>Элементы SQLServerNClob
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  В следующих таблицах перечислены элементы класса [SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md).  
  
## <a name="constructors"></a>Конструкторы  
 Нет.  
  
## <a name="fields"></a>Поля  
 Нет.  
  
## <a name="inherited-fields"></a>Наследуемые поля  
 Нет.  
  
## <a name="methods"></a>Методы  
  
|Имя|Описание|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|Этот метод освобождает объект **NCLOB** и ресурсы, занятые им.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|Извлекает **NCLOB** обозначенный значение **java.sql.NClob** объектом в ASCII-потоке.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|Извлекает **NCLOB** обозначенный значение **java.sql.NClob** объекта.|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|Извлекает копию указанной подстроки в **NCLOB** обозначенный значение **java.sql.NClob** объекта.|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|Возвращает число символов в **NCLOB** обозначенный значение **java.sql.NClob** объекта.|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|Извлекает положение символа указанного объекта **NClob** или подстроки в **NClob** на основании указанной начальной позиции.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|Извлекает поток, используемый для записи символов ASCII в значение **NCLOB**, представленное данным объектом **java.sql.NClob**, начиная с указанной позиции.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|Извлекает поток, используемый для записи символов Юникода в значение **NCLOB**, представленное этим объектом **java.sql.NClob**, начиная с указанной позиции.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|Записывает указанный **строка** для **NCLOB** начиная с указанной позиции.|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|Усекает значение **NCLOB** до указанной длины.|  
  
## <a name="inherited-methods"></a>Наследуемые методы  
  
|Класс, наследуемый от|Методы|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>См. также:  
 [Класс SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
