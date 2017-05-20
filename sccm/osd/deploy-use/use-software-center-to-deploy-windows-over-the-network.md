---
title: "Utilizar o Centro de Software para implementar o Windows através da rede | Documentos do Microsoft"
description: "Pode implementar um sistema operativo para o Centro de Software para atualizar um computador existente com uma nova versão do Windows ou para atualizar o Windows para a versão mais recente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 4c3ec20396da37d36f908af527f445a7a736e0ac
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar o Centro de Software para implementar o Windows através da rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A sequência de tarefas para instalar um sistema operativo no System Center Configuration Manager pode ser disponibilizada no Centro de Software. Pode implementar um sistema operativo no Centro de Software nos seguintes cenários de implementação de sistema operativo:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)  

 Conclua os passos num dos cenários de implementação de sistema operativo e utilize as secções seguintes para se preparar para as implementações disponíveis no Centro de Software.  

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
 Quando pretender que a implementação do sistema operativo fique disponível no Centro de Software, tem de configurar a implementação para disponibilizar o sistema operativo para clientes do Configuration Manager. Pode configurar esta opção na página **Definições de Implementação** do Assistente de Implementação de Software ou no separador **Definições de Implementação** , nas propriedades da implementação.  Na definição **Tornar disponível para o seguinte** , configure **Apenas Clientes do Configuration Manager** ou **Clientes do Configuration Manager, suportes de dados e PXE**. Depois de o sistema operativo ser implementado, será apresentado no Centro de Software para os membros da coleção de destino.  

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas nos computadores  
 Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando implementar sistemas operativos no Centro de Software, pode configurar se a implementação é necessária ou se está disponível.  

-   **Implementação necessária**: Necessário implementações irão disponibilizar o sistema operativo no Centro de Software, mas será automaticamente iniciado no agendamento configurado da atribuição.  

-   **Implementação disponível**: O sistema operativo estarão disponível no Centro de Software e o utilizador pode instalá-lo a pedido.  

