---
title: Настройка воспроизведения в помощнике по базе данных службы "Экспериментирование" для обновления до SQL Server
description: Настройка воспроизведения в помощнике по базе данных службы "Экспериментирование"
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: 8efef6f081395265f641197058b7920162cdde46
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794492"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>Настройка воспроизведения в помощнике по базе данных службы "Экспериментирование"

Помощник по базе данных службы "Экспериментирование" (веб) использует средства распределенного воспроизведения из экземпляра SQL Server для воспроизведения записанной трассировки в обновленной тестовой среде. Мы советуем применить этот тестовый запуск с помощью небольших трассировки файла перед выполнением полного воспроизведения для обеспечения правильного воспроизведения запросов.

## <a name="distributed-replay-requirements"></a>Требования распределенного воспроизведения

- Дополнительные 78% места на жестком диске требуется для создания файлов IRF на компьютере контроллера распределенного воспроизведения.
- 200 МБ или 512 МБ — размер смены идеальный трассировки для трассировки производительности или производства.   
- Минимальные требования к ЦП и ОЗУ для компьютеров, контроллера и клиента распределенного воспроизведения — это для одного ядра ЦП 3,5 ГБ ОЗУ.
- Время воспроизведения приблизительно принимает 1,55 раз больше, чем время записи, так как один контроллер и четыре дочерних машины используются для воспроизведения трассировки рабочей.
- При использовании нашей «опубликованные» версии рабочей среде и файлов определения трассировки производительности и фильтры определение трассировки производительности, данные трассировки для одной базы данных, интерес, анализ показывает, что **трассировки производительности** размер около 15 раз выше, чем **трассировки рабочей** размер.

## <a name="set-up-a-virtual-network-or-domain"></a>Настройка виртуальной сети или домена

Распределенное воспроизведение требует использования общих учетных записей между компьютерами. Из-за этого требования, а также по соображениям безопасности рекомендуется запускать распределенного воспроизведения, в виртуальной сети или сети управлением домена:

- Создание контроллера и клиентских компьютеров в среде.
- Убедитесь, что компьютеры контроллера и клиента можно проверить связь с друг с другом по сети.
- Клиентских компьютеров распределенного воспроизведения должны иметь подключение к целевому компьютеру воспроизведения под управлением SQL Server.

## <a name="set-up-the-controller-service"></a>Настроить службу контроллера

Чтобы настроить службу контроллера:

1. Установите контроллер распределенного воспроизведения с помощью установщика SQL Server. Если вы пропустили шаг мастера установщик SQL Server, который настраивает контроллер распределенного воспроизведения, можно настроить через файл конфигурации контроллера. При обычной установке, файл конфигурации расположен в C:\Program Files (x86) \Microsoft SQL Server\<версии\>\Tools\DReplayController\DReplayController.config.
1. Журналы контроллера распределенного воспроизведения находятся в C:\Program Files (x86) \Microsoft SQL Server\<версии\>\Tools\DReplayController\Log.
1. Откройте оснастку Services.msc и перейти к **контроллера распределенного воспроизведения SQL Server** службы.
1. Щелкните правой кнопкой мыши в службе, а затем выберите **свойства**. Настройка учетной записи службы учетную запись, которая являются общими для контроллера и клиентских компьютеров в сети.
1. Выберите **ОК** закрыть **свойства** окна.
1. Перезапустите **контроллера распределенного воспроизведения SQL Server** службы с помощью команды Services.msc. Вы также выполните следующие команды в командной строке, чтобы перезапустить службу:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. Дополнительные параметры конфигурации, см. в разделе [Настройка распределенного воспроизведения](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="configure-dcom"></a>Настройка DCOM

Эта конфигурация требуется только на компьютере контроллера.

1. Откройте dcomcnfg.exe.
1. Разверните **службы компонентов** > **компьютеров** > **компьютер** > **DCOM Config**.
1. В разделе **DCOM Config**, щелкните правой кнопкой мыши **DReplayController**, а затем выберите **свойства**.
1. Перейдите на вкладку **Безопасность** .
1. В разделе **разрешения запуска и активации**выберите **Настройка**, а затем выберите **изменить**.
1. Добавьте пользователя, и начинается воспроизведение. Предоставьте разрешения локальный запуск и Локальная активация пользователя. Если пользователь планирует запустить или удаленной активации, предоставляются разрешения на удаленный запуск и удаленная активация.
1. Выберите **ОК** чтобы зафиксировать изменения и вернуться к **безопасности** вкладки.
1. В разделе **разрешения на доступ**выберите **Настройка**, а затем выберите **изменить**.
1. Добавьте пользователя, и начинается воспроизведение. Предоставьте разрешения на доступ для локального пользователя. Если пользователь планирует для удаленного доступа к службе контроллера, предоставляются разрешения удаленного доступа.
1. Выберите **ОК** чтобы зафиксировать изменения и вернуться к **безопасности** вкладки.
1. Выберите **ОК** для фиксации изменений.
1. Перезапустите службу контроллера распределенного воспроизведения SQL Server с помощью команды Services.msc. Вы также выполните следующие команды в командной строке, чтобы перезапустить службу:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>Настройка службы клиента

Перед настройкой службы клиента с помощью средства работы с сетью, такие как ping убедитесь, что машины контроллере и клиенте могут взаимодействовать.

1. Установка клиента распределенного воспроизведения с помощью установщика SQL Server.
1. Откройте оснастку Services.msc и перейдите к службе клиента распределенного воспроизведения SQL Server.
1. Щелкните правой кнопкой мыши в службе, а затем выберите **свойства**. Настройка учетной записи службы учетную запись, которая часто на компьютерах контроллера и клиента в сети.
1. Выберите **ОК** закрыть **свойства** окна. Если вы пропустили шаг мастера установки SQL Server для настройки клиента распределенного воспроизведения, его можно настроить в файле конфигурации. При обычной установке, файл конфигурации расположен в C:\Program Files (x86) \Microsoft SQL Server\<версии\>\Tools\DReplayClient\DReplayClient.config.
1. Убедитесь, что файл DReplayClient.config содержит имя компьютера контроллера как его контроллер для регистрации.
1.  Перезапустите службу клиента распределенного воспроизведения SQL Server с помощью команды Services.msc. Вы также выполните следующие команды из командной строки, чтобы перезапустить службу:<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. Журналы контроллера распределенного воспроизведения находятся в C:\Program Files (x86) \Microsoft SQL Server\<версии\>\Tools\DReplayClient\Log. В журналах указывается ли клиент может зарегистрироваться с контроллером.
1. При успешном выполнении конфигурации журнала отображается сообщение «зарегистрирован с контроллером < имя контроллера\>«.
1. Дополнительные параметры конфигурации, см. в разделе [Настройка распределенного воспроизведения](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="set-up-distributed-replay-administration-tools"></a>Настройка средства администрирования распределенного воспроизведения

Чтобы быстро проверить правильность работы в среде распределенного воспроизведения можно использовать средства администрирования распределенного воспроизведения. Тестирование конфигурации может быть особенно полезно в среде, в которой несколько клиентских компьютеров зарегистрированных в контроллере. Может потребоваться установить SQL Server Management Studio (SSMS) для получения средств администрирования.

1. Перейдите в папку установки SSMS и найдите dreplay.exe средство администрирования распределенного воспроизведения и его зависимые компоненты.
1. Откройте окно командной строки и выполните `dreplay.exe status -f 1`.
1. Если приведенные выше действия выполняются успешно, в выходных данных консоли означает, что контроллер может видеть своих клиентов в `READY` состояние.

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>Настройка брандмауэра для удаленного доступа распределенного воспроизведения

Удаленный доступ к распределенного воспроизведения требует открытия портов, которые видимы в домене или виртуальной сети.

1. Откройте **брандмауэра Windows** с **повышенной безопасности**.
1. Перейдите к **правила для входящего трафика**.
1. Создать новое правило брандмауэра для входящих подключений для программы C:\Program Files (x86) \Microsoft SQL Server\<версии\>\Tools\DReplayController\DReplayController.exe.
1. Разрешите режим домена доступ ко всем портам для DReplayController.exe иметь возможность удаленно взаимодействовать со службой контроллера.
1. Сохраните правило.

## <a name="set-up-target-computers"></a>Настройка целевых компьютерах

Два воспроизведения необходимы для запуска A / B-тестирования или эксперимента. То есть может потребоваться два отдельных экземпляра из экземпляров SQL Server для сценария миграции. 

Можно также установить две версии экземпляров SQL Server на одном компьютере. Будьте осторожны — убедиться, что экземпляры полностью изолированы во время воспроизведения.

Для каждого воспроизведения необходимо выполнить следующие действия:

1. Восстановите резервную копию базы данных.
1. Предоставьте разрешения для пользователя учетной записи службы клиента для доступа к базе данных в экземпляре SQL Server. Разрешения требуются для запросов, которые будут выполнены в экземпляре SQL Server.
1. Запустите воспроизведение.

## <a name="next-steps"></a>Следующие шаги

- Чтобы узнать, как для воспроизведения записанной трассировки в обновленной тестовой среде, см. в разделе [воспроизведения трассировки](database-experimentation-assistant-replay-trace.md).

- 19-минутный введение Инициатив и демонстрации в следующем видео:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
