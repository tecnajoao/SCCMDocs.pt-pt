---
title: Utilizar o Centro de Software para implementar o Windows através da rede
titleSuffix: Configuration Manager
description: Pode implementar um sistema operativo ao centro de Software para atualizar um computador existente com uma nova versão do Windows ou para atualizar o Windows para a versão mais recente.
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fd4853a35c4bfa1112e61286add1e1f458e8b6f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346588"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar o Centro de Software para implementar o Windows através da rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Adquirente pode efectuar a sequência de tarefas que instala um sistema operativo no System Center Configuration Manager está disponível no Centro de Software. Pode implementar um sistema operativo ao centro de Software com os seguintes cenários de implementação do sistema operativo:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Atualize o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md)

Conclua os passos dos cenários de implementação do sistema operativo. Utilize as secções seguintes para se preparar para implementações que estão disponíveis no Centro de Software.

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
Para disponibilizar a implementação do sistema operativo no Centro de Software, configure a implementação. Pode configurar a implementação no **definições de implementação** página do Assistente de implementação de Software ou o **definições de implementação** separador nas propriedades para a implementação. Na definição **Tornar disponível para o seguinte** , configure **Apenas Clientes do Configuration Manager** ou **Clientes do Configuration Manager, suportes de dados e PXE**. Depois do sistema implementa o sistema operativo, o sistema operativo será apresentado no Centro de Software para os membros da coleção de destino.

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas nos computadores  
Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Ao implementar sistemas operativos no Centro de Software, pode configurar se a implementação está disponível ou necessário.

-   **Implementação necessária**: Necessário implementações irão disponibilizar o sistema operativo no Centro de Software, mas será iniciado automaticamente no agendamento de atribuição configurado.

-   **Implementação disponível**: O sistema operativo estará disponível no Centro de Software e o utilizador pode instalá-la a pedido.
