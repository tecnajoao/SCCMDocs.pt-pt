---
title: Suporte para o servidor proxy
titleSuffix: Configuration Manager
description: Saiba como servidores de sistema de sites do Configuration Manager utilizam servidores proxy.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5123bd51de9678666b28ec464e811dafdd91a30d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156564"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Suporte de servidor proxy no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Alguns servidores de sistema de sites do Configuration Manager exigem ligações à internet. Se o seu ambiente requer tráfego de internet para utilizar um servidor proxy, configure estas funções de sistema de sites para usar o proxy.  

-   Um computador que aloja um servidor de sistema de sites suporta uma configuração de servidor proxy. Todas as funções de sistema de sites nesse computador partilhem esta mesma configuração de proxy. Se precisar de separar servidores proxy para funções diferentes ou instâncias de uma função, coloca essas funções em servidores de sistema de sites separados.  

-   Ao configurar novas definições de servidor de proxy para um servidor de sistema de sites que já tenha uma configuração de servidor proxy, a configuração original é substituída.  

-   Por predefinição, as ligações ao proxy utilizam a **sistema** conta do computador que aloja a função de sistema de sites.  

-   Se a conta de computador não é possível efetuar a autenticação, o servidor de sistema de sites pode armazenar credenciais de utilizador para ligar ao servidor proxy. Estas credenciais são os **conta de servidor de proxy do sistema de sites**.  



## <a name="site-system-roles-that-use-a-proxy"></a>Funções de sistema de sites que utilizar um proxy

As seguintes funções de sistema de sites ligam à internet e, se necessário, podem utilizar um servidor proxy:  


#### <a name="asset-intelligence-synchronization-point"></a>Ponto de sincronização do Asset Intelligence
Esta função de sistema de sites liga à Microsoft e utiliza uma configuração de servidor proxy no computador que aloja o ponto de sincronização do Asset Intelligence.  


#### <a name="cloud-distribution-point"></a>Ponto de distribuição de nuvem
A distribuição de nuvem do ponto de execuções de função no Microsoft Azure. Não configurar esta função de sistema de sites para utilizar um proxy. Defina a configuração de proxy no servidor do site primário que gere o ponto de distribuição de nuvem.  

Para esta configuração, o servidor do site primário:  

-   Tem de ser capaz de se ligar ao Microsoft Azure para configurar, monitorizar e distribuir conteúdo ao ponto de distribuição de nuvem.  

-   Por predefinição, utiliza o computador **sistema** conta para estabelecer a ligação. Também pode utilizar conta de servidor de proxy do sistema de sites, se necessário.  

-   Usa o navegador da web APIs do Windows.  


#### <a name="exchange-server-connector"></a>Conector do Exchange Server
Esta função de sistema de sites liga-se a um Exchange Server. Ele usa uma configuração de servidor proxy no computador que aloja o conector do Exchange Server.  


#### <a name="service-connection-point"></a>Ponto de ligação de serviço
Esta função de sistema de sites liga ao serviço de nuvem do Configuration Manager para transferir atualizações de versões para o Configuration Manager e liga-se ao Microsoft Intune numa configuração híbrida. Ele usa um servidor proxy que está configurado no computador que aloja o ponto de ligação de serviço.  


#### <a name="software-update-point"></a>Ponto de atualização de software
Esta função de sistema de sites utiliza o proxy para estabelecer a ligação ao Microsoft Update para transferir patches e sincronizar informações sobre atualizações. Como todos os outra função sistema de sites, primeiro de configurar as definições de proxy do sistema de site. Em seguida, configure as seguintes opções específicas para o ponto de atualização de software:  

-   **Utilizar um servidor proxy para sincronizar atualizações de software**  

-   **Utilizar um servidor proxy quando transferir conteúdo usando regras de implementação automática**  

    > [!Note]  
    > Embora esteja disponível para utilização, esta definição não é utilizada pelos pontos de atualização de software em sites secundários.  

Estas definições são sobre o **definições de conta de Proxy e** separador de propriedades de ponto de atualização de software.  

> [!NOTE]  
>  Por predefinição, quando são executadas as regras de implementação automática, o **sistema** conta no servidor do site do site no qual foi criada uma regra de implementação automática é utilizada para ligar à internet e transferir atualizações de software. Em alternativa, configure e utilize a conta de servidor proxy do sistema de sites. 
>   
>  Quando esta conta não é possível aceder à internet, as atualizações de software não conseguirem transferir. A entrada seguinte é registada em **ruleengine**:  
> `Failed to download the update from internet. Error = 12007.`  



## <a name="configure-the-proxy-for-a-site-system-server"></a>Configurar o proxy para um servidor de sistema de sites  

1.  Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração do Site**e, em seguida, selecione a **servidores e funções de sistema de sites** nó.  

2.  Selecione o servidor de sistema de sites que pretende editar. No painel de detalhes, clique com botão direito a **sistema de sites** função e selecione **propriedades**.  

3.  No sistema de sites propriedades, mude para o **Proxy** separador. Configure as seguintes definições de proxy:  

    - **Utilizar um servidor proxy ao sincronizar informações da internet**: Selecione esta opção para ativar o servidor de sistema de sites utilizar um servidor proxy.  

    - **Nome do servidor proxy**: Especifique o nome de anfitrião ou o FQDN do servidor proxy no seu ambiente.  

    - **Porta**: Especifique a porta de rede em que pretende comunicar com o servidor de proxy. Por predefinição, utiliza a porta **80**.  

    - **Utilizar credenciais para ligar ao servidor proxy**: Muitos servidores de proxy exigem que um utilizador autenticar. Por predefinição, o servidor de sistema de sites utiliza sua conta de computador para se ligar ao servidor proxy. Se necessário, ative esta opção, clique em **definir**e, em seguida, escolha um **conta existente** ou especificar uma **nova conta**. Estas credenciais são os **conta de servidor de proxy do sistema de sites**.  Para obter mais informações, consulte [contas utilizadas no Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).  

4.  Escolher **OK** para guardar o proxy de nova configuração de servidor.  
