---
title: Определение источника пакетов с помощью цифровых подписей | Документы Майкрософт
ms.custom: security
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.digitalsigning.f1
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3bc5b6cc425ad04e9ad1f2cafbae2a3d88f8599c
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65718241"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>Определение источника пакетов с помощью цифровых подписей

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Пакет служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] может быть подписан цифровым сертификатом, удостоверяющим его происхождение. После подписи пакета цифровым сертификатом службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] проверяют цифровую подпись перед загрузкой пакета. Чтобы службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] проверяли подпись, необходимо задать параметр в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] или в программе **dtexec** (dtexec.exe) либо задать необязательное значение реестра.  
  
## <a name="sign-a-package-with-a-digital-certificate"></a>Подпись пакета цифровым сертификатом  
 Прежде чем подписывать пакет цифровым сертификатом, сертификат необходимо получить или создать. Цифровая подпись пакета возможна только при наличии сертификата. Дополнительные сведения о получении сертификата и подписи им пакета см. в разделе [Подписание пакета цифровым сертификатом](#cert).  
  
## <a name="set-an-option-to-check-the-package-signature"></a>Задание параметра для проверки подписи пакета  
 И среда [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , и программа **dtexec** позволяют задать параметр, который настраивает проверку цифровой подписи в службе [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] для подписанных пакетов. Выбор средства (среда [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] или программа **dtexec** ) зависит от того, нужно ли проверять все пакеты или лишь некоторые из них.  
  
-   Чтобы во время разработки перед загрузкой проверялась цифровая подпись всех пакетов, установите параметр **Проверять цифровую подпись при загрузке пакета** в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Этот параметр является глобальной настройкой для всех пакетов в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].
  
-   Чтобы проверить цифровую подпись отдельного пакета, укажите параметр **/VerifyS[igned]** при запуске программы **dtexec** для запуска пакета. Дополнительные сведения см. в статье [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
## <a name="set-a-registry-value-to-check-package-signature"></a>Задание значения реестра для проверки подписи пакета  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] также поддерживают необязательное значение реестра **BlockedSignatureStates**, которое позволяет управлять политикой организации в отношении загрузки подписанных и неподписанных пакетов. Этот параметр препятствует загрузке пакетов, которые не подписаны либо имеют неверную или ненадежную подпись. Дополнительные сведения о задании этого значения реестра см. в разделе [Реализация политики подписывания путем задания параметра реестра](#registry).  
  
> **ПРИМЕЧАНИЕ.** Дополнительный раздел реестра **BlockedSignatureStates** может задавать значение, накладывающее более строгое ограничение, чем параметр цифровой подписи, задаваемый в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] или программе командной строки **dtexec** . В этом случае значение в реестре переопределяет другие параметры.  

## <a name="registry"></a> Реализация политики подписывания путем задания параметра реестра
  Для управления организационной политикой при загрузке подписанных и неподписанных пакетов можно использовать необязательный параметр реестра. При использовании данного параметра реестра его необходимо создать на каждом компьютере, где будут выполняться пакеты [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] и где требуется принудительное выполнение этой политики. После задания такого параметра реестра службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] будут проверять наличие и верность подписи перед загрузкой пакетов.  
  
 Процедура, описанная в этой статье, позволяет добавить необязательный параметр **BlockedSignatureStates** типа DWORD в раздел реестра HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS. Значение данных в **BlockedSignatureStates** определяет, должен ли пакет быть заблокирован, если у него ненадежная подпись, недопустимая подпись или он вообще не подписан. В отношении состояния подписей, используемых для пакетов, значение реестра **BlockedSignatureStates** использует следующие определения:  
  
-   *Действительная подпись* — это подпись, которая может быть успешно прочитана.  
  
-   *Недействительная подпись* — это подпись, для которой расшифрованная контрольная сумма (односторонний хэш-код пакета, зашифрованного закрытым ключом), не соответствует расшифрованной контрольной сумме, вычисленной в процессе загрузки пакетов служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   *Надежная подпись* — это подпись, которая создается с использованием цифрового сертификата, подписанного доверенным центром сертификации. При этом не требуется присутствия подписывающей стороны в списке доверенных издателей пользователя.  
  
-   *Ненадежная подпись* — это подпись, которая не может быть подтверждена доверенным центром сертификации, или подпись, которая не является текущей.  
  
 Следующая таблица перечисляет допустимые значения параметра типа DWORD и связанные с ними политики.  
  
|Значение|Описание|  
|-----------|-----------------|  
|0|Нет административного ограничения.|  
|1|Заблокировать недопустимые подписи.<br /><br /> Этот параметр не блокирует неподписанные пакеты.|  
|2|Заблокировать недопустимые и ненадежные подписи.<br /><br /> Этот параметр не блокирует неподписанные пакеты, но блокирует самостоятельно сформированные подписи.|  
|3|Заблокировать недопустимые и ненадежные подписи и неподписанные пакеты.<br /><br /> Это параметр также блокирует самостоятельно сформированные подписи.|  
  
> [!NOTE]  
>  Рекомендуемое значение для параметра **BlockedSignatureStates** равно 3. Это обеспечивает наибольшую защиту от неподписанных пакетов или подписей, которые являются либо недействительными, либо ненадежными. Однако рекомендованное значение не может подходить для всех случаев. Дополнительные сведения о подписывании электронных ресурсов см. в разделе[Введение в подписывание кода](https://go.microsoft.com/fwlink/?LinkId=51414)библиотеки MSDN.  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>Реализация политики подписи пакетов  
  
1.  В меню **Пуск** выберите команду **Выполнить**.  
  
2.  В диалоговом окне "Выполнить" введите **Regedit**, а затем нажмите кнопку **ОК**.  
  
3.  Найдите раздел реестра HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS.  
  
4.  Щелкните правой кнопкой мыши раздел **MSDTS**, укажите пункт **Создать**, а затем щелкните **Параметр DWORD**.  
  
5.  Обновите имя нового значения до **BlockedSignatureStates**.  
  
6.  Щелкните правой кнопкой мыши параметр **BlockedSignatureStates** и выберите пункт **Изменить**.  
  
7.  В диалоговом окне **Изменение параметра DWORD** введите значение 0, 1, 2 или 3.  
  
8.  Нажмите кнопку **ОК**.  
  
9. В меню **Файл** выберите пункт **Выход**.    

## <a name="cert"></a> Подписание пакета цифровым сертификатом
  Данный раздел описывает подписание пакета служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] цифровым сертификатом. Цифровая подпись может использоваться совместно с другими методами предотвращения загрузки и выполнения недействительного пакета.  
  
 Перед подписанием пакета служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] необходимо выполнить следующие действия.  
  
-   Создайте или получите закрытый ключ для сертификата и сохраните его на локальном компьютере.  
  
-   Получите сертификат для цифрового подписывания от доверенной службы сертификации. Для получения или создания сертификата можно воспользоваться одним из следующих методов.  
  
    -   Получите сертификат от публичной, коммерческой службы выдачи сертификатов.  
  
    -   Получите на сервере сертификации сертификат, позволяющий организации самостоятельно выпускать сертификаты внутреннего использования. Корневой сертификат, используемый для подписания этого сертификата, необходимо добавить в хранилище **Доверенные корневые центры сертификации** . Для добавления корневого сертификата можно воспользоваться оснасткой «Сертификаты» в консоли управления [!INCLUDE[msCoName](../../includes/msconame-md.md)] MMC. Дополнительные сведения см. в разделе «[Службы сертификатов](https://go.microsoft.com/fwlink/?LinkId=100755)» библиотеки MSDN.  
  
    -   Создайте собственный сертификат только в тестовых целях. Средство создания сертификатов (Makecert.exe) порождает сертификаты X.509 для тестовых целей. Дополнительные сведения см. в разделе "[Средство создания сертификатов (Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)" библиотеки MSDN.  
  
     Дополнительные сведения о сертификатах см. в электронной документации по оснастке «Сертификаты». Дополнительные сведения о подписывании цифровых активов см. в разделе «[Подписывание и проверка кода при помощи технологии Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100)» библиотеки MSDN.  
  
-   Убедитесь, что сертификат поддерживает подписание кода. Чтобы определить, поддерживает ли сертификат подписание кода, проверьте свойства сертификата в оснастке «Сертификаты».  
  
-   Сохраните сертификат в персональном хранилище.  
  
 После выполнения описанных выше задач можно подписать пакет, следуя приведенной далее процедуре.  
  
### <a name="to-sign-a-package"></a>Подписывание пакета  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , содержащий подписываемый пакет.  
  
2.  Чтобы открыть пакет, дважды щелкните его в обозревателе решений.  
  
3.  В конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] или в меню **Службы SSIS** нажмите **Цифровая подпись**.  
  
4.  В диалоговом окне **Цифровая подпись** нажмите **Подписать**.  
  
5.  Выберите сертификат в диалоговом окне **Выбор сертификата** .  
  
6.  Чтобы просмотреть сведения о сертификате, нажмите кнопку **Просмотреть сертификат**(необязательно).  
  
7.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Выбор сертификата** .  
  
8.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Цифровая подпись** .  
  
9. Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
     Теперь пакет подписан, но службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] необходимо настроить для проверки наличия и корректности цифровой подписи перед загрузкой пакета.  

## <a name="signing_dialog"></a> Справочник по пользовательскому интерфейсу: диалоговое окно "Цифровая подпись"
  С помощью диалогового окна **Цифровая подпись** можно подписать пакет цифровой подписью или удалить подпись. Диалоговое окно **Цифровая подпись** доступно из параметра **Цифровая подпись** в меню **службы SSIS** в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Дополнительные сведения см. в статье [Подписание пакета цифровым сертификатом](#cert).  
  
### <a name="options"></a>Параметры  
 **Подпись**  
 Щелкните, чтобы открыть диалоговое окно **Выбор сертификата** и выберите необходимый сертификат.  
  
 **Удалить**  
 Щелкните, чтобы удалить цифровую подпись.  

## <a name="see-also"></a>См. также раздел  
 [Пакеты служб Integration Services (SSIS)](../../integration-services/integration-services-ssis-packages.md)   
 [Общие сведения о безопасности (службы Integration Services)](../../integration-services/security/security-overview-integration-services.md)  
  
  
