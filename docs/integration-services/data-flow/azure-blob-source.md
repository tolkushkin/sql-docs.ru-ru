---
title: Источник BLOB-объекта Azure | Документы Майкрософт
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobsrc.f1
- sql14.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d0dd556e17d50e66a0d74805fd754318f5226ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727191"
---
# <a name="azure-blob-source"></a>Компонент Azure Blob Source

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Компонент **Azure Blob Source** позволяет пакету служб SSIS считывать данные из большого двоичного объекта Azure. Поддерживаемые форматы файлов: CSV и AVRO.
  
  Чтобы отобразить редактор источников больших двоичных объектов Azure, перетащите компонент **Azure Blob Source** в конструктор потока данных и дважды щелкните его, чтобы открыть редактор.  
  
 Компонент **Источник BLOB-объекта Azure** входит в состав [пакета дополнительных компонентов SQL Server Integration Services (SSIS) для Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
1.  В поле **Диспетчер подключений службы хранилища Azure** укажите существующий диспетчер подключений службы хранилища Azure или создайте новый, который ссылается на учетную запись хранения Azure.  
  
2.  В поле **Имя контейнера больших двоичных объектов** укажите имя контейнера больших двоичных объектов, который содержит исходные файлы.  
  
3.  В поле **Имя большого двоичного объекта** укажите путь к большому двоичному объекту.  
  
4.  В поле **Формат файла большого двоичного объекта** укажите требуемый формат: **Text** или **Avro**.  
  
5.  Если формат файла — **Text**, необходимо указать значение **символа разделителя столбцов**. (Многосимвольные разделители не поддерживаются.)

    Также выберите **Имена столбцов в первой строке данных** , если первая строка файла содержит имена столбцов.

6.  Если файл сжат, выберите **Распаковать файл**.

7.  Если файл сжат, выберите для параметра **Тип сжатия** значение **GZIP**, **DEFLATE** или **BZIP2**. Учтите, что формат ZIP не поддерживается.
  
8.  Указав сведения о соединении, переключитесь на страницу **Столбцы**, чтобы сопоставить столбцы источника со столбцами назначения для потока данных служб SSI.  
  
  
