---
title: "Безопасность и конфиденциальность профилей электронной почты | Документы Майкрософт"
description: "Ознакомьтесь с рекомендациями по обеспечению безопасности при управлении профилями электронной почты для устройств в System Center Configuration Manager."
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 601e3a8d-e9e7-456f-a844-f19c3dae12a9
caps.latest.revision: "3"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 17707f931a4fa58b225ce14f04c2a19648585bc4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-email-profiles-in-system-center-configuration-manager"></a>Безопасность и конфиденциальность профилей электронной почты в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

## <a name="security-best-practices-for-email-profiles"></a>Рекомендации по безопасности для профилей электронной почты  
 При управлении профилями электронной почты для устройств необходимо учитывать следующие рекомендации по безопасности.  

|Рекомендация по безопасности|Дополнительные сведения|  
|----------------------------|----------------------|  
|По возможности выбирайте наиболее безопасные параметры, поддерживаемые инфраструктурой электронной почты и клиентскими операционными системами.|Профили электронной почты предоставляют удобный способ централизованного распределения параметров электронной почты, поддерживаемых вашими устройствами, и управления ими. Configuration Manager не добавляет функции электронной почты.<br /><br /> Определите, реализуйте и выполните все рекомендации по безопасности для устройств и инфраструктуры электронной почты.|  

## <a name="privacy-information-for-email-profiles"></a>Сведения о конфиденциальности профилей электронной почты  
 По умолчанию устройства не проверяют профили электронной почты. Кроме того, необходимо настроить профили VPэлектронной почты, а затем развернуть их для пользователей.  

 Перед настройкой профилей электронной почты следует проанализировать требования к конфиденциальности.  
