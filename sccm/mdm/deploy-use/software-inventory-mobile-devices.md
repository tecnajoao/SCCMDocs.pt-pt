---
title: Inventário de software para dispositivos móveis inscritos com o Microsoft Intune
titleSuffix: Configuration Manager
description: Inventário de software para dispositivos móveis inscritos com o Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91d298dae14c879e215b85483558898382c12055
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120747"
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventário de software para dispositivos móveis inscritos no Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 É possível recolher o inventário de aplicações instaladas em dispositivos móveis. As aplicações que são colocadas no inventários irão depender se o dispositivo é empresarial ou pessoal. Para os dispositivos pessoais, as únicas aplicações que são inventariadas são as aplicações que são geridas pelo Microsoft Intune.  

> [!NOTE]  
>  Inventário nas aplicações instaladas em dispositivos móveis é recolhido como parte da [inventário de hardware](mobile-device-hardware-inventory-hybrid.md) processo.  

 Seguem-se as aplicações que são inventariadas em dispositivos pessoais ou pertencentes à empresa.  

|Plataforma|Em Dispositivos Pessoais|Para Dispositivos Pertencentes à Empresa|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sem o cliente do Configuration Manager)|Apenas aplicações geridas|Apenas aplicações geridas|
|Windows 8.1 (sem o cliente do Configuration Manager)|Apenas aplicações geridas|Apenas aplicações geridas|  
|Windows Phone 8|Apenas aplicações geridas|Apenas aplicações geridas|  
|Windows RT|Apenas aplicações geridas|Apenas aplicações geridas|  
|iOS|Apenas aplicações geridas|Todas as aplicações instaladas no dispositivo|  
|Android|Apenas aplicações geridas|Todas as aplicações instaladas no dispositivo|  

Ver [introdução ao inventário de software](../../core/clients/manage/inventory/introduction-to-software-inventory.md) e [como configurar inventário de software ](../../core/clients/manage/inventory/configure-software-inventory.md) para obter informações detalhadas sobre como utilizar o inventário de software para recolher informações de ficheiros nos dispositivos cliente.
