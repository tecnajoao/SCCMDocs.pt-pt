---
title: "Просмотр данных диагностики | Документация Майкрософт"
description: "Просмотр данных о диагностике и использовании, чтобы убедиться в отсутствии конфиденциальных сведений в иерархии System Center Configuration Manager."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0932e2b2a4f3e13c35d6b7b0446083f1c233ce03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Как просмотреть данные о диагностике и использовании для System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Вы можете просмотреть данные о диагностике и использовании, полученные из иерархии System Center Configuration Manager, чтобы убедиться в отсутствии конфиденциальных сведений или личных данных. Данные телеметрии обобщаются и хранятся в таблице **TEL_TelemetryResults** базы данных сайта и форматируются для обеспечения более удобной и эффективной программной обработки. Хотя перечисленные ниже параметры позволяют просмотреть фактические данные, отправляемые корпорации Майкрософт, они не предназначены для использования в других целях, таких как анализ данных.  

Следующую команду SQL можно использовать для просмотра содержимого этой таблицы — непосредственно отправляемых данных (можно также экспортировать эти данные в текстовый файл):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  До установки версии 1602 данные телеметрии хранились в таблице **TelemetryResults**.  

Когда точка подключения службы находится в автономном режиме, вы можете применять средство подключения службы для экспорта текущих данных о диагностике и использовании в файл с разделителями-запятыми (CSV). Запустите средство подключения службы в точке подключения службы с параметром **-Export**.  

##  <a name="bkmk_hashes"></a> Односторонние хэши  
Некоторые данные состоят из строк случайных буквенно-цифровых символов. Configuration Manager использует алгоритм SHA-256, предусматривающий применение односторонних хэшей, чтобы в собираемые данные не попала потенциально конфиденциальная информация. При этом данные остаются в таком состоянии, которое допускает их использование для корреляции и сравнения. Например, вместо сбора имен таблиц в базе данных сайта для каждого из них записывается односторонний хэш. Благодаря этому любые настраиваемые имена таблиц, созданные вами, или надстройки продуктов сторонних производителей не отображаются. После этого мы можем получить такой же односторонний хэш для имен таблиц SQL, поставляемых по умолчанию в составе продукта, и сравнить результаты двух запросов для определения отклонения вашей схемы базы данных от продукта по умолчанию. Затем эти сведения используются для улучшения обновлений, требующих внесения изменений в схему SQL.  

При просмотре необработанных данных в каждой строке данных будет отображаться общее хэшированное значение. Это идентификатор иерархии. Это хэшированное значение используется, чтобы обеспечить связь данных с соответствующей иерархией, не идентифицируя клиент или источник.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Как увидеть действие одностороннего хэша  

1.  Получите идентификатор иерархии, выполнив в SQL Management Studio для базы данных Configuration Manager следующую инструкцию SQL: **select [dbo].[fnGetHierarchyID]\(\)**.  

2.  Используйте приведенный ниже скрипт Windows PowerShell для одностороннего хэширования идентификатора GUID, полученного из базы данных. После этого можно сравнить полученное значение с идентификатором иерархии в необработанных данных, чтобы посмотреть, как скрыты эти данные.  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  
