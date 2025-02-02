---
title: Подключение S3 для распределения по уровням HDFS
titleSuffix: SQL Server big data clusters
description: В этой статье описывается настройка HDFS, распределение по уровням для монтажа внешней системы S3 файл в HDFS в кластере SQL Server 2019 больших данных (Предварительная версия).
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f126620c4da759a4c56abad05bf2e989d7d1bc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782072"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>Как S3 подключения для HDFS, распределение по уровням в кластере больших данных

Следующие разделы содержат пример того, как настроить распределение по уровням с источником данных S3 хранилища HDFS.

## <a name="prerequisites"></a>предварительные требования

- [Развернутые больших данных кластера](deployment-guidance.md)
- [Средства работы с большими данными](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**
- Создание и передача данных в контейнер S3 
  - Отправить CSV-ФАЙЛ или файлы для контейнера S3 Parquet. Это внешние данные HDFS, который будет подключен к HDFS в кластере больших данных.

## <a name="access-keys"></a>Ключи доступа

1. Откройте командную строку на клиентском компьютере с доступом к кластеру больших данных.

1. Создайте локальный файл с именем **filename.creds** , содержащий учетные данные учетной записи S3 в следующем формате:

   ```text
    fs.s3a.access.key=<Access Key ID of the key>
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > Дополнительные сведения о создании ключей доступа S3 см. в разделе [ключи доступа S3](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).

## <a id="mount"></a> Подключение удаленного хранилища HDFS

Теперь, когда вы подготовили файл учетных данных с помощью ключей доступа, можно начать подключение. Следующие действия подключить внешнее хранилище HDFS в S3 в локальном хранилище HDFS кластера больших данных.

1. Используйте **kubectl** найти IP-адрес для конечной точки **контроллера svc-external** службы в кластере больших данных. Найдите **внешний IP-** .

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Входа в систему **mssqlctl** с помощью внешний IP-адрес конечной точки контроллера с помощью имени пользователя кластера и пароль:

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```

1. Подключение удаленного хранилища HDFS в Azure с помощью **создать монтирования пул носителей кластера mssqlctl**. Замените значения заполнителей перед выполнением следующей команды:

   ```bash
   mssqlctl cluster storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name> --credential-file <path-to-s3-credentials>/file.creds
   ```

   > [!NOTE]
   > Подключения «создать» является асинхронным. В настоящее время отсутствуют сообщения, указывающее, успешно ли выполнено присоединение. См. в разделе [состояние](#status) раздела, чтобы проверить состояние вашей подключение.

В случае если успешно, можно запросить данные HDFS и выполнения заданий Spark на ее основе. Он будет отображаться в HDFS для кластера больших данных в расположении, заданном параметром `--mount-path`.

## <a id="status"></a> Получение состояния подключение

Чтобы получить список состояние всех подключение кластера больших данных, используйте следующую команду:

```bash
mssqlctl cluster storage-pool mount status
```

Чтобы получить список состояние подключения в указанную папку в файловой системе HDFS, используйте следующую команду:

```bash
mssqlctl cluster storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Удаление подключения

Чтобы удалить подключение, используйте **удаления подключения пул носителей кластера mssqlctl** команды и укажите путь подключения в HDFS:

```bash
mssqlctl cluster storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения о кластерах SQL Server 2019 большие данные см. в разделе [Каковы кластеров SQL Server 2019 больших данных?](big-data-cluster-overview.md).
