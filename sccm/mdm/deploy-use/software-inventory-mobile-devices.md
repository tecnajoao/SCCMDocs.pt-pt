---
title: "Инвентаризация программного обеспечения для мобильных устройств, зарегистрированных с помощью Microsoft Intune | Документация Майкрософт"
description: "Инвентаризация программного обеспечения для мобильных устройств, зарегистрированных с помощью Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Инвентаризация программного обеспечения для мобильных устройств, зарегистрированных с помощью Microsoft Intune

*Применимо к: System Center Configuration Manager (Current Branch)*

 Вы можете собирать данные инвентаризации по приложениям, установленным на мобильных устройствах. Перечень приложений будет зависеть от типа владения устройством — принадлежащее компании или личное. В случае если устройство является личным, процесс инвентаризации проходят только приложения, которыми управляет Microsoft Intune.  

> [!NOTE]  
>  Данные инвентаризации по приложениям, установленным на мобильных устройствах, собираются в рамках процесса [инвентаризации оборудования](mobile-device-hardware-inventory-hybrid.md).  

 Ниже указано, какие приложения включаются в данные инвентаризации для личных устройств или устройств, принадлежащих компании.  

|Платформа|Для личных устройств|Для устройств, принадлежащих компании|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (без клиента Configuration Manager)|Только управляемые приложения|Только управляемые приложения|
|Windows 8.1 (без клиента Configuration Manager)|Только управляемые приложения|Только управляемые приложения|  
|Windows Phone 8|Только управляемые приложения|Только управляемые приложения|  
|Windows RT|Только управляемые приложения|Только управляемые приложения|  
|iOS|Только управляемые приложения|Все приложения, установленные на устройстве|  
|Android|Только управляемые приложения|Все приложения, установленные на устройстве|  

Подробные сведения об использовании инвентаризации программного обеспечения для сбора информации о файлах на клиентских устройствах см. в статьях [Общие сведения об инвентаризации программного обеспечения в System Center Configuration Manager](../../core/clients/manage/inventory/introduction-to-software-inventory.md) и [Настройка инвентаризации программного обеспечения в System Center Configuration Manager](../../core/clients/manage/inventory/configure-software-inventory.md).
