---
title: "Cache de mesmo nível do cliente | System Center Configuration Manager"
description: "Use o Cache par para locais de origem de conteúdo do cliente durante a implantação de conteúdo com o System Center Configuration Manager."
ms.custom: na
ms.date: 7/3/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: ed6b65a1a5aabc0970cd0333cb033405cf6d2aea
ms.openlocfilehash: 94802680747a3d371716c1b345b2cba098150716
ms.contentlocale: pt-pt
ms.lasthandoff: 07/03/2017

---

# <a name="peer-cache-for-configuration-manager-clients"></a>Cache de sistemas pares para clientes do Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Começando com o System Center Configuration Manager versão 1610, você pode usar **Cache par** para ajudar a gerenciar a implantação de conteúdo para clientes em locais remotos. Cache de mesmo nível é uma solução interna do Configuration Manager que permite que os clientes compartilhem conteúdo com outros clientes diretamente do seu cache local.   

> [!TIP]  
> Introduzida com a versão 1610, Cache de mesmo nível e o painel de fontes de dados do cliente são recursos de pré-lançamento. Para habilitá-las, consulte [usar recursos de pré-lançamento de atualizações](/sccm/core/servers/manage/pre-release-features).

## <a name="overview"></a>Descrição Geral
Um cliente de Cache de mesmo nível é um cliente do Configuration Manager que está habilitado para usar o Cache par. Um cliente que possui o conteúdo pode compartilhar com outros clientes de Cache de mesmo nível é uma fonte de Cache de mesmo nível.
 -  Você pode usar as configurações do cliente para permitir que os clientes usar o Cache par.
 -  Para compartilhar conteúdo como uma fonte de Cache de mesmo nível, um cliente de Cache de mesmo nível:
    -  Deve ser ingressado no domínio. No entanto, um cliente que não está associado a um domínio pode obter o conteúdo de um domínio ingressou na fonte de Cache par.
    -  Deve ser um membro do grupo de limite atual do cliente que está procurando o conteúdo. Um cliente de Cache de mesmo nível em um grupo de limites de vizinho não está incluído com o pool de locais de origem de conteúdo disponíveis quando um cliente usa fallback para conteúdo de um grupo de limites de vizinho de busca. Para obter mais informações sobre grupos de limite atuais e próximos, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Cada tipo de conteúdo que é mantido no cache de um cliente do Configuration Manager pode ser atendido para outros clientes usando o Cache de mesmo nível.
 -  Cache de mesmo nível não substitui o uso de outras soluções como o BranchCache, mas trabalha lado a lado com ele para fornecer mais opções para estender as soluções tradicionais de implantação de conteúdo, como pontos de distribuição. Esta é uma solução personalizada com nenhuma dependência de BranchCache, portanto, se você não habilitar ou usar o Windows BranchCache, ele ainda funciona.

### <a name="operations"></a>Operações

Depois de implantar configurações de cliente que habilitar o Cache de mesmo nível em uma coleção, os membros da coleção podem agir como uma fonte de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites:
 -  Um cliente que funciona como uma fonte de conteúdo ponto a ponto envia uma lista de conteúdo armazenado em cache disponível para seu ponto de gerenciamento.
 -  Em seguida, quando o próximo cliente no grupo de limite solicita que o conteúdo, cada fonte de cache de mesmo nível que tem o conteúdo é retornado como uma possível fonte de conteúdo juntamente com os pontos de distribuição e outros locais de origem de conteúdo no grupo de limite.
 -  Por que o processo de operação normal, o cliente que está procurando o conteúdo seleciona uma fonte de conteúdo do conjunto de fontes que ele foi fornecido e, em seguida, prossegue para tentar obter o conteúdo.

> [!NOTE]
> Se o fallback para um grupo de limites de vizinho de conteúdo ocorre, o Cache par locais de origem de conteúdo do grupo de limite de vizinho não são adicionados ao pool do cliente potencial conteúdo de locais de origem.  


Embora seja possível fazer todos os clientes participem como uma fonte de cache de mesmo nível, ele é uma prática recomendada para escolher somente a clientes que são mais adequada para sendo par fontes de cache.  A adequação de clientes pode ser avaliada com base no tipo de chassi do cliente, espaço em disco, conectividade de rede e muito mais. Para obter mais informações que podem ajudá-lo a selecionar os melhores clientes usem para o Cache par, consulte [este blog por um consultor de Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Acesso limitado a uma fonte de cache de mesmo nível**  
A partir da versão 1702, um computador de origem do cache de mesmo nível rejeitará uma solicitação de conteúdo quando o computador de origem do cache de mesmo nível atende a qualquer uma das seguintes condições:  
  -  Está no modo de bateria fraca.
  -  Carga da CPU excede 80% no momento em que o conteúdo seja solicitado.
  -  E/s de disco tem um *AvgDiskQueueLength* que exceder 10.
  -  Não há conexões não mais disponíveis no computador.   

Você pode definir essas configurações usando o servidor de configuração de cliente classe WMI para o recurso de origem correspondente (*SMS_WinPEPeerCacheConfig*) quando você usa o System Center Configuration Manager SDK.

Quando o computador rejeita uma solicitação para o conteúdo, do computador solicitante continuará a busca de conteúdo de fontes alternativas em seu pool de locais de origem de conteúdo disponível.   



### <a name="monitoring"></a>Monitorização   
Para ajudá-lo a entender o uso do Cache de mesmo nível, você pode exibir o painel de fontes de dados do cliente. Consulte [painel fontes de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partir da versão 1702, você pode usar três relatórios para exibir o uso de cache de mesmo nível. No console, vá para **monitoramento** > **relatórios** > **relatórios**. Todos os relatórios têm um tipo de **conteúdo de distribuição de Software**:
1.  **Rejeição de conteúdo de origem do cache de mesmo nível**:  
Use esse relatório para entender com que frequência as fontes de cache de mesmo nível em um grupo de limites rejeitou uma solicitação de conteúdo.
 - **Problema conhecido:** Quando fazer uma busca detalhada nos resultados como *MaxCPULoad* ou *MaxDiskIO*, você poderá receber um erro que sugere o relatório ou detalhes não podem ser encontrados. Para resolver esse problema, use os seguintes dois relatórios que mostram os resultados diretamente.

2. **Rejeição de conteúdo de origem do cache de mesmo nível pela condição**:  
Use esse relatório para entender os detalhes de rejeição para um tipo de grupo ou a rejeição de limite especificado. Você pode especificar

  - **Problema conhecido:** Você não poderá selecionar parâmetros disponíveis e em vez disso, deve inseri-los manualmente. Insira os valores para *nome do grupo de limite* e *tipo rejeição* como visto no primeiro relatório. Por exemplo, para *tipo rejeição* você pode inserir *MaxCPULoad* ou *MaxDiskIO*.

3. **Detalhes de rejeição de conteúdo da fonte de cache de mesmo nível**:   
  Use esse relatório para entender o conteúdo que está sendo solicitada quando ele foi rejeitado.

 - **Problema conhecido:** Você não poderá selecionar parâmetros disponíveis e em vez disso, deve inseri-los manualmente. Insira o valor para *tipo rejeição* conforme exibido no primeiro relatório (Peer cache fonte conteúda rejeição) e insira o *ID de recurso* para a fonte de conteúdo que você deseja obter mais informações sobre.  Para localizar a ID de recurso da fonte de conteúdo:  

    1. Localizar o nome do computador que é exibido como o *fonte de cache par* nos resultados do relatório 2º (Peer cache fonte conteúdo rejeição pela condição).  
    2. Em seguida, vá para **ativos e conformidade** > **dispositivos** e, em seguida, procure esse nome de computadores. Use o valor da coluna de ID de recurso.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos e considerações para o Cache par
-   Cache de mesmo nível tem suporte em qualquer sistema operacional Windows que tem suporte como cliente do Configuration Manager. Não há suporte para sistemas operacionais não-Windows para o Cache par.

-   Os clientes só podem transferir conteúdo de clientes de Cache de mesmo nível que estão em seu grupo de limites atual.

-   Cada site em que os clientes usam o Cache de mesmo nível deve ser configurado com um [Network Access Account](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A conta é usada pelo computador de origem de Cache par para autenticar solicitações de download de pares e exige apenas permissões de usuário de domínio para essa finalidade.

-   Como o limite atual de uma fonte de conteúdo do Cache de mesmo nível é determinado pelo último envio de inventário de hardware do cliente, um cliente que passa para um local de rede e está em um grupo de limites diferentes ainda pode ser considerado um membro de seu grupo de limites anterior para fins de Cache de mesmo nível. Isso pode resultar em um cliente que está sendo oferecido a uma fonte de conteúdo de Cache de mesmo nível que não está em seu local de rede imediata. É recomendável excluindo os clientes que estão sujeitos a essa configuração da participação como uma fonte de Cache de mesmo nível.

## <a name="to-configure-client-peer-cache-client-settings"></a>Para definir configurações de cliente de Cache de mesmo nível do cliente
1.  No console do Configuration Manager, vá para **administração** > **configurações do cliente**e, em seguida, abra o objeto de configurações de cliente de dispositivo que você deseja usar. Você também pode modificar o objeto de configurações do cliente padrão.
2.  Na lista de configurações disponíveis, escolha **configurações de Cache do cliente**.
3.  Definir **cliente habilitar o Configuration Manager no SO completo compartilhe conteúdo** para **Sim**.
4.  Defina as seguintes configurações para definir as portas que você deseja usar para o Cache par:  
  -  **Porta para difusão de rede inicial**
  -  **Habilitar HTTPS para comunicação ponto a ponto do cliente**
  -  **Porta para download de conteúdo de pares (HTTP/HTTPS)**

Em cada computador que está habilitado para o Cache de mesmo nível, se o Firewall do Windows está em uso, o Configuration Manager configura-o para permitir o uso de portas que você configurar.

