---
title: Часто задаваемые вопросы (FAQ) о драйвере JDBC | Документация Майкрософт
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bebfb6270d334305ae5684d7cca0c9e6571217e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66781824"
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>Вопросы и ответы по драйверу JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

На этой странице содержатся ответы на часто задаваемые вопросы о драйвере Microsoft JDBC Driver для SQL Server.

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

**Как можно улучшить драйвер JDBC?**  
Драйвер JDBC является драйвером с открытым кодом, который можно найти на [GitHub](https://github.com/microsoft/mssql-jdbc). Драйвер можно улучшить путем регистрации проблем и добавления кода в базу.

**Какие версии SQL Server и Java поддерживает драйвер?**  
Подробные сведения см. в статье [Матрица поддержки драйвера Microsoft JDBC Driver для SQL Server](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md).

**Чем отличаются пакеты драйверов JDBC, доступные в Центре загрузки Майкрософт и на GitHub?**  
Файлы драйвера JDBC, доступные в репозитории GitHub для Microsoft JDBC Driver, являются основой для драйвера JDBC и подпадают под действие лицензии на программное обеспечение с открытым исходным кодом, которая указана в репозитории. Пакеты драйвера Центра загрузки Майкрософт включают в себя дополнительные библиотеки для встроенной проверки подлинности Windows и добавления транзакций XA с помощью драйвера JDBC. Эти дополнительные библиотеки подпадают под действие лицензии, которая включена в скачиваемый пакет.

**Что нужно учитывать при обновлении драйвера?**
Microsoft JDBC Driver 7.2 поддерживает спецификации JDBC 4.2 и JDBC 4.3 (частично) и содержит две библиотеки классов JAR в пакете установки, как показано ниже.

| JAR                        | Спецификация JDBC            | Версия JDK |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.2.2.jre11.jar | JDBC 4.3 (частично) и JDBC 4.2 | JDK 11.0    |
| mssql-jdbc-7.2.2.jre8.jar  | JDBC 4.2                      | JDK 8.0     |

 Microsoft JDBC Driver 7.0 поддерживает спецификации JDBC 4.2 и JDBC 4.3 (частично) и содержит две библиотеки классов JAR в пакете установки, как показано ниже.

| JAR                        | Спецификация JDBC            | Версия JDK |
| -------------------------- | ----------------------------- | ----------- |
| mssql-jdbc-7.0.0.jre10.jar | JDBC 4.3 (частично) и JDBC 4.2 | JDK 10.0    |
| mssql-jdbc-7.0.0.jre8.jar  | JDBC 4.2                      | JDK 8.0     |

Microsoft JDBC Driver 6.4 поддерживает спецификации JDBC 4.1, JDBC 4.2 и JDBC 4.3 (частично) и содержит три библиотеки классов JAR в пакете установки, как показано ниже.

| JAR                       | Спецификация JDBC                 | Версия JDK |
| ------------------------- | ---------------------------------- | ----------- |
| mssql-jdbc-6.4.0.jre9.jar | JDBC 4.3 (частично) и JDBC 4.2 и JDBC 4.1 | JDK 9.0     |
| mssql-jdbc-6.4.0.jre8.jar | JDBC 4.2 и 4.1                  | JDK 8.0     |
| mssql-jdbc-6.4.0.jre7.jar | JDBC 4.1                           | JDK 7.0     |

Microsoft JDBC Driver 6.2 поддерживает спецификации JDBC 4.0, 4.1 и JDBC 4.2 и содержит две библиотеки классов JAR в пакете установки, как показано ниже.

| JAR                       | Спецификация JDBC     | Версия JDK |
| ------------------------- | ---------------------- | ----------- |
| mssql-jdbc-6.2.2.jre8.jar | JDBC 4.2, 4.1 и 4.0 | JDK 8.0     |
| mssql-jdbc-6.2.2.jre7.jar | JDBC 4.1 и 4.0       | JDK 7.0     |

Microsoft JDBC Driver версии 6.0 и 4.2 для SQL Server поддерживают спецификации JDBC 4.0, 4.1 и 4.2 и содержат две библиотеки классов JAR в пакете установки, как показано ниже.

| JAR           | Спецификация JDBC     | Версия JDK |
| ------------- | ---------------------- | ----------- |
| sqljdbc42.jar | JDBC 4.2, 4.1 и 4.0 | JDK 8.0     |
| sqljdbc41.jar | JDBC 4.1 и 4.0       | JDK 7.0     |

Microsoft JDBC Driver 4.1 для SQL Server поддерживает спецификации JDBC 4.0 и содержит одну библиотеку классов JAR в пакете установки, как показано ниже.

| JAR           | Спецификация JDBC | Версия JDK     |
| ------------- | ------------------ | --------------- |
| sqljdbc41.jar | JDBC 4.0           | JDK 7.0 и 6.0 |

**Нужно ли вносить изменения в код моего приложения, если я хочу использовать последнюю версию драйвера с существующей версией SQL Server?**  
Как правило, драйверы создаются с учетом требований обратной совместимости, поэтому вам не нужно изменять существующие приложения при обновлении драйвера. Если новая версия драйвера содержит критические изменения, в разделе [Заметки о выпуске для драйвера JDBC](../../connect/jdbc/release-notes-for-the-jdbc-driver.md) можно найти подробные сведения о них и их влиянии на существующие приложения. Кроме того, в заметках о выпуске новой версии драйвера можно просмотреть список известных проблем и исправленных в новом выпуске ошибок.

**Сколько стоит драйвер?**  
Драйвер Microsoft JDBC Driver for SQL Server доступен бесплатно.

**Могу ли я повторно распространять драйвер?**
Драйверы JDBC версий 4.1, 4.2, 6.0, 6.2, 6.4 и 7.0 являются распространяемыми. В лицензионном соглашении следует ознакомится с разделом "Распространяемый код".

**Можно ли использовать драйвер на компьютере Linux для доступа к Microsoft SQL Server?**
Да. Драйвер позволяет подключаться к SQL Server с компьютеров под управлением Linux, Unix и других платформ, отличных от Windows. Дополнительные сведения см. в статье [Матрица поддержки драйвера Microsoft JDBC Driver for SQL Server](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md).

**Поддерживает ли драйвер SSL-шифрование?**
Драйвер поддерживает SSL-шифрование начиная с версии 1.2. Дополнительные сведения см. в статье [Using SSL Encryption](../../connect/jdbc/using-ssl-encryption.md) (Использование SSL-шифрования).

**Какие типы проверки подлинности поддерживает драйвер Microsoft JDBC для SQL Server?**  
В таблице ниже перечислены варианты проверки подлинности. Обратите внимание, что чистая проверка подлинности Java Kerberos доступна в драйвере начиная с выпуска 4.0.

|             |                                       |
| ----------- | ------------------------------------- |
| Платформа    | Проверка подлинности                        |
| Не Windows | Чистая Java Kerberos                    |
| Не Windows | SQL Server                            |
| Не Windows | Проверка подлинности Azure Active Directory |
| Windows     | Чистая Java Kerberos                    |
| Windows     | SQL Server                            |
| Windows     | Kerberos и NTLM             |
| Windows     | NTLM                                  |
| Windows     | Проверка подлинности Azure Active Directory |

**Поддерживает ли драйвер IP-адреса версии 6 (IPv6)?**  
Да. Драйвер поддерживает использование адресов IPv6. Используйте коллекцию свойств подключения и свойство строки подключения serverName. Дополнительные сведения см. в статье [Building the Connection URL](../../connect/jdbc/building-the-connection-url.md) (Формирование URL-адреса подключения).

**Что такое адаптивная буферизация?**  
Адаптивная буферизация реализована, начиная с JDBC Driver версии 1.2 для Microsoft SQL Server 2005. Адаптивная буферизация разработана для получения любых данных большого объема без затрат на использование серверных курсоров. Функция адаптивной буферизации в драйвере Microsoft JDBC для SQL Server указывает свойство строки подключения responseBuffering, которому можно присвоить значение adaptive или full. В выпуске 1.2 по умолчанию установлен режим полной буферизации, и приложение должно задавать режим адаптивной буферизации явным образом. Начиная с драйвера JDBC версии 2.0 по умолчанию используется значение adaptive. Таким образом, приложению не нужно запрашивать адаптивное поведение явным образом, чтобы получить адаптивное поведение буферизации. Дополнительные сведения см. в статье [Использование адаптивной буферизации](../../connect/jdbc/using-adaptive-buffering.md) и в записи блога [Что такое адаптивная буферизация ответов и зачем она нужна?](https://go.microsoft.com/fwlink/?LinkId=111575).

**Поддерживает ли драйвер создание пулов подключений?**  
Драйвер поддерживает создание пулов соединений на платформе Java Enterprise Edition 5 (Java EE 5). В драйвере реализованы необходимые интерфейсы JDBC 3.0, что позволяет ему участвовать в любой реализации пулов соединений, предоставляемой поставщиками серверов приложений промежуточного слоя. В этих средах драйвер участвует в соединениях, объединенных в пул. Дополнительные сведения см. в статье [Using Connection Pooling](../../connect/jdbc/using-connection-pooling.md). В самом драйвере создание пулов не реализовано. Эту функцию за него выполняют сторонние серверы приложений Java.

**Предоставляется ли техническая поддержка для драйвера?**  
Доступны несколько вариантов поддержки. Вы можете задать свой вопрос или сообщить о проблеме в нашем [репозитории GitHub](https://github.com/microsoft/mssql-jdbc), который отслеживается корпорацией Майкрософт. [Форумы](https://go.microsoft.com/fwlink/?LinkID=246673) также отслеживаются корпорацией Майкрософт, специалистами MVP и сообществом. Кроме того, вы можете обратиться в службу поддержки клиентов Майкрософт. Группа разработчиков может попросить вас воспроизвести проблему без использования сторонних серверов приложений. Если проблему не удастся воспроизвести вне среды размещения контейнера Java, вам нужно будет привлечь к этому вопросу соответствующего стороннего поставщика, чтобы команда разработчиков могла вам помочь. Команда также может попросить вас воспроизвести проблему в операционной системе, например Windows, чтобы определить ее оптимальное решение.

**Сертифицирован ли драйвер для использования со сторонними серверами приложений?**
Драйвер протестирован на различных серверах приложений, включая IBM WebSphere и SAP NetWeaver.

**Как включить трассировку?**  
Драйвер JDBC поддерживает использование трассировки (ведения журнала). Это дает возможность решать проблемы с драйвером, когда он используется в приложении. В драйвере JDBC трассировка JAR на стороне клиента включается в файле java.util.logging через интерфейсы API для ведения журнала. Дополнительные сведения см. в статье [Трассировка операций драйвера](../../connect/jdbc/tracing-driver-operation.md). Сведения о трассировке XA на стороне сервера см. в статье [Data Access Tracing in SQL Server](https://go.microsoft.com/fwlink/?LinkId=248705)(Трассировка доступа к данным в SQL Server).

**Где можно скачать предыдущие версии драйвера, например драйвер JDBC для SQL Server 2000, SQL Server 2005 либо драйвер JDBC версий 1.0, 1.1 или 1.2?**  
Эти версии драйвера не доступны для загрузки, так как они больше не поддерживаются. Мы постоянно работаем над улучшением поддержки возможностей подключения Java. поэтому настоятельно рекомендуем использовать последнюю версию драйвера Microsoft JDBC.

**Я использую JRE 1.4. Какой драйвер совместим с JRE версии 1.4?**  
Если вы используете продукты SAP и вам нужна поддержка JRE 1.4, создайте соответствующий запрос на странице [SAPService Marketplace](https://service.sap.com/) . Там вы сможете получить драйвер Microsoft JDBC 1.2.

**Может ли драйвер обмениваться данными с помощью проверенных алгоритмов FIPS?**  
Драйвер Microsoft JDBC не содержит алгоритмы шифрования. Если клиент использует операционную систему, приложение и алгоритмы JVM, которые считаются приемлемыми согласно Федеральному стандарту обработки информации (FIPS), и настраивает драйвер на использование этих алгоритмов, для обмена данными драйвер использует только назначенные алгоритмы.

## <a name="see-also"></a>См. также:

[Общие сведения о драйвере JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
