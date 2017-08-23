---
title: "Гибридное управление мобильными устройствами (MDM) с помощью Configuration Manager и Microsoft Intune | Документы Майкрософт"
description: "Сведения о гибридном управлении мобильными устройствами (MDM) с помощью System Center Configuration Manager и Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: "34"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e54478a03807c939ffa64ff39a21ef6f9ea4ae2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Гибридное управление мобильными устройствами (MDM) с помощью System Center Configuration Manager и Microsoft Intune

*Применимо к: System Center Configuration Manager (Current Branch)*


Вы можете управлять устройствами iOS, Windows и Android с помощью Configuration Manager и Microsoft Intune. Все задачи управления выполняются из консоли Configuration Manager, причем они легко интегрируются с веб-службой Microsoft Intune через Интернет.  С помощью Configuration Manager можно предоставлять пользователям безопасный, управляемый доступ к ресурсам компании с устройств. Возможности управления устройствами позволяют защитить данные компании, при этом разрешив пользователям регистрировать свои личные или корпоративные устройства для доступа к этим данным. Возможности управления на устройствах:

-   Снятие устройств с учета и их очистка
-   Настройка параметров соответствия, например паролей, безопасности, роуминга, шифрования и беспроводной связи
-   Развертывание бизнес-приложений на устройствах
-   Развертывание приложений на устройствах, которые подключаются к Магазину Windows, Магазину Windows Phone, App Store или Google Play
-   Сбор данных инвентаризации оборудования
-   Сбор данных инвентаризации программного обеспечения с помощью встроенных отчетов.

Сведения о новых возможностях, доступных для гибридного управления мобильными устройствами, см. в разделе [Новые возможности гибридного управления мобильными устройствами](../understand/whats-new-in-hybrid-mobile-device-management.md).

В этом документе предполагается, что вы используете Configuration Manager для управления компьютерами и заинтересованы в расширении возможностей консоли Configuration Manager с помощью Intune для управления мобильными устройствами. Сведения о различиях между Intune и гибридным управлением мобильными устройствами см. в разделе [Выбор между автономной версией Microsoft Intune и гибридным управлением мобильными устройствами с помощью System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

После расширения Configuration Manager с помощью Intune вы можете регистрировать корпоративные устройства и управлять ими либо разрешить пользователям регистрировать свои личные устройства. Управлять корпоративными устройствами также можно с помощью Intune и Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Регистрация для гибридного управления мобильными устройствами
Чтобы обеспечить гибридное управление устройствами, их необходимо зарегистрировать в службе. Способ регистрации устройства зависит от его типа, принадлежности и требуемого уровня контроля.
- Регистрация "Принеси свое устройство" (BYOD) позволяет пользователям регистрировать свои личные телефоны, планшеты и компьютеры.
- Регистрация корпоративных устройств обеспечивает такие возможности управления, как удаленная очистка, совместное использование устройств и сопоставление пользователей с устройством.
- Если вы используете локальную или размещенную в облаке службу [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager), то можете включить простое управление с помощью Intune без регистрации. Компьютерами с ОС Windows также можно управлять с помощью [клиентского ПО Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
