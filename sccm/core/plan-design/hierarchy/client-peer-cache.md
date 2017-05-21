---
title: Cache de elemento de rede do cliente | O System Center Configuration Manager
description: "Utilize Cache ponto a ponto para localizações de origem de conteúdo de cliente quando implementar o conteúdo com o System Center Configuration Manager."
ms.custom: na
ms.date: 4/4/2017
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
ms.sourcegitcommit: 26feb0b166beb7e48cb800a5077d00dbc3eec51a
ms.openlocfilehash: dcd05d7d120f8997562da7d92b38c8b52a512357
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="peer-cache-for-configuration-manager-clients"></a>Cache de elementos para clientes do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Iniciar com o System Center Configuration Manager versão 1610, pode utilizar **cache de elementos da** para ajudar a gerir a implementação de conteúdos para clientes em localizações remotas. Cache de elementos da é uma solução incorporadas do Configuration Manager que permite que os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local.   

> [!TIP]  
> Introduzida com a versão 1610, Cache ponto a ponto e o dashboard de origens de dados do cliente são funcionalidades da versão de pré-lançamento. Para ativá-las, consulte o artigo [utilizar funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/pre-release-features).

## <a name="overview"></a>Descrição Geral
 -     Utilize as definições de cliente para permitir que os clientes utilizam Cache ponto a ponto.
 -     Para partilhar conteúdo, os clientes de Cache ponto a ponto tem ambos de ser membros do grupo de limites atual do cliente que está a procurar o conteúdo. Os clientes de Cache ponto a ponto vizinho grupos de limites não são incluídos com o conjunto de localizações de origem de conteúdo disponível quando um cliente utiliza contingência procurar conteúdo a partir de um grupo de limites de vizinho. Para mais informações sobre grupos de limites atuais e vizinhança, consulte o artigo [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Os clientes que não estão ativados para Cache ponto a ponto, mas são o atual grupo de limites com Cache ponto a ponto ativada clientes, pode obter conteúdos a partir do cliente de Cache de elemento de rede ativada.  
 - Cada tipo de conteúdo que está retido na cache de um cliente do Configuration Manager pode ser servido para outros clientes através da utilização de Cache ponto a ponto.
 -    Cache de elementos da substitui a utilização de outras soluções como o BranchCache, mas funciona em vez disso, lado a lado com o mesmo para dar-lhe mais opções para expandir as soluções de implementação de conteúdos tradicional, tais como pontos de distribuição. Esta é uma solução personalizada com nenhuma dependência no BranchCache, para que se não ativar ou utilizar o Windows BranchCache, ainda funcione.

### <a name="operations"></a>Operações

Depois de implementar as definições de cliente que permitem Cache ponto a ponto para uma coleção, os membros da coleção de que podem agir como uma origem de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites:
 -    Um cliente que funciona como uma origem de conteúdo ponto a ponto submete uma lista de conteúdo em cache disponível para o respetivo ponto de gestão.
 -    Em seguida, quando o cliente seguinte nesse grupo de limites solicita que o conteúdo, cada origem de cache de elemento de rede que tenha o conteúdo é devolvida como uma potencial origem de conteúdo, juntamente com os pontos de distribuição e de outras localizações de origem de conteúdo nesse grupo de limites.
 -    Pelo processo normal de sistema operativo, o cliente que está a procurar o conteúdo seleciona uma origem de conteúdo do conjunto de origens forneceu e, em seguida, procede para tentar obter o conteúdo.

> [!NOTE]
> No caso de contingência para um grupo de limites de vizinho para conteúdo ocorre, a cache de elementos da localizações de origem de conteúdo a partir do grupo de limites de vizinho não são adicionadas ao agrupamento do cliente de potenciais localizações de origem de conteúdo.  


Embora o pode fazer com que todos os clientes participam como uma origem de cache ponto a ponto, é melhor prática para selecionar apenas os clientes que são melhores adequada para ser ponto a ponto origens de cache.  A adequabilidade dos clientes pode ser avaliada com base no tipo de chassis de um cliente, espaço em disco, a conectividade da rede e muito mais. Para obter mais informações que podem ajudar a selecionar os clientes para utilizar para a cache de elementos da melhor, consulte o artigo [esta blogue por um consultor de Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Acesso limitado a uma origem de cache ponto a ponto**  
A partir da versão 1702, um computador de origem de cache ponto a ponto irão rejeitar um pedido de conteúdo quando o computador de origem de cache ponto a ponto cumpra qualquer um dos seguintes condições:  
  -  Está no modo de bateria baixo.
  -  Carga de CPU excede 80% o momento que o conteúdo de exemplos é solicitado.
  -  E/s de disco tem um *AvgDiskQueueLength* que excede 10.
  -  Não existem ligações não mais disponíveis para o computador.   

Pode configurar estas definições utilizando o servidor de configuração de cliente classe WMI para a funcionalidade de origem do elemento de rede (*SMS_WinPEPeerCacheConfig*) ao utilizar o SDK do System Center Configuration Manager.

Quando o computador rejeita um pedido para o conteúdo, o computador que efetuou irão continuar a pesquisa de conteúdo a partir de fontes alternativas no seu agrupamento das localizações de origem de conteúdo disponível.   



### <a name="monitoring"></a>Monitorização   
Para ajudar a compreender a utilização da Cache ponto a ponto, pode ver o dashboard de origens de dados de cliente. Consulte o artigo [dashboard de origens de dados de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partir da versão 1702, pode utilizar três relatórios para ver a utilização de cache ponto a ponto. Na consola, vá para **monitorização** > **relatórios** > **relatórios**. Os relatórios todos os têm um tipo de **conteúdo de distribuição do Software**:
1.  **Elemento de rejeição de conteúdo de origem de cache**:  
Utilize este relatório para compreender com que frequência as origens de cache ponto a ponto num grupo de limites rejeitaram um pedido de conteúdo.
 - **Problemas conhecidos:** Quando a desagregação num resultados goste *MaxCPULoad* ou *MaxDiskIO*, poderá receber um erro que sugere o relatório ou não não possível encontrar os detalhes. Para contornar este problema, utilize os seguintes dois relatórios que mostram os resultados diretamente.

2. **Elemento de rejeição de conteúdo de origem de cache pela condição**:  
Utilize este relatório para compreender os detalhes de rejeição de um tipo de grupo ou rejeição do limite especificado. Pode especificar

  - **Problemas conhecidos:** Não é possível selecionar a partir de parâmetros disponíveis e em vez disso, tem de introduzi-los manualmente. Introduza os valores para *nome do grupo de limites* e *rejeição tipo* conforme se verificava em primeiro o relatório. Por exemplo, para *rejeição tipo* poderá introduzir *MaxCPULoad* ou *MaxDiskIO*.

3. **Detalhes de rejeição de conteúdo de origem de cache de elemento**:   
  Utilize este relatório para compreender o conteúdo que estava a ser solicitado quando foi rejeitado.

 - **Problemas conhecidos:** Não é possível selecionar a partir de parâmetros disponíveis e em vez disso, tem de introduzi-los manualmente. Introduza o valor para *rejeição tipo* tal como apresentados no primeiro relatório (elemento de rede cache origem conteúda rejeição) e, em seguida, introduza o *ID do recurso* para a origem de conteúdo que pretende obter mais informações.  Para localizar o ID de recurso da origem de conteúdo:  

    1. Localizar o nome do computador que é apresentado como o *origem de cache ponto a ponto* nos resultados do relatório 2. (ponto a ponto cache origem conteúdo rejeição pela condição).  
    2. Em seguida, aceda à **ativos e compatibilidade** > **dispositivos** e, em seguida, procure esse nome de computadores. Utilize o valor da coluna ID do recurso.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos e considerações para a Cache ponto a ponto
-   Cache de elementos da é suportada em qualquer sistema operativo Windows que é suportado como o cliente do Configuration Manager. Sistemas operativos Windows não não são suportados para Cache ponto a ponto.

-   Os clientes apenas podem transferir conteúdos a partir de clientes de Cache ponto a ponto que estejam no respetivo grupo de limites atual.

-   Cada site onde os clientes utilizam a cache de elementos da deve ser configurado com um [conta de acesso à rede](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A conta é utilizada pelo computador de origem de Cache ponto a ponto para autenticar pedidos de transferência de elementos da rede e necessita de permissões de utilizador de domínio apenas para esta finalidade.

-     Porque o limite atual de uma origem de conteúdo de Cache de elementos é determinado por submissão de inventário de hardware esse cliente último, um cliente fizer roaming para uma localização de rede e está num grupo de limites diferentes pode ainda ser considerado um membro do respetivo grupo de limites anterior para as finalidades de Cache ponto a ponto. Isto pode resultar num cliente que está a ser oferecido numa origem de conteúdo da Cache de elemento de rede que não se encontra na respetiva localização de rede imediata. É recomendável excluir clientes que estejam propensas a esta configuração a participação como uma origem de Cache ponto a ponto.

## <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar as definições de cliente de Cache do cliente ponto a ponto
1.    Na consola do Configuration Manager, aceda a **administração** > **definições de cliente**e, em seguida, abra o objeto de definições de cliente de dispositivo que pretende utilizar. Também pode modificar o objeto de predefinições de cliente.
2.    A partir da lista de definições disponíveis, escolha **definições de Cache do cliente**.
3.    Definir **cliente de ativar o Configuration Manager no SO completo para partilhar conteúdo** para **Sim**.
4.    Configure as seguintes definições para definir as portas que pretende utilizar para a cache de elementos da:  
  -  **Porta para difusão de rede inicial**
  -  **Ativar HTTPS para comunicação do cliente ponto a ponto**
  -  **Porta para transferência de conteúdo a partir do ponto a ponto (HTTP/HTTPS)**

Em cada computador que está ativada para a Cache ponto a ponto, se a Firewall do Windows está a ser utilizado, o Configuration Manager configura-o para permitir a utilização das portas que configurar.

