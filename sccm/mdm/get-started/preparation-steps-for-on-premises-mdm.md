---
title: "Шаги подготовки | Документация Майкрософт"
description: "Подготовьтесь к управлению устройствами с помощью локального управления мобильными устройствами в System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
caps.latest.revision: "4"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 85bdadaaaeed9a42cfa5165d2b9f0f3ef434dc03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Шаги подготовки к локальному управлению мобильными устройствами в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Для управления устройствами с помощью локального управления мобильными устройствами System Center Configuration Manager требуется настроить инфраструктуру Configuration Manager, чтобы необходимые роли системы сайта (прокси-точка регистрации, точка регистрации, точка управления устройствами и точки распространения) могли взаимодействовать через надежный канал с управляемыми мобильными устройствами.  

 Чтобы подготовить систему Configuration Manager для локального управления мобильными устройствами, необходимо выполнить указанные ниже общие задачи.  

-   [Настройка подписки Microsoft Intune для локального управления мобильными устройствами в System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     В рамках этой задачи вы регистрируетесь в Microsoft Intune, а затем добавляете подписку в Configuration Manager с помощью консоли Configuration Manager. Этот шаг необходим только с точки зрения лицензирования. Intune не используется для управления устройствами или хранения данных управления. Все операции по координации устройств и управлению ими осуществляются в корпоративной среде вашей организации с помощью локальной инфраструктуры Configuration Manager.  

-   [Установка ролей системы сайта для локального управления мобильными устройствами в System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     В этой задаче вы устанавливаете и настраиваете роли системы сайта, необходимые для управления устройствами с помощью локальной инфраструктуры Configuration Manager. Для локального управления мобильными устройствами требуются по меньшей мере следующие роли системы сайта: прокси-точка регистрации, точка регистрации, точка управления устройствами и точка распространения.  

-   [Настройка сертификатов для доверенного взаимодействия для локального управления мобильными устройствами в System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     В этой задаче вы настраиваете локальную инфраструктуру Configuration Manager, позволяющую осуществлять доверенное взаимодействие (HTTPS) между управляемыми устройствами и серверами, на которых размещены нужные роли системы сайта.  

-   [Настройка регистрации устройств для локального управления мобильными устройствами в System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     В этой задаче вы предоставляете пользователям разрешение на регистрацию компьютеров и устройств, а также устанавливаете доверенный корневой сертификат на устройствах (которые обычно не присоединены к домену), чтобы разрешить подключения по протоколу HTTPS к серверам системы сайта.  
