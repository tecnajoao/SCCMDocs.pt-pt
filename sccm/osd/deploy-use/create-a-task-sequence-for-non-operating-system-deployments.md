---
title: "Criar uma sequência de tarefas para implementações do sistema de operativo | Documentos do Microsoft"
description: "Crie sequências de tarefas que não estão relacionadas com a implementação de sistemas operativos, tais como a distribuição de software, atualizar controladores, edição dos Estados do utilizador, etc."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: b4b04907f2cd48d81e864e46ca47c14a0b98a9f7
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Criar uma sequência de tarefas para implementações do sistema de operativo com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Sequências de tarefas no System Center Configuration Manager são utilizadas para automatizar uma variedade de tarefas no seu ambiente. Estas tarefas são principalmente concebidas e testadas para implementar sistemas operativos.  O Configuration Manager possui muitas outras funcionalidades que devem ser a tecnologia primária que utiliza para cenários, tais como [instalação da aplicação](../../apps/understand/introduction-to-application-management.md), [instalação de atualizações de software](../../sum/understand/software-updates-introduction.md), [configuração definição](../../compliance/understand/ensure-device-compliance.md), ou automatização personalizada. Existem outras tecnologias de automatização do Microsoft System Center, tais como [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) e [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) que também deve ter em conta.  

Potência de sequências de tarefas situam-se no respetivo flexibilidade e como pode utilizá-los para configurar definições de cliente, distribua o software, atualizar controladores, editar dos Estados do utilizador e efetuar outras tarefas independentes da implementação do sistema operativo. Pode criar uma sequência de tarefas personalizada para adicionar qualquer número de tarefas. A utilização de sequências de tarefas personalizadas para implementação do sistema de operativo é suportada no Configuration Manager. No entanto, se um resultados de sequência de tarefas nos resultados indesejados ou inconsistentes, observe formas para simplificar a operação. Pode consegui-utilizando os passos mais simples, dividir as ações em vários sequências de tarefas, ou, efetuando um faseada abordagem de criar e testar a sequência de tarefas.

 Os seguintes passos são suportados para utilização numa sequência de tarefas personalizada a implementação do sistema de operativo:  

-   [Verificar disponibilidade](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Ligar à pasta de rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Transferir o conteúdo do pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Instalar aplicação](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Instalar pacote](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Instalar atualizações de Software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Reiniciar computador](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [Executar linha de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Executar Script do PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Definir variáveis dinâmicas](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Definir variável da sequência de tarefas](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Passos seguintes
[Implementar a sequência de tarefas](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)

