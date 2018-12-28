---
title: Atualizar para o Windows 10
titleSuffix: Configuration Manager
description: Saiba como utilizar o Configuration Manager para atualizar um sistema operacional do Windows 7 ou posterior para o Windows 10.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35312c92a20f8e3842b5ee47dd3b916631671e45
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417358"
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Atualizar o Windows para a versão mais recente com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece os passos no Configuration Manager para atualizar o sistema operacional num computador. Pode escolher de entre vários métodos de implementação diferentes, como um suporte de dados autónomo ou o Centro de Software. O cenário de atualização no local tem as seguintes funcionalidades:  

-   Atualiza o sistema operacional nos computadores atualmente com:
    - O Windows 7, Windows 8 ou Windows 8.1. Também pode efetuar atualizações de compilação em compilação do Windows 10. Por exemplo, pode atualizar o Windows 10 versão 1607 para o Windows 10, versão 1709.  
    
    - Windows Server 2012. Também pode fazer atualizações de compilação para compilação do Windows Server 2016. Para obter mais informações sobre os caminhos de atualização suportados, consulte [caminhos de atualização suportados](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Mantém as aplicações, definições e dados do utilizador no computador.  

-   Não tem dependências externas, como o Windows ADK.  

-   É mais rápido e mais resiliente do que as Implantações de SO tradicionais.  


> [!Note]  
> A partir da versão 1802, a sequência de tarefas de atualização in-loco do Windows 10 suporta a implementação para clientes baseados na internet geridos através da [gateway de gestão da nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Esta capacidade permite aos usuários remotos mais facilmente atualizar para o Windows 10, sem terem de se ligar à intranet. Para obter mais informações, consulte [atualização in-loco de implementar o Windows 10 através do CMG](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->



##  <a name="BKMK_Plan"></a> Planearear  

### <a name="task-sequence-requirements-and-limitations"></a>Requisitos de sequência de tarefas e limitações

Reveja os seguintes requisitos e limitações da sequência de tarefas atualizar um sistema operacional para se certificar de que ele atenda às suas necessidades:  

- Adicione apenas passos de sequência de tarefas que estão relacionadas com a tarefa principal de atualizar o sistema operativo. Estes passos incluem, principalmente, instalar pacotes, aplicações ou atualizações. Utilize também os passos que executam linhas de comando, PowerShell ou definir variáveis dinâmicas.  

- Reveja os controladores e aplicações que estão instalados nos computadores para se certificar de que são compatíveis com o Windows 10 antes de implementar a sequência de tarefas de atualização.  

- As seguintes tarefas não são compatíveis com a atualização no local. Eles exigem a utilização de Implantações de SO tradicionais:  

  - Alterar a associação de domínio do computador ou a atualizar o grupo de administradores local.  

  - Implementar uma alteração fundamental no computador, tal como: 
    - Mudança de partições de disco
    - Alteração da arquitetura do sistema de x86 para x64
    - Implementação de UEFI. (Para obter mais informações sobre uma opção viável, consulte [converter BIOS para UEFI durante uma atualização in-loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).)
    - Modificar o idioma base do SO  

  - Tem requisitos personalizados, incluindo a utilização de uma imagem base personalizada, utilizando a encriptação de disco de terceiros ou exigir operações offline de WinPE.  

### <a name="infrastructure-requirements"></a>Requisitos de infraestrutura  

O único pré-requisito para o cenário de atualização é ter um ponto de distribuição disponível. Distribua o pacote de atualização de SO e outros pacotes que incluir na sequência de tarefas. Para mais informações, consulte [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).



##  <a name="BKMK_Configure"></a> Configurar  

### <a name="prepare-the-os-upgrade-package"></a>Preparar o pacote de atualização de SO  

  O pacote de atualização do Windows 10 contém os ficheiros de origem necessários para atualizar o sistema operacional no computador de destino. O pacote de atualização tem de ser a mesma edição, arquitetura e linguagem que os clientes que atualizar. Para obter mais informações, consulte [gerir pacotes de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  


### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Criar uma sequência de tarefas para atualizar o sistema operacional  

  Utilize os passos em [criar uma sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para automatizar a atualização do sistema operacional.  

   > [!NOTE]  
   > Normalmente, utilize os passos em [criar uma sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para criar uma sequência de tarefas para atualizar um sistema operacional para o Windows 10. A sequência de tarefas inclui o passo Atualizar sistema operativo, bem como passos recomendados adicionais e o processo de atualização de grupos para lidar com o ponto-a-ponto. No entanto, pode criar uma sequência de tarefas personalizado e adicionar as [atualizar sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS) passo de sequência de tarefas para atualizar o sistema operacional. Este passo é o único necessário para atualizar o sistema operacional para Windows 10. Se escolher este método, adicione também o passo [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) , a seguir ao passo Atualizar Sistema Operativo, para concluir a atualização. Certifique-se de que utilize o **o sistema de operativo predefinido atualmente instalado** definição para reiniciar o computador para o SO instalado e não para o Windows PE.  



##  <a name="BKMK_Deploy"></a> Implementar  

Para implementar o sistema operacional, utilize um dos seguintes métodos de implementação:  

  -   [Utilizar o Centro de Software para implementar o Windows através da rede](use-software-center-to-deploy-windows-over-the-network.md)  

  -   [Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

      > [!IMPORTANT]  
      > Quando utiliza suportes de dados autónomos, tem de incluir uma imagem de arranque na sequência de tarefas para que fique disponível no Assistente de suporte de dados de sequência de tarefas.




## <a name="monitor"></a>Monitor  

Para monitorizar a implementação de sequência de tarefas para atualizar o sistema operacional, consulte [monitorizar implementações do sistema operativo](monitor-operating-system-deployments.md).  
