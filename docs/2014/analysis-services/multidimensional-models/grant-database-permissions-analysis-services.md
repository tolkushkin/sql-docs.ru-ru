---
title: Предоставление разрешений базы данных (службы Analysis Services) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 335fe6deeb3d89483f5f5adb040b0788891053cd
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074950"
---
# <a name="grant-database-permissions-analysis-services"></a>Предоставление разрешений базы данных (службы Analysis Services)
  Если вы подходите к администрированию базы данных службы Analysis Services с квалификацией в смежных базах данных, первое, что вам необходимо понять, с точки зрения доступа к данным, это то, что база данных не является первичным защищаемым объектом службы Analysis Services.  
  
 Первичной структурой запроса в службе Analysis Services является куб (или табличная модель), с пользовательскими разрешениями, установленными на эти отдельные объекты. В отличие от родственного ядра СУБД ─ в котором имена для входа и разрешения пользователя (часто `db_datareader`) установлены на саму базу данных ─ база данных службы Analysis Services в большинстве случаев является контейнером для основных объектов запроса в модели данных. Если вашей ближайшей целью является активация доступа к данным для куба или табличной модели, можете сейчас пропустить разрешения базы данных и перейти прямо к этой статьи: [Предоставление разрешений кубу или модели &#40;служб Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md).  
  
 Разрешения базы данных в службе Analysis Services активируют функции управления; в общих чертах, как и регистр разрешения базы данных Полный Доступ или более детализированные, если вы делегируете операции обработки. Уровни разрешений для базы данных службы Analysis Services указаны на вкладке **Общие** диалогового окна **Создать Роль** показанного на следующей иллюстрации и описанного ниже.  
  
 В службе Analysis Services нет имен для входа. Вы просто создаете роли и назначаете учетные записи Windows на вкладке **Членство** . Все пользователи, включая администраторов, подключаются к службе Analysis Services используя учетную запись Windows.  
  
 ![Создание роли разрешения базы данных Отображение диалогового окна](../media/ssas-permsdbrole.png "Создание роли разрешения базы данных Отображение диалогового окна")  
  
 Существует три типа разрешений, определенных на уровне базы данных.  
  
 **Полный доступ (Администратор)** — это наиболее широкое разрешение, предоставляющее все возможности работы с базой данных Analysis Services, например, возможность запрашивать или обрабатывать любые объекты в базе данных, управлять безопасностью ролей. Разрешение Полный Доступ идентично статусу администратора базы данных. Когда вы выбираете `Full Control`, разрешения `Process Database` и `Read Definition` также выбираются и не могут быть удалены.  
  
> [!NOTE]  
>  Администраторы сервера (элементы роли Администратора Сервера) также обладают безоговорочным Полным Доступом к каждой базе данных на сервере.  
  
 `Process Database` ─ Это разрешение используется для делегирования обработки на уровне базы данных. В качестве администратора вы можете разгрузить данное задание, создав роль, которая позволяет другому лицу или службе запускать операции обработки в отношении любого объекта в базе данных. Вы также можете создать роль, которая активирует обработку на определенных объектах. Дополнительные сведения см. в разделе [Предоставление разрешений на обработку (службы Analysis Services)](grant-process-permissions-analysis-services.md) .  
  
 `Read Definition` ─ Это разрешение предоставляет возможность читать метаданные объекта, но не просматривать связанные данные. Обычно данное разрешение используется в ролях, созданных для выделенной обработки, с добавлением возможности использовать такие средства, как [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] или [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] для интерактивной обработки базы данных. Без разрешения `Read Definition`, разрешение `Process Database` эффективно только в автоматических сценариях. Если вы планируете автоматизировать процесс обработки, например, посредством службы SSIS или другого планировщика, вы, возможно, захотите создать роль, которая обладает разрешением `Process Database` без разрешения `Read Definition`. С другой стороны, соединение двух свойств вместе в одной и той же роли для поддержки и автоматической и интерактивной обработки через средства SQL Server, которые визуализируют модель данных в пользовательском интерфейсе.  
  
## <a name="full-control-administrator-permissions"></a>Разрешения Полного Доступа (Администратора)  
 В службе [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], администратором базы данных является любое удостоверение пользователя Windows, назначенное на роль, которая включает разрешения Полного Доступа (Администратора). Администратор базы данных может выполнять любое задание в рамках базы данных, включая:  
  
-   Обработка объектов  
  
-   Чтение данных и метаданных для всех объектов в базе данных, включая кубы, измерения, группы мер, перспективы и интеллектуальный анализ данных  
  
-   Создание или изменение ролей базы данных посредством добавления пользователей или разрешений, включая добавление пользователей ролям, которые также имеют разрешения Полного Доступа  
  
-   Удаление ролей базы данных или членства роли  
  
-   Регистрация сборок (или сохраненных процедур) для базы данных  
  
 Обратите внимание на то, что администратор базы данных не может добавлять или удалять базы данных на сервере или предоставлять права администратора другим базам данных на одном и том же сервере. Данная привилегия принадлежит только администраторам сервера. См. в разделе [предоставление разрешений администратора сервера &#40;служб Analysis Services&#41; ](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) Дополнительные сведения об этом уровне разрешений.  
  
 Так как все роли определяются пользователем, мы рекомендуем вам создать роль, предназначенную для данной цели (например, роль с названием "dbadmin"), а затем соответственно назначить учетные записи пользователя или группы Windows.  
  
#### <a name="create-roles-in-ssms"></a>Создание ролей в службе SSMS  
  
1.  В [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]подключитесь к экземпляру [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], откройте папку **Базы данных** , выберите базу данных и щелкните правой кнопкой мыши **Роли** | **Создать роль**.  
  
2.  На вкладке **Общие** введите название, например DBAdmin.  
  
3.  Выберите флажок **Полный доступ (Администратор)** для куба. Обратите внимание на то, что разрешение `Process Database` и разрешение `Read Definition` выбираются автоматически. Оба данных разрешения всегда включены в роли, которые содержат `Full Control`.  
  
4.  На вкладке **Членство** , введите учетные записи пользователя Windows и группы, которые подключаются к Analysis Services, используя данную роль.  
  
5.  Нажмите **ОК** для завершения процесса создания роли.  
  
## <a name="process-database"></a>Process Database  
 При определении роли, которая предоставляет разрешения базы данных, вы можете пропустить `Full Control` и выбрать только `Process Database`. Данное разрешение, установленное на уровне базы данных, позволяет обрабатывать все объекты в рамках базы данных. Дополнительные сведения см. в разделе [Grant process permissions &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
## <a name="read-definition"></a>Read Definition  
 Как и `Process Database`, задание `Read Definition` разрешения на уровне базы данных обладает последовательным воздействием на другие объекты в базе данных. Если вы хотите установить разрешения Чтение Описания на более детализированном уровне, вы должны удалить Чтение Описания в качестве свойства базы данных на вкладке Общие. Дополнительные сведения см. в разделе [Предоставление разрешений на чтение описания метаданным объекта (службы Analysis Services)](grant-read-definition-permissions-on-object-metadata-analysis-services.md).  
  
## <a name="see-also"></a>См. также  
 [Предоставление разрешений администратора сервера &#40;служб Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Предоставление разрешений на обработку (службы Analysis Services)](grant-process-permissions-analysis-services.md)  
  
  
