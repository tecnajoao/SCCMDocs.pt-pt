---
title: "Inventário de software para dispositivos móveis inscritos com o Microsoft Intune | Documentos do Microsoft"
description: "Inventário de software para dispositivos móveis inscritos com o Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventário de software para dispositivos móveis inscritos no Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 É possível recolher o inventário para as aplicações instaladas em dispositivos móveis. As aplicações que são colocadas no inventários irão depender se o dispositivo é empresarial ou pessoal. Para dispositivos pessoais, as aplicações apenas que são inventariadas são as aplicações que são geridas pelo Microsoft Intune.  

> [!NOTE]  
>  Inventário nas aplicações instaladas em dispositivos móveis é recolhido como parte de [inventário de hardware](mobile-device-hardware-inventory-hybrid.md) processo.  

 Seguem-se as aplicações que são inventariadas para dispositivos de propriedade pessoal ou pertencendo à empresa.  

|Plataforma|Em Dispositivos Pessoais|Para Dispositivos Pertencentes à Empresa|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sem cliente do Configuration Manager)|Apenas aplicações geridas|Apenas aplicações geridas|
|Windows 8.1 (sem cliente do Configuration Manager)|Apenas aplicações geridas|Apenas aplicações geridas|  
|Windows Phone 8|Apenas aplicações geridas|Apenas aplicações geridas|  
|Windows RT|Apenas aplicações geridas|Apenas aplicações geridas|  
|iOS|Apenas aplicações geridas|Todas as aplicações instaladas no dispositivo|  
|Android|Apenas aplicações geridas|Todas as aplicações instaladas no dispositivo|  

Consulte o artigo [introdução ao inventário de software](../../core/clients/manage/inventory/introduction-to-software-inventory.md) e [como configurar inventário de software ](../../core/clients/manage/inventory/configure-software-inventory.md) para obter informações detalhadas sobre como utilizar o inventário de software para recolher informações do ficheiro em dispositivos cliente.

