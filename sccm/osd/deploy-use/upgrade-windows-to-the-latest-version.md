---
title: Atualizar para o Windows 10
titleSuffix: Configuration Manager
description: Saiba como utilizar o Configuration Manager para atualizar o sistema operativo do Windows 7 ou posterior para Windows 10.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: ''
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 976a65ad27fe615a997ef795e3acf7a175f363af
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Atualizar o Windows para a versão mais recente com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece os passos no Configuration Manager para atualizar o sistema operativo num computador. Pode escolher de entre vários métodos de implementação diferentes, como um suporte de dados autónomo ou o Centro de Software. O cenário de atualização no local tem as seguintes funcionalidades:  

-   Atualiza o sistema operativo em computadores que executam atualmente:
    - Windows 7, Windows 8 ou Windows 8.1. Também pode efetuar atualizações de compilação em compilação do Windows 10. Por exemplo, pode atualizar o Windows 10 versão 1607 para Windows 10, versão 1709.  
    
    - Windows Server 2012. Também pode fazer atualizações de compilação em compilação do Windows Server 2016. Para mais informações sobre caminhos de atualização suportados, consulte [caminhos de atualização suportados](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Mantém as aplicações, definições e dados do utilizador no computador.  

-   Não tem dependências externas, como o Windows ADK.  

-   É mais rápido e mais resiliente do que as implementações tradicionais do SO.  


> [!Note]  
> A partir de versão 1802, a sequência de tarefas de atualização no local do Windows 10 suporta a implementação de clientes baseados na internet geridos através de [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Esta capacidade permite aos utilizadores remotos mais facilmente atualizar para o Windows 10, sem necessitar de ligar à intranet. Para obter mais informações, consulte [atualização no local de implementar o Windows 10 através de CMG](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->



##  <a name="BKMK_Plan"></a> Planearear  

### <a name="task-sequence-requirements-and-limitations"></a>Requisitos de sequência de tarefas e limitações

Reveja os seguintes requisitos e limitações da sequência de tarefas atualizar o sistema operativo para se certificar de que satisfaz as suas necessidades:  

  -   Adicione apenas passos de sequência de tarefas que estão relacionados com a tarefa principal de atualização de SO. Estes passos incluem principalmente instalar pacotes, aplicações ou atualizações. Utilize também passos que executam linhas de comando, PowerShell ou definem variáveis dinâmicas.  

  -   Reveja os controladores e aplicações que estão instalados nos computadores para se certificar de que são compatíveis com o Windows 10 antes de implementar a sequência de tarefas de atualização.  

  -   As tarefas seguintes não são compatíveis com a atualização no local. Necessitam que utilize implementações tradicionais do SO:  

     -   A alteração de associação de domínio do computador ou a atualizar o grupo de administradores local.  

     -   Implementar uma alteração fundamental no computador, tais como: 
         - Mudança de partições de disco
         - Alterar a arquitetura de sistema de x86 para x64
         - Implementação de UEFI. (Para obter mais informações sobre uma opção de possíveis, consulte [converter da BIOS UEFI durante uma atualização no local](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).)
         - Modificar o idioma do SO base  

     -   Tem requisitos personalizados, incluindo uma imagem base personalizada, utilizando a encriptação de disco de terceiros ou necessitar de operações offline de WinPE.  

### <a name="infrastructure-requirements"></a>Requisitos de infraestrutura  

O único pré-requisito para o cenário de atualização é ter um ponto de distribuição disponível. Distribua o pacote de atualização do SO e quaisquer outros pacotes que incluir na sequência de tarefas. Para obter mais informações, consulte [instalar ou modificar um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).



##  <a name="BKMK_Configure"></a> Configurar  

### <a name="prepare-the-os-upgrade-package"></a>Preparar o pacote de atualização do SO  

  O pacote de atualização do Windows 10 contém os ficheiros de origem necessários para atualizar o sistema operativo no computador de destino. O pacote de atualização tem de ser a mesma edição, arquitetura e de idioma que os clientes que atualizar. Para obter mais informações, consulte [gerir pacotes de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  


### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Criar uma sequência de tarefas para atualizar o sistema operativo  

  Utilize os passos em [criar uma sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para automatizar a atualização do SO.  

   > [!NOTE]  
   > Normalmente, utilize os passos em [criar uma sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para criar uma sequência de tarefas para atualizar o sistema operativo para o Windows 10. A sequência de tarefas inclui o passo Atualizar sistema operativo, bem como passos recomendados adicionais e processo de atualização de grupos para lidar com o ponto-a-ponto. No entanto, pode criar uma sequência de tarefas personalizada e adicionar o [atualizar sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS) passo de sequência de tarefas para atualizar o sistema operativo. Este passo é a única necessária para atualizar o sistema operativo para o Windows 10. Se escolher este método, adicione também o [reiniciar o computador](../understand/task-sequence-steps.md#BKMK_RestartComputer) passo após o passo Atualizar sistema operativo para concluir a atualização. Certifique-se de utilizar o **o sistema operativo predefinido atualmente instalado** definição para reiniciar o computador para o SO instalado e não do Windows PE.  



##  <a name="BKMK_Deploy"></a> Implementar  

Para implementar o sistema operativo, utilize um dos seguintes métodos de implementação:  

  -   [Utilizar o Centro de Software para implementar o Windows através da rede](use-software-center-to-deploy-windows-over-the-network.md)  

  -   [Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

      > [!IMPORTANT]  
      > Quando utilizar suportes de dados autónomos, tem de incluir uma imagem de arranque na sequência de tarefas para que seja disponível no Assistente de suporte de dados de sequência de tarefas.




## <a name="monitor"></a>Monitor  

Para monitorizar a implementação de sequência de tarefas para atualizar o sistema operativo, consulte [monitorizar implementações do sistema operativo](monitor-operating-system-deployments.md).  
