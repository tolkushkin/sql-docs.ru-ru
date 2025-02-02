---
title: Преобразование "Аудит" | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.audittrans.f1
- sql13.dts.designer.audittransformation.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9161fe71f82d2ca0f2f31805dc07beba387bc28d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726304"
---
# <a name="audit-transformation"></a>преобразование «Аудит»

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Преобразование «Аудит» позволяет включать поток данных в пакет для передачи данных о среде, в которой запускается этот пакет. Например, в поток данных можно добавлять имя пакета, компьютера и оператора. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] предусмотрены системные переменные, предоставляющие эти сведения.  
  
## <a name="system-variables"></a>Системные переменные  
 В приведенной ниже таблице описаны системные переменные, применяемые в преобразовании «Аудит».  
  
|Системная переменная|Индекс |Описание|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|Идентификатор GUID, определяющий экземпляр выполнения пакета.|  
|**PackageID**|1|Уникальный идентификатор пакета.|  
|**PackageName**|2|Имя пакета.|  
|**VersionID**|3|Версия пакета.|  
|**ExecutionStartTime**|4|Время начала выполнения пакета.|  
|**MachineName**|5|имя компьютера.|  
|**UserName**|6|Имя входа пользователя, который запустил пакет.|  
|**TaskName**|7|Имя задачи потока данных, с которой связано преобразование «Аудит».|  
|**TaskId**|8|Уникальный идентификатор задачи потока данных.|  
  
## <a name="configuration-of-the-audit-transformation"></a>Настройка преобразования «Аудит»  
 Чтобы настроить преобразование «Аудит», необходимо добавить имя нового выходного столбца в выход преобразования, затем сопоставить системную переменную с выходным столбцом. Можно сопоставить одну системную переменную с несколькими столбцами.  
  
 Это преобразование имеет один вход и один выход. Вывод ошибок не поддерживается.  
  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами.  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Пользовательские свойства преобразований](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Дополнительные сведения о настройке свойств см. в разделе [Установление свойств компонента потока данных](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="audit-transformation-editor"></a>редактор преобразования «Аудит»
  Преобразование «Аудит» позволяет включать поток данных в пакет для передачи данных о среде, в которой запускается этот пакет. Например, в поток данных можно добавлять имя пакета, компьютера и оператора. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] предусмотрены системные переменные, предоставляющие эти сведения.  
  
### <a name="options"></a>Параметры  
 **Имя выходного столбца**  
 Введите имя для нового выходного столбца, который будет содержать данные аудита.  
  
 **Тип аудита**  
 Выберите доступную системную переменную для предоставления данных аудита.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Идентификатор GUID экземпляра выполнения**|Укажите идентификатор GUID, который уникально идентифицирует экземпляр выполнения пакета.|  
|**Идентификатор пакета**|Укажите идентификатор GUID, который уникально идентифицирует пакет.|  
|**Имя пакета**|Укажите имя пакета.|  
|**Идентификатор версии**|Укажите идентификатор GUID, который уникально идентифицирует версию пакета.|  
|**Время начала выполнения**|Укажите время, когда было начато выполнение пакета.|  
|**Имя компьютера**|Укажите имя компьютера, на котором был запущен пакет.|  
|**User name**|Укажите имя входа пользователя, который запустил пакет.|  
|**Имя задачи**|Укажите имя задачи потока данных, с которой связано преобразование «Аудит».|  
|**Идентификатор задачи**|Укажите идентификатор GUID, который уникально идентифицирует задачу потока данных, с которой связано преобразование «Аудит».|  
  
  
