---
title: "Monitorizar o estado de implementação de cliente | Documentos do Microsoft"
description: "Monitorizar o estado de implementação de cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
caps.latest.revision: 11
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 3d9d02d8c56aea17e563112f92173c2b56781da6
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-monitor-client-deployment-status-in-system-center-configuration-manager"></a>Como monitorizar o estado de implementação do cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A implementação de clientes no seu site demora algum tempo e algumas instalações não são bem sucedidas à primeira vez. A consola do System Center Configuration Manager fornece uma forma de estar atento implementações de clientes numa coleção pelo relatório de estado de implementação do cliente em tempo real.  

> [!NOTE]  
>  A forma melhor e mais fiável para monitorizar a implementação do cliente é com a consola do Configuration Manager (como descrito neste artigo). A secção **Estado do Cliente** da área de trabalho **Monitorização** na consola mostra o estado da implementação do cliente com precisão e em tempo real. Pode monitorizar as implementações de cliente com outras ferramentas, como o Gestor de Servidores no Windows Server ou o System Center Operations Manager, mas pode receber alarmes da atividade normal de instalação de cliente. Devido à maneira como o programa de instalação de cliente (CCMSetup.exe) é executado em vários ambientes, estas outras ferramentas podem gerar alarmes e avisos falsos que não refletem com precisão o estado das implementações de cliente.  

 Na área de trabalho **Monitorização** da consola, pode monitorizar os seguintes estados para as implementações de cliente executadas numa coleção que especificar:  

-   Compatível  

-   Em curso  

-   Não compatível  

-   Falhou  

-   Desconhecido  

 Os relatórios do Gestor de Configuração sobre implementações para clientes de produção ou de clientes de pré-produção. A consola do Configuration Manager também fornece um gráfico das implementações de cliente falhadas durante um determinado período de tempo para o ajudar a determinar se as ações que toma para resolver implementações estão a melhorar a taxa de sucesso de implementação com o tempo.  

## <a name="to-monitor-client-deployments"></a>Monitorizar as implementações do cliente  

-   Na consola do Configuration Manager, clique em **monitorização** > **estado do cliente**.  

-   Clique em **Implementação do Cliente de Produção** ou em **Implementação do Cliente de Pré-produção** consoante a versão do cliente que pretende monitorizar.  

-   Reveja os gráficos do estado de implementação do cliente e de falha de implementação do cliente.  

-   Se pretender alterar o âmbito do relatório, clique em **procurar...**  e selecione uma coleção diferente.  

 Para obter mais informações sobre implementações de cliente de pré-produção, consulte o artigo [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).

 > [!NOTE]
 > Será possível reportar o estado de implementação em computadores que alojam funções de sistema de sites numa coleção de pré-produção como **não compatíveis** mesmo quando o cliente foi implementado com êxito. Ao promover o cliente para produção, o estado de implementação é reportado corretamente.   

 Para monitorizar o estado dos clientes implementados, veja [Como monitorizar clientes no System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md)  

 Pode utilizar os relatórios do Configuration Manager para saber mais informações sobre o estado de clientes no seu site. Para obter mais informações sobre como executar relatórios, veja [Os relatórios do System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

