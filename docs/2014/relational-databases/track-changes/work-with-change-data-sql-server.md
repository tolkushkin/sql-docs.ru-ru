---
title: Работа с информацией об изменениях (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data [SQL Server]
- change data capture [SQL Server], query function scenarios
- change data capture [SQL Server], LSN boundaries
- change data capture [SQL Server], query functions
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: eaafa011f1b99ea90afce2902c877d0a25b9e6e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269893"
---
# <a name="work-with-change-data-sql-server"></a>Работа с информацией об изменениях (SQL Server)
  Информация об изменениях сделана доступной для клиентов системы отслеживания измененных данных через функции с табличным значением. Всем запросам этих функций требуются два параметра для определения диапазона регистрационных номеров транзакций в журнале, которые нужно учитывать при разработке возвращаемого результирующего набора. Необходимо рассмотреть как верхнее, так и нижнее значения номеров LSN, ограничивающие этот интервал.  
  
 Для помощи в определении соответствующих значений LSN имеется несколько функций, которые можно использовать в запросах с возвращающими табличное значение функциями. Функция [sys.fn_cdc_get_min_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql) возвращает наименьший номер LSN, связанный с периодом действия экземпляра системы отслеживания. Периодом действия является интервал времени, в течение которого информация об изменениях остается доступной для экземпляров системы отслеживания. Функция [sys.fn_cdc_get_max_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql) возвращает наибольший номер LSN для периода действия. Функции [sys.fn_cdc_map_time_to_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql) и [sys.fn_cdc_map_lsn_to_time](/sql/relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql) помогают расположить значения номеров LSN на стандартной временной шкале. Поскольку система отслеживания измененных данных использует закрытые интервалы запроса, иногда требуется создать следующий номер LSN, чтобы убедиться, что изменения не повторяются в последовательных окнах запроса. Функции [sys.fn_cdc_increment_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql) и [sys.fn_cdc_decrement_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql) используются, если значению номера LSN необходима добавочная корректировка.  
  
##  <a name="LSN"></a> Проверка границ номера LSN  
 Рекомендуется проверять границы диапазона номера LSN перед использованием их в запросе возвращающей табличное значение функции. Конечные точки, имеющие значения null или выходящие за границы периода действия экземпляра отслеживания, вызовут ошибку, которую возвратит возвращающая табличное значение функция отслеживания измененных данных.  
  
 Например, если параметр, с помощью которого определяется интервал запроса, является недопустимым или выходит за пределы допустимого диапазона значений, либо если он не является допустимым параметр фильтра строки, то для запроса возвращается следующая ошибка для всех изменений.  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 Следующая ошибка возвращается для запроса `net changes`.  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  Установлено, что содержимое сообщения 313 неверно и поэтому не объясняет действительную причину ошибки. Это неверное применение сообщения объясняется неспособностью получить явную ошибку из  возвращающей табличное значение функции. Тем не менее сочли, что лучше возвратить пусть даже неверное значение ошибки, чем возвратить пустой результат. Ведь пустой результирующий набор невозможно отличить от допустимого запроса, возвращающего отсутствие изменений.  
  
 Ошибки авторизации возвращают ошибку при запросе всех изменений, как показано ниже.  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 То же самое относится к запросам суммарных изменений.  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 Представленный ниже шаблон «Перечисление суммарных изменений с помощью TRY CATCH» показывает, как перехватить эти известные ошибки возвращающих табличные значения функций и возвратить более понятные сведения об ошибке.  
  
> [!NOTE]  
>  Чтобы найти шаблоны системы отслеживания измененных данных в среде SQL Server Management Studio, в меню **Вид** выберите **Обозреватель шаблонов**, разверните элемент **Шаблоны SQL Server** , затем папку **Система отслеживания измененных данных** .  
  
##  <a name="Functions"></a> Функции запросов  
 В зависимости от характеристик отслеживаемой исходной таблицы и конфигурации экземпляра системы отслеживания создается одна или две возвращающие табличное значение функции для выполнения запросов информации об изменениях.  
  
-   Функция [cdc.fn_cdc_get_all_changes_<экземпляр_отслеживания>](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql) возвращает все изменения, внесенные в течение указанного интервала. Эта функция создается всегда. Записи всегда возвращаются отсортированными, вначале по номеру LSN зафиксированной транзакции изменения, затем по порядковому значению изменения в его транзакции. В зависимости от выбранного параметра фильтра строки возвращается обновленная строка (параметр фильтра строки «all») или новое и старое значения обновленной строки (параметр фильтра строки «all update old»).  
  
-   Функция [cdc.fn_cdc_get_net_changes_<экземпляр_отслеживания>](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql) создается, если параметр @supports_net_changes имеет значение 1, когда включена исходная таблица.  
  
    > [!NOTE]  
    >  Этот параметр поддерживается, только если в исходной таблице определен первичный ключ либо параметр @index_name использовался для идентификации уникального индекса.  
  
     Функция **netchanges** возвращает одно изменение на каждую измененную строку исходной таблицы. Если в течение интервала запроса для строки было зарегистрировано несколько изменений, то значения столбцов будут отражать конечное содержимое строки. Чтобы правильно определить операцию, необходимую для обновления целевой среды, возвращающая табличное значение функция должна учитывать как начальную, так и конечную операции со строкой в течение интервала запроса. При указании параметра фильтра строк «all» запрос `net changes` будет возвращать операции вставки, удаления или обновления (новые значения). Обратите внимание, что этот параметр всегда возвращает значение маски обновления как значение NULL, потому что вычисление статистической маски требует значительных затрат. Если требуется статистическая маска, отражающая все изменения строки, используется параметр «all with mask». Если для последующей обработки не требуется разделения операций вставки и обновления, то используется параметр «all with merge». В этом случае будут присутствовать только операции над двумя значениями: 1 для удаления и 5 для операции, которое может быть вставкой или обновлением. Этот параметр отключает дополнительные вычисления, позволяющие определить тип производной операции: операция вставки или обновления. Если в таком различении нет необходимости, то использование этого параметра может увеличить производительность.  
  
 Маска обновления, возвращаемая функцией запроса — это компактное представление всех изменений столбцов, связанных со строкой информации об изменениях. Обычно такие данные нужны только для небольшого подмножества отслеживаемых столбцов. Имеются функции, способные помочь при извлечении информации из маски в форме, которая напрямую может использоваться приложениями. Функция [sys.fn_cdc_get_column_ordinal](/sql/relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql) возвращает порядковый номер именованного столбца для данного экземпляра системы отслеживания. Функция [sys.fn_cdc_is_bit_set](/sql/relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql) возвращает четность бита в предоставленной маске на основе переданного функцией порядкового номера. Совместное использование этих двух функций позволяет эффективно извлекать информацию из маски обновления и возвращать ее в информации об изменениях. См. представленный ниже шаблон «Перечисление суммарных изменений с помощью параметра "All With Mask"», в котором показано использование этих функций.  
  
##  <a name="Scenarios"></a> Сценарий функции запроса  
 В следующем разделе описан типичный сценарий запроса сведений системы отслеживания измененных данных с использованием функций запроса cdc.fn_cdc_get_all_changes_<экземпляр_отслеживания> и cdc.fn_cdc_get_net_changes_<экземпляр_отслеживания>.  
  
### <a name="querying-for-all-changes-within-the-capture-instance-validity-interval"></a>Выполнение запроса для получения всех изменений в течение периода действия экземпляра системы отслеживания  
 Наиболее простым запросом информации об изменениях является запрос, который возвращает всю текущую информацию об изменениях за период действия экземпляра системы отслеживания. Чтобы выполнить такой запрос, вначале определите нижнюю и верхнюю границу номера LSN периода действия. Затем с помощью этих значений определите параметры @from_lsn и @to_lsn, передаваемые функции запроса cdc.fn_cdc_get_all_changes_<экземпляр_отслеживания> или cdc.fn_cdc_get_net_changes_<экземпляр_отслеживания>. Для получения нижней границы воспользуйтесь функцией [sys.fn_cdc_get_min_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql) , для получения верхней границы — функцией [sys.fn_cdc_get_max_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql) . Образец кода для запроса всех текущих действительных изменений с помощью помощи функции запроса cdc.fn_cdc_get_all_changes_<экземпляр_отслеживания> см. в шаблоне «Перечисление всех изменений для действительного диапазона». См. шаблон «Перечисление суммарных изменений для действительного диапазона», в котором демонстрируется подобный пример использования функции cdc.fn_cdc_get_net_changes_<экземпляр_отслеживания>.  
  
### <a name="querying-for-all-new-changes-since-the-last-set-of-changes"></a>Выполнение запроса для получения всех новых изменений со времени последнего набора изменений  
 Для типичных приложений выполнение запросов для получения информации об изменениях будет бесконечным процессом, выполняющим периодические запросы всех изменений, внесенных со времени последнего запроса. Для таких запросов можно с помощью функции [sys.fn_cdc_increment_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql) получать нижнюю границу текущего запроса из верхней границы предыдущего запроса. Этот метод гарантирует, что строки не повторяются, поскольку интервал запроса рассматривается как замкнутый интервал (интервал, в который включены обе конечные точки). Затем с помощью функции [sys.fn_cdc_get_max_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql) получите верхнюю конечную точку интервала нового запроса. См. шаблон «Перечисление всех изменений со времени предыдущего запроса», в котором демонстрируется образец кода для систематического перемещения окна запроса для получения всех изменений со времени последнего запроса.  
  
### <a name="querying-for-all-new-changes-up-until-now"></a>Запрос всех новых изменений до настоящего момента  
 Типичным ограничением, которое накладывается на изменения, возвращаемые функцией запроса, является включение только изменений, которые были внесены между предыдущим запросом до текущих даты и времени. Для такого запроса примените функцию sys.fn_cdc_increment_lsn к значению @from_lsn, с помощью которого определялась нижняя граница в предыдущем запросе. Поскольку верхняя граница на интервале времени выражается как момент времени, она может быть преобразована в значение номера LSN до его использования функцией запроса. Перед преобразованием значения типа данных datetime в соответствующее значение номера LSN необходимо убедиться, чтобы процесс отслеживания обработал все изменения, зафиксированные до заданной верхней границы. Это необходимо для того, чтобы гарантировать распространение всех соответствующих изменений в таблицу изменений. Одним из способов сделать это является структурирование цикла ожидания, который периодически проверяет, не превышено ли заданное время завершения интервала запроса текущим зафиксированным номером LSN, максимальным по всем таблицам изменений базы данных.  
  
 После того как в цикле задержки будет установлено, что процесс отслеживания уже обработал все релевантные записи журнала, определите с помощью [sys.fn_cdc_map_time_to_lsn](/sql/relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql) новую верхнюю конечную точку, выражаемую как значение номера LSN. Чтобы гарантировать получение всех записей, зафиксированных до указанного времени, вызовите функцию sys.fn_cdc_map_time_to_lsn с параметром «largest less than or equal» (самое большое значение, меньше или равно).  
  
> [!NOTE]  
>  В периоды отсутствия активности в таблицу cdc.lsn_time_mapping добавляется фиктивная запись, чтобы отметить тот факт, что процесс отслеживания обработал изменения вплоть до данного времени фиксации. Это позволяет избежать впечатления, будто процесс отслеживания задержался, если для процесса просто нет недавних изменений.  
  
 Шаблон «Перечисление всех изменений вплоть до настоящего момента» демонстрирует, как используется предыдущая стратегия для запроса информации об изменениях.  
  
### <a name="adding-a-commit-time-to-an-all-changes-result-set"></a>Добавление времени фиксации к результирующему набору всех изменений  
 Время фиксации каждой транзакции с соответствующей записью в таблице изменений базы данных доступно в таблице [cdc.lsn_time_mapping](/sql/relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql). Соединяя значение __$start_lsn, возвращаемое в запросе для всех изменений, со значением start_lsn записи таблицы cdc.lsn_time_mapping, можно возвратить tran_end_time вместе с информвцией об изменениях для отметки изменения временем фиксации транзакции в источнике. Шаблон «Добавление времени фиксации к результирующему набору всех изменений» демонстрирует, как выполнить такое соединение.  
  
### <a name="joining-change-data-with-other-data-from-the-same-transaction"></a>Соединение информации об изменениях с другими данными из той же транзакции  
 Иногда имеет смысл соединить информацию об изменениях с другими данными, касающимися транзакции, если она зафиксирована на источнике. Из столбца tran_begin_lsn в таблице cdc.lsn_time_mapping передается информация, необходимая для выполнения такого соединения. Когда происходит обновление источника, значение database_transaction_begin_lsn из системного динамического представления [sys.dm_tran_database_transactions](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql) должно быть сохранено вместе со всеми другими данными, соединяемыми с информацией об изменениях. Функция fn_convertnumericlsntobinary используется для сравнения значений database_transaction_begin_lsn и tran_begin_lsn. Код для создания этой функции доступен в шаблоне «Создание функции fn_convertnumericlsntobinary». Шаблон «Возвращение всех изменений с помощью конкретного значения tran_begin_lsn» демонстрирует, как можно повлиять на соединение.  
  
### <a name="querying-using-datetime-wrapper-functions"></a>Выполнение запросов с помощью функций-оболочек DateTime  
 В сценарии типичного приложения для выполнения запросов информации об изменениях периодически запрашиваются при помощи скользящего окна, ограниченного значениями типа datetime. Для этого класса клиентов в системе отслеживания измененных данных предусмотрена хранимая процедура [sys.sp_cdc_generate_wrapper_function](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql) , которая формирует скрипты создания пользовательских функций-оболочек для функций запроса системы отслеживания измененных данных. Эти пользовательские оболочки позволяют выражать интервал запроса как пару даты и времени.  
  
 Параметры вызова хранимой процедуры позволяют формировать оболочки для всех экземпляров системы отслеживания, к которым вызывающий имеет доступ, или только для указанного экземпляра системы отслеживания. Среди поддерживаемых параметров также есть возможность указывать, должна ли включаться верхняя конечная точка интервала отслеживания, какие из доступных отслеживаемых столбцов должны быть включены в результирующий набор и какие из включенных столбцов должны иметь соответствующие флаги обновления. Процедура возвращает результирующий набор с двумя столбцами: имя формируемой функции, производное от имени экземпляра системы отслеживания, и инструкция создания для хранимой процедуры оболочки. Также создается функция упаковки запроса всех изменений. Если во время создания экземпляра системы отслеживания параметр @supports_net_changes установлен, то формируется также функция-оболочка для функции суммарных изменений.  
  
 За вызов хранимой процедуры создания скрипта формирующей инструкции создания для хранимых процедур оболочки, а также за выполнение результирующих скриптов создания функций отвечает разработчик. Это не происходит автоматически при создании экземпляра системы отслеживания.  
  
 Оболочками datetime владеет пользователь, и эти оболочки не создаются в схеме (используемой по умолчанию) вызывающего. Сформированная функция подходит без каких-либо изменений для большинства пользователей. Однако созданный скрипт всегда можно настроить дополнительно до создания функции.  
  
 Именем функции-оболочки для запроса всех изменений является fn_all_changes_, за которым следует имя экземпляра системы отслеживания. Для оболочки суммарных изменений используется префикс fn_net_changes_. Обе функции принимают три аргумента, так же как и соответствующие им возвращающие табличные значения функции системы отслеживания измененных данных. Однако интервал запроса для оболочек ограничен двумя значениями datetime вместо двух значений LSN. Параметр @row_filter_option для обоих наборов функций один и тот же.  
  
 Функции-оболочки поддерживают следующее соглашение об систематического прохода для временной шкалы системы отслеживания измененных данных изменений: Предполагается, что параметр @end_time предыдущего интервала будет использоваться как параметр @start_time последующего интервала. Функция-оболочка обеспечивает сопоставление значений datetime со значениями номера LSN. Она также обеспечивает, что при соблюдении этого соглашения не будет потерь или повторений данных.  
  
 Оболочки можно создавать для поддержки закрытой или открытой верхней границы для заданного окна запроса. Это означает, что вызывающий может указывать, будут ли включаться в интервал записи, для которых время фиксации совпадает с верхней границей интервала извлекаемых данных. По умолчанию верхняя граница включается в интервал.  
  
 Если в качестве значения параметра @from_lsn или @to_lsn функции созданного запроса, возвращающей табличное значение, указано NULL, то она не завершается успешно, тогда как функции-оболочки datetime используют значение NULL, чтобы оболочки datetime могли возвратить все текущие изменения. Это означает, что если значение NULL передается оболочке datetime как нижняя конечная точка окна запроса, то нижняя конечная точка периода действия экземпляра системы отслеживания используется в базовой инструкции SELECT, которая применяется к функции запроса, возвращающей табличное значение. Аналогично, если NULL передается как верхняя конечная точка окна запроса, то верхняя конечная точка периода действия экземпляра системы отслеживания используется при выборе из функции запроса, возвращающей табличное значение.  
  
 В результирующий набор, возвращаемый функцией-оболочкой, включаются все запрошенные столбцы, за которыми следует столбец операции, записанный как один или два символа для идентификации операции, связанной со строкой. Флаги обновления при запросе возвращаются как битовые столбцы после кода операции в порядке, указанном параметром @update_flag_list. Сведения о параметрах вызова для настройки формируемых оболочек datetime см. в разделе [sys.sp_cdc_generate_wrapper_function (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql).  
  
 Шаблон «Создание возвращающей табличное значение функции-оболочки с помощью флага обновления» показывает, как настроить в созданной функции-оболочке присоединение флага обновления для заданного столбца к результирующему набору запросом суммарных изменений. Шаблон «Возвращающие табличное значение функции-оболочки CDC для схемы» показывает, как создавать оболочки datetime для возвращающих табличное значение функций запроса для всех экземпляров системы отслеживания, созданных для исходных таблиц в схеме конкретной базы данных.  
  
 Использование оболочки datetime для запроса информации об изменениях, см. на примере шаблона «Получение суммарных изменений с помощью оболочки с флагами обновления». Этот шаблон демонстрирует, как выполнить запрос для суммарных изменений, если в функции-оболочке настроено возвращение флагов обновления. Следует отметить, что параметр фильтра строки «all with mask» необходим для того, чтобы базовая функция запроса при обновлении возвращала маску обновления, отличную от NULL. Значения NULL передаются для нижней и верхней границ интервала datetime, чтобы функция использовала нижнюю и верхнюю конечные точки интервала действия для экземпляра системы отслеживания при выполнении базового запроса на основе LSN. Запрос возвращает одну строку для каждого изменения исходной строки, которое происходит в допустимом диапазоне для экземпляра системы отслеживания.  
  
### <a name="using-the-datetime-wrapper-functions-to-transition-between-capture-instances"></a>Переход между экземплярами системы отслеживания с помощью функций-оболочек datetime  
 Система отслеживание измененных данных поддерживает до двух экземпляров для одной отслеживаемой исходной таблицы. Основным случаем применения этой возможности является согласование перехода между несколькими экземплярами системы отслеживания, если изменения языка описания данных DDL в исходной таблице расширяют набор доступных для отслеживания столбцов. При переходе к новому экземпляру системы отслеживания одним из способов защиты приложения более высокого уровня от изменений в именах базовых функций запроса является использование функции-оболочки для упаковки базового вызова. Затем следует обеспечить, чтобы имя функции-оболочки оставалось неизменным. Когда должно произойти переключение, старая функция-оболочка должна быть удалена; при этом должна быть создана новая функция-оболочка с тем же именем, содержащая ссылку на новые функции запроса. При первом изменении созданного скрипта создания функции-оболочки с тем же именем можно сделать переключение на новый экземпляр системы отслеживания, не затрагивая приложение более высокого уровня.  
  
## <a name="see-also"></a>См. также:  
 [Отслеживание измененных данных (SQL Server)](../track-changes/track-data-changes-sql-server.md)   
 [О фиксации измененных данных (SQL Server)](../track-changes/about-change-data-capture-sql-server.md)   
 [Включение и отключение отслеживания измененных данных (SQL Server)](../track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [Администрирование и наблюдение за отслеживанием измененных данных (SQL Server)](../track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
