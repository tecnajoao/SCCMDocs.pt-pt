---
title: "Поддерживаемые конфигурации | Документы Майкрософт"
description: "Ознакомьтесь с основными конфигурациями и требованиями для планирования, развертывания и обслуживания правильно работающей среды System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: aad46e9ab893b9bb3e32d35c17b9678b3a265c99
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>Поддерживаемые конфигурации для System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Локальное решение System Center Configuration Manager использует ваши серверы, клиенты, сетевые конфигурации и дополнительные продукты, такие как Microsoft Intune, SQL Server и Azure.

Информация в этом и последующих разделах необходима для понимания основных конфигураций, требований и ограничений с целью планирования, развертывания и обслуживания правильно работающей среды Configuration Manager.  Эта информация относится к инфраструктуре сайтов, иерархий и управляемых устройств Configuration Manager.

Если функция или возможность Configuration Manager требует более конкретной настройки, соответствующую информацию можно найти в документации по этой функции. Эта информация дополняет общие сведения о конфигурации.  

 Продукты и технологии, описываемые в следующих разделах, поддерживаются в Configuration Manager. Однако их указание здесь не подразумевает расширения поддержки этих продуктов за пределы их индивидуальных жизненных циклов поддержки. Продукты, жизненный цикл поддержки которых уже истек, не поддерживаются в Configuration Manager. Дополнительные сведения о жизненных циклах поддержки Майкрософт см. на веб-сайте [Правила по срокам поддержки продуктов Майкрософт](http://go.microsoft.com/fwlink/p/?LinkId=208270).  

> [!NOTE]  
>  Сведения о политике сроков поддержки продуктов корпорации Майкрософт см. на веб-сайте [Вопросы и ответы о правилах по срокам поддержки продуктов корпорации Майкрософт](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Кроме того, продукты и версии продуктов, которые не указаны в следующих разделах, не поддерживаются в System Center Configuration Manager, если только иное не указано в [блоге рабочей группы по корпоративной мобильности и безопасности](https://blogs.technet.microsoft.com/enterprisemobility/).  Иногда содержимое в этом блоге может обновляться раньше, чем текст данного документа.


-  [Данные по размерам и масштабированию](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Сведения о количестве сайтов, ролей системы сайта на каждый сайт, а также клиентов или устройств, поддерживаемом в различных типах иерархии Configuration Manager.

-  [Предварительные требования к сайтам и системе сайта](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Сведения о конфигурациях, необходимых для поддержки различных типов сайтов и ролей системы сайта на сервере Windows Server.

-  [Поддерживаемые операционные системы для серверов системы сайта](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Узнайте, какие операционные системы можно использовать в качестве сервера сайта или сервера системы сайта.

-  [Поддерживаемые операционные системы для клиентов и устройств](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Узнайте, какими операционными системами можно управлять с помощью Configuration Manager, включая Windows, Windows Embedded, Linux и UNIX, Mac и операционные системы мобильных устройств.

-  [Поддерживаемые операционные системы для консоли](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Узнайте, в каких операционных системах может размещаться консоль Configuration Manager, которая служит точкой доступа для управления развертыванием.  

-  [Поддержка версий SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Сведения о версиях SQL Server, в которых могут размещаться база данных сайта и база данных отчетов, а также об обязательных и необязательных конфигурациях, которые можно использовать.

-  [Параметры высокой доступности](../../../protect/understand/high-availability-options.md)  
Сведения о вариантах, которые можно реализовать при разработке среды, чтобы обеспечить высокий уровень доступности служб для развертывания Configuration Manager.

-  [Рекомендуемое оборудование](../../../core/plan-design/configs/recommended-hardware.md)  
Рекомендации, которые помогут вам определить соответствующее оборудование и конфигурации для размещения сайтов Configuration Manager и основных служб.

-  [Поддержка доменов Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Сведения о поддерживаемых конфигурациях домена Active Directory, которые необходимы для Configuration Manager.

-  [Поддержка функций и сетей Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Сведения о поддерживаемых технологиях Windows (например, BranchCache и дедупликации данных) и ограничениях на их использование с Configuration Manager.

-  [Поддержка сред виртуализации](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Дополнительные сведения о поддерживаемых технологиях виртуальных машин.
