---
title: Добавление фрагментов кода Transact-SQL | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 901c7995-8eb5-4d12-8bb0-de0a922b48f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d79989e37483342e5cc1624a0529f9df98ae980
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064291"
---
# <a name="add-transact-sql-snippets"></a>Добавление фрагментов кода Transact-SQL
  В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]можно добавить собственные фрагменты кода Transact-SQL в набор предварительно определенных фрагментов.  
  
## <a name="creating-a-transact-sql-snippet-file"></a>Создание файла фрагмента Transact-SQL  
 Первая часть создания фрагмента кода [!INCLUDE[tsql](../../includes/tsql-md.md)] заключается в создании XML-файла с текстом фрагмента кода. Файл должен иметь расширение SNIPPET и отвечать требованиям [Схемы фрагментов кода](https://go.microsoft.com/fwlink/?LinkId=207504). Укажите SQL в качестве языка фрагмента кода.  
  
 Можно использовать предварительно определенные фрагменты, которые поставляются вместе с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в качестве примеров. Чтобы найти предустановленные фрагменты кода, откройте среду [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], а затем в меню **Сервис** выберите пункт **Диспетчер фрагментов кода**. Выберите **SQL** из списка полей **Язык** , путь к фрагментам [!INCLUDE[tsql](../../includes/tsql-md.md)] отображается в поле **Расположение** .  
  
## <a name="registering-the-code-snippet"></a>Регистрация фрагмента кода  
 После создания файла фрагмента используйте диспетчер фрагментов кода для регистрации фрагмента с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Можно либо добавить папку, содержащую несколько фрагментов, либо импортировать отдельные фрагменты в папку **Мои фрагменты кода** .  
  
## <a name="procedures"></a>Процедуры  
  
#### <a name="adding-a-snippet-folder"></a>Добавление папки фрагментов  
  
1.  Откройте [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Выберите меню **Сервис** и нажмите кнопку **Диспетчер фрагментов кода**.  
  
3.  Нажмите кнопку **Добавить** .  
  
4.  Перейдите к папке, содержащей собственные фрагменты кода, и нажмите кнопку **Выбор папки** .  
  
#### <a name="importing-a-snippet"></a>Импорт фрагмента  
  
1.  Откройте [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Выберите меню **Сервис** и нажмите кнопку **Диспетчер фрагментов кода**.  
  
3.  Нажмите кнопку **Импорт** .  
  
4.  Перейдите к папке, содержащей собственный фрагмент кода, выберите файл с расширением SNIPPET и нажмите кнопку **Открыть** .  
  
## <a name="examples"></a>Примеры  
 В следующем примере создается окружающий блок `TRY-CATCH` для фрагмента кода, который будет импортирован в среду [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
1.  Вставьте следующий код в блокнот, сохраните файл с именем TryCatch.snippet.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CodeSnippets  xmlns="https://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
    <_locDefinition xmlns="urn:locstudio">  
        <_locDefault _loc="locNone" />  
        <_locTag _loc="locData">Title</_locTag>  
        <_locTag _loc="locData">Description</_locTag>  
        <_locTag _loc="locData">Author</_locTag>  
        <_locTag _loc="locData">ToolTip</_locTag>  
       <_locTag _loc="locData">Default</_locTag>  
    </_locDefinition>  
    <CodeSnippet Format="1.0.0">  
    <Header>  
    <Title>TryCatch</Title>  
                            <Shortcut></Shortcut>  
    <Description>Example Snippet for Try-Catch.</Description>  
    <Author>SQL Server Books Online Example</Author>  
    <SnippetTypes>  
                                    <SnippetType>SurroundsWith</SnippetType>  
    </SnippetTypes>  
    </Header>  
    <Snippet>  
    <Declarations>  
                                    <Literal>  
                                    <ID>CatchCode</ID>  
                                    <ToolTip>Code to handle the caught error</ToolTip>  
                                    <Default>CatchCode</Default>  
                                    </Literal>  
    </Declarations>  
    <Code Language="SQL"><![CDATA[  
    BEGIN TRY  
  
    $selected$ $end$  
  
    END TRY  
    BEGIN CATCH  
  
    $CatchCode$  
  
    END CATCH;  
    ]]>  
    </Code>  
    </Snippet>  
    </CodeSnippet>  
    </CodeSnippets>  
    ```  
  
2.  Откройте среду [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
3.  Выберите меню **Сервис** и нажмите кнопку **Диспетчер фрагментов кода**.  
  
4.  Нажмите кнопку **Импорт** .  
  
5.  Перейдите к папке, содержащей файл TryCatch.snippet, щелкните файл TryCatch.snippet и нажмите кнопку **Открыть** . В папке **Мои фрагменты кода** не должно быть фрагмента TryCatch.  
  
## <a name="see-also"></a>См. также  
 [Вставка фрагментов кода окружения Transact-SQL](insert-surround-with-transact-sql-snippets.md)  
  
  
