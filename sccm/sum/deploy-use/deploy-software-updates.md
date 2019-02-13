---
title: Implementar atualizações de software
titleSuffix: Configuration Manager
description: Saiba como manual ou automaticamente implementar atualizações de software na consola do Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.collection: M365-identity-device-management
ms.openlocfilehash: cabcb57a429e0fb14732cead98902ca5b43957af
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156768"
---
# <a name="deploy-software-updates"></a>Implementar atualizações de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A fase de implementação da atualização de software é o processo de implementar as atualizações de software. Não importa como implementar atualizações de software, o site:
- Adiciona as atualizações a um grupo de atualização de software
- Distribui o conteúdo da atualização para pontos de distribuição
- Implementa o grupo de atualização de clientes  

Depois de criar a implementação, o site envia uma política de atualização de software associados a clientes de destinados. Os clientes transferem os ficheiros de conteúdo de atualização de software a partir de uma origem de conteúdo para a respetiva cache local. Os clientes da internet sempre transferir conteúdo do serviço de nuvem do Microsoft Update. As atualizações de software, em seguida, estão disponíveis para instalação pelo cliente.   

> [!Tip]  
>  Se um ponto de distribuição não estiver disponível, os clientes da intranet também podem transferir as atualizações de software do Microsoft Update.  

> [!NOTE]  
>  Ao contrário de outros tipos de implementação, atualizações de software são todos transferidas para a cache do cliente. Isto é, independentemente da definição de tamanho máximo da cache no cliente. Para obter mais informações sobre a definição de cache do cliente, consulte [configurar a cache do cliente para clientes do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  

Se configurar uma implementação da atualização de software necessária, as atualizações de software são instaladas automaticamente no prazo agendado. Em alternativa, o utilizador no computador cliente pode agendar ou iniciar a instalação da atualização de software antes do termo do prazo. Após a instalação tentada, os computadores cliente enviam mensagens de estado de volta para o servidor de site para indicar se a instalação da atualização de software foi concluída com êxito. Para obter mais informações sobre implementações de atualização de software, veja [Fluxos de trabalho de implementação de atualizações de software](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentWorkflows).  

Existem três cenários principais para implementar atualizações de software: 
- [Implementação manual](#BKMK_ManualDeployment)  
- [Implementação automática](#bkmk_auto)  
- [Implementação faseada](#bkmk_phased)  

Normalmente, começa ao implementar manualmente atualizações de software para criar uma linha de base para seus clientes e, em seguida, gerir atualizações de software nos clientes, utilizando um automático ou por fases de implementação.  

> [!Note]  
> Não é possível utilizar uma regra de implementação automática com uma implementação faseada.



## <a name="BKMK_ManualDeployment"></a> Implementar manualmente atualizações de software
Selecione as atualizações de software na consola do Configuration Manager e iniciar manualmente o processo de implantação. Geralmente usa este método de implementação para:  

- Obter os clientes atualizados com atualizações de software necessárias antes de criar regras de implementação automática que gerir implementações mensais  

- Implementar atualizações de software fora de banda  


A lista seguinte apresenta o fluxo de trabalho geral para a implementação manual de atualizações de software:  

1. Filtre para atualizações de software que utilizam requisitos específicos. Por exemplo, fornece critérios que obtém todas as atualizações de software crítico que são necessárias em mais de 50 clientes ou de segurança.  

2. Crie um grupo de atualização de software que contém as atualizações de software.  

3. Transfira o conteúdo das atualizações de software no grupo de atualização de software.  

4. Implemente manualmente o grupo de atualização de software.  

Para obter mais informações e passos detalhados, consulte [implementar manualmente atualizações de software](manually-deploy-software-updates.md).

> [!Tip]  
> Ao implementar manualmente atualizações de cliente do Office 365, encontrá-los no **atualizações do Office 365** no nó **gestão de clientes do Office 365** do **biblioteca de Software** área de trabalho.  



## <a name="bkmk_auto"></a> Implementar automaticamente atualizações de software

Configure a implementação de atualizações de software automáticas, utilizando uma regra de implementação automática (ADR). Este método de implementação é comum para atualizações de software mensais (geralmente conhecidas como "Patch Terça") e para gerir atualizações de definições. Definir os critérios para uma ADR automatizar o processo de implantação. A lista seguinte apresenta o fluxo de trabalho geral para implementar automaticamente atualizações de software:  

1.  Crie uma ADR que especifique as definições de implementação.  

2.  O site adiciona as atualizações de software a um grupo de atualização de software.  

3.  O site implementa o grupo de atualizações de software para os clientes da coleção de destino.  

Primeiro, determine sua estratégia de implementação de atualização de software automáticas. Por exemplo, crie a ADR para destino inicialmente uma coleção de clientes de teste. Depois de verificar que o grupo de teste instalado com êxito as atualizações de software, adicione uma nova implementação à regra. Também pode alterar a coleção de destino da implementação existente para um que inclui um conjunto maior de clientes. Considere os seguintes comportamentos decisão sobre a estratégia a utilizar:  

- Pode modificar as propriedades dos objetos de atualização de software que cria a ADR.   

- A ADR implementa automaticamente as atualizações de software nos clientes, quando os adicionar à coleção de destino.  

- Quando ou a ADR adiciona novas atualizações de software para o grupo de atualizações de software, o site implementa-las automaticamente para os clientes da coleção de destino.  

- Ativar ou desativar implementações em qualquer altura para a ADR.  


Depois de criar uma ADR, adicione implementações adicionais para a regra. Esta ação ajuda a gerir a complexidade da implantação de atualizações de diferentes para diferentes coleções. Cada nova implementação tem acesso a todas as funcionalidades e à experiência de monitorização da implementação.  

Cada nova implementação que adiciona:  

- Utiliza o mesmo atualizar grupo e pacote, que a ADR cria quando é executada pela primeira vez  
- Pode visar uma coleção diferente  
- Suporta propriedades de implementação exclusivas, incluindo:  
  -   Hora de ativação  
  -   Prazo  
  -   Experiência de utilizador  
  -   Alertas separadas para cada implementação  


Para obter mais informações e passos detalhados, consulte [implementar automaticamente atualizações de software](automatically-deploy-software-updates.md)



## <a name="bkmk_phased"></a> Implementar atualizações de software em fases

<!--1358146--> A partir da versão 1810, crie implementações faseadas para atualizações de software. As implementações faseadas permitem-lhe organizar uma implementação coordenada e sequenciada de software com base em critérios personalizáveis e grupos.

Para obter mais informações, consulte [criar implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

