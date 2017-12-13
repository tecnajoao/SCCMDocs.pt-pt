---
title: "Atualizar o Windows para a versão mais recente"
titleSuffix: Configuration Manager
description: "Saiba como utilizar o Gestor de configuração para atualizar um sistema operativo do Windows 7 ou posterior para Windows 10."
ms.custom: na
ms.date: 02/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: "13"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 30c2c2d3d2a59006e7f2ad490537a7d5bb55003a
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/12/2017
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Atualizar o Windows para a versão mais recente com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico fornece os passos no System Center Configuration Manager, para atualizar um sistema operativo num computador do Windows 7 ou posterior para o Windows 10 ou do Windows Server 2012 para o Windows Server 2016, num computador de destino. Pode escolher de entre vários métodos de implementação diferentes, como um suporte de dados autónomo ou o Centro de Software. O cenário de atualização no local:  

-   Atualiza o sistema operativo nos computadores atualmente com:
    - Windows 7, Windows 8 ou Windows 8.1. Também pode efetuar atualizações de compilação em compilação do Windows 10. Por exemplo, pode atualizar o Windows 10 RTM para o Windows 10, versão 1511.  
    - Windows Server 2012. Também pode fazer atualizações de compilação em compilação do Windows Server 2016. Para obter mais informações sobre caminhos de atualização suportados, consulte [caminhos de atualização suportados](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Mantém as aplicações, definições e dados do utilizador no computador.  

-   Não tem dependências externas, como o Windows ADK.  

-   É mais rápido e mais resiliente do que as implementações tradicionais do sistema operativo.  

 Utilize as secções seguintes para implementar sistemas operativos na rede utilizando uma sequência de tarefas.  

##  <a name="BKMK_Plan"></a> Planearear  

-   **Reveja as limitações da sequência de tarefas para atualizar um sistema operativo**  

     Reveja os seguintes requisitos e limitações da sequência de tarefas para atualizar um sistema operativo para se certificar de que satisfaz as suas necessidades:  

    -   Apenas deve adicionar passos de sequência de tarefas que estejam relacionados com a tarefa principal de implementar sistemas operativos e configurar computadores depois de a imagem estar instalada. Isto inclui passos que instalam pacotes, aplicações ou atualizações e passos que executam linhas de comandos, o PowerShell ou definem variáveis dinâmicas.  

    -   Reveja os controladores e aplicações que estão instalados nos computadores para se certificar de que são compatíveis com o Windows 10 antes de implementar a sequência de tarefas de atualização.  

    -   As tarefas seguintes não são compatíveis com a atualização no local e necessitam que utilize uma implementação do sistema operativo tradicional:  

        -   Alterar a associação ao domínio dos computadores ou atualizar os Administradores Locais.  

        -   Implementar uma alteração fundamental no computador, incluindo a criação de partições no disco, a transição de uma arquitetura x86 para x64, a implementação de UEFI ou a modificação do idioma base do sistema operativo.  

        -   Tem requisitos personalizados, incluindo uma imagem base personalizada, com 3<sup>rd</sup> encriptação de disco de terceiros ou necessitar de operações offline de WinPE.  

-   **Planear e implementar requisitos de infraestrutura**  

     Os únicos pré-requisitos para o cenário de atualização são que têm um ponto de distribuição disponível para o pacote de atualização do sistema operativo e quaisquer outros pacotes que incluir na sequência de tarefas. Para obter mais informações, consulte [instalar ou modificar um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

##  <a name="BKMK_Configure"></a> Configurar  

1.  **Preparar o pacote de atualização do sistema operativo**  

     O pacote de atualização do Windows 10 contém os ficheiros de origem necessários para atualizar o sistema operativo no computador de destino. O pacote de atualização tem de ser a mesma edição, arquitetura e de idioma que os clientes que atualizar.  Para obter mais informações, consulte [gerir pacotes de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

2.  **Criar uma sequência de tarefas para atualizar o sistema operativo**  

     Utilize os passos em [criar uma sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para automatizar a atualização do sistema operativo.  

    > [!IMPORTANT]
    > Quando utilizar suportes de dados autónomos, tem de incluir uma imagem de arranque na sequência de tarefas para que seja disponível no Assistente de suporte de dados de sequência de tarefas.

    > [!NOTE]  
    > Normalmente, utilize os passos em [criar uma sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para criar uma sequência de tarefas para atualizar um sistema operativo para o Windows 10. A sequência de tarefas inclui o passo Atualizar sistema operativo, bem como passos recomendados adicionais e processo de atualização de grupos para lidar com o ponto-a-ponto. No entanto, pode criar uma sequência de tarefas personalizada e adicionar o [atualizar sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS) passo de sequência de tarefas para atualizar o sistema operativo. Este é o único passo necessário para atualizar o sistema operativo para o Windows 10. Se escolher este método, adicione também o [reiniciar o computador](../understand/task-sequence-steps.md#BKMK_RestartComputer) passo após o passo Atualizar sistema operativo para concluir a atualização. Certifique-se de utilizar o **o sistema operativo predefinido atualmente instalado** definição para reiniciar o computador para o sistema operativo instalado e não do Windows PE.  

##  <a name="BKMK_Deploy"></a> Implementar  

-   Utilize um dos seguintes métodos de implementação para implementar o sistema operativo:  

    -   [Utilizar o Centro de Software para implementar o Windows através da rede](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Monitorizar a implementação da sequência de tarefas**  

     Para monitorizar a implementação de sequência de tarefas para atualizar o sistema operativo, consulte [monitorizar implementações do sistema operativo](monitor-operating-system-deployments.md).  
