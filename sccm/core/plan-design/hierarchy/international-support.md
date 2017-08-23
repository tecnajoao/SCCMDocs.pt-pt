---
title: "Международная поддержка | Документы Майкрософт"
description: "Настройка System Center Configuration Manager в соответствии с определенными международными требованиями."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3bab51be96445f766e8f5bbf54eee854e5d09cee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="international-support-in-system-center-configuration-manager"></a>Международная поддержка в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

В следующих разделах приводятся технические сведения, помогающие привести System Center Configuration Manager в соответствие с определенными международными требованиями.  

## <a name="gb18030-requirements"></a>Требования GB18030  
 Configuration Manager отвечает стандартам, установленным в GB18030, поэтому Configuration Manager можно использовать в Китае. Для соответствия требованиям GB18030 при развертывании Configuration Manager должны использоваться следующие конфигурации.  

-   На каждом компьютере сервера сайта и компьютере с SQL Server, используемом с Configuration Manager, должна быть установлена операционная система на китайском языке.  

-   В базе данных каждого сайта и в каждом экземпляре SQL Server в иерархии должна использоваться одна и та же сортировка, а именно:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Такие параметры сортировки являются исключением из требований, описанных в статье [Поддержка версий SQL Server в System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Необходимо разместить файл с именем **GB18030.SMS** в корневой папке системного тома на каждом компьютере сервера сайта в иерархии. Этот файл не содержит данных и может представлять собой пустой текстовый файл с именем, соответствующим данному требованию.  
