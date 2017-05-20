---
title: "Utilize o multicast para implementar o Windows através da rede | Documentos do Microsoft"
description: "Utilizar multicast no ambiente do System Center Configuration Manager para que vários computadores em simultâneo possam transferir a imagem do sistema operativo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 55266696aa7340fddda3a57ff90e20222ff665a5
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilize o multicast para implementar o Windows através da rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Multicast é um método de otimização de rede que pode utilizar no seu ambiente do System Center Configuration Manager onde se prevê a transferência da mesma imagem do sistema operativo em simultâneo por vários clientes. Quando é utilizado o multicast, a imagem do sistema operativo é transferida em simultâneo por vários computadores à medida que é multidifundida pelo ponto de distribuição, em vez de ter um ponto de distribuição que envia uma cópia dos dados para cada cliente através de uma ligação separada.  

 Pode implementar sistemas operativos na rede através de multicast nos seguintes cenários de implementação de sistema operativo:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

 Execute os passos num dos cenários de implementação do sistema operativo e utilize as secções seguintes para suporte de multicast.  

##  <a name="BKMK_Configure"></a> Configurar um ponto de distribuição para suportar multicast  
 Para utilizar multicast quando implementa sistemas operativos, tem de configurar um ponto de distribuição para suportar multicast. Para obter mais informações, consulte o artigo [configurar pontos de distribuição para suportar multicast](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Preparar uma imagem do sistema operativo para implementações multicast  
 Para configurar o pacote de imagem do sistema operativo para suportar multicast, consulte o artigo [preparar a imagem do sistema operativo para implementações por multicast](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas  
 Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

