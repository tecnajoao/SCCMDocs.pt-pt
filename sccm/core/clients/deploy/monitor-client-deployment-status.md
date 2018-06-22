---
title: Monitorizar o estado de implementação do cliente
titleSuffix: Configuration Manager
description: Monitorizar o estado de implementação do cliente no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9454183b390a6ff0267ac853f514ce87530c1519
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32331755"
---
# <a name="how-to-monitor-client-deployment-status-in-system-center-configuration-manager"></a>Como monitorizar o estado de implementação do cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A implementação de clientes no seu site demora algum tempo e algumas instalações não são bem sucedidas à primeira vez. A consola do System Center Configuration Manager fornece uma forma atento em implementações de cliente numa coleção pelo relatório de estado de implementação do cliente em tempo real.  

> [!NOTE]  
>  A forma de melhor e mais fiável de monitorizar a implementação do cliente é com a consola do Configuration Manager (como descrito neste artigo). A secção **Estado do Cliente** da área de trabalho **Monitorização** na consola mostra o estado da implementação do cliente com precisão e em tempo real. Pode monitorizar as implementações de cliente com outras ferramentas, como o Gestor de Servidores no Windows Server ou o System Center Operations Manager, mas pode receber alarmes da atividade normal de instalação de cliente. Devido à maneira como o programa de instalação de cliente (CCMSetup.exe) é executado em vários ambientes, estas outras ferramentas podem gerar alarmes e avisos falsos que não refletem com precisão o estado das implementações de cliente.  

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

-   Se pretender alterar o âmbito do relatório, clique em **procurar...**  e escolha uma coleção diferente.  

 Para obter mais informações sobre implementações de cliente de pré-produção, consulte [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).

 > [!NOTE]
 > O estado de implementação em computadores que alojam funções do sistema de sites de uma coleção de pré-produção, pode ser comunicado como **não compatíveis** , mesmo quando o cliente foi implementado com êxito. Ao promover o cliente para produção, o estado de implementação é reportado corretamente.   

 Para monitorizar o estado dos clientes implementados, veja [Como monitorizar clientes no System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md)  

 Pode utilizar os relatórios do Configuration Manager para obter mais informações sobre o estado de clientes do site. Para obter mais informações sobre como executar relatórios, veja [Os relatórios do System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
