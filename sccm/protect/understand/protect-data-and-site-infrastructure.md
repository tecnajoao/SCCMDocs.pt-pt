---
title: "Защита данных и инфраструктуры сайтов | Документы Майкрософт"
description: "Узнайте, как защитить ресурсы организации от раскрытия или вредоносных атак с помощью System Center Configuration Manager."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
caps.latest.revision: "8"
author: Robstack
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d527cb4bfb55ca50c8d2a0fed7c427af5747fe99
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="protect-data-and-site-infrastructure-with-system-center-configuration-manager"></a>Защита данных и инфраструктуры сайтов с помощью System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*


Требуется, чтобы пользователи могли осуществлять безопасный доступ к ресурсам организации, а инфраструктура и данные были защищены от раскрытия или вредоносной атаки. В приведенных ниже разделах описывается включение доступа и защита ресурсов вашей организации с помощью System Center Configuration Manager (SCCM).  

-   Свести к минимуму усилия пользователей для подключения к корпоративным ресурсам можно, включив VPN-подключение с использованием профилей VPN. Дополнительные сведения см. в разделе [Профили VPN в System Center Configuration Manager](../deploy-use/vpn-profiles.md).  

-   Профили Wi-Fi включают набор средств и ресурсов, которые позволяют создавать, развертывать и отслеживать параметры беспроводных сетей на устройствах в организации. Развертывание этих параметров упрощает подключение пользователей к корпоративным беспроводным сетям. Дополнительные сведения см. в разделе [Профили Wi-Fi в System Center Configuration Manager](/sccm/protect/deploy-use/create-wifi-profiles).  

-   В разделе [Профили сертификатов в System Center Configuration Manager](../deploy-use/introduction-to-certificate-profiles.md) описывается способ подготовки устройств пользователей с помощью сертификатов, необходимых для подключения к ресурсам компании.  

-   [System Center Endpoint Protection](../deploy-use/endpoint-protection.md) позволяет управлять политиками защиты от вредоносных программ и параметрами безопасности брандмауэра Windows для клиентских компьютеров.  

-   Вы можете использовать условный доступ для защиты электронной почты и других служб на устройствах, зарегистрированных в Microsoft Intune, как описано в разделе [Управление доступом к службам в System Center Configuration Manager](../deploy-use/manage-access-to-services.md).  

-   Профили электронной почты предоставляют набор средств и ресурсов, помогающих создавать, развертывать и отслеживать параметры электронной почты на устройствах. Это предоставляет пользователям возможность получения доступа к корпоративной электронной почте на личных устройствах без каких-либо необходимых настроек с их стороны. Дополнительные сведения см. в разделе [Профили электронной почты в System Center Configuration Manager](../deploy-use/introduction-to-email-profiles.md).  

-   Configuration Manager поддерживает интеграцию с Windows Hello для бизнеса (прежнее название Microsoft Passport for Work) альтернативным методом входа, использующим учетную запись Active Directory или Azure Active Directory для замены пароля, смарт-карты или виртуальной смарт-карты. Дополнительные сведения см. в разделе [Параметры Windows Hello для бизнеса в System Center Configuration Manager](../deploy-use/windows-hello-for-business-settings.md).  
