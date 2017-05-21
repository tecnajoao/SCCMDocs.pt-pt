---

title: "Integração com o Windows Update para empresas no Windows 10 | Documentos do Microsoft"
description: "Utilize o Windows Update para empresas para manter os dispositivos baseados no Windows 10 na sua organização atualizados para dispositivos ligados ao serviço Windows Update."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.translationtype: Machine Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 8bdbacd54632475ac69a0d0a9a34b2567c3daa13
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integração com o Windows Update for Business no Windows 10

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Windows Update for Business (WUfB) permite-lhe manter os dispositivos baseados no Windows 10 da sua organização sempre atualizados com as mais recentes defesas e funcionalidades de segurança do Windows quando estes dispositivos se ligam diretamente ao serviço Windows Update (WU). O Configuration Manager possui a capacidade para fazer a distinção entre computadores Windows 10 que utilizam WUfB e o WSUS para obter as atualizações de software.  

 Algumas funcionalidades do Configuration Manager já não estão disponíveis quando os clientes do Configuration Manager estão configurados para receber atualizações do WU, que inclui WUfB ou Insiders do Windows:  

-   Relatórios de conformidade do Windows Update:  

    -   O Configuration Manager irá ter conhecimento das atualizações de que são publicadas WU. Clientes do Configuration Manager configurados para atualizações recebidas a partir do WU apresentará **desconhecido** para estas atualizações na consola do Configuration Manager.  

    -   Resolver o problema do estado de conformidade geral é difícil, porque o estado **desconhecido** destinava-se, anteriormente, apenas aos clientes que não tinham comunicado o estado da análise do WSUS.  Agora também inclui os clientes do Configuration Manager que recebem atualizações do WU.  

    -   Acesso condicional (para os recursos da empresa) com base no estado de conformidade de atualização não funcionará conforme esperado para os clientes que recebem atualizações a partir do WU porque iria satisfizerem nunca de compatibilidade do Configuration Manager.  

    -   A conformidade das Atualizações de Definições faz parte dos relatórios de conformidade de atualização gerais e também não funcionará conforme esperado.  A conformidade das atualizações de definições também faz parte da avaliação de acesso condicional  

-   Os relatórios globais do Endpoint Protection para o Defender baseados no estado de conformidade das atualizações não devolverão resultados precisos devido aos dados de análise em falta.  

-   O Configuration Manager não será possível implementar atualizações da Microsoft, tais como o Office, o Internet Explorer e o Visual Studio para clientes que estão ligados a WUfB receber atualizações.  

-   O Configuration Manager não poderá implementar atualizações de terceiros 3º publicadas no WSUS e geridas através do Configuration Manager para os clientes que estão ligados a WUfB a receber atualizações.  

-   Implementação de cliente completa do Configuration Manager que utiliza a infraestrutura de atualizações de software não irá funcionar para clientes que estão ligados a WUfB a receber atualizações.  

## <a name="identify-clients-that-use--wufb-for-windows-10-updates"></a>Identificar clientes que utilizam o WUfB para atualizações do Windows 10  
 Utilize o procedimento seguinte para identificar os clientes que utilizam o WUfB para obter atualizações do Windows 10, configurar estes clientes para deixarem de utilizar o WSUS para obter atualizações e implementar uma definição do agente de cliente para desativar o fluxo de trabalho de atualizações de software nestes clientes.  

 **Pré-requisitos**  

-   Clientes com Windows 10 Desktop Pro ou Windows 10 Enterprise Edition, versão 1511 ou posterior  

-   O[Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) é implementado e os clientes utilizam o WUfB para obter atualizações do Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Para identificar os clientes que utilizam o WUfB  

1.  Desative o Agente do Windows Update para que não faça análises no WSUS, se tiver sido ativado previamente.   
    A chave de registo **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** pode ser definida para indicar se o computador é análise contra WSUS ou o Windows Update.  Quando o valor é 2, não é análise contra WSUS.  

2.  Existe um novo atributo **UseWUServer**, no **Windows Update** nó no Explorador de recursos do Configuration Manager.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores ligados através de WUfB para obter atualizações e melhoramentos.  

4.  Crie uma definição de agente de cliente para desativar o fluxo de trabalho de atualização de software e implemente-a na coleção de computadores ligados diretamente ao WUfB.  

5.  Os computadores que são geridos através de WUfB apresentará **desconhecido** no estado de compatibilidade e não irá ser contados como parte da percentagem de conformidade geral.  

