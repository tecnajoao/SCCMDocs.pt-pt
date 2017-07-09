---
title: "Use a mídia inicializável para implantar o Windows pela rede | Microsoft Docs"
description: "Use implantações de mídia inicializável no System Center Configuration Manager para implantar o sistema operacional quando o computador de destino é iniciado."
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: mattbriggs
ms.author: mattbriggs
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: 9b20e5e2a66d92038033e816e6fc701581c48a7f
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Use a mídia inicializável para implantar o Windows pela rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Você pode implantar o sistema operacional quando o computador de destino é iniciado usando uma implantação de mídia inicializável. A mídia contém um ponteiro para a sequência de tarefas, a imagem do sistema operacional e outro conteúdo necessário da rede. Quando o computador de destino é iniciado, o computador recupera os itens mencionados no ponteiro. Com a mídia inicializável livre de conteúdo, você pode atualizar o destino sem a necessidade de substituí-lo na mídia.

Você pode implantar sistemas operacionais na rede usando multicast nos seguintes cenários de implantação de sistema operacional:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir definições](replace-an-existing-computer-and-transfer-settings.md)  

Conclua os passos num dos cenários de implementação do sistema operativo e, em seguida, utilize as secções seguintes para utilizar suportes de dados de arranque para implementar o sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
Quando você usa mídia inicializável para iniciar o processo de implantação de sistema operacional, configure a implantação para disponibilizar o sistema operacional para a mídia. Você pode definir essa opção no **configurações de implantação** página de Assistente de implantação de Software ou no **configurações de implantação** guia nas propriedades de implantação. Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:

-   Clientes do Configuration Manager, mídia e PXE

-   Apenas suportes de dados e PXE

-   Apenas suportes de dados e PXE (oculto)

## <a name="create-the-bootable-media"></a>Criar suportes de dados de arranque
Você pode especificar se a mídia inicializável é uma unidade flash USB ou conjunto de CD/DVD. O computador que inicia a mídia deve dar suporte a opção que você escolher como uma unidade inicializável. Para obter mais informações, consulte [criar uma mídia inicializável](create-bootable-media.md).  

##  <a name="BKMK_Deploy"></a> Instalar o sistema operativo a partir de suportes de dados de arranque  
Insira o suporte de dados numa unidade de arranque no computador e ligue-o para instalar o sistema operativo.

