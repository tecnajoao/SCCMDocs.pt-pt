---
title: Noções básicas da gestão de conteúdo
titleSuffix: Configuration Manager
description: Utilize ferramentas e opções no Configuration Manager para gerir o conteúdo que implementar.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c3af900bae26262ba402ea258b8859ba07b999b
ms.sourcegitcommit: 4f05517f7b284696a492a1b184cc5f25c5cda5e6
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/09/2018
ms.locfileid: "48891219"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Conceitos fundamentais da gestão de conteúdos no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager suporta um sistema robusto de ferramentas e opções para gerir o conteúdo de software. Tem de implementações de software como aplicações, pacotes, atualizações de software e implementações de sistema operacional todos os conteúdos. Gestor de configuração armazena o conteúdo nos servidores de site e pontos de distribuição. Este conteúdo requer uma grande quantidade de largura de banda de rede quando estiverem a ser transferido entre localizações. Para planear e utilizar a infraestrutura de gerenciamento de conteúdo de forma eficaz, primeiro compreenda as opções disponíveis e as configurações. Necessidades de implementação de conteúdos e, em seguida, considerar como utilizá-las para melhor se adequa a seu ambiente de rede.  

> [!TIP]    
> Para obter mais informações sobre o processo de distribuição de conteúdo e para encontrar ajuda no diagnóstico e a resolução de problemas gerais de distribuição de conteúdo, consulte [compreensão e resolução de problemas de distribuição de conteúdo no Configuration Manager ](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Os tópicos seguintes são conceitos chave para a gestão de conteúdos. Quando um conceito precisar de informações complexas ou adicionais, são fornecidas hiperligações para direcioná-lo para esses detalhes.



## <a name="accounts-used-for-content-management"></a>Contas utilizadas para a gestão de conteúdos  
 As contas que se seguem podem ser utilizadas com a gestão de conteúdos:  

-   **Conta de acesso de rede**: Utilizada por clientes para ligar a um ponto de distribuição e aceder a conteúdo. Por predefinição, a conta de computador é experimentada em primeiro lugar.  

     Esta conta é também utilizada pelos pontos de distribuição de extração transferir conteúdo de um ponto de distribuição de origem numa floresta remota.  

-   **Conta de acesso a pacote**: Por predefinição, o Configuration Manager concede acesso a conteúdo num ponto de distribuição às contas de acesso genérico utilizadores e administradores. No entanto, pode configurar permissões adicionais para restringir o acesso.   

-   **Conta de ligação de multicast**: Utilizada para implementações de sistema operacional.  

Para obter mais informações sobre estas contas, consulte [gerir contas para aceder a conteúdo](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content).



## <a name="bandwidth-throttling-and-scheduling"></a>Limitação de largura de banda e agendamento  
 Tanto a limitação como o agendamento são opções que o ajudam a controlar quando o conteúdo é distribuído de um servidor do site para pontos de distribuição. Estas capacidades são semelhantes, mas não diretamente relacionado a controlos de largura de banda para replicação baseada em ficheiros de site a site.  

 Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Replicação diferencial binária  
 Replicação diferencial binária (BDR) é um pré-requisito para pontos de distribuição. Por vezes, é conhecido como a replicação de diferenças. Quando está a distribuir atualizações de conteúdo que implementou anteriormente para outros sites ou para pontos de distribuição remoto, a BDR é automaticamente utilizada para reduzir a largura de banda.  

 A BDR minimiza a largura de banda de rede utilizada para enviar atualizações de conteúdo distribuído. Reenviar apenas o conteúdo novo ou alterado, em vez de enviar o conjunto completo de arquivos de origem do conteúdo sempre que alterar esses ficheiros.  

 Quando a BDR é usada, o Configuration Manager identifica as alterações que ocorrem para ficheiros de origem para cada conjunto de conteúdo que tenha anteriormente distribuído.  

-   Quando os ficheiros no conteúdo de origem são alterados, o site cria uma nova versão incremental do conteúdo. Em seguida, replica apenas os ficheiros alterados para sites de destino e de pontos de distribuição. Um ficheiro será considerado alterado se mudar o nome ou movê-la, ou se tiver alterado o conteúdo do ficheiro. Por exemplo, se substituir um único ficheiro de controlador para um pacote de controladores que tenha anteriormente distribuído por vários sites, apenas o ficheiro de controlador alterado é replicado.  

-   O Configuration Manager suporta até cinco versões incrementais de um conjunto antes de reenviar o conjunto de conteúdos completo de conteúdos. Após a quinta atualização, a próxima alteração para o conjunto de conteúdos faz com que o site para criar uma nova versão do conjunto de conteúdos. Em seguida, o Configuration Manager distribui a nova versão do conteúdo definido como substituir o conjunto anterior e todas suas as versões incrementais. Depois do novo conjunto de conteúdo é distribuído, as alterações incrementais subsequentes aos ficheiros de origem serão novamente replicadas por BDR.  

A BDR é suportada entre cada site principal e site subordinado numa hierarquia. A BDR é suportada num site entre o servidor do site e os respetivos pontos de distribuição regular. No entanto, os pontos de distribuição de extração e pontos de distribuição de cloud não é suportada a BDR para transferir o conteúdo. Pontos de distribuição de extração suportam deltas de ao nível dos ficheiros, transferir os ficheiros novos, mas não os blocos dentro de um arquivo.

As aplicações utilizam sempre a replicação diferencial de binários. A BDR é opcional para pacotes e não está ativada por predefinição. Para utilizar a BDR para pacotes, ative esta funcionalidade para cada pacote. Selecione a opção **ativar a replicação diferencial de binários** quando criar ou editar um pacote.   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) é uma tecnologia do Windows. Os clientes que suportam o BranchCache e que tenham transferido uma implementação que configurou para o BranchCache, em seguida, servem como uma origem de conteúdo para outros clientes habilitados para BranchCache.  

 Por exemplo, tem um ponto de distribuição que executa o Windows Server 2012 ou posterior e é configurado como servidor BranchCache. Quando o primeiro cliente de capacidade para BranchCache pede conteúdo a partir deste servidor, o cliente transfere esse conteúdo e armazena em cache.  

- Esse cliente, em seguida, disponibiliza o conteúdo de capacidade para BranchCache clientes adicionais na mesma sub-rede que também colocam em cache o conteúdo.  
- Outros clientes na mesma sub-rede não precisam de transferir o conteúdo do ponto de distribuição.  
- O conteúdo é distribuído por vários clientes para futuras transferências.  

Para obter mais informações, consulte [suporte para o Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache).



## <a name="delivery-optimization"></a>Otimização da entrega
<!-- 1324696 --> Utilizar grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo em sua rede empresarial e em escritórios remotos. [Otimização da entrega do Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) é uma tecnologia baseada na cloud, o ponto-a-ponto para partilhar conteúdo entre os dispositivos Windows 10. A partir da versão 1802, configure a otimização de entrega a utilizar os grupos de limites, quando partilha de conteúdo entre elementos de rede. Definições de cliente aplicam-se o identificador de grupo de limites como o identificador de grupo de Otimização da entrega no cliente. Quando o cliente comunica com o serviço de cloud de otimização de entrega, ele usa esse identificador para localizar os colegas com os conteúdos pretendidos. Para obter mais informações, consulte [Otimização da entrega](/sccm/core/clients/deploy/about-client-settings#delivery-optimization) as definições de cliente.

Otimização da entrega é a tecnologia recomendada para [Otimize a entrega de atualização do Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery) de ficheiros de instalação rápida para as atualizações de qualidade do Windows 10.



## <a name="windows-ledbat"></a>Windows LEDBAT
<!--1358112--> Windows baixa Extra atraso em segundo plano transporte (LEDBAT) é uma funcionalidade de controlo de congestionamento de rede do Windows Server para o ajudar a gerir as transferências de rede em segundo plano. Para pontos de distribuição em execução em versões suportadas do Windows Server, ative uma opção para o ajudar a ajustar o tráfego de rede. Em seguida, os clientes só utilizam largura de banda de rede quando estiver disponível. 

Para obter mais informações sobre Windows LEDBAT em geral, consulte a [avanços de transporte de New](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) postagem de blog.

Para obter mais informações sobre como utilizar o Windows LEDBAT com pontos de distribuição do Configuration Manager, consulte a definição para **ajustar a velocidade de transferência para utilizar a largura de banda de rede não utilizadas (Windows LEDBAT)** quando [configurar as definições gerais de um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-general).



## <a name="peer-cache"></a>Cache ponto a ponto
Cache ponto a ponto de cliente ajuda-o a gerir a implementação de conteúdo para clientes em localizações remotas. Cache ponto a ponto é uma solução incorporada do Configuration Manager que permite que os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local.

Primeiro, implemente definições de cliente que permitem a cache ponto a ponto para uma coleção. Em seguida, os membros dessa coleção podem agir como uma origem de conteúdo de ponto a ponto para outros clientes no mesmo grupo de limites.

A partir da versão 1806, origens de cache ponto a ponto do cliente podem dividir o conteúdo em partes. Estas peças minimizam a transferência de rede para reduzir a utilização da WAN. O ponto de gestão fornece controlo mais detalhado das partes de conteúdo. Ele tenta eliminar mais do que uma transferência do conteúdo do mesmo por grupo de limites.<!--1357346-->

Para obter mais informações, consulte [configurar o Peering em cache para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Cache ponto a ponto do Windows PE
Quando implementa um novo sistema operacional com o Configuration Manager, os computadores que executam a sequência de tarefas podem utilizar a cache de ponto a ponto do Windows PE. Transferem conteúdo de uma origem de cache ponto a ponto, em vez de partir de um ponto de distribuição. Este comportamento ajuda a minimizar a WAN de tráfego em cenários de sucursais onde não existe nenhum ponto de distribuição local.

Para obter mais informações, consulte [cache de ponto a ponto do Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).



## <a name="client-locations"></a>Localizações de clientes  
 Seguem-se as localizações a partir das quais os clientes acedem a conteúdo:  

-   **Intranet** (no local):  

    -   Pontos de distribuição podem utilizar HTTP ou HTTPs.  

    -   Utilize apenas um ponto de distribuição de nuvem para contingência quando os pontos de distribuição no local não estão disponíveis.  

-   **Internet**:  

    -   Requer acesso à internet de pontos de distribuição para aceitar HTTPS.  

    -   Pode utilizar um ponto de distribuição de nuvem.  

-   **Grupo de Trabalho**:  

    -   Necessita de pontos de distribuição para aceitar HTTPS.  

    -   Pode utilizar um ponto de distribuição de nuvem.  



## <a name="content-source-priority"></a>Prioridade de origem de conteúdo

Quando um cliente tem de conteúdo, faz um pedido de localização de conteúdo ao ponto de gestão. O ponto de gestão devolve uma lista de localizações de origem que são válidas para o conteúdo solicitado. Esta lista varia consoante o cenário específico, tecnologias em uso, design de site, grupos de limites e as definições de implementação. A lista seguinte contém todas as localizações de origem de conteúdo possível que um cliente pode utilizar, na ordem em que ele estabelece uma prioridade:  

1.  O ponto de distribuição no mesmo computador que o cliente
2.  Uma origem ponto a ponto na mesma sub-rede de rede
3.  Um ponto de distribuição na mesma sub-rede de rede
4.  Uma origem ponto a ponto no mesmo grupo de limites
5.  Um ponto de distribuição no grupo de limites atual
6.  Um ponto de distribuição num grupo de limite vizinho configurado para contingência
9.  Um ponto de distribuição no grupo de limite de site predefinido 
10. O serviço em nuvem do Windows Update
11. Um ponto de distribuição de acesso à internet
12. Um ponto de distribuição de nuvem no Azure



## <a name="content-library"></a>Biblioteca de conteúdos  
 A biblioteca de conteúdos é o armazenamento de instância única de conteúdo no Configuration Manager. Esta biblioteca reduz o tamanho geral do conteúdo que distribui.  

- Saiba mais sobre o [biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library).
- Utilize o [ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo que já não está associado um aplicativo.  



## <a name="distribution-points"></a>Pontos de distribuição  
 Configuration Manager utiliza pontos de distribuição para armazenar os ficheiros que são necessários para o software seja executado em computadores cliente. Os clientes devem ter acesso a, pelo menos, um ponto de distribuição do qual possam transferir os ficheiros para conteúdo que implementar.  

 O ponto de distribuição básico (não especializado) é frequentemente referido como um ponto de distribuição padrão. Existem duas variações no ponto de distribuição padrão que recebem especial atenção:  

-   **Ponto de distribuição de extração**: Uma variação de um ponto de distribuição em que o ponto de distribuição obtém conteúdo de outro ponto de distribuição (um ponto de distribuição de origem). Este processo é semelhante à forma como os clientes transferem conteúdo de pontos de distribuição. Pontos de distribuição de extração podem ajudar a evitar congestionamentos de largura de banda de rede que ocorrem quando o servidor do site tem de distribuir diretamente conteúdo para cada ponto de distribuição. [Utilizar um ponto de distribuição de extração](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Ponto de distribuição da nuvem**: Uma variação de um ponto de distribuição que está instalado no Microsoft Azure. [Saiba como utilizar um ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point).  


Pontos de distribuição padrão suportam uma variedade de configurações e funcionalidades:  

- Utilizar como controles **agendas** ou **limitação de largura de banda** para ajudar a controlar a transferência.  

- Utilizar outras opções, incluindo **conteúdo pré-configurado**, e **pontos de distribuição de extração** para minimizar e controlar o consumo de rede.  

- **BranchCache**, **configurar o peering em cache**, e **Otimização da entrega** são tecnologias ponto a ponto para reduzir a largura de banda de rede que é utilizada na implementação de conteúdo.  

- Existem diferentes configurações para Implantações de SO, tais como **[PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)** e  **[Multicast](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_DPMulticast)**  

- Opções de **dispositivos móveis**   
  
Pontos de distribuição de nuvem e de solicitação suportam muitas destas mesmas configurações, mas têm limitações específicas para cada variação de ponto de distribuição.  



## <a name="distribution-point-groups"></a>Grupos de pontos de distribuição  
 Grupos de pontos de distribuição são agrupamentos lógicos de pontos de distribuição que podem simplificar a distribuição de conteúdo.  

 Para obter mais informações, consulte [gerir grupos de pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage).



## <a name="distribution-point-priority"></a>Prioridade de pontos de distribuição  
 O valor de prioridade do ponto de distribuição baseia-se na quantidade de tempo necessária para transferir implementações anteriores para esse ponto de distribuição.  

-   Este valor é o ajuste automático. Ele é definido em cada ponto de distribuição para o ajudar a Configuration Manager mais rapidamente transferir conteúdo para mais pontos de distribuição.  

-   Quando distribui conteúdo para vários pontos de distribuição, ao mesmo tempo ou para um grupo de pontos de distribuição, o site envia pela primeira vez o conteúdo para o servidor com a prioridade mais alta. Em seguida, envia os mesmos conteúdos para um ponto de distribuição com uma prioridade mais baixa.  

-   Prioridade de ponto de distribuição não substitui a prioridade de distribuição de pacotes. Prioridade do pacote permanece o fator decisivo de quando o site envia conteúdo diferente.  

Por exemplo, tiver um pacote que tenha uma prioridade elevada do pacote. Distribuí-la para um servidor com uma prioridade de ponto de distribuição baixa. Este pacote de alta prioridade sempre transferido antes de um pacote que tenha uma prioridade mais baixa. A prioridade do pacote aplica-se mesmo que o site distribui pacotes de prioridade mais baixas para servidores com prioridades superiores de ponto de distribuição.

Alta prioridade do pacote garante que o Configuration Manager distribui esse conteúdo aos pontos de distribuição antes de enviar quaisquer pacotes com uma prioridade mais baixa.  

> [!NOTE]  
>  Os pontos de distribuição de extração também utilizam um conceito de prioridade para ordenar a sequência dos respetivos pontos de distribuição de origem.  
>   
>  -   A prioridade de ponto de distribuição para as transferências de conteúdo para o servidor é distinta da prioridade que os pontos de distribuição de extração utilizam. Os pontos de distribuição de extração utilizam sua prioridade quando estes procurem conteúdo de um ponto de distribuição de origem.  
>  -   Para obter mais informações, consulte [utilizar um ponto de distribuição de extração](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  



## <a name="fallback"></a>Contingência  
 Várias coisas mudaram com o Configuration Manager Current Branch da forma que os clientes localizam um ponto de distribuição que tenha o conteúdo, incluindo de contingência. 

Os clientes que não é possível localizar o conteúdo de um ponto de distribuição associada ao respetivo grupo de limites atual revertam para utilizar localizações de origem de conteúdo associadas a grupos de limites de vizinho. Para ser usado para contingência, um grupo de limite vizinho tem de ter uma relação definida com o grupo de limites atual do cliente. Esta relação inclui um tempo configurado que deve passar antes de um cliente que não é possível localizar o conteúdo localmente inclui fontes de conteúdo do grupo de limite vizinho como parte da sua pesquisa.

Os conceitos de já não são utilizados pontos de distribuição preferenciais e configurações para **permitir que as localizações de origem de contingência para conteúdo** já não estão disponíveis ou imposto.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).



## <a name="network-bandwidth"></a>Largura de banda da rede  
 Para ajudar a gerir a quantidade de largura de banda de rede que é utilizada quando distribui conteúdo, pode utilizar as seguintes opções:  

-   **Conteúdo pré-configurado**: Transferir conteúdo para um ponto de distribuição sem a distribuição de conteúdos através da rede.  

-   **Agendamento e limitação**: Configurações que o ajudam a controlar quando e como o conteúdo é distribuído para pontos de distribuição.  

Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Velocidade da ligação de rede à origem de conteúdo  
 Várias coisas mudaram com o Configuration Manager Current Branch da forma que os clientes localizam um ponto de distribuição que tenha o conteúdo. Estas alterações incluem a velocidade da rede a uma origem de conteúdo. 

Velocidades de conexão de rede que definem uma distribuição ponto a como **rapidamente** ou **lenta** já não são utilizadas. Em vez disso, cada sistema de sites que está associada um grupo de limites é Tratado da mesma.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).



## <a name="on-demand-content-distribution"></a>Distribuição de conteúdo a pedido  
 Distribuição de conteúdo a pedido é uma opção para implementações de pacotes e aplicações individuais. Esta opção permite a distribuição de conteúdo a pedido para os servidores preferenciais.  

-   Para ativar esta definição para uma implementação, ative: **Distribuir o conteúdo do pacote para pontos de distribuição preferenciais**.  

-   Quando ativa esta opção para uma implementação e um cliente solicita que o conteúdo, mas o conteúdo não está disponível em qualquer um dos pontos de distribuição preferenciais do cliente, o Configuration Manager distribui automaticamente esse conteúdo para o cliente preferencial pontos de distribuição.  

-   Embora isto acione o Configuration Manager para distribuir automaticamente o conteúdo para pontos de distribuição preferenciais desse cliente, o cliente poderá obter esse conteúdo de outros pontos de distribuição antes dos pontos de distribuição preferenciais do cliente receba a implementação. Quando este comportamento ocorre, o conteúdo estará presente nesse ponto de distribuição para utilização pelo cliente seguinte que procura essa implementação.  

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).



## <a name="package-transfer-manager"></a>Gestor de transferência de pacotes  
 Gestor de transferência de pacotes é o componente de servidor do site transfere conteúdo para pontos de distribuição noutros computadores.  

 Para obter mais informações, consulte [Gestor de transferência de pacotes](/sccm/core/plan-design/hierarchy/package-transfer-manager).  



## <a name="prestage-content"></a>Pré-configurar conteúdo  
 Pré-configurar o conteúdo é um processo de transferência de conteúdo para um ponto de distribuição sem a distribuição de conteúdos através da rede.  

 Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
