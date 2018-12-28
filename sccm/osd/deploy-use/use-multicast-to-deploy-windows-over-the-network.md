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
ms.openlocfilehash: ec623e6cf7a2616058b63bb1206f5403c4ff792a
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417411"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar multicast para implementar o Windows através da rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Multicast é um método de otimização de rede que pode utilizar no seu ambiente do System Center Configuration Manager em que se prevê a transferência da mesma imagem do sistema operativo em simultâneo por vários clientes. Quando é utilizado o multicast, a imagem do sistema operativo é transferida em simultâneo por vários computadores à medida que é multidifundida pelo ponto de distribuição, em vez de ter um ponto de distribuição que envia uma cópia dos dados para cada cliente através de uma ligação separada.  

 Pode implementar sistemas operativos na rede através de multicast nos seguintes cenários de implementação de sistema operativo:  

- [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

  Execute os passos num dos cenários de implementação do sistema operativo e utilize as secções seguintes para suporte de multicast.  

##  <a name="BKMK_Configure"></a> Configurar um ponto de distribuição para suportar multicast  
 Para utilizar multicast quando implementa sistemas operativos, tem de configurar um ponto de distribuição para suportar multicast. Para mais informações, consulte [Configure distribution points to support multicast](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Preparar uma imagem do sistema operativo para implementações multicast  
 Para configurar o pacote de imagem do sistema operativo para suportar multicast, consulte [Prepare the operating system image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas  
 Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
