---
title: "Функции и возможности | Документы Майкрософт"
description: "Описание основных возможностей управления в System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4691f43dccdf73936107f4635321897b9779bead
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Функции и возможности в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Ознакомьтесь с основными возможностями управления в System Center Configuration Manager. Каждая возможность предусматривает собственные необходимые условия, а возможности, которые будут вами использоваться, могут повлиять на проектирование и реализацию иерархии Configuration Manager. Например, если требуется выполнить развертывание программного обеспечения на устройствах в вашей иерархии, необходимо установить роль системы сайта "точка распространения".  

 Дополнительные сведения о том, как планировать и устанавливать Configuration Manager для поддержки этих возможностей управления в вашей среде, см. в статье [Подготовка к использованию System Center Configuration Manager](../../../core/plan-design/get-ready.md).  

 **Управление приложениями**  

 Предоставляет набор средств и ресурсов, упрощающих создание, развертывание, отслеживание приложений и управление ими на обширном спектре обслуживаемых устройств. Кроме того, Configuration Manager предоставляет средства, помогающие защитить данные компании в приложениях пользователей. См. статью [Введение в управление приложениями](/sccm/apps/understand/introduction-to-application-management).

 **Доступ к ресурсам компании**  

 Обеспечивает набор средств и ресурсов, которые позволяют предоставлять пользователям в организации доступ к данным и приложениям из удаленных расположений. К этим средствам относятся профили Wi-Fi, профили VPN, профили сертификатов и условный доступ к Exchange и SharePoint Online. См. статьи [Защита данных и инфраструктуры сайтов с помощью System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) и [Управление доступом к службам в System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md).  

 **Параметры соответствия**  

 Представляет собой набор средств и ресурсов, которые помогают оценивать, отслеживать и исправлять несоответствие конфигураций клиентских компьютеров в организации. Кроме того, можно использовать параметры соответствия для настройки различных компонентов и параметров безопасности на управляемых устройствах. См. статью [Обеспечение соответствия устройств с помощью System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

 **Endpoint Protection**  

 Обеспечивает безопасность, защиту от вредоносных программ и управление брандмауэром Windows для компьютеров предприятия. См. статью [Endpoint Protection в System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Инвентаризация**  

 Предоставляет набор средств, упрощающих идентификацию и отслеживание активов.  

-   **Инвентаризация оборудования.**Осуществляет сбор подробных сведений об оборудовании устройств на предприятии. См. статью [Общие сведения об инвентаризации оборудования в System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

-   **Инвентаризация ПО.**Осуществляет сбор сведений о файлах, находящихся на клиентских компьютерах организации, и предоставляет соответствующие отчеты. См. статью [Общие сведения об инвентаризации программного обеспечения в System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md).  

-   **Аналитика ресурсов-контейнеров.**Предоставляет средства для сбора данных инвентаризации и отслеживания использования лицензий на ПО в организации. См. статью [Общие сведения об аналитике активов в System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

**Управление мобильными устройствами с помощью Microsoft Intune**  

 Вы можете использовать Configuration Manager для управления устройствами iOS, Android (включая Samsung KNOX Standard), Windows Phone и Windows с помощью службы Microsoft Intune через Интернет.

 Несмотря на использование службы Intune, задачи по управлению выполняются с помощью роли системы сайта подключения службы, доступной на консоли Configuration Manager. См. статью [Гибридное управление мобильными устройствами (MDM) с помощью System Center Configuration Manager и Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

 **Локальное управление мобильными устройствами**  

 Регистрирует компьютеры и мобильные устройства и управляет ими с помощью локальной инфраструктуры Configuration Manager и функций, встроенных в платформы устройств (не полагаясь на отдельно устанавливаемый клиент Configuration Manager). В настоящее время поддерживает управление устройствами Windows 10 Корпоративная и Windows 10 Mobile. См. статью [Управление мобильными устройствами с помощью локальной инфраструктуры в System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Развертывание операционной системы**  

 Предоставляет средство для создания образов операционных систем. Такие образы можно применять для развертывания операционных систем на компьютерах с использованием загрузки PXE или загрузочных носителей, например набора компакт-дисков, DVD-дисков или USB-накопителей. Обратите внимание на то, что это относится как к компьютерам под управлением Configuration Manager, так и к неуправляемым компьютерам. См. статью [Общие сведения о развертывании операционной системы в System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md).  

 **Управление питанием**  

 Предоставляет инструменты и ресурсы для мониторинга и управления энергопотреблением клиентских компьютеров в организации. См. статью [Общие сведения об управлении питанием в System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md).  

 **Запросы**  

 Представляет собой средство для получения сведений о ресурсах в иерархии, а также информации о данных инвентаризации и сообщениях о состоянии. Эти сведения можно использовать для составления отчетов, а также для определения коллекций устройств или пользователей с целью развертывания программного обеспечения и настройки параметров конфигурации. См. статью [Общие сведения о запросах в System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md).  

 **Профили удаленного подключения**  

 Обеспечивают набор средств и ресурсов, которые позволяют создавать, развертывать и отслеживать параметры удаленных подключений на устройствах в организации. Развертывание этих параметров упрощает подключение пользователей к их компьютерам в корпоративной сети. См. статью [Работа с профилями удаленного подключения в System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

 **Элементы конфигурации данных и профилей пользователя**  

 Элементы конфигурации данных и профилей пользователя в Configuration Manager содержат параметры, управляющие перенаправлением папок, автономными файлами и перемещаемыми профилями на компьютерах с Windows 8 и более поздней версии для пользователей вашей иерархии. См. статью [Работа с элементами конфигурации данных и профилей пользователя в System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

 **Удаленное управление**  

 Предоставляет средства для удаленного администрирования клиентских компьютеров из консоли Configuration Manager. См. статью [Общие сведения об удаленном управлении в System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md).  

 **Отчеты**  

 Включает набор средств и ресурсов, которые позволяют использовать функции расширенных отчетов SQL Server Reporting Services из консоли Configuration Manager. См. статью [Общие сведения о ведении отчетов в System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md).  

 **Контроль за использованием программного обеспечения**  

 Предоставляет средства мониторинга и сбора данных об использовании программного обеспечения на клиентах Configuration Manager. См. статью [Отслеживание применения приложений с помощью функции контроля использования программных продуктов в System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Обновления программного обеспечения**  

 Предоставляет набор средств и ресурсов, обеспечивающих управление обновлениями, их развертывание и отслеживание на предприятии. См. статью [Общие сведения об обновлениях программного обеспечения в System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).  
