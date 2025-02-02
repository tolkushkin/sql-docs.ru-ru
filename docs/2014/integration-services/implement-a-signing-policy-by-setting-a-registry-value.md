---
title: Реализация политики подписывания путем задания параметра реестра | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing policies [Integration Services]
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 21bda8729c30df9493c4f969c5af05b6dd80386f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058219"
---
# <a name="implement-a-signing-policy-by-setting-a-registry-value"></a>Реализация политики подписывания путем задания параметра реестра
  Для управления организационной политикой при загрузке подписанных и неподписанных пакетов можно использовать необязательный параметр реестра. При использовании данного параметра реестра его необходимо создать на каждом компьютере, где будут выполняться пакеты [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] и где требуется принудительное выполнение этой политики. После задания такого параметра реестра службы [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] будут проверять наличие и верность подписи перед загрузкой пакетов.  
  
 Процедура, описанная в этом разделе, позволяет добавить необязательный параметр `BlockedSignatureStates` типа DWORD в раздел реестра «HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS». Значение данных в `BlockedSignatureStates` определяет, должен ли пакет быть заблокирован, если у него ненадежная подпись, недопустимая подпись или он вообще не подписан. Что касается состояния подписей, используемых для пакетов, то в значении реестра `BlockedSignatureStates` используются следующие определения:  
  
-   *Действительная подпись* — это подпись, которая может быть успешно прочитана.  
  
-   *Недействительная подпись* — это подпись, для которой расшифрованная контрольная сумма (односторонний хэш-код пакета, зашифрованного закрытым ключом), не соответствует расшифрованной контрольной сумме, вычисленной в процессе загрузки пакетов служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
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
>  Рекомендованное значение для `BlockedSignatureStates` — 3. Это обеспечивает наибольшую защиту от неподписанных пакетов или подписей, которые являются либо недействительными, либо ненадежными. Однако рекомендованное значение не может подходить для всех случаев. Дополнительные сведения о подписывании электронных ресурсов см. в разделе[Введение в подписывание кода](https://go.microsoft.com/fwlink/?LinkId=51414)библиотеки MSDN.  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>Реализация политики подписи пакетов  
  
1.  В меню **Пуск** выберите команду **Выполнить**.  
  
2.  В диалоговом окне выполнения введите `Regedit`, а затем нажмите кнопку **ОК**.  
  
3.  Найдите раздел реестра HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS.  
  
4.  Щелкните правой кнопкой мыши раздел **MSDTS**, укажите пункт **Создать**, а затем щелкните **Параметр DWORD**.  
  
5.  Обновите имя нового значения до `BlockedSignatureStates`.  
  
6.  Щелкните правой кнопкой мыши `BlockedSignatureStates` и нажмите кнопку **изменить**.  
  
7.  В диалоговом окне **Изменение параметра DWORD** введите значение 0, 1, 2 или 3.  
  
8.  Нажмите кнопку **ОК**.  
  
9. В меню **Файл** выберите пункт **Выход**.  
  
## <a name="see-also"></a>См. также  
 [Общие сведения о безопасности (службы Integration Services)](security/security-overview-integration-services.md)   
 [Определение источника пакетов с помощью цифровых подписей](security/identify-the-source-of-packages-with-digital-signatures.md)  
  
  
