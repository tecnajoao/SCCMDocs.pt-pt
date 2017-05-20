---
title: "Noções básicas de gestão de conteúdo | Documentos do Microsoft"
description: "Utilize as opções de ferramentas e no System Center Configuration Manager para gerir o conteúdo que implementar."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 212628639300e9c361f7cee61b3df6b1cb6874ce
ms.openlocfilehash: f73dde64e0e8a0fc49f45b3afb3b8f00c926a820
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager suporta um sistema robusto de ferramentas e opções para gerir o conteúdo que é implementada como aplicações, pacotes, atualizações de software e implementações do sistema operativo.  

O conteúdo que implementa é armazenado em ambos os servidores do site e nos servidores do sistema de sites de ponto de distribuição. Este conteúdo pode necessitar de uma grande quantidade de largura de banda da rede quando é que está a ser transferido entre localizações. Para efetivamente planear e utilizar a infraestrutura de gestão de conteúdo, é recomendável que compreender as opções disponíveis e as configurações e, em seguida, considere como utilizá-las melhor Ajustar tamanho do seu ambiente de rede e necessita de implementação de conteúdos.  

> [!TIP]    
> Pode obter mais informações sobre o processo de distribuição de conteúdo e obter ajuda no diagnosticar e resolver problemas gerais de distribuição de conteúdo. Consulte o artigo [compreender e resolução de problemas de conteúdo no Configuration Manager de distribuição](https://support.microsoft.com/help/4000401/content-distribution-in-mcm) em support.microsoft.com.

Seguem-se conceitos chave para gestão de conteúdo. Quando um conceito precisar de informações complexas ou adicionais, são fornecidas hiperligações para direcioná-lo para esses detalhes.

## <a name="accounts-used-for-content-management"></a>Contas utilizadas para a gestão de conteúdos  
 As contas que se seguem podem ser utilizadas com a gestão de conteúdos:  

-   **Conta de acesso de rede**: Utilizada pelos clientes para ligar a um ponto de distribuição e aceder ao conteúdo. Por predefinição, a conta de computador está experimentada em primeiro lugar.  

     Esta conta também é utilizada pelos pontos de distribuição de solicitação obter conteúdos a partir de um ponto de distribuição de origem localizado numa floresta remota.  

-   **Conta de acesso do pacote**: Por predefinição, o Configuration Manager concede acesso ao conteúdo de um ponto de distribuição para contas de acesso genéricas utilizadores e administradores. No entanto, pode configurar permissões adicionais para restringir o acesso.   

-   **Conta de ligação de multicast**: Utilizado para implementações do sistema operativo.  

Para mais informações sobre estas contas, consulte o artigo [gerir contas para aceder ao conteúdo](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).

## <a name="bandwidth-throttling-and-scheduling"></a>Limitação de largura de banda e agendamento  
 Tanto a limitação como o agendamento são opções que o ajudam a controlar quando o conteúdo é distribuído de um servidor do site para pontos de distribuição. Isto é semelhante a, mas não está diretamente relacionado com controlos de largura de banda para replicação baseada em ficheiros de site para site.  

 Para obter mais informações, consulte o artigo [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="binary-differential-replication"></a>Replicação diferencial binária  
 Um pré-requisito para pontos de distribuição, replicação de diferencial binário (BDR), que por vezes conhecida como replicação de diferenças, é automaticamente utilizado para reduzir a utilização de largura de banda quando está a distribuir atualizações de conteúdo que implementou anteriormente para outros sites ou para pontos de distribuição remotos.  

 A BDR minimiza a largura de banda de rede utilizada para enviar atualizações de conteúdo distribuído ao reenviar apenas o conteúdo novo ou alterado, em vez de enviar o conjunto completo de ficheiros de origem do conteúdo sempre que é efetuada uma alteração nesses ficheiros.  

 Quando é utilizada a replicação diferencial de binários, o Configuration Manager identifica as alterações que ocorrem para ficheiros de origem para cada conjunto de conteúdos que tem sido anteriormente distribuído.  

-   Quando alterar ficheiros o conteúdo de origem, o Configuration Manager cria uma nova versão incremental do conjunto de conteúdos e replica apenas os ficheiros alterados para sites de destino e os pontos de distribuição. Um ficheiro é considerado alterados se tiver sido mudado ou movido ou se tiver alterado o conteúdo do ficheiro. Por exemplo, se substituir um único ficheiro de controlador num pacote de implementação de sistema operativo que tenha anteriormente distribuído por vários sites, apenas o ficheiro de controlador alterado será replicado para esses sites de destino.  

-   O Configuration Manager suporta até cinco versões incrementais de um conjunto antes de reenviar o conjunto completo de conteúdo de conteúdos. Após a quinta atualização, a alteração seguinte para o conjunto de conteúdo faz com que o Configuration Manager para criar uma nova versão do conjunto de conteúdos. O Configuration Manager, em seguida, distribui a nova versão do conteúdo definido para substituir o conjunto anterior e todas as versões incrementais. Após a distribuição do novo conjunto de conteúdos, as alterações incrementais subsequentes aos ficheiros de origem serão novamente replicadas por replicação diferencial de binários.  


A BDR é suportada entre cada site principal e site subordinado numa hierarquia. Num site, BDR é suportada entre o servidor do site e os respetivos pontos de distribuição normal. No entanto, os pontos de distribuição de solicitação e pontos de distribuição baseado na nuvem não suportam a replicação diferencial de binários para transferência de conteúdo. Os pontos de distribuição de solicitação suportam deltas de nível de ficheiros, transferir novos ficheiros, mas não blocos dentro de um ficheiro.

As aplicações utilizam sempre a replicação diferencial de binários. Para pacotes, a replicação diferencial de binários é opcional e não está ativada por predefinição. Para utilizar a replicação diferencial de binários para pacotes, tem de ativar esta funcionalidade para cada pacote. Para o fazer, selecione a opção **Ativar replicação de diferencial binário** quando criar um novo pacote ou quando editar o separador **Origem de Dados** das propriedades do pacote.  

## <a name="branchcache"></a>BranchCache  
 Uma tecnologia do Windows que permite que os clientes que suportam o BranchCache e transferiu uma implementação que está configurada para Branch Cache servir, em seguida, como uma origem de conteúdo para outros clientes com capacidade para BranchCache.  

 Por exemplo, quando o primeiro computador cliente com capacidade BranchCache pedir conteúdo de um ponto de distribuição com o Windows Server 2012 e estiver configurado como servidor BranchCache, o computador cliente transfere esse conteúdo e coloca-o em cache.  

-   Nesse computador cliente pode, em seguida, disponibilizar o conteúdo para adicionais com capacidade para BranchCache clientes na mesma sub-rede que também colocam o conteúdo em cache.  

-   Desta forma, os clientes seguintes da mesma sub-rede não necessitam de transferir o conteúdo a partir do ponto de distribuição e o conteúdo é distribuído por vários clientes para futuras transferências.  

## <a name="peer-cache"></a>Cache ponto a ponto
A partir da versão 1610, o cliente cache de elementos da ajuda-o a gerir a implementação de conteúdo para clientes em localizações remotas. Cache de elementos da é uma solução incorporadas do Configuration Manager que permite que os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local.

Depois de implementar as definições de cliente que permitem Cache ponto a ponto para uma coleção, os membros da coleção de que podem agir como uma origem de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites.

Para obter mais informações, consulte o artigo [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).


## <a name="windows-pe-peer-cache"></a>Cache ponto a ponto do Windows PE
Quando implementa um novo sistema operativo no System Center Configuration Manager, os computadores que executam a sequência de tarefas podem utilizar a Cache de elemento de rede do Windows PE obter conteúdos a partir de um elemento local (uma origem de cache ponto a ponto) em vez de transferir conteúdo a partir de um ponto de distribuição. Isto ajuda a minimizar o tráfego da rede alargada (WAN) em cenários de uma sucursal onde não existe um ponto de distribuição local.

Para obter mais informações, consulte o artigo [cache de elemento de rede do Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="client-locations"></a>Localizações de clientes  
 Seguem-se as localizações a partir das quais os clientes acedem a conteúdo:  

-   **Intranet** (no local):  

    -   Pontos de distribuição podem utilizar HTTP ou HTTPs.  

    -   Utilize apenas um ponto de distribuição baseado na nuvem para contingência quando os pontos de distribuição no local não estão disponíveis.  

-   **Internet**:  

    -   Necessita de pontos de distribuição para aceitar o HTTPS.  

    -   Pode utilizar um ponto de distribuição baseado na nuvem para contingência.  

-   **Grupo de Trabalho**:  

    -   Necessita de pontos de distribuição para aceitar o HTTPS.  

    -   Pode utilizar um ponto de distribuição baseado na nuvem para contingência.  



## <a name="content-library"></a>Biblioteca de conteúdos  
 A biblioteca de conteúdos é o arquivo de instância única de conteúdo que o Configuration Manager utiliza para reduzir o tamanho geral do corpo combinado de conteúdos que distribuir.  

- Saiba mais sobre o [biblioteca de conteúdos](../../../core/plan-design/hierarchy/the-content-library.md).
- Utilize o [ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo que já não se encontra associado a uma aplicação.  


## <a name="distribution-points"></a>Pontos de distribuição  
 Configuration Manager utiliza pontos de distribuição para armazenar ficheiros que são necessários para o software seja executado em computadores cliente. Os clientes tem de ter acesso a pelo menos um ponto de distribuição a partir do qual possam transferir os ficheiros de conteúdo que implementar.  

 O ponto de distribuição básica (sem especializadas) é normalmente denominado como um ponto de distribuição padrão. Existem duas variações no ponto de distribuição padrão que recebem especial atenção:  

-   **Ponto de distribuição de solicitação**: Uma variação de um ponto de distribuição em que o ponto de distribuição possa obter conteúdo a partir de outro ponto de distribuição (um ponto de distribuição de origem). Este processo é semelhante à forma como os clientes transferem conteúdo a partir de pontos de distribuição. Pontos de distribuição de solicitação podem ajudar a evitar congestionamentos de largura de banda de rede que ocorrem quando o servidor do site diretamente terá de distribuir conteúdo para cada ponto de distribuição.  [Utilizar um ponto de distribuição de solicitação com o System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Ponto de distribuição baseado na nuvem**: Uma variação de um ponto de distribuição que está instalado no Microsoft Azure. [Saiba como utilizar um ponto de distribuição baseado na nuvem com o System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Pontos de distribuição padrão suportam uma variedade de configurações e funcionalidades, tais como Otimização e agendamento, PXE e Multicast, ou suportes de conteúdo.  

-   Pode utilizar controlos, tais como **agendas** ou **limitação de largura de banda** para ajudar a controlar a transferência.  

-   Também pode utilizar outras opções, incluindo **pré-configurado conteúdo**, e **pontos de distribuição de solicitação**. Além disso, pode tirar partido **BranchCache** para reduzir a largura de banda de rede que é utilizada na implementação de conteúdo.  

-   Pontos de distribuição suportam configurações diferentes, tais como  **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)**  e  **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**  para implementações do sistema operativo ou configurações para suportar **dispositivos móveis**.  

 Baseado na nuvem e de pontos de distribuição de solicitação suportam muitos destas configurações mesmas, mas têm limitações que são específicas para cada variação de ponto de distribuição.  

## <a name="distribution-point-groups"></a>Grupos de pontos de distribuição  
 Grupos de pontos de distribuição são agrupamentos lógicos de pontos de distribuição que podem simplificar a distribuição de conteúdo.  

 Para obter mais informações, consulte o artigo [gerir grupos de pontos de distribuição](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).

## <a name="distribution-point-priority"></a>Prioridade de pontos de distribuição  
 O valor de prioridade do ponto de distribuição baseia-se na quantidade de tempo necessária para transferir implementações anteriores para esse ponto de distribuição.  

-   Este é um valor de sintonização personalizada que é atribuído a um ponto de distribuição que o ajuda a conteúdo de transferência do Configuration Manager a mais pontos de distribuição num período de tempo mais curto.  

-   Quando distribui conteúdos a vários pontos de distribuição em simultâneo ou a uma distribuição grupo de pontos, do Configuration Manager envia os conteúdos ao ponto de distribuição com a máxima prioridade, antes de enviar os mesmos conteúdos para um ponto de distribuição com uma prioridade mais baixa.  

-   Esta não substitui a prioridade de distribuição de pacotes, que permanece o fator decisivo na sequência do momento de transferência das diversas distribuições.  


Por exemplo, se distribuir conteúdo com uma prioridade de distribuição elevada a um ponto de distribuição que tenha uma prioridade de ponto de distribuição baixa, este pacote de prioridade de distribuição elevada será sempre transferido antes de um pacote que tenha uma prioridade de distribuição baixa. A prioridade de distribuição aplica-se mesmo que os pacotes que tenham uma prioridade de distribuição mais baixa sejam distribuídos a pontos de distribuição com prioridade de ponto de distribuição mais elevada.

A prioridade de distribuição elevada do pacote garante que do Configuration Manager distribui esse conteúdo aos pontos de distribuição aplicáveis antes de quaisquer pacotes com uma prioridade mais baixa distribuição são enviados.  

> [!NOTE]  
>  Os pontos de distribuição de extração também utilizam um conceito de prioridade para ordenar a sequência dos respetivos pontos de distribuição de origem.  
>   
>  -   A prioridade de ponto de distribuição para as transferências de conteúdo ao ponto de distribuição é distinta da prioridade que os pontos de distribuição de extração utilizam quando procuram conteúdo de um ponto de distribuição de origem.  
>  -   Para obter mais informações, consulte o artigo [utilizar um ponto de distribuição de solicitação com o System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  


## <a name="fallback"></a>Contingência  
 Várias coisas a partir da versão 1610, foram alterados de forma que os clientes encontrem um ponto de distribuição que tenha o conteúdo, incluindo contingência. Utilize as seguintes informações aplicam-se para a versão que utiliza:

**Versão 1610 e posterior**   
Os clientes que não é possível localizar o conteúdo a partir de um ponto de distribuição associado à respetiva atual grupo de limites podem reverter para utilizar localizações de origem de conteúdo que estão associadas a grupos de limites de vizinho. Para ser utilizado para contingência, um grupo de limites de vizinho tem de ter uma relação definida com o grupo de limites atual do cliente. Esta relação inclui uma hora configurada que tem de passar antes de um cliente que não é possível localizar o conteúdo localmente pode incluir origens de conteúdo a partir do grupo de limites de vizinho como parte da sua pesquisa.

Conceitos de distribuição preferenciais pontos já não são utilizados e as definições para **permitir localizações de origem de contingência para conteúdo** já não estão disponíveis ou imposta.

Para obter mais informações, consulte o artigo [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Versão 1511, 1602 e 1606**   
Definições de contingência estão relacionadas com a utilização de **pontos de distribuição de preferencial** e localizações de origem de conteúdo que são utilizadas pelos clientes.

-   Por predefinição, os clientes transferem apenas o conteúdo a partir do ponto de distribuição preferencial (um que estejam associadas a grupos de limites do cliente).  

-   No entanto, quando um ponto de distribuição está configurado com a definição **Permitir que os clientes utilizem este sistema de sites como uma localização de origem de contingência para o conteúdo**, esse ponto de distribuição só é oferecido como uma origem de conteúdo válida a qualquer cliente que não consiga obter uma implementação de um dos respetivos pontos de distribuição preferenciais.  


Para obter informações sobre os cenários de contingência e outra localização de conteúdo, consulte o artigo [cenários de localização de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Para obter informações sobre grupos de limites, consulte o artigo [grupos de limites para versões 1511,1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## <a name="network-bandwidth"></a>Largura de banda da rede  
 Para ajudar a gerir a quantidade de largura de banda de rede que é utilizada quando distribui conteúdo, pode utilizar as seguintes opções:  

-   **Pré-configurado conteúdo**:  Um processo de transferência de conteúdo para um ponto de distribuição sem entidade confiadora no Configuration Manager para distribuir os conteúdos através da rede.  

-   **Agendamento e limitação**: Configurações de que o ajudam a controlam quando e como o conteúdo é distribuído aos pontos de distribuição.  

Para obter mais informações, consulte o artigo [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="network-connection-speed-to-content-source"></a>Velocidade da ligação de rede à origem de conteúdo  
Várias coisas a partir da versão 1610, foram alterados de forma que os clientes encontrem um ponto de distribuição que tenha o conteúdo, incluindo a velocidade da ligação de rede a uma origem de conteúdo. Utilize as seguintes informações aplicam-se para a versão que utiliza:

**Versão 1610 e posterior**   
Velocidades de ligação de rede que definem uma distribuição ponto como **rapidamente** ou **lenta** já não são utilizadas. Em vez disso, cada sistema de sites que está associada um grupo de limites é Tratado da mesma.

Para obter mais informações, consulte o artigo [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Versão 1511, 1602 e 1606**   
 É possível configurar a velocidade da ligação de rede de cada ponto de distribuição num grupo de limites:  

-   Os clientes utilizam este valor quando se ligam ao ponto de distribuição.

-   Por predefinição, a velocidade da ligação de rede está configurada como **rapidamente**, mas também pode ser definido como **lenta**.  

-   O **velocidade da ligação de rede**, juntamente com a configuração de uma implementação, determinar se um cliente pode transferir conteúdo a partir de um ponto de distribuição quando o cliente se encontra num grupo de limites associado  

Para obter informações sobre os cenários de contingência e outra localização de conteúdo, consulte o artigo [cenários de localização de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Para obter informações sobre grupos de limites, consulte o artigo [grupos de limites para versões 1511,1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## <a name="on-demand-content-distribution"></a>Distribuição de conteúdo a pedido  
 Distribuição de conteúdo a pedido é uma opção, pode definir para individuais de pontos de distribuição preferenciais distribuição de conteúdo de aplicações e pacotes (implementações) para ativar a pedido.  

-   Para ativar esta opção para uma implementação, ative **distribuir o conteúdo do pacote para pontos de distribuição preferenciais**.  

-   Quando esta opção está ativada para uma implementação e um cliente tenta pedir que o conteúdo, mas o conteúdo não está disponível em qualquer um dos pontos de distribuição preferenciais do cliente, o Configuration Manager distribui automaticamente esse conteúdo aos pontos de distribuição preferenciais do cliente.  

-   Apesar de isto aciona do Configuration Manager distribuísse automaticamente o conteúdo para pontos de distribuição preferenciais esse cliente, o cliente poderá obter esse conteúdo a partir de outros pontos de distribuição antes dos pontos de distribuição preferidos para o cliente recebem a implementação. Quando isto ocorre, o conteúdo, em seguida, estará presente nesse ponto de distribuição para ser utilizado pelo cliente seguinte que procura dessa implementação.  

Se utilizar a versão 1610 ou posterior, consulte o artigo [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
Se utilizar a versão 1511, 1602 ou 1606, consulte o artigo [cenários de localização de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) para obter informações sobre os cenários de contingência e localização de conteúdo diferentes.  



## <a name="package-transfer-manager"></a>Gestor de Transferência de Pacotes  
 Gestor de transferência de pacotes é o componente de servidor do site que transfere o conteúdo para pontos de distribuição noutros computadores.  

 Saiba mais sobre o [Gestor de transferência do](../../../core/plan-design/hierarchy/package-transfer-manager.md).  

## <a name="preferred-distribution-point"></a>Ponto de distribuição preferencial  
 Um ponto de distribuição preferenciais inclui quaisquer pontos de distribuição que estão associados a grupos de limites atual do cliente.  

 Tem a opção de associar cada ponto de distribuição a um ou mais grupos de limites:  

-   Esta associação ajuda o cliente de identificar os pontos de distribuição a partir do qual pode transferi-lo.  
-   Por predefinição, os clientes apenas podem transferir conteúdo a partir do ponto de distribuição preferencial.  


Para obter mais informações:
 - Se utilizar a versão 1610 ou posterior, consulte o artigo [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - Se utilizar a versão 1511, 1602 ou 1606, consulte o artigo [cenários de localização de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).

## <a name="prestage-content"></a>Pré-configurar conteúdo  
 Pré-configurar o conteúdo é um processo de transferência de conteúdo para um ponto de distribuição sem entidade confiadora no Configuration Manager para distribuir os conteúdos através da rede.  

 Para obter mais informações, consulte o artigo [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

