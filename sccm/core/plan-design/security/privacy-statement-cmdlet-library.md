---
title: "Заявление о конфиденциальности System Center Configuration Manager — библиотека командлетов Configuration Manager | Документы Майкрософт"
description: "Узнайте, как корпорация Майкрософт собирает и использует данные, связанные с библиотекой командлетов System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3936075555cc0bb370ea6e42c7e720b864d565f7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Заявление о конфиденциальности System Center Configuration Manager — библиотека командлетов Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

В настоящем заявлении о конфиденциальности описаны функции библиотеки командлетов System Center Configuration Manager.  

## <a name="usage-data"></a>Данные об использовании  
 **Назначение:**   
библиотека командлетов System Center Configuration Manager позволяет управлять иерархией Configuration Manager с помощью командлетов и скриптов Windows PowerShell. Библиотека командлетов собирает сведения об использовании командлетов в библиотеке, чтобы определить тенденции и шаблоны использования. Библиотека командлетов также собирает сведения о типах и количестве ошибок, возникших при использовании командлетов.  

 **Собираемые, обрабатываемые и передаваемые сведения:**   
Собранные данные об использовании включают запуск, остановку и завершение командлетов, запуск нерекомендуемых командлетов и метрики действий для операций поставщика Systems Management Server (SMS), связанного с командлетами. Эти сведения не позволяют установить вашу личность.  Собранные сведения об ошибках содержат ошибки, возвращенные командлетами, и сведения об ошибках для исключений Некоторые подробные отчеты об ошибках могут непреднамеренно содержать отдельные идентификаторы, например серийный номер устройства, подключенного к компьютеру. Библиотека командлетов фильтрует и анонимизирует сведения, содержащиеся в отчетах об ошибках, чтобы удалить отдельные идентификаторы перед их отправкой в Майкрософт.  

 **Использование сведений:**   
мы используем эти сведения для повышения качества, безопасности и целостности предлагаемых продуктов и служб.  

 **Выбор и управление:**   
эта функция данных об использовании включена по умолчанию. Библиотека командлетов System Center Configuration Manager имеет два раздела реестра для управления этой функцией.  

 Чтобы полностью отказаться от участия, необходимо установить эти два значения разделов реестра: один для каждого из поставщиков трассировки событий для Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (отказ от сбора данных об использовании для поставщика драйверов)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (отказ от сбора данных об использовании для командлетов)  

 Изменения параметров сбора данных об использовании зависят от компьютера, на котором они были созданы.  

 Дополнительные сведения о настройке сбора данных об использовании см. в разделе [Документация по библиотеке командлетов System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).   
