---
title: "Noções básicas de gestão de conteúdo"
titleSuffix: Configuration Manager
description: "Utilizar as ferramentas e opções no System Center Configuration Manager para gerir o conteúdo que implementar."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: "28"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d550d18de93f5e11c7538de24473d36c788145e6
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager suporta um sistema robusto de ferramentas e opções para gerir o conteúdo que implementar como aplicações, pacotes, atualizações de software e implementações do sistema operativo.  

O conteúdo que implementa é armazenado em ambos os servidores de site e nos servidores do sistema de sites de ponto de distribuição. Este conteúdo pode exigir uma grande quantidade de largura de banda de rede quando está a ser transferido entre localizações. Para planear e utilizar a infraestrutura de gestão de conteúdos eficazmente, recomendamos que compreender as opções disponíveis e as configurações e, em seguida, considerar como utilizá-las para melhor opção do seu ambiente de rede e necessidades de implementação de conteúdo.  

> [!TIP]    
> Pode obter mais informações sobre o processo de distribuição de conteúdo e encontrar ajuda no diagnosticar e resolver problemas gerais de distribuição de conteúdo. Consulte [compreender e resolver problemas de conteúdo no Configuration Manager de distribuição](https://support.microsoft.com/help/4000401/content-distribution-in-mcm) em support.microsoft.com.

Seguem-se conceitos chave para gestão de conteúdo. Quando um conceito precisar de informações complexas ou adicionais, são fornecidas hiperligações para direcioná-lo para esses detalhes.

## <a name="accounts-used-for-content-management"></a>Contas utilizadas para a gestão de conteúdos  
 As contas que se seguem podem ser utilizadas com a gestão de conteúdos:  

-   **Conta de acesso de rede**: Utilizada pelos clientes para ligar a um ponto de distribuição e aceder ao conteúdo. Por predefinição, a conta de computador está experimentada em primeiro lugar.  

     Esta conta é também utilizada pelos pontos de distribuição de extração para obter conteúdo de um ponto de distribuição de origem numa floresta remota.  

-   **Conta de acesso a pacote**: Por predefinição, o Configuration Manager concede acesso a conteúdo num ponto de distribuição para as contas de acesso genérico utilizadores e administradores. No entanto, pode configurar permissões adicionais para restringir o acesso.   

-   **Conta de ligação de multicast**: Utilizado para implementações do sistema operativo.  

Para mais informações sobre estas contas, consulte [gerir contas para aceder ao conteúdo](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).

## <a name="bandwidth-throttling-and-scheduling"></a>Limitação de largura de banda e agendamento  
 Tanto a limitação como o agendamento são opções que o ajudam a controlar quando o conteúdo é distribuído de um servidor do site para pontos de distribuição. Isto é semelhante a, mas não está diretamente relacionado com controlos de largura de banda para replicação baseada em ficheiros de site para site.  

 Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="binary-differential-replication"></a>Replicação diferencial binária  
 Um pré-requisito para pontos de distribuição, a replicação diferencial binária (BDR), que é por vezes conhecida como replicação delta, é automaticamente utilizado para reduzir a utilização de largura de banda ao que está a distribuir atualizações de conteúdo que tenha implementado anteriormente para outros sites ou para pontos de distribuição remotos.  

 A BDR minimiza a largura de banda de rede utilizada para enviar atualizações de conteúdo distribuído ao reenviar apenas o conteúdo novo ou alterado, em vez de enviar o conjunto completo de ficheiros de origem do conteúdo sempre que é efetuada uma alteração nesses ficheiros.  

 Quando é utilizada a replicação diferencial de binários, o Configuration Manager identifica as alterações que ocorrem nos ficheiros de origem para cada conjunto de conteúdos que tem sido anteriormente distribuído.  

-   Quando alterar ficheiros de conteúdo de origem, o Configuration Manager cria uma nova versão incremental do conjunto de conteúdos e replica apenas os ficheiros alterados para sites de destino e de pontos de distribuição. Um ficheiro é considerado alterado se foi mudado ou movido ou se o conteúdo do ficheiro foram alterados. Por exemplo, se substituir um único ficheiro de controlador num pacote de implementação de sistema operativo que tenha anteriormente distribuído por vários sites, apenas o ficheiro de controlador alterado será replicado para esses sites de destino.  

-   O Configuration Manager suporta até cinco versões incrementais de um conjunto antes de reenviar o conjunto completo de conteúdo de conteúdos. Após a quinta atualização, a próxima alteração ao conjunto de conteúdos faz com que o Configuration Manager para criar uma nova versão do conjunto de conteúdos. Em seguida, o Configuration Manager distribui a nova versão de conteúdo definida para substituir o conjunto anterior e todas as versões incrementais. Após a distribuição do novo conjunto de conteúdos, as alterações incrementais subsequentes aos ficheiros de origem serão novamente replicadas por replicação diferencial de binários.  


A BDR é suportada entre cada site principal e site subordinado numa hierarquia. Num site, a BDR é suportada entre o servidor do site e os respetivos pontos de distribuição normal. No entanto, os pontos de distribuição de solicitação e pontos de distribuição baseado na nuvem não suportam a replicação diferencial de binários para transferência de conteúdo. Os pontos de distribuição de solicitação suportam deltas de nível de ficheiros, transferir os novos ficheiros, mas não os blocos de um ficheiro.

As aplicações utilizam sempre a replicação diferencial de binários. Para pacotes, a replicação diferencial de binários é opcional e não está ativada por predefinição. Para utilizar a replicação diferencial de binários para pacotes, tem de ativar esta funcionalidade para cada pacote. Para o fazer, selecione a opção **Ativar replicação de diferencial binário** quando criar um novo pacote ou quando editar o separador **Origem de Dados** das propriedades do pacote.  

## <a name="branchcache"></a>BranchCache  
 Uma tecnologia do Windows que permite aos clientes que suportam o BranchCache e que tenham transferido uma implementação que está configurada para Branch Cache, em seguida, servir como uma origem de conteúdo para outros clientes com capacidade para BranchCache.  

 Por exemplo, quando o primeiro computador cliente com capacidade BranchCache pedir conteúdo de um ponto de distribuição com o Windows Server 2012 e estiver configurado como servidor BranchCache, o computador cliente transfere esse conteúdo e coloca-o em cache.  

-   Esse computador cliente pode, em seguida, disponibilizar o conteúdo para a capacidade de BranchCache clientes adicionais na mesma sub-rede que também colocam em cache o conteúdo.  

-   Desta forma, os clientes seguintes da mesma sub-rede não necessitam de transferir o conteúdo a partir do ponto de distribuição e o conteúdo é distribuído por vários clientes para futuras transferências.  

## <a name="peer-cache"></a>Cache ponto a ponto
A partir da versão 1610, a Cache de cliente ajuda-o a gerir a implementação de conteúdo para clientes em localizações remotas. A Cache é uma solução incorporada do Configuration Manager que permite que os clientes partilhem conteúdos com outros clientes diretamente a partir da respetiva cache local.

Depois de implementar as definições de cliente que permitem a Cache ponto a ponto numa coleção, os membros dessa coleção podem agir como uma origem de conteúdo ponto a ponto para outros clientes no mesmo grupo de limites.

Para obter mais informações, consulte [Cache ponto a ponto para clientes do Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).


## <a name="windows-pe-peer-cache"></a>Cache ponto a ponto do Windows PE
Quando implementa um novo sistema operativo no System Center Configuration Manager, computadores que executam a sequência de tarefas podem utilizar a Cache do Windows PE para obter conteúdo de um elemento de rede local (uma origem de cache ponto a ponto) em vez de transferirem conteúdo de um ponto de distribuição. Isto ajuda a minimizar o tráfego da rede alargada (WAN) em cenários de uma sucursal onde não existe um ponto de distribuição local.

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
 A biblioteca de conteúdos é o arquivo de instância única de conteúdo que o Configuration Manager utiliza para reduzir o tamanho geral do corpo combinado de conteúdo que distribui.  

- Saiba mais sobre o [biblioteca de conteúdos](../../../core/plan-design/hierarchy/the-content-library.md).
- Utilize o [ferramenta de limpeza da biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) para remover o conteúdo que já não está associado uma aplicação.  


## <a name="distribution-points"></a>Pontos de distribuição  
 Configuration Manager utiliza pontos de distribuição para armazenar os ficheiros que são necessários para o software seja executado em computadores cliente. Os clientes devem ter acesso a, pelo menos, um ponto de distribuição partir dos quais poderão transferir os ficheiros de conteúdo que implementar.  

 O ponto de distribuição básico (não especializado) é normalmente denominado como um ponto de distribuição padrão. Existem duas variações no ponto de distribuição padrão que recebem especial atenção:  

-   **Ponto de distribuição de solicitação**: Uma variação de um ponto de distribuição em que o ponto de distribuição obtém conteúdo de outro ponto de distribuição (um ponto de distribuição de origem). Este processo é semelhante à forma como os clientes transferem conteúdo de pontos de distribuição. Pontos de distribuição de solicitação podem ajudar a evitar congestionamentos de largura de banda de rede que ocorrem quando o servidor do site tem de distribuir diretamente conteúdo para cada ponto de distribuição.  [Utilizar um ponto de distribuição de extração com o System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Ponto de distribuição baseado na nuvem**: Uma variação de um ponto de distribuição que está instalado no Microsoft Azure. [Saiba como utilizar um ponto de distribuição baseado na nuvem com o System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Pontos de distribuição padrão suportam uma variedade de configurações e funcionalidades, tais como Otimização e agendamento, PXE e Multicast, ou de conteúdo pré-configurado.  

-   Pode utilizar os controlos como **agendas** ou **limitação de largura de banda** para ajudar a controlar a transferência.  

-   Também pode utilizar outras opções, incluindo **conteúdo pré-configurado**, e **pontos de distribuição de solicitação**. Além disso, pode tirar partido do **BranchCache** para reduzir a largura de banda de rede que é utilizada quando implementar o conteúdo.  

-   Pontos de distribuição suportam diferentes configurações, tais como  **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)**  e  **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**  para implementações do sistema operativo ou configurações para suportar **dispositivos móveis**.  

 Baseado na nuvem e de pontos de distribuição de solicitação suportam muitas destas configurações, mas têm limitações específicas para cada variação de ponto de distribuição.  

## <a name="distribution-point-groups"></a>Grupos de pontos de distribuição  
 Grupos de pontos de distribuição são agrupamentos lógicos de pontos de distribuição que podem simplificar a distribuição de conteúdo.  

 Para obter mais informações, consulte [gerir grupos de pontos de distribuição](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).

## <a name="distribution-point-priority"></a>Prioridade de pontos de distribuição  
 O valor de prioridade do ponto de distribuição baseia-se na quantidade de tempo necessária para transferir implementações anteriores para esse ponto de distribuição.  

-   Este é um valor de sintonização automática atribuído a um ponto de distribuição que ajuda o conteúdo de transferência do Configuration Manager a mais pontos de distribuição num período de tempo mais curto.  

-   Quando distribuir conteúdos a vários pontos de distribuição em simultâneo ou a distribuição de uma grupo de pontos, Configuration Manager envia o conteúdo ao ponto de distribuição com a máxima prioridade, antes de enviar os mesmos conteúdos para um ponto de distribuição com uma prioridade mais baixa.  

-   Isto não substitui a prioridade de distribuição para pacotes, que permanece o fator decisivo na sequência do momento de transferência das diversas distribuições.  


Por exemplo, se distribuir conteúdo que tenha uma prioridade de distribuição elevada a um ponto de distribuição que tenha uma prioridade de ponto de distribuição baixa, este pacote de prioridade de distribuição elevada será sempre transferido antes de um pacote que tenha uma prioridade de distribuição baixa. A prioridade de distribuição aplica-se mesmo que os pacotes que tenham uma prioridade de distribuição mais baixa sejam distribuídos a pontos de distribuição com prioridade de ponto de distribuição mais elevada.

A prioridade de distribuição elevada do pacote garante que o Configuration Manager distribui esse conteúdo aos pontos de distribuição aplicáveis antes do envio de quaisquer pacotes com uma prioridade de distribuição mais baixa.  

> [!NOTE]  
>  Os pontos de distribuição de extração também utilizam um conceito de prioridade para ordenar a sequência dos respetivos pontos de distribuição de origem.  
>   
>  -   A prioridade de ponto de distribuição para transferências de conteúdo ao ponto de distribuição é distinta da prioridade que os pontos de distribuição de extração utilizam quando procuram conteúdo de um ponto de distribuição de origem.  
>  -   Para obter mais informações, consulte [utilizar um ponto de distribuição de extração com o System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  


## <a name="fallback"></a>Contingência  
 A partir da versão 1610, vários aspetos mudaram de forma que os clientes localizam um ponto de distribuição que tenha o conteúdo, incluindo contingência. Utilize as seguintes informações que se aplica à versão que utiliza:

**Versão 1610 e posterior**   
Os clientes que não é possível localizar o conteúdo de um ponto de distribuição associado ao respetivo grupo de limites atual podem reverter para utilizarem as localizações de origem de conteúdo que estão associadas a grupos de limites de vizinho. Para ser utilizado para contingência, um grupo de limites de vizinho tem de ter uma relação definida com o grupo de limites atual do cliente. Esta relação inclui uma vez configurada que tem de passar antes de um cliente que não é possível localizar o conteúdo localmente pode incluir origens de conteúdo do grupo de limites de vizinho como parte da sua pesquisa.

Os conceitos do já não são utilizados pontos de distribuição preferenciais e definições de **permitir que as localizações de origem de contingência para conteúdo** já não estão disponíveis ou imposta.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Versão 1511, 1602 e 1606**   
As definições de contingência estão relacionadas com a utilização de **pontos de distribuição de preferencial** e para localizações de origem de conteúdo que são utilizadas pelos clientes.

-   Por predefinição, os clientes transferem apenas conteúdo de um ponto de distribuição preferencial (um que estão associados com grupos de limites do cliente).  

-   No entanto, quando um ponto de distribuição está configurado com a definição **Permitir que os clientes utilizem este sistema de sites como uma localização de origem de contingência para o conteúdo**, esse ponto de distribuição só é oferecido como uma origem de conteúdo válida a qualquer cliente que não consiga obter uma implementação de um dos respetivos pontos de distribuição preferenciais.  


Para obter informações sobre os cenários de contingência e localização de conteúdo diferente, consulte [cenários de localização de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Para obter informações sobre grupos de limites, consulte [grupos de limites para versões 1511,1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## <a name="network-bandwidth"></a>Largura de banda da rede  
 Para ajudar a gerir a quantidade de largura de banda de rede que é utilizada quando distribui conteúdo, pode utilizar as seguintes opções:  

-   **Conteúdo pré-configurado**:  Um processo de transferência de conteúdo para um ponto de distribuição sem entidade confiadora no Configuration Manager para distribuir o conteúdo pela rede.  

-   **Agendamento e limitação**: As configurações que o ajudam a controlam quando e como o conteúdo é distribuído para pontos de distribuição.  

Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="network-connection-speed-to-content-source"></a>Velocidade da ligação de rede à origem de conteúdo  
A partir da versão 1610, vários aspetos mudaram de forma que os clientes localizam um ponto de distribuição que tenha o conteúdo, incluindo a velocidade da ligação de rede a uma origem de conteúdo. Utilize as seguintes informações que se aplica à versão que utiliza:

**Versão 1610 e posterior**   
Velocidades de ligação de rede que definem uma distribuição apontar como **Rápido** ou **lenta** já não são utilizadas. Em vez disso, cada sistema de sites que está associada um grupo de limites é Tratado da mesma.

Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Versão 1511, 1602 e 1606**   
 É possível configurar a velocidade da ligação de rede de cada ponto de distribuição num grupo de limites:  

-   Os clientes utilizam este valor quando se ligam ao ponto de distribuição.

-   Por predefinição, a velocidade da ligação de rede é configurada como **Rápido**, mas também podem ser definida como **lenta**.  

-   O **velocidade da ligação de rede**, juntamente com a configuração de uma implementação, determinam se um cliente pode transferir conteúdo de um ponto de distribuição quando o cliente está num grupo de limites associado  

Para obter informações sobre os cenários de contingência e localização de conteúdo diferente, consulte [cenários de localização de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Para obter informações sobre grupos de limites, consulte [grupos de limites para versões 1511,1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## <a name="on-demand-content-distribution"></a>Distribuição de conteúdo a pedido  
 Distribuição de conteúdo a pedido é uma opção que pode ser definido para indivíduo distribuição para os pontos de distribuição preferencial de conteúdo de aplicações e pacotes (implementações) para ativar a pedido.  

-   Para ativar esta opção para uma implementação, ative **distribuir o conteúdo do pacote para pontos de distribuição preferenciais**.  

-   Quando esta opção está ativada para uma implementação e um cliente tenta pedir esse conteúdo, mas o conteúdo não está disponível em qualquer um dos pontos de distribuição preferenciais do cliente, o Configuration Manager distribui automaticamente esse conteúdo aos pontos de distribuição preferenciais do cliente.  

-   Embora isto acione o Configuration Manager para distribuir automaticamente o conteúdo para pontos de distribuição preferenciais desse cliente, o cliente poderá obter esse conteúdo de outros pontos de distribuição antes dos pontos de distribuição preferencial para o cliente recebem a implementação. Quando isto ocorre, o conteúdo estará presente nesse ponto de distribuição para utilização pelo cliente seguinte que procura essa implementação.  

Se utilizar a versão 1610 ou posterior, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
Se utilizar a versão 1511, versão 1602 ou 1606, consulte [cenários de localização de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) para obter informações sobre os cenários de contingência e localização de conteúdo diferente.  



## <a name="package-transfer-manager"></a>Gestor de Transferência de Pacotes  
 Gestor de transferência do pacote é o componente de servidor do site transfere conteúdo para pontos de distribuição noutros computadores.  

 Saiba mais sobre o [Gestor de transferência de pacotes](../../../core/plan-design/hierarchy/package-transfer-manager.md).  

## <a name="preferred-distribution-point"></a>Ponto de distribuição preferencial  
 Um ponto de distribuição preferenciais inclui quaisquer pontos de distribuição que estão associados a grupos de limites atuais de um cliente.  

 Tem a opção de associar cada ponto de distribuição a um ou mais grupos de limites:  

-   Esta associação ajuda o cliente a identificar os pontos de distribuição a partir da qual pode transferir conteúdo.  
-   Por predefinição, os clientes só podem transferir conteúdo de um ponto de distribuição preferenciais.  


Para obter mais informações:
 - Se utilizar a versão 1610 ou posterior, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - Se utilizar a versão 1511, versão 1602 ou 1606, consulte [cenários de localização de origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).

## <a name="prestage-content"></a>Pré-configurar conteúdo  
 Pré-configuração de conteúdo é um processo de transferência de conteúdo para um ponto de distribuição sem entidade confiadora no Configuration Manager para distribuir o conteúdo pela rede.  

 Para obter mais informações, consulte [gerir a largura de banda de rede](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
