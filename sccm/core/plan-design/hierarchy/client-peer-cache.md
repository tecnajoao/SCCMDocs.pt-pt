---
title: A Cache do cliente | O System Center Configuration Manager
description: "Utilize a Cache ponto a ponto para localizações de origem de conteúdo de cliente quando implementar o conteúdo com o System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 89fcd16887ae77299f9d18472ee6a1ba56794eca
ms.contentlocale: pt-pt
ms.lasthandoff: 07/29/2017

---

# <a name="peer-cache-for-configuration-manager-clients"></a>Cache ponto a ponto para clientes do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Começando com o System Center Configuration Manager versão 1610, pode utilizar **Cache ponto a ponto** para ajudar a gerir a implementação de conteúdos para clientes em localizações remotas. A Cache é uma solução incorporada do Configuration Manager que permite que os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local.   

> [!TIP]  
> Introduzido com a versão 1610, Cache ponto a ponto e o dashboard de origens de dados de cliente são funcionalidades de pré-lançamento. Para ativá-los, consulte o artigo [utilizar as funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/pre-release-features).

## <a name="overview"></a>Descrição Geral
Um cliente de Cache ponto a ponto é um cliente de Configuration Manager que está ativado para utilizar a Cache ponto a ponto. Uma Cache ponto a ponto cliente que tem o conteúdo pode partilhar com clientes adicionais é uma origem de Cache ponto a ponto.
 -  Pode utilizar as definições de cliente para permitir que os clientes utilizar a Cache ponto a ponto.
 -  Para partilhar conteúdo como uma origem de Cache ponto a ponto, um cliente de Cache ponto a ponto:
    -  Tem de ser associados a um domínio. No entanto, um cliente que não está associado a um domínio pode obter conteúdo de um domínio associado a origem de Cache ponto a ponto.
    -  Tem de ser um membro do grupo de limites atual do cliente que está a pesquisa o conteúdo. Um cliente de Cache ponto a ponto num grupo de limites vizinho não está incluído com o conjunto de localizações de origem de conteúdo disponível quando um cliente utiliza a contingência para conteúdo a partir de um grupo de limites de vizinho de pesquisa. Para mais informações sobre grupos de limites atuais e vizinhança, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Cada tipo de conteúdo que é mantido na cache do cliente do Configuration Manager pode ser fornecido para outros clientes através da utilização de Cache ponto a ponto.
 -  Cache ponto a ponto não substitui a utilização de outras soluções como o BranchCache, mas em vez disso, funciona lado lado a lado com o mesmo para lhe dar mais opções para expandir as soluções de implementação de conteúdos tradicionais, como pontos de distribuição. Esta é uma solução personalizada com nenhuma dependência em BranchCache, pelo que o se não ativar ou utilizar o Windows BranchCache, ainda funciona.

### <a name="operations"></a>Operações

Depois de implementar as definições de cliente que permitem a Cache ponto a ponto numa coleção, os membros dessa coleção podem atuar como uma origem de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites:
 -  Um cliente que funciona como uma origem de conteúdo do elemento de rede envia uma lista de conteúdos em cache disponíveis para o respetivo ponto de gestão.
 -  Em seguida, quando o cliente seguinte nesse grupo de limites pede esse conteúdo, cada origem de cache ponto a ponto que tem o conteúdo é devolvida como uma origem de conteúdo potencial juntamente com os pontos de distribuição e outras localizações de origem de conteúdo nesse grupo de limites.
 -  Pelo processo normal de sistema operativo, o cliente que está a pesquisa o conteúdo seleciona uma origem de conteúdo do agrupamento de origens que forneceu e, em seguida, continua a tentar obter o conteúdo.

> [!NOTE]
> Se contingência para um grupo de limites de vizinho para conteúdo ocorrer, a Cache ponto a ponto localizações de origem de conteúdo do grupo de limites de vizinho não são adicionadas ao agrupamento do cliente de potenciais localizações de origem de conteúdo.  


Apesar do que pode efetuar todos os clientes participam como uma origem de cache ponto a ponto, o seu melhor prática de escolher apenas os clientes que são melhor adequada que está a ser ponto a ponto origens de cache.  A adequabilidade dos clientes pode ser avaliada com base no tipo de chassis de um cliente, espaço em disco, a conectividade de rede e muito mais. Para obter mais informações que podem ajudar a selecionar os melhor clientes a utilizar para a Cache ponto a ponto, consulte [este blogue por um consultor de Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Acesso limitado a uma origem de cache ponto a ponto**  
A partir da versão 1702, um computador de origem de cache ponto a ponto irão rejeitar um pedido para o conteúdo quando o computador de origem de cache ponto a ponto cumpre qualquer uma das seguintes condições:  
  -  Está no modo de bateria baixo.
  -  Carga da CPU excede 80% momento solicitados.
  -  E/s de disco tem um *AvgDiskQueueLength* excede que 10.
  -  Não existem ligações mais não disponíveis para o computador.   

Pode configurar estas definições com o servidor de configuração de cliente classe WMI para a funcionalidade de origem do elemento de rede (*SMS_WinPEPeerCacheConfig*) ao utilizar o SDK do System Center Configuration Manager.

Quando o computador rejeita um pedido para o conteúdo, o computador que efetuou irá continuar a pesquisa de conteúdo a partir de origens alternativas no seu conjunto das localizações de origem de conteúdo disponível.   



### <a name="monitoring"></a>Monitorização   
Para ajudar a compreender a utilização de Cache ponto a ponto, pode ver o dashboard de origens de dados de cliente. Consulte [dashboard de origens de dados de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partir da versão 1702, pode utilizar três relatórios para ver a utilização de cache ponto a ponto. Na consola, aceda a **monitorização** > **relatórios** > **relatórios**. Os relatórios de todas as tem um tipo de **conteúdo de distribuição de Software**:
1.  **Elemento de rejeição de conteúdo de origem de cache**:  
Utilize este relatório para compreender a frequência as origens de cache ponto a ponto num grupo de limites rejeitaram um pedido de conteúdo.
 - **Problema conhecido:** Quando desagregar os resultados como *MaxCPULoad* ou *MaxDiskIO*, poderá receber um erro que sugere o relatório ou não não possível encontrar os detalhes. Para contornar este problema, utilize os dois relatórios seguintes que mostram os resultados diretamente.

2. **Elemento de rejeição de conteúdo de origem de cache pela condição**:  
Utilize este relatório para compreender a rejeição os detalhes para um tipo de grupo ou rejeição de limite especificado. Pode especificar

  - **Problema conhecido:** Não é possível selecionar a partir de parâmetros disponíveis e em vez disso, tem de introduzi-los manualmente. Introduza os valores para *nome do grupo de limites* e *rejeição tipo* visto no relatório do primeiro. Por exemplo, para *rejeição tipo* poderá introduzir *MaxCPULoad* ou *MaxDiskIO*.

3. **Detalhes de rejeição de conteúdo de origem de cache de elemento**:   
  Utilize este relatório para compreender os conteúdos que está a ser pedida quando foi rejeitado.

 - **Problema conhecido:** Não é possível selecionar a partir de parâmetros disponíveis e em vez disso, tem de introduzi-los manualmente. Introduza o valor para *rejeição tipo* tal como apresentado no primeiro relatório (ponto a ponto cache origem conteúda rejeição) e, em seguida, introduza o *ID de recurso* para a origem de conteúdo que pretende obter mais informações sobre.  Para localizar o ID de recurso da origem de conteúdo:  

    1. Localizar o nome do computador que mostra como o *origem de cache ponto a ponto* nos resultados do relatório 2nd (ponto a ponto cache origem conteúdo rejeição pela condição).  
    2. Em seguida, aceda a **ativos e compatibilidade** > **dispositivos** e, em seguida, procure esse nome de computadores. Utilize o valor da coluna de ID de recurso.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos e considerações para a Cache ponto a ponto
-   Cache ponto a ponto é suportada em qualquer sistema operativo Windows que é suportado como cliente do Configuration Manager. Sistemas operativos Windows não não são suportados para Cache ponto a ponto.

-   Os clientes só podem transferir conteúdo a partir de clientes de Cache ponto a ponto que se encontrem no respetivo grupo de limites atuais.

-   Antes de versão 1706, cada site onde os clientes utilizam a Cache ponto a ponto deve ser configurado com um [conta de acesso à rede](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A partir da versão 1706, que a conta já não é necessária com uma exceção.  A exceção é quando um cliente utiliza a cache ponto a ponto para obter e executar uma sequência de tarefas a partir do Centro de Software e a sequência de tarefas reinicia o cliente no WinPE.  Neste cenário, o cliente ainda requer que a conta de acesso de rede quando estiver no WinPE para que possam aceder a origem de cache ponto a ponto ao obter conteúdo.

    Quando tem necessário, a conta de acesso de rede é utilizada pelo computador de origem de Cache ponto a ponto para autenticar pedidos de transferência de elementos de rede e requer apenas permissões de utilizador de domínio para esta finalidade.

-   Porque o limite atual de uma origem de conteúdo de Cache ponto a ponto é determinado pela submissão de inventário de hardware do que o cliente último, um cliente fizer roaming para uma localização de rede e está num grupo de limites diferentes pode ainda ser considerados como estando um membro do respetivo grupo de limites anteriores para efeitos de Cache ponto a ponto. Isto pode resultar num cliente oferecido uma origem de conteúdo de Cache ponto a ponto que não se encontra na respetiva localização de rede imediata. Recomendamos, excluindo os clientes que são suscetíveis a esta configuração de participar como uma origem de Cache ponto a ponto.

## <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar as definições de cliente de Cache ponto a ponto do cliente
1.  Na consola do Configuration Manager, vá para **administração** > **as definições de cliente**e, em seguida, abra o objeto de definições de cliente de dispositivo que pretende utilizar. Também pode modificar o objecto de predefinições de cliente.
2.  A partir da lista de definições disponíveis, escolha **as definições de Cache do cliente**.
3.  Definir **cliente de ativar o Configuration Manager no SO completo para partilhar conteúdo** para **Sim**.
4.  Configure as seguintes definições para definir as portas que pretende utilizar para a Cache ponto a ponto:  
  -  **Porta para difusão de rede inicial**
  -  **Ativar HTTPS para comunicação de ponto a ponto do cliente**
  -  **Porta para transferência do conteúdo de elemento de rede (HTTP/HTTPS)**

Em cada computador que está ativada para a Cache ponto a ponto, se a Firewall do Windows está a ser utilizado, o Configuration Manager configura-la para permitir a utilização das portas que configurar.

