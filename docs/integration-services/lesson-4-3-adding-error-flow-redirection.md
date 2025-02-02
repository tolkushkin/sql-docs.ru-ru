---
title: Шаг 3. Добавление перенаправления потока ошибок | Документация Майкрософт
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ae385bd59de5f282ce383c6f819c6b5feb6521e6
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2019
ms.locfileid: "65721798"
---
# <a name="lesson-4-3-add-error-flow-redirection"></a>Занятие 4-3. Добавление перенаправления потока ошибок

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



В предыдущей задаче преобразование "Поиск ключа валюты" при попытке обработки поврежденного образца неструктурированного файла не может сформировать соответствие, из-за чего выдается ошибка. Поскольку преобразование использует установки по умолчанию для вывода ошибки, любая возникшая ошибка приводит к неудачному завершению преобразования. При неудачном завершении преобразования выполнение пакета также завершается с ошибкой.  
  
Чтобы предотвратить завершение преобразования с ошибкой, можно настроить вывод ошибок в этом компоненте таким образом, чтобы строка с ошибкой перенаправлялась на другой путь обработки. Использование отдельного пути обработки ошибок предоставляет дополнительные возможности. Например, можно очистить данные, а затем заново обработать строку с ошибкой. Кроме того, можно сохранить строку с ошибкой вместе со сведениями об ошибке для последующей проверки и повторной обработки.  
  
В этой задаче вы настраиваете преобразование "Поиск ключа валюты" так, чтобы все строки с ошибками перенаправлялись на вывод ошибок. В ветке ошибок потока данных [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] записывают эти строки в файл.  
  
По умолчанию два дополнительных столбца в выводе ошибок служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], **ErrorCode** и **ErrorColumn**, содержат только числовой код ошибки и идентификатор столбца, в котором возникла ошибка. В этой задаче перед тем, как пакет запишет строки с ошибками в файл, следует с помощью компонента скрипта получить доступ к API-интерфейсу служб [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] и извлечь описание ошибки.  
  
## <a name="configure-an-error-output"></a>Настройка вывода ошибок  
  
1.  В окне **Область элементов SSIS**разверните узел **Общие**и перетащите элемент **Компонент скрипта** в область конструктора на вкладке **Поток данных** . Поместите **Скрипт** справа от преобразования **Поиск ключа валюты** .  
  
2.  В диалоговом окне **Выбор типа компонента скрипта** выберите **Преобразование** и нажмите кнопку **ОК**.  
  
3.  Чтобы соединить эти два компонента, щелкните преобразование **Поиск ключа валюты** и перетащите его красную стрелку на вновь созданное преобразование **Скрипт**.  
  
    Красная стрелка отображает вывод ошибок преобразования **Поиск ключа валюты** . Используя красную стрелку для подключения преобразования к компоненту скрипта, можно перенаправить любые ошибки обработки в компонент скрипта, который обрабатывает их и отправляет по назначению.  
  
4.  В диалоговом окне **Настройка вывода ошибок** в столбце **Ошибка** выберите **Перенаправить строку**и нажмите кнопку **ОК**.  
  
5.  В области конструктора **Поток данных** щелкните имя **Компонент скрипта** в только что добавленном преобразовании **ScriptComponent** и измените это имя на **Получение описания ошибки**.  
  
6.  Дважды щелкните преобразование **Получение описания ошибки** .  
  
7.  В диалоговом окне **Редактор преобразования «Скрипт»** на странице **Входные столбцы** выберите столбец **ErrorCode** .  
  
8.  На странице **Входы и выходы** разверните **Выход 0**, выберите **Выходные столбцы** и нажмите кнопку **Добавить столбец**.  
  
9. Для свойства **Name** введите *ErrorDescription* и задайте для свойства **DataType** значение **Unicode string [DT_WSTR]**.  
  
10. На странице **Скрипт** убедитесь в том, что свойство **LocaleID** имеет значение **Английский (США)**.
  
11. Нажмите кнопку **Изменить скрипт**, чтобы открыть среду [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA). В методе **Input0_ProcessInputRow** введите или вставьте следующий код:  
  
    [Visual Basic]  
  
    ```vb  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
    [Visual C#]  
  
    ```cs
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
    Готовая подпрограмма должна выглядеть так:  
  
    [Visual Basic]  
  
    ```vb
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
    [Visual C#]  
  
    ```cs
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. В меню **Сборка** выберите команду **Построить решение**, чтобы создать скрипт и сохранить изменения, а затем закройте средства VSTA.  
  
13. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Редактор преобразования "Скрипт"**.  
  
## <a name="go-to-next-task"></a>Перейти к следующему шагу
[Шаг 4. Добавление назначения "Неструктурированный файл"](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
  
  
