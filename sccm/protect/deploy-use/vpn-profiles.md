---
title: "Профили VPN в System Center Configuration Manager | Документы Майкрософт"
description: "Узнайте, как использовать профили VPN в System Center Configuration Manager, чтобы развернуть параметры VPN для пользователей в вашей организации."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: e07a80c1a59043b74cda7219f78c5fef66989ba8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Профили VPN в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*


Используйте профили VPN в System Center Configuration Manager (SCCM), чтобы развернуть параметры VPN для пользователей в вашей организации. Развертывание этих параметров упрощает для конечного пользователя подключение к ресурсам в локальной сети.  

 Например, если нужно подготовить все устройства, запущенные в операционной системе Windows RT с параметрами, необходимыми для подключения к общей папке в корпоративной сети. Можно создать профиль VPN, содержащий параметры, необходимые для подключения к корпоративной сети, а затем развернуть этот профиль для всех пользователей с устройствами под управлением Windows RT в иерархии. Пользователи устройств Windows RT увидят VPN-подключение в списке доступных сетей и смогут подключаться к этой сети с минимальными усилиями.  

 При создании профиля VPN можно использовать широкий спектр параметров безопасности, включая сертификаты для проверки сервера и проверки подлинности клиента, наличие которых обеспечивается с помощью профилей сертификатов в System Center Configuration Manager. Дополнительные сведения о профилях сертификатов см. в разделе [Профили сертификатов в System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 В следующих разделах описывается, какие устройства можно настроить с помощью профилей VPN при использовании Configuration Manager.

 Сведения о том, где просмотреть устройства, которые можно настроить при использовании Configuration Manager в Microsoft Intune, см. в статье [Профили VPN на мобильных устройствах в System Center Configuration Manager](/sccm/mdm/deploy-use/create-vpn-profiles).  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Профили VPN при использовании Configuration Manager  
 В приведенной ниже таблице описываются профили VPN, которые можно настроить для различных платформ устройств.  

|Тип подключения|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|Нет|Нет|Нет|Нет|  
|**Pulse Secure**|Да|Нет|Да|Да|  
|**F5 Edge Client**|Да|Нет|Да|Да|  
|**Dell SonicWALL Mobile Connect**|Да|Нет|Да|Да|  
|**Check Point Mobile VPN**|Да|Нет|Да|Да|  
|**Microsoft SSL (SSTP)**|Да|Да|Да|Нет|  
|**Microsoft Automatic**|Да|Да|Да|Нет|  
|**IKEv2**|Да|Да|Да|Нет|  
|**PPTP**|Да|Да|Да|Нет|  
|**L2TP**|Да|Да|Да|Нет|  

### <a name="next-steps"></a>Дальнейшие действия  
 Приведенные ниже разделы содержат справочные сведения о планировании, настройке, использовании и обслуживании профилей VPN в Configuration Manager.  

-   [Необходимые условия для профилей VPN в System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Безопасность и конфиденциальность профилей VPN в System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
