---
title: Implementar atualizações de software
titleSuffix: Configuration Manager
description: Escolha as atualizações de software na consola do Configuration Manager para iniciar o processo de implementação manualmente ou implementar automaticamente atualizações.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/16/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: e6a825f0d4333dc551405e38db70f8417ee2b5ce
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_SUMDeploy"></a> Implementar atualizações de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A fase de implementação da atualização de software é o processo de implementar as atualizações de software. Independentemente de como implementar atualizações de software, as atualizações são, normalmente:
- Adicionada a um grupo de atualização de software.
- Transferidos para pontos de distribuição.
- O grupo de atualização é implementado para os clientes. Depois de criar a implementação, uma política de atualização de software associado é enviada para computadores cliente. Os ficheiros de conteúdo de atualização de software são transferidos a partir de um ponto de distribuição para a cache local nos computadores cliente. As atualizações de software, em seguida, estão disponíveis para instalação pelo cliente. Os clientes na Internet transferem conteúdo a partir do Microsoft Update.  

> [!NOTE]  
>  Se um ponto de distribuição não estiver disponível, pode configurar um cliente na intranet para transferir as atualizações de software do Microsoft Update.  

> [!NOTE]  
>  Ao contrário de outros tipos de implementação, as atualizações de software são todos transferidas para a cache do cliente. Isto é, independentemente da definição de tamanho máximo da cache no cliente. Para obter mais informações sobre a definição da cache do cliente, veja [Configurar a Cache do Cliente para Clientes do Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Se configurar uma implementação da atualização de software necessária, as atualizações de software são instaladas automaticamente no prazo agendado. Em alternativa, o utilizador no computador cliente pode agendar ou iniciar a instalação da atualização de software antes do termo do prazo. Após a instalação tentada, os computadores cliente enviam mensagens de estado de volta para o servidor de site para indicar se a instalação da atualização de software foi concluída com êxito. Para obter mais informações sobre implementações de atualização de software, veja [Fluxos de trabalho de implementação de atualizações de software](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Existem dois cenários principais para implementar atualizações de software: implementação manual e implementação automática. Normalmente, começar por implementar manualmente atualizações de software para criar uma linha de base para o cliente, computadores e, em seguida, gerir as atualizações de software em clientes utilizando a implementação automática.  

## <a name="BKMK_ManualDeployment"></a> Implementar manualmente atualizações de software
Pode selecionar as atualizações de software na consola do Configuration Manager e iniciar o processo de implementação manualmente. Normalmente, utiliza este método de implementação para garantir a atualização dos computadores cliente com atualizações de software necessárias antes de criar regras de implementação automática para gerir implementações mensais em curso de atualização de software, e para implementar requisitos de atualização de software fora de banda. A lista seguinte apresenta o fluxo de trabalho geral para a implementação manual de atualizações de software:  

1. Filtre para atualizações de software que utilizam requisitos específicos. Por exemplo, pode fornecer critérios que obtém todas as atualizações de software de segurança ou críticas que são necessárias em mais de 50 computadores clientes.  
2. Crie um grupo de atualização de software que contém as atualizações de software.  
3. Transfira o conteúdo das atualizações de software no grupo de atualização de software.  
4. Implemente manualmente o grupo de atualização de software.

Para obter passos detalhados, consulte [implementar manualmente atualizações de software](manually-deploy-software-updates.md).

>[!NOTE]
>A partir de atualizações de cliente do Configuration Manager versão 1706 do Office 365 movido para o **gestão de clientes do Office 365** >**atualizações do Office 365** nós. Esta ação não irá afetar a sua configuração de ADR mas afetar a implementação manual de atualizações do Office 365. 

## <a name="automatically-deploy-software-updates"></a>Implementar automaticamente atualizações de software
A implementação automática de atualizações de software é configurada utilizando uma regra de implementação automática (ADR). Este é um método comum de implementação para atualizações de software mensais (normalmente, denominadas "Patch Terça") e para gerir atualizações de definições. Quando a regra for executada, as atualizações são removidas do grupo de atualização de software (se existente a utilizar um grupo de atualização) do software, as atualizações de software que cumprem os critérios especificados (por exemplo, todas as atualizações de software de segurança publicadas no mês passado) são adicionadas a um grupo de atualização de software, os ficheiros de conteúdo para as atualizações de software são transferidos e copiados para pontos de distribuição e as atualizações de software são implementadas nos clientes da coleção de destino. A lista seguinte apresenta o fluxo de trabalho geral para implementar automaticamente atualizações de software:  

1.  Crie uma ADR que especifique as definições de implementação.
2.  As atualizações de software são adicionadas a um grupo de atualização de software.  
3.  O grupo de atualização de software é implementado nos computadores cliente da coleção de destino, se for especificada.  

Tem de determinar qual a estratégia de implementação a utilizar no seu ambiente. Por exemplo, poderá criar a ADR e ter por alvo uma coleção de clientes de teste. Depois de verificar se as atualizações de software estão instaladas no grupo de teste, pode adicionar uma nova implementação à regra ou alterar a coleção na implementação automática para uma coleção de destino que inclua um conjunto maior de clientes. Os objetos de atualização de software que são criados pelas ADRs são interativos.  

-   As atualizações de software que foram implementadas através da utilização de uma ADR são implementadas automaticamente em novos clientes adicionados à coleção de destino.  
-   Novas atualizações de software adicionadas a um grupo de atualização de software são implementadas automaticamente aos clientes na coleção de destino.  
-   Pode ativar ou desativar implementações em qualquer altura para a ADR.  

Depois de criar uma ADR, pode adicionar mais implementações à regra. Isto pode ajudá-lo a gerir a complexidade da implementação de diferentes atualizações em diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação e cada nova implementação que adiciona:  

-   Utiliza a mesma atualização de grupo e pacote, que é criado quando a ADR é executada pela primeira vez  
-   Pode especificar uma coleção diferente  
-   Suporta propriedades de implementação exclusivas, incluindo:  
   -   Hora de ativação  
   -   Prazo  
   -   Mostrar ou ocultar a experiência do utilizador final  
   -   Separa alertas para esta implementação  

Para obter passos detalhados, consulte [implementar automaticamente atualizações de software](automatically-deploy-software-updates.md)

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->
