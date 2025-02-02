---
title: Обнаружение пустого неструктурированного файла в задаче "Скрипт" | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 34462589141133e04ca8728361e3a173f0944f12
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895503"
---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>Обнаружение пустого неструктурированного файла в задаче «Скрипт»
  Источник данных «Неструктурированный файл» не проверяет до начала обработки, содержит ли неструктурированный файл строки данных. Можно повысить эффективность пакета, особенно работающего с многочисленными неструктурированными файлами, если пропускать файлы, не содержащие строки данных. Задача «Скрипт» может проверять, не является ли неструктурированный файл пустым, до начала обработки пакетом потока данных.  
  
> [!NOTE]  
>  Если нужно создать задачу, которую будет удобно использовать в нескольких пакетах, рекомендуется начать разработку пользовательской задачи с этого образца задачи «Скрипт». Дополнительные сведения см. в разделе [Разработка пользовательской задачи](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Описание  
 В следующем примере методы из пространства имен `System.IO` используются для проверки неструктурированного файла, указанного в диспетчере соединений с неструктурированными файлами, чтобы определить, не является ли этот файл пустым и не состоит ли он только из строк, не содержащих данные (например, заголовков столбцов или пустой строки). Сначала скрипт проверяет размер файла; если размер равен нулю, значит, файл пуст. Если размер файла отличен от нуля, скрипт читает строки из файла, пока они не кончатся или пока число строк не превысит ожидаемое число рядов без данных. Если количество строк в файле меньше или равно ожидаемому числу рядов без данных, то файл считается пустым. Результат возвращается как логическое значение в пользовательской переменной и может использоваться для переключения потока управления пакета. `FireInformation` Метод также отображает результат в **вывода** окно [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA).  
  
#### <a name="to-configure-this-script-task-example"></a>Настройка этого образца задачи «Скрипт»  
  
1.  Создание и настройка диспетчера соединения с неструктурированными файлами с именем `EmptyFlatFileTest`.  
  
2.  Создайте переменную целого типа с именем `FFNonDataRows` и присвойте ей в качестве значения количество ожидаемых в неструктурированном файле строк без данных.  
  
3.  Создайте логическую переменную с именем `FFIsEmpty`.  
  
4.  Добавьте переменную `FFNonDataRows` к свойству задачи "Скрипт" **ReadOnlyVariables**.  
  
5.  Добавьте переменную `FFIsEmpty` к свойству задачи "Скрипт" **ReadWriteVariables**.  
  
6.  Импортируйте в код пространство имен `System.IO`.  
  
 При использовании перечислителя с циклом по каждому файлу нужно вместо использования одного диспетчера соединений с неструктурированными файлами изменить приведенный ниже образец код для получения имени и пути файла из переменной, в которой хранится перечисляемая величина, а не из диспетчера соединений.  
  
### <a name="code"></a>Код  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
![Значок служб Integration Services (маленький)](../media/dts-16.gif "значок служб Integration Services (маленький)")**оставаться до даты со службами Integration Services**<br /> Чтобы загрузить новейшую документацию, статьи, образцы и видеоматериалы корпорации Майкрософт, а также лучшие решения участников сообщества, посетите страницу служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] на сайте MSDN:<br /><br /> [Посетите страницу служб Integration Services на сайте MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Чтобы получать автоматические уведомления об этих обновлениях, подпишитесь на RSS-каналы, предлагаемые на этой странице.  
  
## <a name="see-also"></a>См. также  
 [Примеры задачи «Скрипт»](../extending-packages-scripting-task-examples/script-task-examples.md)  
  
  
