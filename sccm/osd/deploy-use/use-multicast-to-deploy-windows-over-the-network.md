---
title: Utilizar multicast para implementar o Windows através da rede
titleSuffix: Configuration Manager
description: Utilizar multicast no seu ambiente do System Center Configuration Manager para que vários computadores em simultâneo podem transferir a imagem do sistema operativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 648146f11336489f30f03c35cb3d648f161b5e69
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar multicast para implementar o Windows através da rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Multicast é um método de otimização de rede que pode utilizar no seu ambiente do System Center Configuration Manager em que se prevê a transferência da mesma imagem do sistema operativo em simultâneo por vários clientes. Quando é utilizado o multicast, a imagem do sistema operativo é transferida em simultâneo por vários computadores à medida que é multidifundida pelo ponto de distribuição, em vez de ter um ponto de distribuição que envia uma cópia dos dados para cada cliente através de uma ligação separada.  

 Pode implementar sistemas operativos na rede através de multicast nos seguintes cenários de implementação de sistema operativo:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

 Execute os passos num dos cenários de implementação do sistema operativo e utilize as secções seguintes para suporte de multicast.  

##  <a name="BKMK_Configure"></a> Configurar um ponto de distribuição para suportar multicast  
 Para utilizar multicast quando implementa sistemas operativos, tem de configurar um ponto de distribuição para suportar multicast. Para obter mais informações, consulte [configurar pontos de distribuição para suportar multicast](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Preparar uma imagem do sistema operativo para implementações multicast  
 Para configurar o pacote de imagem do sistema operativo para suportar multicast, consulte [preparar a imagem do sistema operativo para implementações por multicast](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas  
 Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
