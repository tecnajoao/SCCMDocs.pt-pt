---
title: "Регистрация устройств | Документация Майкрософт"
description: "Ознакомьтесь со способами регистрации устройств для локального управления мобильными устройствами в System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: "6"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4abaef35969ef1a5340ae8ca8aa5699cd3942642
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Регистрация устройств для локального управления мобильными устройствами в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Для управления компьютерами и устройствами с помощью функции локального управления мобильными устройствами System Center Configuration Manager устройства должны быть зарегистрированы, чтобы среда Configuration Manager могла связываться с устройствами для выполнения задач управления. Configuration Manager предоставляет два метода регистрации устройств.  

-   **Регистрация пользователем** : в этом методе пользователь инициирует процесс регистрации на устройствах. Для успешной регистрации пользователем на устройстве должен быть установлен доверенный корневой сертификат, а сам пользователь — быть подготовлен к регистрации в Configuration Manager.  Чтобы зарегистрировать устройство, пользователь просто предоставляет рабочие учетные данные.  

     Дополнительные сведения см. в разделе [Регистрация устройств пользователями с помощью локального управления мобильными устройствами в System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

-   **Массовая регистрация** : в этом методе пользователю устройства не требуется инициировать процесс регистрации. Вместо этого в Configuration Manager создается пакет массовой регистрации, который затем передается на устройство и открывается. При этом пакет предоставляет сведения, необходимые для регистрации устройства.  

     Дополнительные сведения см. в разделе [Массовая регистрация устройств с помощью локального управления мобильными устройствами в System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md).  

 > [!NOTE]  
>  Текущая ветвь Configuration Manager поддерживает регистрацию локального управления мобильными устройствами для устройств со следующими операционными системами:  
>   
>  -   Windows 10 Корпоративная  
> -   Windows 10 Pro  
> -   Windows 10 для совместной работы 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Корпоративная   
