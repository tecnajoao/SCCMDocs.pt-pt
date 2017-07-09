---
title: Use o Centro de Software para implantar o Windows pela rede | Microsoft Docs
description: "Você pode implantar um sistema operacional no Centro de Software para atualizar um computador existente com uma nova versão do Windows ou para atualizar o Windows para a versão mais recente."
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: 8988409c68b7f69439ed03872c316b2139d25616
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar o Centro de Software para implementar o Windows através da rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Você pode fazer a sequência de tarefas que instala um sistema operacional no System Center Configuration Manager disponível no Centro de Software. Você pode implantar um sistema operacional no Centro de Software nos seguintes cenários de implantação de sistema operacional:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Atualize o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)

Conclua as etapas em um dos cenários de implantação de sistema operacional. Em seguida, use as seções a seguir para preparar para implantações que estão disponíveis no Centro de Software.

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
Para fazer a implantação de sistema operacional disponíveis no Centro de Software, configure a implantação. Você pode configurar a implantação no **configurações de implantação** página do Assistente de implantação de Software ou o **configurações de implantação** guia nas propriedades de implantação. Na definição **Tornar disponível para o seguinte** , configure **Apenas Clientes do Configuration Manager** ou **Clientes do Configuration Manager, suportes de dados e PXE**. Depois que o sistema implanta o sistema operacional, o sistema operacional será exibido no Centro de Software para membros da coleção de destino.

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas nos computadores  
Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando você implanta sistemas operacionais para o Centro de Software, você pode configurar se a implantação será obrigatória ou estará disponível.

-   **Implantação necessária**: Necessário implantações tornará o sistema operacional disponível no Centro de Software, mas ele será iniciado automaticamente no agendamento de atribuição configurado.

-   **Implantação disponível**: O sistema operacional estará disponível no Centro de Software e o usuário poderá instalá-lo sob demanda.

