---
title: Criar uma sequência de tarefas para implementações do sistema de operativo
titleSuffix: Configuration Manager
description: Crie sequências de tarefas não relacionadas à implantação de sistemas operativos, tais como distribuição de software, atualizar controladores, editar Estados do utilizador, etc.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c8ef75ea9b0948a932c1b146d0f4fe7051017759
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140318"
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Criar uma sequência de tarefas para implementações não pertencentes ao sistema operativo com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Sequências de tarefas no System Center Configuration Manager são utilizadas para automatizar uma variedade de tarefas no ambiente. Estas tarefas são principalmente concebidas e testadas para implementar sistemas operativos.  O Configuration Manager possui muitos outros recursos que devem ser a tecnologia central que utiliza para cenários como [instalação do aplicativo](../../apps/understand/introduction-to-application-management.md), [instalação de atualizações de software](../../sum/understand/software-updates-introduction.md), [ configuração de definição](../../compliance/understand/ensure-device-compliance.md), ou automatização personalizada. Existem outras tecnologias de automatização do Microsoft System Center, tais como [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) e [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) que também deve ter em conta.  

O poder das sequências de tarefas reside na respetiva flexibilidade e como pode usá-los para configurar definições de cliente, distribuir software, atualizar controladores, editar Estados do utilizador e realizar outras tarefas independentes da implementação do sistema operativo. Pode criar uma sequência de tarefas personalizada para adicionar qualquer número de tarefas. A utilização de sequências de tarefas personalizadas para implementação do sistema de operativo é suportada no Configuration Manager. No entanto, se um resultados de sequência de tarefas nos resultados inconsistentes ou indesejáveis, buscar formas para simplificar a operação. Isso pode ser feito com os passos mais simples, dividindo as ações em várias sequências de tarefas, ou fazendo uma faseada abordar a criação e teste a sequência de tarefas.

 Os seguintes passos são suportados para utilização numa sequência de tarefas personalizados de implementação do sistema de operativo:  

-   [Verificar estado de preparação](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Ligar à pasta de rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Transferir conteúdo do pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Instalar aplicação](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Instalar pacote](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Instalar atualizações de Software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Reiniciar computador](../understand/task-sequence-steps.md#BKMK_RestartComputer)   

-   [Executar linha de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Executar Script do PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Definir variáveis dinâmicas](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Definir variável da sequência de tarefas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Passos seguintes 
[Implementar a sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
