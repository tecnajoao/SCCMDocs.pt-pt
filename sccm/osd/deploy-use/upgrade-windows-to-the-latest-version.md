---
title: "Atualizar o Windows para a versão mais recente | Documentos do Microsoft"
description: Saiba como utilizar o Configuration Manager para atualizar um sistema operativo a partir do Windows 7 ou posterior para Windows 10.
ms.custom: na
ms.date: 02/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 288a4c649f371d9701fe7249449356aa222bf372
ms.openlocfilehash: 35f04e237efffbdb12893f658950a99dc0b98b85
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Atualizar o Windows para a versão mais recente com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico fornece os passos no System Center Configuration Manager, para atualizar um sistema operativo num computador a partir do Windows 7 ou posterior para Windows 10. Pode escolher de entre vários métodos de implementação diferentes, como um suporte de dados autónomo ou o Centro de Software. Cenário de atualização no local do Windows 10:  

-   Atualiza o sistema operativo nos computadores atualmente com o Windows 7, Windows 8 ou Windows 8.1. Também pode efetuar atualizações de compilação em compilação do Windows 10. Por exemplo, pode atualizar o Windows 10 RTM para o Windows 10, versão 1511.  

-   Mantém as aplicações, definições e dados do utilizador no computador.  

-   Não tem dependências externas, como o Windows ADK.  

-   Geralmente, é mais rápida e mais resiliente do que as implementações de sistema operativo tradicionais.  

 Utilize as secções seguintes para implementar sistemas operativos na rede utilizando uma sequência de tarefas.  

##  <a name="BKMK_Plan"></a> Planearear  

-   **Reveja as limitações da sequência de tarefas para atualizar um sistema operativo**  

     Reveja os seguintes requisitos e limitações da sequência de tarefas para atualizar um sistema operativo para se certificar de que satisfaz as suas necessidades:  

    -   Apenas deve adicionar passos de sequência de tarefas que estejam relacionados com a tarefa principal de implementar sistemas operativos e configurar computadores depois de a imagem estar instalada. Isto inclui passos que instalam pacotes, aplicações ou atualizações e passos que executam linhas de comandos, o PowerShell ou definem variáveis dinâmicas.  

    -   Reveja os controladores e aplicações que estão instalados nos computadores para se certificar de que são compatíveis com o Windows 10 antes de implementar a sequência de tarefas de atualização.  

    -   As tarefas seguintes não são compatíveis com a atualização no local e necessitam que utilize uma implementação do sistema operativo tradicional:  

        -   Alterar a associação ao domínio dos computadores ou atualizar os Administradores Locais.  

        -   Implementar uma alteração fundamental no computador, incluindo a criação de partições no disco, a transição de uma arquitetura x86 para x64, a implementação de UEFI ou a modificação do idioma base do sistema operativo.  

        -   Que ter requisitos personalizados, incluindo a utilização de uma imagem base personalizada, com 3<sup>rd</sup> encriptação de disco de terceiros ou requerem WinPE offline operações.  

-   **Planear e implementar requisitos de infraestrutura**  

     Os únicos pré-requisitos para o cenário de atualização é que tenha um ponto de distribuição disponível para o pacote de atualização do sistema operativo e outros pacotes que incluir na sequência de tarefas. Para obter mais informações, consulte o artigo [instalar ou modificar um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

##  <a name="BKMK_Configure"></a> Configurar  

1.  **Preparar o pacote de atualização do sistema operativo**  

     O pacote de atualização do Windows 10 contém os ficheiros de origem necessários para atualizar o sistema operativo no computador de destino. O pacote de atualização tem de ser da mesma edição, ter a mesma arquitetura e o mesmo idioma que os clientes que irá atualizar.  Para obter mais informações, consulte o artigo [gerir pacotes de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

2.  **Criar uma sequência de tarefas para atualizar o sistema operativo**  

     Utilize os passos no [criar uma sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para automatizar a atualização do sistema operativo.  

    > [IMPORTANTE] Quando utiliza suportes de dados autónomos, tem de incluir uma imagem de arranque na sequência de tarefas para este ficar disponível no Assistente de suporte de dados de sequência de tarefas.


    > [!NOTE]  
    >  Normalmente, irá utilizar os passos no [criar uma sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) para criar uma sequência de tarefas para atualizar um sistema operativo para o Windows 10. A sequência de tarefas inclui o passo de atualizar o sistema operativo, bem como passos recomendados adicionais e grupos para lidar com o ponto-a-ponto do processo de atualização. No entanto, pode criar uma sequência de tarefas personalizada e adicione o [atualizar o sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS) passo de sequência de tarefas para atualizar o sistema operativo. Este é o único passo necessário para atualizar o sistema operativo para o Windows 10. Se escolher este método, adicione também o [reiniciar o computador](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) passo após o passo de atualizar o sistema operativo para concluir a atualização. Certifique-se de que utiliza o **o sistema operativo predefinido atualmente instalado** definição para reiniciar o computador para o sistema operativo instalado e não do Windows PE.  

##  <a name="BKMK_Deploy"></a> Implementar  

-   Utilize um dos seguintes métodos de implementação para implementar o sistema operativo:  

    -   [Utilizar o Centro de Software para implementar o Windows através da rede](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Utilize suportes de dados autónomos para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Monitorizar a implementação da sequência de tarefas**  

     Para monitorizar a implementação de sequência de tarefas para atualizar o sistema operativo, consulte o artigo [monitorizar implementações do sistema operativo](monitor-operating-system-deployments.md).  

