---
title: A Cache do cliente
titleSuffix: Configuration Manager
description: Utilize a Cache ponto a ponto para localizações de origem de conteúdo de cliente quando implementar o conteúdo com o System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b705a2cb8eccae3abe63c5de0680c712ab2e181e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache ponto a ponto para clientes do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1101436-->
Utilize **Cache ponto a ponto** para ajudar a gerir a implementação de conteúdos para clientes em localizações remotas. A Cache é uma solução incorporada do Configuration Manager que permite que os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local.   

> [!TIP]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1610 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1710, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  


> [!Note]  
> O Configuration Manager não ativar esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="overview"></a>Descrição Geral
Um cliente de Cache ponto a ponto é um cliente de Configuration Manager que está ativado para utilizar a Cache ponto a ponto. Uma Cache ponto a ponto cliente que tem o conteúdo pode partilhar com clientes adicionais é uma origem de Cache ponto a ponto.
 -  Pode utilizar as definições de cliente para permitir que os clientes utilizar a Cache ponto a ponto.
 -  Para partilhar conteúdo como uma origem de Cache ponto a ponto, um cliente de Cache ponto a ponto:
    -  Tem de ser associados a um domínio. No entanto, um cliente que não está associado a um domínio pode obter conteúdo de um domínio associado a origem de Cache ponto a ponto.
    -  Tem de ser um membro do grupo de limites atual do cliente que está a pesquisa o conteúdo. Quando um cliente utiliza a contingência para conteúdo a partir de um grupo de limites de vizinho de pesquisa, a lista de localizações de origem de conteúdo não inclui um cliente de Cache ponto a ponto num grupo de limites vizinho. Para mais informações sobre grupos de limites atuais e vizinhança, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - O cliente do Configuration Manager serve cada tipo de conteúdo na cache para outros clientes através da utilização de Cache ponto a ponto. Este conteúdo inclui ficheiros do Office 365 e expresse de precisa de ficheiros de instalação.<!--SMS.500850-->
 -  Cache ponto a ponto não substitui a utilização de outras soluções como o BranchCache. Cache ponto a ponto funciona juntamente com outras soluções para lhe dar mais opções para expandir as soluções de implementação de conteúdos tradicionais, como pontos de distribuição. A Cache é uma solução personalizada com nenhuma dependência no BranchCache. Se não ativar ou utilizar o Windows BranchCache, Cache ponto a ponto ainda funciona.

### <a name="operations"></a>Operações

Para ativar a cache ponto a ponto, implemente as definições de cliente numa coleção. Em seguida, os membros dessa coleção agirem como uma origem de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites.
 -  Um cliente que funciona como uma origem de conteúdo do elemento de rede envia uma lista de conteúdos em cache disponíveis para o respetivo ponto de gestão.
 -  Quando o cliente seguinte nesse grupo de limites pede esse conteúdo, cada origem de cache ponto a ponto, que tem o conteúdo e estiver online, é devolvida na lista de origens de conteúdo potenciais. Esta lista inclui também os pontos de distribuição e outras localizações de origem de conteúdo nesse grupo de limites.
 -  Pelo processo normal, o cliente que está a pesquisa o conteúdo seleciona uma origem da lista fornecida. O cliente tenta, em seguida obter o conteúdo.

> [!NOTE]
> Se o cliente retrocede para um grupo de limites de vizinho para conteúdo, não adiciona as localizações de origem de conteúdo de Cache ponto a ponto do grupo de limites de vizinho à lista de potenciais localizações de origem de conteúdo.  


A melhor prática é escolher apenas clientes melhor adequados como origens de cache ponto a ponto. Avalie a adequabilidade do cliente com base em atributos como tipo de chassis, espaço em disco e conectividade de rede. Para obter mais informações que podem ajudar a selecionar os melhor clientes a utilizar para a Cache ponto a ponto, consulte [este blogue por um consultor de Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Acesso limitado a uma origem de cache ponto a ponto**  
A partir da versão 1702, um computador de origem de cache ponto a ponto rejeita pedidos para o conteúdo quando o computador de origem de cache ponto a ponto cumpre qualquer uma das seguintes condições:  
  -  Está no modo de bateria baixo.
  -  Carga da CPU excede 80% momento solicitados.
  -  E/s de disco tem um *AvgDiskQueueLength* excede que 10.
  -  Não existem ligações mais não disponíveis para o computador.   

Configurar estas definições com o servidor de configuração de cliente classe WMI para a funcionalidade de origem do elemento de rede (*SMS_WinPEPeerCacheConfig*) no SDK do Configuration Manager.

Quando o computador rejeita um pedido para o conteúdo, o computador que efetuou continua a pesquisa o conteúdo da lista de localizações de origem de conteúdo disponível.   



### <a name="monitoring"></a>Monitorização   
Para ajudar a compreender a utilização de Cache ponto a ponto, pode ver o dashboard de origens de dados de cliente. Consulte [dashboard de origens de dados de cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partir da versão 1702, pode utilizar três relatórios para ver a utilização de cache ponto a ponto. Na consola, aceda a **monitorização** > **relatórios** > **relatórios**. Os relatórios de todas as tem um tipo de **conteúdo de distribuição de Software**:
1.  **Elemento de rejeição de conteúdo de origem de cache**:  
Utilize este relatório para compreender a frequência as origens de cache ponto a ponto num grupo de limites rejeitar um pedido de conteúdo.
 - **Problema conhecido:** Quando desagregar os resultados como *MaxCPULoad* ou *MaxDiskIO*, poderá receber um erro que sugere o relatório ou não não possível encontrar os detalhes. Para contornar este problema, utilize os dois relatórios seguintes que diretamente mostram os resultados.

2. **Elemento de rejeição de conteúdo de origem de cache pela condição**:  
Utilize este relatório para compreender a rejeição os detalhes para um tipo de grupo ou rejeição de limite especificado. Pode especificar

  - **Problema conhecido:** Não é possível selecionar a partir de parâmetros disponíveis e em vez disso, tem de introduzi-los manualmente. Introduza os valores para *nome do grupo de limites* e *rejeição tipo* visto no relatório do primeiro. Por exemplo, para *rejeição tipo* poderá introduzir *MaxCPULoad* ou *MaxDiskIO*.

3. **Detalhes de rejeição de conteúdo de origem de cache de elemento**:   
  Utilize este relatório para compreender o conteúdo que o cliente pediu quando rejeitado.

 - **Problema conhecido:** Não é possível selecionar a partir de parâmetros disponíveis e em vez disso, tem de introduzi-los manualmente. Introduza o valor para *rejeição tipo* tal como apresentado no **elemento rejeição de conteúdo de origem de cache** relatório. Em seguida, introduza o *ID de recurso* para a origem de conteúdo sobre os quais pretende obter mais informações. Para localizar o ID de recurso da origem de conteúdo:  

    1. Localizar o nome do computador que mostra como o *origem de cache ponto a ponto* nos resultados do **elemento rejeição de conteúdo de origem de cache pela condição** relatório.  
    2. Em seguida, aceda a **ativos e compatibilidade** > **dispositivos** e, em seguida, procure esse nome de computadores. Utilize o valor da coluna de ID de recurso.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisitos e considerações para a Cache ponto a ponto
-   Cache ponto a ponto é suportada em qualquer sistema operativo Windows que é suportado como cliente do Configuration Manager. Sistemas operativos Windows não não são suportados para Cache ponto a ponto.

-   Os clientes só podem transferir conteúdo a partir de clientes de Cache ponto a ponto que se encontrem no respetivo grupo de limites atuais.

-   Antes de versão 1706, cada site onde os clientes utilizam a Cache ponto a ponto deve ser configurado com um [conta de acesso à rede](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A partir da versão 1706, que a conta já não é necessária com uma exceção. O cenário de exceção é quando um cliente de ativar a cache ponto a ponto executa uma sequência de tarefas a partir do Centro de Software e de que a sequência de tarefas reinicia a uma imagem de arranque. Neste cenário, o cliente ainda requer a conta de acesso de rede. Quando o cliente está no Windows PE, utiliza a conta de acesso de rede para obter conteúdo a partir da origem de cache ponto a ponto.

    Quando necessário, o computador de origem de Cache ponto a ponto utiliza a conta de acesso de rede para autenticar pedidos de transferência de elementos. Esta conta requer permissões de utilizador de domínio apenas para esta finalidade.

-   Submissão de inventário de hardware do cliente último determina o limite atual de uma origem de conteúdo de Cache ponto a ponto. Um cliente fizer roaming para um grupo de limites diferentes ainda poderá ser um membro do respetivo grupo de limites anteriores para efeitos de Cache ponto a ponto. Este comportamento resulta num cliente oferecido uma origem de conteúdo de Cache ponto a ponto que não se encontra na respetiva localização de rede imediata. Recomendamos, excluindo os clientes que são suscetíveis a esta configuração de participar como uma origem de Cache ponto a ponto.
-    A partir da versão 1706, o cliente de cache ponto a ponto primeiro valida que a origem de conteúdo de cache ponto a ponto online antes de tentar transferir conteúdo. <!--sms.498675-->

## <a name="to-configure-client-peer-cache-client-settings"></a>Para configurar as definições de cliente de Cache ponto a ponto do cliente
Para obter informações sobre como configurar as definições de cliente, consulte [as definições de cache do cliente](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). Para obter mais informações, consulte [como configurar as definições de cliente](/sccm/core/clients/deploy/configure-client-settings).

No elemento de rede ativada em cache os clientes que utiliza a Firewall do Windows, o Configuration Manager configura as portas de firewall que especificou nas definições do cliente.
