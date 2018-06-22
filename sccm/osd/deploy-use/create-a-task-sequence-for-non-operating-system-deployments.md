---
title: Criar uma sequência de tarefas para implementações do sistema de operativo
titleSuffix: Configuration Manager
description: Crie sequências de tarefas que não estão relacionadas com a implementação de sistemas operativos, tais como a distribuição de software, atualizar controladores, editar Estados do utilizador, etc.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42c56b048afe768cd04cd5c91d659535ad5ffc9e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347489"
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Criar uma sequência de tarefas para implementações do sistema de operativo com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Sequências de tarefas no System Center Configuration Manager são utilizadas para automatizar uma variedade de tarefas no seu ambiente. Estas tarefas são principalmente concebidas e testadas para implementar sistemas operativos.  O Configuration Manager tem muitas outras funcionalidades que devem ser a tecnologia central que utiliza para cenários como [instalação da aplicação](../../apps/understand/introduction-to-application-management.md), [instalação de atualizações de software](../../sum/understand/software-updates-introduction.md), [configuração definição](../../compliance/understand/ensure-device-compliance.md), ou automatização personalizada. Existem outras tecnologias de automatização do Microsoft System Center, tais como [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) e [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) que também deve ter em conta.  

O poder das sequências de tarefas reside na respetiva flexibilidade e como pode utilizá-las para configurar definições de cliente, distribuir software, atualizar controladores, editar Estados do utilizador e efetuar outras tarefas independentes da implementação do sistema operativo. Pode criar uma sequência de tarefas personalizada para adicionar qualquer número de tarefas. A utilização de sequências de tarefas personalizadas para implementação do sistema de operativo é suportada no Configuration Manager. No entanto, se um resultados de sequência de tarefas nos resultados inconsistentes ou indesejáveis, observe formas para simplificar a operação. Pode conseguir isto, utilizando os passos mais simples, dividindo as ações em sequências de tarefas múltiplas, ou efetuando uma faseada abordagem para criar e testar a sequência de tarefas.

 Os seguintes passos são suportados para utilização de uma sequência de tarefas personalizada de implementação do sistema de operativo:  

-   [Verificar preparação](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Ligar à pasta de rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Transferir conteúdo do pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Instalar a aplicação](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Instalar pacote](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Instalar atualizações de Software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Reiniciar computador](../understand/task-sequence-steps.md#BKMK_RestartComputer)   

-   [Executar linha de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Executar Script do PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Definir variáveis dinâmicas](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Definir variável da sequência de tarefas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Passos seguintes 
[Implementar a sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
