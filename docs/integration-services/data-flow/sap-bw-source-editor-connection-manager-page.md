---
title: Редактор источника SAP BW (страница "Диспетчер соединений")
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.connection.f1
ms.assetid: 2a6dc531-85ca-43c5-a65f-3ad3f7d537c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 041f05a2d7ae623ee40db320676555dad5468459
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726389"
---
# <a name="sap-bw-source-editor-connection-manager-page"></a>Редактор источников SAP BW (страница «Диспетчер соединений»)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Используйте страницу **Диспетчер соединений** диалогового окна **Редактор источника SAP BW** , чтобы выбрать диспетчер соединений SAP BW для источника SAP BW. На этой странице можно также выбрать режим выполнения и параметры для извлечения данных из источника данных системы SAP Netweaver BW.  
  
 Для получения дополнительных сведений о компоненте источника SAP BW для [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 для SAP BW см. раздел [Источник SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  Документация по Microsoft Connector 1.1 для SAP BW предполагает, что читатель знаком со средой SAP Netweaver BW. Дополнительные сведения о SAP Netweaver BW или сведения о настройке объектов и процессов SAP Netweaver BW см. в документации SAP.  
  
> [!IMPORTANT]  
>  Для извлечения данных из SAP Netweaver BW требуется дополнительная лицензия SAP. Обратитесь к SAP, чтобы уточнить требования.  
  
 **Открытие страницы «Диспетчер соединений»**  
  
1.  В [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте пакет [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , содержащий источник SAP BW.  
  
2.  На вкладке **Поток данных** дважды щелкните источник SAP BW.  
  
3.  В **Редакторе источника SAP BW**щелкните **Диспетчер соединений** , чтобы открыть страницу редактора **Диспетчер соединений** .  
  
## <a name="static-options"></a>Статические параметры  
  
> [!NOTE]  
>  Если вы не знаете все значения, необходимые для настройки источника, может потребоваться связаться с администратором SAP.  
  
 **Диспетчер соединений SAP BW**  
 Выберите из списка существующий диспетчер соединений или создайте новое соединение, нажав кнопку **Создать**.  
  
 **Создать**  
 Создайте новый диспетчер соединений с помощью диалогового окна **Диспетчер соединений SAP BW** .  
  
 Дополнительные сведения об этом диалоговом окне см. в разделе [SAP BW Connection Manager Editor](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md).  
  
 **Назначение OHS**  
 Выберите пункт назначения концентратора службы (OHS) для извлечения данных из источника.  
  
 **Режим выполнения**  
 Укажите метод извлечения данных из источника.  
  
|Параметр|Описание|  
|------------|-----------------|  
|**P – запустить цепочку процесса**|Запустите цепочку процессов. В этом случае пакет [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] запустит процесс извлечения.|  
|**W – ждать уведомления**|Подождите уведомления системы SAP Netweaver BW перед тем, как начать извлечение данных. В этом случае система SAP Netweaver BW запустит процесс извлечения.|  
|**E – только извлечь**|Выполните извлечение данных, связанных с запросом с определенным идентификатором. В этом случае система SAP Netweaver BW уже извлекла данные во внутреннюю таблицу и пакет [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] просто считывает данные.|  
  
 **Предварительный просмотр**  
 Откройте диалоговое окно **Предварительный просмотр** , в котором можно просмотреть предварительные результаты. Дополнительные сведения см. в статье [Preview](../../integration-services/data-flow/preview.md).  
  
> [!IMPORTANT]  
>  Параметр **Предварительный просмотр** , доступный на странице **Диспетчер соединений** Редактора источника SAP BW, непосредственно извлекает данные. Если настроить SAP Netweaver BW для извлечения только тех данных, которые изменились со времени предыдущего сеанса извлечения, то при выборе параметра **Предварительный просмотр** просматриваемые данные будут исключены из следующего сеанса извлечения.  
  
 При нажатии кнопки **Предварительный просмотр**можно также открыть диалоговое окно **Журнал запросов** . Это диалоговое окно может использоваться для просмотра событий, зарегистрированных в момент запроса, который выполняется в системе SAP Netweaver BW для образцов данных. Дополнительные сведения см. в статье [Request Log](../../integration-services/data-flow/request-log.md).  
  
## <a name="execution-mode-dynamic-options"></a>Динамические параметры режима выполнения  
  
> [!NOTE]  
>  Если вы не знаете все значения, необходимые для настройки источника, может потребоваться связаться с администратором SAP.  
  
### <a name="execution-mode--p---trigger-process-chain"></a>Режим выполнения = p — цепь обработки триггера.  
  
#### <a name="rfc-destination-options"></a>Параметры назначения RFC  
 Нет необходимости в изучении или вводе этих значений заранее. Нажмите кнопку **Поиск** , чтобы найти и выбрать соответствующее назначение RFC. После выбора назначения RFC компонент вводит соответствующие значения для этих параметров.  
  
 **Узел шлюза**  
 Введите имя или IP-адрес сервера узла шлюза. Обычно имя или IP-адрес совпадают с аналогичными данными сервера приложений SAP.  
  
 **Служба шлюза**  
 Введите имя службы шлюза в формате **sapgwNN**, где **NN** — номер системы.  
  
 **ID программы**  
 Введите идентификатор программы, связанный с назначением RFC.  
  
 **Найти**  
 Выполните поиск назначения RFC с помощью диалогового окна **Поиск назначения RFC** . Дополнительные сведения об этом диалоговом окне см. в разделе [Look Up RFC Destination](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
#### <a name="process-chain-options"></a>Параметры обработки цепочек  
 Нет необходимости в изучении или вводе этих значений заранее. Нажмите кнопку **Поиск** , чтобы найти и выбрать соответствующую цепочку процессов. После выбора цепочки процесса компонент вводит нужное значение для этого параметра.  
  
 **Цепочка процесса**  
 Введите имя процесса цепочки, которое будет вызвано источником.  
  
 **Найти**  
 Выполните поиск цепочки процесса при помощи диалогового окна **Найти цепочку процесса** . Дополнительные сведения об этом диалоговом окне см. в разделе [Look Up Process Chain](../../integration-services/data-flow/look-up-process-chain.md).  
  
### <a name="execution-mode--w---wait-for-notify"></a>Режим выполнения — W = Ожидать уведомления  
  
#### <a name="rfc-destination-options"></a>Параметры назначения RFC  
 Нет необходимости в изучении или вводе этих значений заранее. Нажмите кнопку **Поиск** , чтобы найти и выбрать соответствующее назначение RFC. После выбора назначения RFC компонент вводит соответствующие значения для этих параметров.  
  
 **Узел шлюза**  
 Введите имя или IP-адрес сервера узла шлюза. Обычно имя или IP-адрес совпадают с аналогичными данными сервера приложений SAP.  
  
 **Служба шлюза**  
 Введите имя службы шлюза в формате **sapgwNN**, где **NN** — номер системы.  
  
 **ID программы**  
 Введите идентификатор программы, связанный с назначением RFC.  
  
 **Найти**  
 Выполните поиск назначения RFC с помощью диалогового окна **Поиск назначения RFC** . Дополнительные сведения об этом диалоговом окне см. в разделе [Look Up RFC Destination](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
### <a name="execution-mode--e---extract-only"></a>Режим выполнения = E — только извлечение  
 **Идентификатор запроса**  
 Введите идентификатор запроса, связанный с извлечением.  
  
## <a name="see-also"></a>См. также:  
 [Редактор источника SAP BW (страница "Столбцы")](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [Редактор источника SAP BW (страница "Вывод ошибок")](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Редактор источника SAP BW (страница "Дополнительно")](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)   
 [Справка F1 по Microsoft Connector для SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
