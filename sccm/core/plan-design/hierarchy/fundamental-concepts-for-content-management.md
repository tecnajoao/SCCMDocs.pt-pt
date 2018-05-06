---
title: Noções básicas de gestão de conteúdo
titleSuffix: Configuration Manager
description: Utilizar as ferramentas e opções no Configuration Manager para gerir o conteúdo que implementar.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5dfe33e7182eae158c15afb848d3a9f1702678ba
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager suporta um sistema robusto de ferramentas e opções para gerir o conteúdo que implementar como aplicações, pacotes, atualizações de software e implementações de SO. O Configuration Manager armazene o conteúdo nos servidores de site e pontos de distribuição. Este conteúdo necessita de uma grande quantidade de largura de banda de rede quando está a ser transferido entre localizações. Para planear e utilizar a infraestrutura de gestão de conteúdos eficazmente, recomendamos que compreende as opções disponíveis e as configurações. Em seguida, considerar como utilizá-las para melhor opção do seu ambiente de rede e as necessidades de implementação de conteúdos.  

> [!TIP]    
> Para obter mais informações sobre o processo de distribuição de conteúdo e para encontrar ajuda no diagnosticar e resolver problemas gerais de distribuição de conteúdo, consulte [Noções e resolução de problemas de distribuição de conteúdo no Configuration Manager ](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Os tópicos seguintes são conceitos chave para gestão de conteúdo. Quando um conceito precisar de informações complexas ou adicionais, são fornecidas hiperligações para direcioná-lo para esses detalhes.



## <a name="accounts-used-for-content-management"></a>Contas utilizadas para a gestão de conteúdos  
 As contas que se seguem podem ser utilizadas com a gestão de conteúdos:  

-   **Conta de acesso de rede**: Utilizada pelos clientes para ligar a um ponto de distribuição e aceder ao conteúdo. Por predefinição, a conta de computador está experimentada em primeiro lugar.  

     Esta conta é também utilizada pelos pontos de distribuição de solicitação transferir conteúdo de um ponto de distribuição de origem numa floresta remota.  

-   **Conta de acesso a pacote**: Por predefinição, o Configuration Manager concede acesso a conteúdo num ponto de distribuição para as contas de acesso genérico utilizadores e administradores. No entanto, pode configurar permissões adicionais para restringir o acesso.   

-   **Conta de ligação de multicast**: Utilizado para implementações de SO.  

Para mais informações sobre estas contas, consulte [gerir contas para aceder ao conteúdo](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).



## <a name="bandwidth-throttling-and-scheduling"></a>Limitação de largura de banda e agendamento  
 Tanto a limitação como o agendamento são opções que o ajudam a controlar quando o conteúdo é distribuído de um servidor do site para pontos de distribuição. Estas capacidades são semelhantes, mas não diretamente relacionado com controlos de largura de banda para replicação baseada em ficheiros do site para site.  

 Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Replicação diferencial binária  
 A replicação diferencial binária (BDR) é um pré-requisito para pontos de distribuição. Este é por vezes conhecida como replicação delta. Quando está a distribuir atualizações de conteúdo que implementou anteriormente para outros sites ou para pontos de distribuição remoto, a BDR é automaticamente utilizado para reduzir a largura de banda.  

 A BDR minimiza a largura de banda de rede utilizada para enviar atualizações de conteúdo distribuído. Reenviar apenas o conteúdo novo ou alterado, em vez de enviar o conjunto completo de ficheiros de origem do conteúdo sempre que alterar esses ficheiros.  

 Quando a BDR é utilizada, o Configuration Manager identifica as alterações que ocorrem nos ficheiros de origem para cada conjunto de conteúdos que tenha anteriormente distribuído.  

-   Quando alterar ficheiros de conteúdo de origem, o site cria uma nova versão incremental do conjunto de conteúdos. Em seguida, replica apenas os ficheiros alterados para sites de destino e de pontos de distribuição. Um ficheiro é considerado alterado se mudar o nome ou moveu-o, ou se tiver alterado o conteúdo do ficheiro. Por exemplo, se substituir um único ficheiro de controlador para um pacote de controladores que tenha anteriormente distribuído por vários sites, é replicado apenas o ficheiro de controlador alterado.  

-   O Configuration Manager suporta até cinco versões incrementais de um conjunto antes de reenviar o conjunto completo de conteúdo de conteúdos. Após a quinta atualização, a próxima alteração ao conjunto de conteúdos faz com que o site para criar uma nova versão do conjunto de conteúdos. Em seguida, o Configuration Manager distribui a nova versão de conteúdo definida para substituir o conjunto anterior e todas as versões incrementais. Depois do novo conjunto de conteúdo é distribuído, as alterações incrementais subsequentes aos ficheiros de origem serão novamente replicadas por BDR.  

A BDR é suportada entre cada site principal e site subordinado numa hierarquia. A BDR é suportada num site entre o servidor do site e os respetivos pontos de distribuição normal. No entanto, os pontos de distribuição de solicitação e pontos de distribuição baseado na nuvem não suportam BDR para transferir conteúdo. Os pontos de distribuição de solicitação suportam deltas de nível de ficheiros, transferir os novos ficheiros, mas não os blocos de um ficheiro.

As aplicações utilizam sempre a replicação diferencial de binários. BDR é opcional para pacotes e não está ativada por predefinição. Para utilizar a BDR para pacotes, ative esta funcionalidade para cada pacote. Selecione a opção **ativar a replicação diferencial de binários** quando criar ou editar um pacote.   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](/windows-server/networking/branchcache/branchcache) é uma tecnologia do Windows. Clientes que suportam o BranchCache e que tenham transferido uma implementação que configurou para Branch Cache, em seguida, servirem como uma origem de conteúdo para outros clientes com capacidade para BranchCache.  

 Por exemplo, tiver um ponto de distribuição que executa o Windows Server 2012 ou posterior e está configurado como servidor BranchCache. Quando o primeiro cliente com capacidade BranchCache pede conteúdo a partir deste servidor, o cliente transfere esse conteúdo e coloca em cache-lo.  

- Que o cliente, em seguida, disponibiliza o conteúdo para a capacidade de BranchCache clientes adicionais na mesma sub-rede que também colocam em cache o conteúdo.  
- Outros clientes na mesma sub-rede não tem de transferir conteúdo do ponto de distribuição.  
- O conteúdo é distribuído por vários clientes para futuras transferências.  



## <a name="delivery-optimization"></a>Otimização de entrega
<!-- 1324696 -->
Utilize grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo através da rede empresarial em escritórios remotos. [Otimização de entrega de Windows](/windows/deployment/update/waas-delivery-optimization) é uma tecnologia de baseado na nuvem, ponto a ponto para partilhar conteúdo entre dispositivos Windows 10. A partir de versão 1802, configure a otimização de entrega a utilizar os grupos de limites, quando a partilha de conteúdo entre elementos. Definições de cliente aplicam-se o identificador do grupo de limites como o identificador do grupo de otimização de entrega no cliente. Quando o cliente comunica com o serviço de nuvem de otimização de entrega, utiliza este identificador para localizar os elementos de rede com os conteúdos pretendidos. Para obter mais informações, consulte [otimização de entrega](/sccm/core/clients/deploy/about-client-settings#delivery-optimization) as definições de cliente.



## <a name="peer-cache"></a>Cache ponto a ponto
A cache de cliente ajuda-o a gerir a implementação de conteúdo para clientes em localizações remotas. A cache é uma solução incorporada do Configuration Manager que permite que os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local.

Depois de implementar as definições de cliente que permitem a cache ponto a ponto numa coleção, os membros dessa coleção podem agir como uma origem de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites.

Para obter mais informações, consulte [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Cache ponto a ponto do Windows PE
Quando implementa um novo SO com o Configuration Manager, computadores que executam a sequência de tarefas podem utilizar a cache de ponto a ponto do Windows PE. Transferem conteúdo de uma origem de cache ponto a ponto, em vez de um ponto de distribuição. Este comportamento ajuda a minimizar WAN tráfego em cenários de sucursais onde não existe nenhum ponto de distribuição local.

Para obter mais informações, consulte [cache de ponto a ponto do Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).



## <a name="client-locations"></a>Localizações de clientes  
 Seguem-se as localizações a partir das quais os clientes acedem a conteúdo:  

-   **Intranet** (no local):  

    -   Pontos de distribuição podem utilizar HTTP ou HTTPs.  

    -   Utilize apenas um ponto de distribuição baseado na nuvem para contingência quando pontos de distribuição no local não estão disponíveis.  

-   **Internet**:  

    -   Necessita de pontos de distribuição para aceitar HTTPS.  

    -   Pode utilizar um ponto de distribuição baseado na nuvem para contingência.  

-   **Grupo de Trabalho**:  

    -   Necessita de pontos de distribuição para aceitar HTTPS.  

    -   Pode utilizar um ponto de distribuição baseado na nuvem para contingência.  



## <a name="content-library"></a>Biblioteca de conteúdos  
 A biblioteca de conteúdos é o arquivo de instância única de conteúdo no Configuration Manager. Esta biblioteca reduz o tamanho geral do conteúdo que distribui.  

- Saiba mais sobre o [biblioteca de conteúdos](../../../core/plan-design/hierarchy/the-content-library.md).
- Utilize o [ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo que já não está associado uma aplicação.  



## <a name="distribution-points"></a>Pontos de distribuição  
 Configuration Manager utiliza pontos de distribuição para armazenar os ficheiros que são necessários para o software seja executado em computadores cliente. Os clientes devem ter acesso a, pelo menos, um ponto de distribuição partir dos quais poderão transferir os ficheiros de conteúdo que implementar.  

 O ponto de distribuição básico (não especializado) é normalmente denominado como um ponto de distribuição padrão. Existem duas variações no ponto de distribuição padrão que recebem especial atenção:  

-   **Ponto de distribuição de solicitação**: Uma variação de um ponto de distribuição em que o ponto de distribuição obtém conteúdo de outro ponto de distribuição (um ponto de distribuição de origem). Este processo é semelhante à forma como os clientes transferem conteúdo de pontos de distribuição. Pontos de distribuição de solicitação podem ajudar a evitar congestionamentos de largura de banda de rede que ocorrem quando o servidor do site tem de distribuir diretamente conteúdo para cada ponto de distribuição. [Utilizar um ponto de distribuição de solicitação](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Ponto de distribuição baseado na nuvem**: Uma variação de um ponto de distribuição que está instalado no Microsoft Azure. [Saiba como utilizar um ponto de distribuição baseado na nuvem](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Um intervalo de configurações e funcionalidades de suporte de pontos de distribuição padrão:  

- Utilize os controlos, tais como **agendas** ou **limitação de largura de banda** para ajudar a controlar a transferência.  
- Utilizar outras opções, incluindo **conteúdo pré-configurado**, e **pontos de distribuição de solicitação** para minimizar e controlar o consumo de rede. 
- **BranchCache**, **elemento cache**, e **otimização de entrega** são tecnologias ponto a ponto para reduzir a largura de banda de rede que é utilizada quando implementar o conteúdo.  
- Existem diferentes configurações para implementações do SO, tais como **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** e  **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**
- As opções para **dispositivos móveis**   
  
  
Baseado na nuvem e de pontos de distribuição de solicitação suportam muitas destas configurações, mas têm limitações específicas para cada variação de ponto de distribuição.  



## <a name="distribution-point-groups"></a>Grupos de pontos de distribuição  
 Grupos de pontos de distribuição são agrupamentos lógicos de pontos de distribuição que podem simplificar a distribuição de conteúdo.  

 Para obter mais informações, consulte [gerir grupos de pontos de distribuição](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).



## <a name="distribution-point-priority"></a>Prioridade de pontos de distribuição  
 O valor de prioridade do ponto de distribuição baseia-se na quantidade de tempo necessária para transferir implementações anteriores para esse ponto de distribuição.  

-   Este valor é sintonização automática. Está definido em cada ponto de distribuição para o ajudar a Configuration Manager mais rapidamente transferir conteúdo para pontos de distribuição mais.  

-   Quando distribui conteúdos a vários pontos de distribuição em simultâneo, ou para um grupo de pontos de distribuição, o site envia pela primeira vez o conteúdo para o servidor com a prioridade mais elevada. Em seguida, envia mesmos conteúdos para um ponto de distribuição com uma prioridade mais baixa.  

-   Prioridade de ponto de distribuição não substitui a prioridade de distribuição de pacotes. Prioridade de pacote permanece o fator decisivo de quando o site envia um conteúdo diferente.  

Por exemplo, tiver um pacote que tenha uma prioridade elevada do pacote. Distribui-lo para um servidor com uma prioridade de ponto de distribuição baixa. Este pacote de prioridade elevada será sempre transferido antes de um pacote que tenha uma prioridade mais baixa. A prioridade do pacote aplica-se mesmo que o site, distribui pacotes de prioridade inferiores aos servidores com superiores prioridades de ponto de distribuição.

A prioridade elevada do pacote garante que o Configuration Manager distribui esse conteúdo aos pontos de distribuição antes de enviar quaisquer pacotes com uma prioridade mais baixa.  

> [!NOTE]  
>  Os pontos de distribuição de extração também utilizam um conceito de prioridade para ordenar a sequência dos respetivos pontos de distribuição de origem.  
>   
>  -   A prioridade de ponto de distribuição para transferências de conteúdo para o servidor é distinta da prioridade que os pontos de distribuição de solicitação utilizam. Pontos de distribuição de solicitação utilizam a sua prioridade quando procuram conteúdo de um ponto de distribuição de origem.  
>  -   Para obter mais informações, consulte [utilizar um ponto de distribuição de solicitação](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  



## <a name="fallback"></a>Contingência  
 Vários aspetos foram alterados com o ramo do Gestor de configuração atual da forma que os clientes localizam um ponto de distribuição que tenha o conteúdo, incluindo contingência. 

Clientes que não é possível localizar o conteúdo de um ponto de distribuição associado ao respetivo grupo de limites atuais revertam para utilizarem as localizações de origem de conteúdo associadas a grupos de limites de vizinho. Para ser utilizado para contingência, um grupo de limites de vizinho tem de ter uma relação definida com o grupo de limites atual do cliente. Esta relação inclui uma vez configurada que deve passar antes de um cliente que não é possível localizar o conteúdo localmente inclui origens de conteúdo do grupo de limites de vizinho como parte da sua pesquisa.

Os conceitos do já não são utilizados pontos de distribuição preferenciais e definições de **permitir que as localizações de origem de contingência para conteúdo** já não estão disponíveis ou imposta.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that can't get a deployment from one of its preferred distribution points.  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="network-bandwidth"></a>Largura de banda da rede  
 Para ajudar a gerir a quantidade de largura de banda de rede que é utilizada quando distribui conteúdo, pode utilizar as seguintes opções:  

-   **Conteúdo pré-configurado**: Transferir conteúdo para um ponto de distribuição sem a distribuição de conteúdos através da rede.  

-   **Agendamento e limitação**: As configurações que o ajudam a controlam quando e como o conteúdo é distribuído para pontos de distribuição.  

Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Velocidade da ligação de rede à origem de conteúdo  
 Vários aspetos foram alterados com o ramo do Gestor de configuração atual da forma que os clientes localizam um ponto de distribuição que tenha o conteúdo. Estas alterações incluem a velocidade da rede a uma origem de conteúdo. 

Velocidades de ligação de rede que definem uma distribuição apontar como **Rápido** ou **lenta** já não são utilizadas. Em vez disso, cada sistema de sites que está associada um grupo de limites é Tratado da mesma.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="on-demand-content-distribution"></a>Distribuição de conteúdo a pedido  
 Distribuição de conteúdo a pedido é uma opção para implementações de aplicações e pacotes individuais. Esta opção permite a distribuição de conteúdo a pedido para servidores preferenciais.  

-   Para ativar esta definição para uma implementação, ative: **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais**.  

-   Quando esta opção está ativada para uma implementação e um cliente tenta pedir esse conteúdo, mas o conteúdo não está disponível em qualquer um dos pontos de distribuição preferenciais do cliente, o Configuration Manager distribui automaticamente esse conteúdo aos pontos de distribuição preferenciais do cliente.  

-   Embora isto acione o Configuration Manager para distribuir automaticamente o conteúdo para pontos de distribuição preferenciais desse cliente, o cliente poderá obter esse conteúdo de outros pontos de distribuição antes dos pontos de distribuição preferencial para o cliente recebem a implementação. Quando este comportamento ocorre, o conteúdo estará presente nesse ponto de distribuição para utilização pelo cliente seguinte que procura essa implementação.  

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.
-->



## <a name="package-transfer-manager"></a>Gestor de transferência de pacotes  
 Gestor de transferência de pacotes é o componente de servidor do site transfere conteúdo para pontos de distribuição noutros computadores.  

 Para obter mais informações, consulte [Gestor de transferência de pacotes](../../../core/plan-design/hierarchy/package-transfer-manager.md).  



<!--
## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).
-->



## <a name="prestage-content"></a>Pré-configurar conteúdo  
 Pré-configuração de conteúdo é um processo de transferência de conteúdo para um ponto de distribuição sem a distribuição de conteúdos através da rede.  

 Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
