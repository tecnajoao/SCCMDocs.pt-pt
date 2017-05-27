---
title: Suporte de servidor proxy | Documentos do Microsoft
description: Saiba mais sobre o suporte do System Center Configuration Manager para os servidores de proxy que utilizam servidores de sistema de sites e clientes.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c4f30e4839709722b216262b21d7b51c07d24d1e
ms.openlocfilehash: dc36be47310d2c2178c974a2b503d0b5f9f6e2ec
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>Suporte para o servidor proxy no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Servidores de sistema de sites do System Center Configuration Manager e os clientes podem utilizar um servidor proxy.  

## <a name="site-system-servers"></a>Servidores do sistema de sites  
Quando precisar de funções do sistema de sites estabelecer ligação à Internet, pode configurá-los para utilizar um servidor proxy.  

-   Um computador que aloja um servidor de sistema de sites suporta uma configuração de servidor proxy que é partilhada por todas as funções de sistema de sites nesse mesmo computador. Se precisar de separar servidores proxy para funções diferentes ou instâncias de uma função, tem de colocar essas funções nos servidores do sistema de sites separadas.  

-   Quando configurar novas definições de servidor proxy para um servidor de sistema de sites que já tenha uma configuração de servidor proxy, a configuração original será substituída.  

-   As ligações ao proxy utilizam a conta do **Sistema** do computador que aloja a função de sistema de sites.  

As seguintes funções de sistema de sites liga à Internet e podem exigir um servidor proxy.  Com uma exceção, as funções de sistema de sites que podem utilizar um proxy fazem-no sem qualquer configuração adicional. A exceção é o ponto de atualização de software. A lista seguinte contém informações sobre as configurações adicionais que necessite de um ponto de atualização de software:  

**Ponto de sincronização do Asset Intelligence** -esta função do sistema de sites liga à Microsoft e utiliza uma configuração de servidor proxy no computador que aloja o ponto de sincronização do Asset Intelligence.  

**Ponto de distribuição baseado na nuvem** - para configurar um servidor proxy para um ponto de distribuição baseado na nuvem, pode configurar o proxy no site primário que gere o ponto de distribuição baseado na nuvem.  

Para esta configuração, o servidor do site primário:  

-   Tem de ser capaz de ligar ao Microsoft Azure para configurar, monitorizar e distribuir conteúdo ao ponto de distribuição.  

-   Utiliza a conta do sistema nesse computador para estabelecer a ligação.  

-   Utiliza o browser predefinido desse computador.  

Não é possível configurar um servidor proxy no ponto de distribuição em nuvem com base no Microsoft Azure.  

**Ponto de ligação da nuvem** -esta função do sistema de sites liga ao serviço de nuvem do Configuration Manager para transferir atualizações de versões para o Configuration Manager e utilizar um servidor proxy que está configurado no computador que aloja o ponto de ligação de serviço.  

**Conector do Exchange Server** -esta função do sistema de sites liga a um Exchange Server e utiliza uma configuração de servidor proxy no computador que aloja o conector do Exchange Server.  

**Ponto de ligação de serviço** -esta função do sistema de sites liga ao Microsoft Intune e utiliza uma configuração de servidor proxy no computador que aloja o ponto de ligação de serviço.  

**Ponto de atualização de software** - Esta função do sistema de site pode utilizar a proxy ao ligar o Microsoft Update para transferir patches e sincronizar informações sobre atualizações. Pontos de atualização de software utilizam um proxy apenas para as seguintes opções quando ativar essa opção, tal como configurar o ponto de atualização de software:  

-   **Utilizar um servidor proxy para sincronizar atualizações de software**  

-   **Utilizar um servidor proxy quando transferir conteúdo usando regras de implementação automática** (enquanto disponível para utilização, esta definição não é utilizada pelos pontos de atualização de software em sites secundários.)  

Configurar as definições do servidor proxy na página do Assistente para adicionar funções do sistema de sites ou no ponto de atualização de Software ativo o **geral** separador **propriedades de componente de ponto de atualização de Software**.  

-   As definições do servidor proxy estão associadas apenas ao ponto de atualização de software no site.  

-   Opções de servidor proxy apenas estão disponíveis quando um servidor proxy já está configurado para o servidor de sistema de sites que aloja o ponto de atualização de software.  

> [!NOTE]  
>  Por predefinição, a conta **Sistema** para o servidor onde foi criada uma regra de implementação automática é utilizada para ser ligada à Internet e transferir atualizações de software quando são executadas as regras de implementação automática.  
>   
>  Quando esta conta não é possível aceder à Internet, as atualizações de software não são transferidas e a entrada seguinte é registada para ruleengine. log: **Falha ao transferir a atualização a partir da internet. Erro = 12007.**  

#### <a name="to-set-up-the-proxy-server-for-a-site-system-server"></a>Para configurar o servidor proxy para um servidor de sistema de sites  

1.  Na consola do Configuration Manager, escolha **administração**, expanda **configuração do Site**e, em seguida, escolha **servidores e funções de sistema de sites**.  

2.  Selecione o servidor de sistema de sites que pretende editar, no contexto de painel de detalhes **sistema de sites**e, em seguida, escolha **propriedades**.  

3.  Nas propriedades do sistema de sites, selecione o **Proxy** separador e, em seguida, configure as definições de proxy para este servidor de site primário.  

4.  Escolher **OK** para guardar o proxy de nova configuração de servidor.  

