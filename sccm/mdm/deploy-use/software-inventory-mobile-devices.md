---
title: "Inventário de software para dispositivos móveis inscritos com o Microsoft Intune"
titleSuffix: Configuration Manager
description: "Inventário de software para dispositivos móveis inscritos com o Microsoft Intune."
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
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c0a583de1a0b24bd31c0d55c1acb54f480bb4230
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventário de software para dispositivos móveis inscritos no Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode recolher inventário para as aplicações instaladas em dispositivos móveis. As aplicações que são colocadas no inventários irão depender se o dispositivo é empresarial ou pessoal. Para dispositivos pessoais, as únicas aplicações que são colocadas em inventário são as aplicações que são geridas pelo Microsoft Intune.  

> [!NOTE]  
>  Inventário nas aplicações instaladas em dispositivos móveis é recolhido como parte do [inventário de hardware](mobile-device-hardware-inventory-hybrid.md) processo.  

 Seguem-se as aplicações que são colocadas em inventário para dispositivos de propriedade pessoal ou pertencendo à empresa.  

|Plataforma|Em Dispositivos Pessoais|Para Dispositivos Pertencentes à Empresa|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sem o cliente do Configuration Manager)|Apenas aplicações geridas|Apenas aplicações geridas|
|Windows 8.1 (sem o cliente do Configuration Manager)|Apenas aplicações geridas|Apenas aplicações geridas|  
|Windows Phone 8|Apenas aplicações geridas|Apenas aplicações geridas|  
|Windows RT|Apenas aplicações geridas|Apenas aplicações geridas|  
|iOS|Apenas aplicações geridas|Todas as aplicações instaladas no dispositivo|  
|Android|Apenas aplicações geridas|Todas as aplicações instaladas no dispositivo|  

Consulte [introdução ao inventário de software](../../core/clients/manage/inventory/introduction-to-software-inventory.md) e [como configurar inventário de software ](../../core/clients/manage/inventory/configure-software-inventory.md) para obter informações detalhadas sobre como utilizar o inventário de software para recolher informações de ficheiros nos dispositivos cliente.
