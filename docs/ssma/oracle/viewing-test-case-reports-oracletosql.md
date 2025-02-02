---
title: Просмотр отчетов о тестовых случаях (OracleToSQL) | Документация Майкрософт
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2d40fd986c68968680bcd39821d762101723b87b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283637"
---
# <a name="viewing-test-case-reports-oracletosql"></a>Просмотр отчетов о тестовых случаях (OracleToSQL)
В отчете тестовый случай отображаются результаты проверки и тестирования, общие сведения. В случае сбоя теста сведения о любой несоответствующие данные в объектах проверенных также отображается.  
  
## <a name="report-structure"></a>Структура отчета  
В верхней части отчета показывают эти статистические данные:  
  
-   Общее число проверенных объекты и число объектов, для которых проверка будет выполнена успешно.  
  
-   Общее число проверенных таблиц и внешние ключи и число таблиц и внешние ключи, которые успешно совпадают.  
  
-   Время начала, время окончания тестового случая и общее время, необходимое для выполнения.  
  
В остальной части отчета показаны сведения в четырех категориях:  
  
**Необходимые условия ошибки**  
Отображаются все ошибки, которые произошли на **шаг предварительные требования.** Как правило он пропускается.  
  
**Инициализация**  
Показывает состояние выполнения как **успех** или **сбоя**.  
  
**Объекты результатов теста**  
Сравнение результаты (успех или сбой), а также несоответствия SSMA тест-инженер, обнаруженных в случае сбоя.  
  
**Финализация**  
Показывает состояние выполнения как **успех** или **сбоя**.  
  
## <a name="see-also"></a>См. также  
[Выполнение тестовых случаев &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Тестирование объектов базы данных после миграции &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
