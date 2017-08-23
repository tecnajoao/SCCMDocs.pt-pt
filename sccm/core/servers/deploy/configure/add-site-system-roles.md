---
title: "Добавление ролей системы сайта | Документы Майкрософт"
description: "Сведения о ролях системы сайта Configuration Manager и их добавлении для расширения функциональных возможностей и емкости сайта."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1ad4abf1f06ed24bd1d505648280b5e5d80220c7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>Добавление ролей системы сайта для System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Каждый сайт System Center Configuration Manager поддерживает несколько ролей системы сайта. Каждая роль расширяет функциональность и возможности вашего сайта по предоставлению служб, а также управлению устройствами и пользователями. Каждая роль системы сайта на сервере системы сайта должна быть с того же сайта.   

В Configuration Manager не поддерживается установка ролей нескольких сайтов на одном сервере системы сайта.  

> [!TIP]  
>  Если вы не знакомы с основами использования ролей системы сайта или не знаете различия между сервером сайта, серверами системы сайта и ролями системы сайта, см. раздел [Основные сведения о System Center Configuration Manager](../../../../core/understand/fundamentals.md).  

 В следующих разделах подробно описаны процедуры и приведены дополнительные сведения для установки ролей системы сайта.  

-   [Установка ролей системы сайта для System Center Configuration Manager](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     Этот раздел содержит основные рекомендации по работе с двумя мастерами в консоли, которые можно использовать для установки новых ролей системы сайта.  

-   [Установка облачных точек распространения в Microsoft Azure для System Center Configuration Manager](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    Если вы хотите использовать Microsoft Azure, чтобы разместить содержимое для развертывания на клиентах, информация в этом разделе поможет вам настроить необходимые файлы сертификатов, чтобы позволить Configuration Manager обмениваться данными с вашей подпиской Microsoft Azure и использовать ее. Кроме того, понадобится настроить разрешение имен, чтобы клиенты могли находить облачные точки распространения.  

-   [Установка ролей системы сайта для локального управления мобильными устройствами в System Center Configuration Manager](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Этот раздел поможет вам успешно настроить роли системы сайта, чтобы обеспечить управление современными устройствами с помощью локального управления мобильными устройствами Configuration Manager.  

-   [Параметры конфигурации для ролей системы сайта для System Center Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Некоторые роли системы сайта поддерживают конфигурации, которые требуют больше информации, чем может быть описано в пользовательском интерфейсе. Эта информация представлена в данном разделе.  
