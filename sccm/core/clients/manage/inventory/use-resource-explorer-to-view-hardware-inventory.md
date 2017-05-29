---
title: "Exibir o inventário de hardware | Microsoft Docs | Gerenciador de recursos"
description: "Use o Gerenciador de recursos para exibir o inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: e39fa60a5d215fa1b0a98d4463058497e63a4d4f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/29/2017


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Como utilizar o Explorador de Recursos para ver o inventário de hardware no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Use o Gerenciador de recursos no System Center Configuration Manager para exibir informações sobre o inventário de hardware que foi coletado dos clientes em sua hierarquia.  

> [!NOTE]  
>  O Explorador de Recursos não apresentará quaisquer dados de inventário até ser executado um ciclo de inventário de hardware no cliente ao qual está a ligar.  

 Gerenciador de recursos tem as seguintes seções relacionadas ao inventário de hardware:  

-   **Hardware** -contém o inventário de hardware mais recente coletado do dispositivo cliente especificado.  **Status de estação de trabalho** tem a hora e data quando o dispositivo executou um inventário de hardware pela última vez.  

-   **Histórico de hardware** -contém um histórico de inventariado itens que foram alterados desde o último inventário de hardware ocorreu. Cada item contém um **atual** nó e um ou mais *< data\>*  nós. Você pode comparar as informações do nó atual para um de nós do históricos para descobrir os itens que foram alterados.  

    > [!NOTE]  
    >  Configuration Manager retém o histórico de inventário de hardware para o número de dias que você especifica na **Excluir histórico antigo de inventário** tarefas de manutenção do site  

> [!NOTE]  
>  Para obter informações sobre como visualizar o inventário de hardware a partir de clientes que executam o Linux e UNIX, veja [Como monitorizar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Como executar o Explorador de Recursos a partir da consola do Configuration Manager  

1.  No console do Configuration Manager, escolha **ativos e conformidade** > **dispositivos**, ou abra qualquer coleção que exiba dispositivos.  

3.  Escolha o computador que contém o estoque que você deseja exibir e, em seguida, o **início** guia > **dispositivos** grupo, escolha **iniciar** >  **Gerenciador de recursos**.   

4.  Clique qualquer item no painel à direita do **Resource Explorer** janela e escolha **propriedades** para abrir o *< nome do item\>***propriedades** caixa de diálogo para exibir as informações de inventário coletadas em um formato mais legível.  


