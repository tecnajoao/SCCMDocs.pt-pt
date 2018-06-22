---
title: Suporte para o servidor proxy
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte do System Center Configuration Manager para servidores de proxy que utilizam servidores do sistema de sites e clientes.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 480ab29bbd97f2cdc173019b1b3cccd90403d011
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337824"
---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>Suporte para o servidor proxy no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ambos os clientes e servidores de sistema de sites do System Center Configuration Manager, podem utilizar um servidor proxy.  

## <a name="site-system-servers"></a>Servidores do sistema de sites  
Quando precisam de funções de sistema de sites estabelecer ligação à Internet, pode configurar para utilizar um servidor proxy.  

-   Um computador que aloja um servidor de sistema de sites suporta uma configuração de servidor proxy que é partilhada por todas as funções de sistema de sites nesse mesmo computador. Se precisar de separar servidores proxy para funções diferentes ou instâncias de uma função, tem de colocar essas funções em servidores de sistema de sites à parte.  

-   Quando configurar novas definições do servidor proxy para um servidor de sistema de sites que já tem uma configuração de servidor proxy, a configuração original é substituída.  

-   As ligações ao proxy utilizam a conta do **Sistema** do computador que aloja a função de sistema de sites.  

As seguintes funções do sistema de sites ligam à Internet e podem exigir um servidor proxy.  Com uma exceção, as funções de sistema de sites que podem utilizar um proxy fazem-no sem qualquer configuração adicional. A exceção é o ponto de atualização de software. A lista seguinte tem informações sobre as configurações adicionais que necessite de um ponto de atualização de software:  

**O ponto de sincronização do Asset Intelligence** -esta função de sistema de sites liga à Microsoft e utiliza uma configuração de servidor proxy no computador que aloja o ponto de sincronização do Asset Intelligence.  

**Ponto de distribuição baseado na nuvem** - para configurar um servidor proxy para um ponto de distribuição baseado na nuvem, pode configurar o proxy no site primário que gere o ponto de distribuição baseados na nuvem.  

Para esta configuração, o servidor do site primário:  

-   Tem de ser capaz de ligar ao Microsoft Azure para configurar, monitorizar e distribuir conteúdo ao ponto de distribuição.  

-   Utiliza a conta do sistema nesse computador para efetuar a ligação.  

-   Utiliza o browser predefinido de nesse computador.  

Não é possível configurar um servidor proxy no ponto de distribuição em nuvem com base no Microsoft Azure.  

**Ponto de ligação da nuvem** -esta função de sistema de sites liga ao serviço de nuvem do Configuration Manager para transferir atualizações de versão para o Configuration Manager e utiliza um servidor proxy que está configurado no computador que aloja a ligação de serviço ponto.  

**Conector do Exchange Server** -esta função de sistema de sites liga a um Exchange Server e utiliza uma configuração de servidor proxy no computador que aloja o conector do Exchange Server.  

**Ponto de ligação de serviço** -esta função de sistema de sites liga-se ao Microsoft Intune e utiliza uma configuração de servidor proxy no computador que aloja o ponto de ligação de serviço.  

**Ponto de atualização de software** - Esta função do sistema de site pode utilizar a proxy ao ligar o Microsoft Update para transferir patches e sincronizar informações sobre atualizações. Pontos de atualização de software utilizam uma proxy apenas para as opções seguintes quando ativa essa opção, como configurar o ponto de atualização de software:  

-   **Utilizar um servidor proxy para sincronizar atualizações de software**  

-   **Utilizar um servidor proxy quando transferir conteúdo usando regras de implementação automática** (embora esteja disponível para utilização, esta definição não é utilizada pelos pontos de atualização de software em sites secundários.)  

Configurar as definições do servidor proxy na página ponto de atualização de Software ativo do Assistente Adicionar funções do sistema de sites ou no **geral** separador **propriedades de componente de ponto de atualização de Software**.  

-   As definições do servidor proxy estão associadas apenas ao ponto de atualização de software no site.  

-   As opções de servidor proxy apenas estão disponíveis quando um servidor proxy já está definido para o servidor de sistema de sites que aloja o ponto de atualização de software.  

> [!NOTE]  
>  Por predefinição, a conta **Sistema** para o servidor onde foi criada uma regra de implementação automática é utilizada para ser ligada à Internet e transferir atualizações de software quando são executadas as regras de implementação automática.  
>   
>  Quando esta conta não é possível aceder à Internet, as atualizações de software falharem transferir e a entrada seguinte é registada em ruleengine.log: **Falha ao transferir a atualização a partir da internet. Erro = 12007.**  

#### <a name="to-set-up-the-proxy-server-for-a-site-system-server"></a>Para configurar o servidor proxy para um servidor de sistema de sites  

1.  Na consola do Configuration Manager, escolha **administração**, expanda **configuração do Site**e, em seguida, escolha **servidores e funções de sistema de sites**.  

2.  Selecione o servidor de sistema de site que pretende editar, no contexto de painel de detalhes **sistema de sites**e, em seguida, escolha **propriedades**.  

3.  Nas propriedades do sistema de sites, selecione o **Proxy** separador e, em seguida, configure as definições de proxy para este servidor de site primário.  

4.  Escolha **OK** para guardar o proxy de nova configuração de servidor.  
