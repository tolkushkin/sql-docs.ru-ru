---
title: srv_paramsetoutput (интерфейс API расширенных хранимых процедур) | Документы Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramsetoutput
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 26dd8add089f27c3ea9db22204548196bc887faf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127138"
---
# <a name="srvparamsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (API-интерфейс расширенных хранимых процедур)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Используйте вместо этого интеграцию со средой CLR.  
  
 Устанавливает значение возвращаемого параметра. Эта функция заменяет функцию **srv_paramset**.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
```  
  
## <a name="arguments"></a>Аргументы  
 *srvproc*  
 Является дескриптором клиентского соединения.  
  
 *n*  
 Является порядковым номером параметра, который должен быть установлен. Первый параметр имеет значение 1.  
  
 *pbData*  
 Является указателем на значение данных, которое должно быть отправлено обратно клиенту как возвращаемый параметр процедуры.  
  
 *cbLen*  
 Является фактической длиной данных, которые должны быть возвращены. Если тип данных параметра указывает значения постоянной длины и не допускает значений NULL (например, *srvbit* или *srvint1*), аргумент*cbLen* не учитывается. Значение, равное 0, указывает на данные нулевой длины, если значение *fNull* равно FALSE.  
  
 *fNull*  
 Является флагом, показывающим, равно ли NULL значение возвращаемого параметра. Установите этот флаг в значение TRUE, если параметр должен быть установлен в значение NULL. Значение по умолчанию — FALSE. Если *fNull* установлен в значение TRUE, то аргумент *cbLen* должен быть установлен в значение 0, иначе функция завершится с ошибкой.  
  
## <a name="returns"></a>Возвращает  
 Если сведения о параметре были успешно установлены, возвращается значение SUCCEED, в противном случае — FAIL. Значение FAIL возвращается, если:  
  
-   параметр не является возвращаемым параметром, или  
  
-   аргумент *cbLen* недопустим.  
  
## <a name="remarks"></a>Примечания  
 **Примечание по безопасности.** Необходимо тщательно просмотреть исходный код расширенных хранимых процедур и проверить скомпилированные DLL-библиотеки перед их установкой на рабочий сервер. Сведения о проверке безопасности см. на следующем [веб-сайте Майкрософт](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
  
