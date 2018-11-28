---
title: Configurar grupos de limites
titleSuffix: Configuration Manager
description: Ajudar os clientes a localizar sistemas de sites através de grupos de limites para organizar logicamente as localizações de rede relacionados chamadas limites
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9b2eaaf3581bdb951b23541c96532c5b049aac1
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456367"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Configurar grupos de limites para o Configuration Manager


*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizar grupos de limites no Configuration Manager para organizar logicamente as localizações de rede relacionadas ([limites](/sccm/core/servers/deploy/configure/boundaries)) para que seja mais fácil de gerir a sua infraestrutura. Atribua os limites a grupos de limites antes de utilizar o grupo de limites.

Por predefinição, o Configuration Manager cria um grupo de limites de site padrão em cada site.

Para configurar grupos de limites, associar limites (localizações de rede) e funções de sistema de sites, como pontos de distribuição, ao grupo de limites. Esta configuração ajuda a associar os clientes para servidores do sistema de sites, como pontos de distribuição que estão localizados perto os clientes na rede.

Para aumentar a disponibilidade dos servidores a um maior número de localizações de rede, atribua o mesmo limite de tempo e o mesmo servidor a mais do que um grupo de limites.

Os clientes utilizam um grupo de limites para:  

-   Atribuição automática de site  
-   Para localizar um servidor de sistema de sites que pode fornecer um serviço, incluindo:  
    - Pontos de distribuição para localização de conteúdo  
    - Pontos de atualização de software  
    - Pontos de migração de estado  
    - Pontos de gestão preferenciais  

        > [!Note]  
        > Se utilizar pontos de gestão preferenciais, ative esta opção para a hierarquia, não a partir de dentro da configuração do grupo de limites. Para obter mais informações, consulte [ativar a utilização de pontos de gestão preferenciais](#to-enable-use-of-preferred-management-points).  



##  <a name="boundary-groups-and-relationships"></a>Grupos de limites e relações

Para cada grupo de limites na sua hierarquia, pode atribuir:

- Um ou mais limites. Um cliente **atual** grupo de limites for uma localização de rede que é definida como um limite atribuído a um grupo de limites específicos. Um cliente pode ter mais de um grupo de limites atual.  

- Uma ou mais funções de sistema de sites. Os clientes podem sempre utilizar funções associadas do seu grupo de limites atual. Dependendo de configurações adicionais, podem utilizar funções em grupos de limites adicionais.  

Para cada grupo de limites que criar, pode configurar uma ligação unidirecional para outro grupo de limites. A ligação é chamada um **relação**. Cria uma ligação para os grupos de limites são chamados **vizinho** grupos de limites. Um grupo de limites pode ter mais de uma relação, cada um com um grupo de limite vizinho específico.

Quando um cliente não consegue encontrar um sistema de sites disponíveis no seu grupo de limites atual, a configuração de cada relação determina quando começa a procurar um grupo de limite vizinho. Esta pesquisa de grupos adicionais é chamada **contingência**.

Para obter mais informações, consulte os seguintes procedimentos:  
- [Criar um grupo de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_create)  
- [Configurar um grupo de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_config)  



## <a name="fallback"></a>Contingência

Para evitar problemas quando os clientes não é possível localizar um sistema de sites disponíveis no seu grupo de limite atual, defina a relação entre grupos de limites para o comportamento de contingência. Contingência permite que um cliente expandir sua pesquisa para grupos de limites adicionais para localizar um sistema de sites disponíveis.

As relações são configuradas nas propriedades do grupo de limites **relações** separador. Ao configurar uma relação, define uma ligação para um grupo de limite vizinho. Para cada tipo de função do sistema de sites suportados, as configurações independente para contingência para o grupo de limite vizinho. Para obter mais informações, consulte [configurar o comportamento de contingência](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_bg-fallback).

Por exemplo, quando configurar uma relação a um grupo de limites específicos, defina contingência para pontos de distribuição de ocorrer após 20 minutos. A predefinição é 120 minutos para obter um exemplo mais extensivo, consulte [exemplo de como utilizar grupos de limites](#example-of-using-boundary-groups).

Se um cliente não conseguir encontrar uma função de sistema de sites disponíveis no seu grupo de limites atual, o cliente utiliza o tempo de contingência em minutos. Este tempo de contingência determina quando o cliente começa a procurar um sistema de sites disponíveis associado ao grupo de limite vizinho.  

Quando um cliente não é possível localizar um sistema de sites disponíveis, ele começa pesquisar localizações de grupos de limite vizinho. Este comportamento aumenta o conjunto de sistemas de sites disponíveis. A configuração de grupos de limites e seus relacionamentos define a utilização do cliente deste agrupamento de sistemas de sites disponíveis.

- Um grupo de limites pode ter mais de uma relação. Com esta configuração, pode configurar a contingência para cada tipo de sistema de sites com diferentes vizinhos de ocorrer após diferentes períodos de tempo.    

- Clientes só contingência para um grupo de limites que é um vizinho direto do respetivo grupo de limites atual.  

- Quando um cliente for membro de mais do que um grupo de limites, define o seu grupo de limites atual como uma União de todos os respetivos grupos de limites. O cliente reverterá para vizinhos de qualquer um desses grupos de limite original.  


### <a name="the-default-site-boundary-group"></a>O grupo de limites de site predefinido

Pode criar seus próprios grupos de limites e cada site tem um grupo de limites de site predefinido do Configuration Manager cria. Este grupo é designado **predefinição---grupo de limite Site&lt;sitecode >**. Por exemplo, o grupo para o site ABC teria o nome **predefinição---grupo de limite Site&lt;ABC >**.

Para cada grupo de limites que cria, o Configuration Manager cria automaticamente uma ligação implícita para cada grupo de limites de site padrão na hierarquia.  

- A ligação implícita é uma opção de contingência de padrão de um grupo de limites atual para o grupo de limite predefinido do site. O tempo de contingência predefinido é 120 minutos.  

- Para os clientes não de um limite associado a nenhum grupo de limites: para identificar as funções do sistema de site válido, utilize o grupo de limites de site predefinido do respetivo site atribuído.  


Para gerir a contingência para o grupo de limites de site padrão:  

- Abra as propriedades do grupo de limite predefinido do site e alterar os valores no **comportamento padrão** separador. As alterações que fizer aqui aplicam-se ao *todos os* implícito links para este grupo de limites. Ao configurar uma ligação explícita para este grupo de limites de site predefinido do outro grupo de limites, é substituir estas predefinições.  

- Abra as propriedades de um grupo de limites personalizado. Altere os valores para a ligação explícita para um grupo de limites de site padrão. Ao definir uma nova hora em minutos para reversão ou reversão de bloco, essa alteração afeta apenas a ligação que estiver a configurar. Configuração da ligação explícita substitui as definições no **comportamento padrão** separador de um grupo de limites de site padrão.  



## <a name="site-assignment"></a>Atribuição de site  

 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recentemente instalado que utilize a atribuição automática de site é associado ao site atribuído de um grupo de limites que contém a localização de rede atual do cliente.  

-   Depois de atribuir a um site, um cliente não altera sua atribuição de site ao alterar a respetiva localização de rede. Por exemplo, um cliente fizer roaming para uma nova localização de rede. Esta localização é um limite num grupo de limites com uma atribuição de site diferente. Site atribuído do cliente não é alterado.  

-   Quando a deteção de sistema do Active Directory Deteta um novo recurso, o site avaliar as informações de rede para o recurso com os limites em grupos de limites. Este processo associa o novo recurso a um site atribuído que será utilizado pelo método de instalação push do cliente.  

-   Quando um limite é um membro de mais do que um grupos de limites que possuem diferentes sites atribuídos, os clientes selecionam aleatoriamente um dos sites.  

-   Alterações a um site de grupos atribuídos limites só se aplicam a novas ações de atribuição de site. Os clientes atribuídos anteriormente a um site não reavaliar a atribuição do site com base nas alterações à configuração de um grupo de limites (ou a sua própria localização de rede).  

Para obter mais informações sobre a atribuição de sites do cliente, consulte [utilizar a atribuição automática de site de computadores](/sccm/core/clients/deploy/assign-clients-to-a-site#BKMK_AutomaticAssignment).  

Para obter mais informações sobre como configurar a atribuição de sites, consulte os seguintes procedimentos:
- [Configurar a atribuição de site e selecionar servidores do sistema de sites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_references)
- [Configurar um site de contingência para atribuição automática de site](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_site-fallback)



## <a name="distribution-points"></a>Pontos de distribuição

Quando um cliente solicita o local de um ponto de distribuição, o Configuration Manager envia ao cliente uma lista de sistemas de sites. Estes sistemas de sites são do tipo adequado associado a cada grupo de limites que inclui a localização de rede atual do cliente:

-   **Durante a distribuição de software**, os clientes solicitam uma localização para o conteúdo de implementação numa fonte de conteúdo válido. Esta localização pode ser um ponto de distribuição ou uma origem de cache ponto a ponto.  

-   **Durante a implementação do sistema operacional**, os clientes solicitam uma localização para enviar ou receber as respetivas informações de migração de estado.  

    - Os clientes a partir da versão 1810, adquirir o conteúdo com base em comportamentos do grupo de limites. Para obter mais informações, consulte [grupos de limites suporte a sequência de tarefas](#bkmk_bgr-osd).  

Durante a implementação de conteúdos, se um cliente solicita conteúdo que não está disponível de uma origem no seu grupo de limite atual, o cliente continua a pedem esse conteúdo. O cliente tenta diferente fontes de conteúdo no seu grupo de limites atual até atingir o período de contingência para um vizinho ou do grupo de limites de site predefinido. Se o cliente ainda não foi encontrado conteúdo, em seguida, expande sua pesquisa por fontes de conteúdo incluir grupos de limite vizinho.

Se configurar o conteúdo para distribuir a pedido e ele não está disponível num ponto de distribuição quando um cliente solicita-lo, o site começa-se transferir o conteúdo para esse ponto de distribuição. É possível que o cliente localiza esse servidor como uma origem de conteúdo antes de reverter para utilizar um grupo de limite vizinho.


### <a name="bkmk_ccmsetup"></a> Instalação do cliente
<!--1358840-->

Ao instalar o cliente do Configuration Manager, o processo de ccmsetup entra em contacto com o ponto de gestão para localizar os conteúdos necessários. Durante este processo nas versões 1806 e anteriores, o ponto de gestão devolve apenas os pontos de distribuição no grupo de limite atual do cliente. Se nenhum conteúdo estiver disponível, o processo de configuração é retrocede para transferir o conteúdo do ponto de gestão. Não existe nenhuma opção para reverter para pontos de distribuição em outros grupos de limites que podem ter o conteúdo necessário. 

A partir da versão 1810, o ponto de gestão devolve pontos de distribuição com base na configuração do grupo de limites. Se definir relações no grupo de limites, o ponto de gestão devolve pontos de distribuição na seguinte ordem:
1. Grupo de limites atual  
2. Grupos de limites de vizinho  
3. O grupo de limites do site predefinido  

> [!Note]  
> O processo de configuração de cliente não usa o tempo de contingência. Para localizar o conteúdo mais rapidamente possível, imediatamente vai para o grupo de limites próximo.  


### <a name="bkmk_bgr-osd"></a> Suporte de sequência de tarefas para grupos de limites
<!--1359025-->

A partir da versão 1810, quando um dispositivo é executada uma sequência de tarefas e tem de adquirir o conteúdo, ele agora usa comportamentos de grupo de limites semelhantes para o cliente do Configuration Manager.   

Configurar este comportamento ao utilizar as seguintes definições sobre o **pontos de distribuição** página da implementação da sequência de tarefas: 

- **Se estiver disponível nenhum ponto de distribuição local, utilizar um ponto de distribuição remoto**: Para esta implementação, a sequência de tarefas pode reverter para pontos de distribuição num grupo de limite vizinho.  

- **Permitir aos clientes utilizar pontos de distribuição do grupo de limite de site predefinido**: Para esta implementação, a sequência de tarefas pode reverter para pontos de distribuição no grupo de limite de site predefinido.  

Para usar esse novo comportamento, certifique-se atualizar clientes para a versão mais recente.

#### <a name="location-priority"></a>Prioridade de localização  

A sequência de tarefas tenta adquirir o conteúdo pela seguinte ordem:  

1. Origens de cache ponto a ponto  

2. Pontos de distribuição no *atual* grupo de limites  

3. Pontos de distribuição numa *vizinho* grupo de limites  

    > [!Important]  
    > Devido à natureza do processamento de sequência de tarefas em tempo real, ele não espera até que o tempo de ativação pós-falha num grupo de limite vizinho. Ele usa os tempos de ativação pós-falha para priorizar os grupos de limite vizinho. Por exemplo, se a sequência de tarefas não conseguir adquirir o conteúdo de um ponto de distribuição no seu grupo de limite atual, imediatamente tenta um ponto de distribuição num grupo de limite vizinho com a hora de ativação pós-falha mais curto. Se esse processo falhar, em seguida, falhar ao longo para um ponto de distribuição de um grupo de limite vizinho com um maior tempo de ativação pós-falha.  

4. Pontos de distribuição no *predefinido do site* grupo de limites  

O ficheiro de registo de sequência de tarefas **smsts** mostra a prioridade das origens de localização que utiliza com base nas propriedades de implementação.


### <a name="bkmk_bgoptions"></a> Opções de grupos de limites para configurar o peering downloads

<!--1356193--> A partir da versão 1806, grupos de limites incluem as seguintes definições adicionais para lhe dar mais controle sobre a distribuição de conteúdo no seu ambiente:  

- [Permitir transferências de ponto a ponto neste grupo de limites](#bkmk_bgoptions1)  

- [Durante downloads de ponto a ponto, utilize apenas colegas dentro da mesma sub-rede](#bkmk_bgoptions2)  

<!--1358749--> Versão 1810 adiciona as seguintes opções:  

- [Prefira pontos de distribuição através de protocolos de mesmo nível com a mesma sub-rede](#bkmk_bgoptions3)  

- [Prefira pontos de distribuição de cloud através de pontos de distribuição](#bkmk_bgoptions4)  

Para obter mais informações sobre como configurar estas definições, consulte [configurar um grupo de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_config).


#### <a name="bkmk_bgoptions1"></a> Permitir transferências de ponto a ponto neste grupo de limites
Esta definição está ativada por predefinição. O ponto de gestão fornece aos clientes uma lista de localizações de conteúdo que inclui a origens de ponto a ponto. Esta definição afeta também aplicar IDs de grupo para o [Otimização da entrega](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).  

Existem dois cenários comuns nos quais deve considerar a desativar esta opção:  

- Se tiver um grupo de limites que inclui os limites de geograficamente dispersos localizações, como uma VPN. Dois clientes possível no mesmo grupo de limites que estão ligados através de VPN, mas em diferentes locais que não apropriadas para o mesmo nível de partilha de conteúdo.  

- Se utilizar um grupo de limites única e grandes para a atribuição de sites que não façam referência a quaisquer pontos de distribuição.  

#### <a name="bkmk_bgoptions2"></a> Durante downloads de ponto a ponto, utilize apenas colegas dentro da mesma sub-rede
Esta definição é dependente da opção anterior. Se ativar esta opção, o ponto de gestão inclui apenas nas fontes de mesmo nível de lista de localização de conteúdo que estão na mesma sub-rede que o cliente.

Cenários comuns para ativar esta opção:

- A estrutura de grupo de limites para distribuição de conteúdos inclui um grupo de limites de grandes dimensões que sobrepõe-se a outros grupos de limites mais pequenos. Com esta nova definição, a lista de fontes de conteúdo que o ponto de gestão fornece aos clientes inclui apenas as origens de ponto a ponto da mesma sub-rede.

- Tem um grupo de limites de grandes único para todas as localizações de escritórios remotos. Ative esta opção e os clientes apenas de partilhar conteúdos dentro da sub-rede na localização do escritório remoto, em vez de correr o risco de partilha de conteúdo entre localizações.

#### <a name="bkmk_bgoptions3"></a> Prefira pontos de distribuição através de protocolos de mesmo nível com a mesma sub-rede
Por predefinição, o ponto de gestão, atribui prioridades aos origens da cache ponto a ponto na parte superior da lista de localizações de conteúdo. Esta definição reverte essa prioridade para clientes que estejam na mesma sub-rede que a origem de cache ponto a ponto.  

#### <a name="bkmk_bgoptions4"></a> Prefira pontos de distribuição de cloud através de pontos de distribuição
Se tiver uma filial com um link da internet mais rápida, agora pode priorizar o conteúdo em nuvem.  



## <a name="software-update-points"></a>Pontos de atualização de software

Os clientes utilizam grupos de limites para localizar um ponto de atualização de software novo. Para controlar quais os servidores de um cliente pode encontrar, adicione pontos de atualização de software individuais aos grupos de limites diferentes.

Se atualizar a partir de uma versão anterior 1702, cada site adiciona todos os pontos de atualização de software existente para o grupo de limites de site padrão. Esse comportamento de atualização do site mantém o comportamento do cliente anterior para selecionar um ponto de atualização de software a partir do agrupamento de servidores disponíveis. Este comportamento é mantido até optar por adicionar pontos de atualização de software individuais para grupos de limites diferentes para seleção controlada e o comportamento fallback.

Se instalar um novo site, os pontos de atualização de software não são adicionados ao grupo de limites de site padrão. Atribua pontos de atualização de software a um grupo de limites para que os clientes possam encontrar e utilizá-los.


### <a name="fallback-for-software-update-points"></a>Contingência para pontos de atualização de software

Contingência para pontos de atualização de software está configurada como outras funções de sistema de sites, mas tem os seguintes avisos:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Novos clientes utilizam grupos de limites para selecionar pontos de atualização de software
Quando instalar novos clientes, eles selecionarem um ponto de atualização de software desses servidores associados com os grupos de limites que configurar. Este comportamento substitui o comportamento anterior em que os clientes selecionam um ponto de atualização de software aleatoriamente de uma lista dos servidores que partilham na floresta do cliente.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Os clientes continuam a utilizar um último ponto de atualização de software de boa conhecida até eles fallback para localizar um novo
Os clientes que já tenham um ponto de atualização de software continuam a utilizá-lo até que ele não pode ser alcançado. Este comportamento inclui o uso contínuo de um ponto de atualização de software que não está associado ao grupo de limites atual do cliente.

Este comportamento é intencional. O cliente continua a utilizar um ponto de atualização de software existentes, mesmo quando não está no grupo de limite atual do cliente. Quando as alterações de ponto de atualização de software, o cliente sincroniza os dados com o novo servidor, o que faz com que a utilização de rede significativo. Se todos os clientes, mude para um novo servidor, ao mesmo tempo, o atraso em transição ajuda a evitar saturar a rede.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Um cliente tenta sempre gera o último ponto de atualização de software de boa conhecida por 120 minutos antes de começar contingência
Depois de 120 minutos, se o cliente ainda não estabelecer contacto, em seguida, começa contingência. Quando inicia de contingência, o cliente recebe uma lista de todos os pontos de atualização de software no seu grupo de limite atual. Pontos num limite de padrão de vizinho e o site de grupos estão disponíveis com base nas configurações de contingência de atualização de software adicional.


### <a name="fallback-configurations-for-software-update-points"></a>Configurações de contingência para pontos de atualização de software

Pode configurar **tempos de contingência (em minutos)** para atualização de software pontos para ter menos de 120 minutos. No entanto, o cliente ainda tenta contactar o respetivo ponto de atualização de software original para 120 minutos. Em seguida, expande sua pesquisa para servidores adicionais. Tempos de contingência do grupo de limites iniciar quando o cliente pela primeira vez não consegue contactar o respetivo servidor original. Quando o cliente se expande a sua pesquisa, o site fornece todos os grupos de limites configurados para menos de 120 minutos.

Para bloquear a contingência para um ponto de atualização de software para um grupo de limite vizinho, configurar a definição para **Never contingência**.

Depois de a conseguir contactar o respetivo servidor original de duas horas, o cliente utiliza um ciclo mais curto para estabelecer uma ligação para um novo ponto de atualização de software. Este comportamento permite que o cliente pesquisar rapidamente a lista de expansão de possíveis pontos de atualização de software.

#### <a name="example"></a>Exemplo
Configurar pontos de atualização de software no grupo de limites *uma* a contingência após **10** minutos. Configurar a mesma definição de grupo de limites *B* ao **130** minutos. Um cliente no grupo de limites *Z* falhar para atingir o seu software de boa conhecida último ponto de atualização.

- Durante os próximos 120 minutos, o cliente tenta contactar o respetivo servidor original no grupo de limite Z. Após 10 minutos, o Configuration Manager adiciona os pontos de atualização de software do grupo de limites A para o conjunto de servidores disponíveis. No entanto, o cliente não tente contactá-los ou qualquer outro servidor, até decorrido o período inicial de 120 minutos.  

- Depois de tentar contactar o ponto de atualização de software original para 120 minutos, o cliente se expande a sua pesquisa. Ele adiciona servidores para o conjunto de disponibilidade de pontos de atualização de software que estão no mesmo da atual e quaisquer grupos de limite vizinho configurado para 120 minutos ou menos. Este conjunto inclui os servidores num grupo de limites, que tenham sido previamente adicionados ao agrupamento de servidores disponíveis.  

- Depois de 10 minutos, o cliente se expande a pesquisa para incluir pontos de atualização de software do grupo de limite B. Este período é de 130 minutos de tempo total após o primeiro o cliente não conseguiu alcançar o último ponto de atualização de software de boa conhecida.  


### <a name="manually-switch-to-a-new-software-update-point"></a>Mude manualmente para um novo ponto de atualização de software

Juntamente com o fallback, utilizar a notificação de cliente para forçar manualmente um dispositivo para mudar para um novo ponto de atualização de software.

Quando mudar para um novo servidor, os dispositivos utilizam contingência para encontrar esse servidor novo. Reveja as configurações do grupo de limites. Antes de começar esta alteração, certifique-se de que seus pontos de atualização de software são os grupos de limites correto.

Para obter mais informações, consulte [mudar manualmente clientes para um novo ponto de atualização de software](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Pontos de gestão
<!-- 1324594 --> A partir da versão 1802, configure as relações de contingência para pontos de gestão entre grupos de limites. Esse comportamento fornece maior controle para os pontos de gestão que os clientes utilizam. Sobre o **relações** separador de propriedades do grupo de limites, há uma coluna para o ponto de gestão. Quando adiciona um novo grupo de limites de contingência, o tempo de contingência para o ponto de gestão é atualmente sempre zero (0). Este comportamento é o mesmo para o **comportamento padrão** no grupo de limite predefinido do site.

Anteriormente, um problema comum ocorre quando tem um protegido ponto de gestão numa rede segura. Os clientes na rede corporativa principal recebem uma política que inclui este ponto de gestão protegidos, mesmo que não conseguem comunicar com ele através de uma firewall. Para resolver esse problema, utilize o **Never contingência** opção para se certificar de que apenas fallback para a gestão de clientes aponta com que eles possam comunicar.

Ao atualizar o site para a versão 1802, o Configuration Manager adiciona todos os pontos de gestão de intranet ao grupo de limite predefinido do site. (Este grupo de servidores não inclui pontos de gestão que são apenas de Internet). Esse comportamento de atualização certifica-se de que as versões mais antigas do cliente continuam a comunicar com pontos de gestão. Para tirar partido desta funcionalidade, mova os pontos de gestão para os grupos de limites pretendido.

> [!Note]  
> Se ativar pontos de distribuição do grupo de limite predefinido de site para contingência e um ponto de gestão é colocalizado num ponto de distribuição, o site também adiciona que do ponto de gestão para o grupo de limites do site predefinido.<!--VSO 2841292-->  

Se for um cliente num grupo de limites que, com não atribuído gestão, ponto, o site atribui o cliente toda a lista de pontos de gestão. Este comportamento certifica-se de que um cliente recebe sempre uma lista de pontos de gestão.

Contingência de grupo de limite de ponto de gestão não altera o comportamento durante a instalação de cliente (ccmsetup.exe). Se a linha de comandos não especifica o ponto de gestão inicial usando o parâmetro /MP, o novo cliente recebe a lista completa de pontos de gestão disponíveis. Para o processo de arranque de configuração inicial, o cliente utiliza o primeiro ponto de gestão que possa aceder. Assim que o cliente registra com o site, ele recebe a lista de pontos de gestão ordenada corretamente com esse novo comportamento. 

Para obter mais informações sobre o comportamento do cliente para adquirir o conteúdo durante a instalação, consulte [instalação do cliente](#bkmk_ccmsetup).

Durante a atualização de cliente, se não especificar o parâmetro de linha de comando /MP, apontam as origens de consultas de cliente, como o Active Directory e o WMI para qualquer gestão disponíveis. A atualização de cliente não honrar a configuração do grupo de limites. <!--VSO 2841292-->  

Para os clientes utilizar esta capacidade, ative a definição seguinte: **Os clientes preferem utilizar pontos de gestão especificados em grupos de limites** no **definições de hierarquia**. 

> [!Note]  
> Processos de implantação de SO não têm consciência de grupos de limites para pontos de gestão.  


### <a name="troubleshooting"></a>Resolução de Problemas

Novas entradas são apresentados no **Locationservices**. O **Localidade** atributo identifica um dos seguintes Estados:

- **0**: Desconhecido  

- **1**: O ponto de gestão especificado é apenas o grupo de limite predefinido de site de contingência  

- **2**: O ponto de gestão especificado está num grupo de limites da vizinhança ou remoto. Quando o ponto de gestão está num vizinho e os grupos de limites do site padrão, a Localidade é 2.  

- **3**: O ponto de gestão especificado está no grupo de limites atual ou local. Quando o ponto de gestão está no grupo de limites atual e um vizinho ou o grupo de limite predefinido de site, a Localidade é 3. Se não ativar os pontos de gestão preferenciais definição nas definições de hierarquia, a Localidade é sempre 3, independentemente da que limite o ponto de gestão de grupo está em.  

Os clientes utilizam pontos de gestão local primeiro (Localidade de 3), segundo remoto (Localidade de 2), em seguida, contingência (Localidade de 1). 

Quando um cliente recebe erros de cinco em 10 minutos e não consegue comunicar com um ponto de gestão no seu grupo de limite atual, ele tenta contactar um ponto de gestão num vizinho ou do grupo de limite predefinido do site. Se o ponto de gestão no grupo de limites atual mais tarde fica online novamente, o cliente devolve para o ponto de gestão local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando reinicia o serviço de agente do Configuration Manager.



## <a name="bkmk_preferred"></a> Pontos de gestão preferenciais

 > [!Note]
 > O comportamento desta definição, da hierarquia **os clientes preferem utilizar pontos de gestão especificados em grupos de limites**, alterações a partir da versão 1802. Quando ativa esta definição, o Configuration Manager utiliza a funcionalidade de grupo de limites para o ponto de gestão atribuído. Para obter mais informações, consulte [pontos de gestão](#management-points). 

 Pontos de gestão preferenciais permitem a um cliente identificar um ponto de gestão que está associada à sua localização de rede atual (limite).  

- Um cliente tenta utilizar um ponto de gestão preferencial a partir do site atribuído antes de utilizar um não configurado como preferencial do seu site atribuído.  

- Para utilizar esta opção, ative **os clientes preferem utilizar pontos de gestão especificados em grupos de limites** na **definições de hierarquia**. Em seguida, configure grupos de limites em sites primários individuais. Inclua os pontos de gestão que devem ser associados aos limites associados desse grupo de limites. Para obter mais informações, consulte [ativar a utilização de pontos de gestão preferenciais](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_proc-prefer).  

- Quando configura pontos de gestão preferenciais e um cliente organiza a respetiva lista de pontos de gestão, o cliente coloca os pontos de gestão preferenciais no topo da lista. Esta lista inclui todos os pontos de gestão do site atribuído do cliente.  

> [!NOTE]  
>  Roaming de cliente significa que ele altera respetivas localizações de rede. Por exemplo, quando um computador portátil circula para uma localização de escritórios remotos. Quando um cliente faz roaming, poderá utilizar um ponto de gestão do local site antes de tentar para utilizar um servidor do seu site atribuído. Esta lista de servidores do seu site atribuído inclui os pontos de gestão preferenciais. Para obter mais informações, consulte [compreender como os clientes localizam os recursos de site e os serviços](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  



## <a name="overlapping-boundaries"></a>Sobreposição de limites  

 O Configuration Manager suporta configurações de limites sobrepostos para localização de conteúdo. Quando a localização de rede do cliente pertence a mais do que um grupo de limites:

-   Quando um cliente solicita conteúdo, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que possuem o conteúdo.  

-   Quando um cliente solicita a um servidor para enviar ou receber as respetivas informações de migração de estado, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado associados um grupo de limites que inclui a localização de rede atual do cliente.  

Este comportamento permite que o cliente selecione o servidor mais próximo para transferir o conteúdo ou as informações de migração de estado.  



## <a name="example-of-using-boundary-groups"></a>Exemplo de como utilizar grupos de limites

O exemplo seguinte utiliza um cliente pesquisar conteúdo de um ponto de distribuição. Este exemplo pode ser aplicado a outras funções de sistema de sites que utilizam grupos de limites. 

Crie três grupos de limites que não partilham limites ou servidores de sistema de sites:  

- Grupo BG_A com pontos de distribuição DP_A1 e DP_A2   

- Grupo BG_B com pontos de distribuição DP_B1 e DP_B2  

- Grupo BG_C com pontos de distribuição DP_C1 e DP_C2  

Adicione as localizações de rede dos seus clientes como limites ao apenas o grupo de limites BG_A. Em seguida, configure as relações a partir desse grupo de limites para os outros dois grupos de limites:  

- Configurar pontos de distribuição para os primeiros *vizinho* grupo (BG_B) a ser usado após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos são boas para localizações de limite do primeiro grupo.  

- Configurar a segunda *vizinho* grupo (BG_C) a ser utilizado depois de 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos são numa WAN de outros grupos de limites de dois.  

- Também adicione ao grupo de limites de site padrão outro ponto de distribuição que está no servidor do site. Esse servidor é a localização de origem de conteúdo menos preferencial, mas é centralmente localizados para todos os grupos de limites.

    Exemplo de grupos de limites e tempos de contingência:

     ![Exemplo de grupos de limites e tempos de contingência](media/BG_Fallback.png)


Com esta configuração:  

- O cliente começa a procurar o conteúdo a partir de pontos de distribuição no respetivo *atual* (BG_A) do grupo de limites. Ele procura cada ponto de distribuição de dois minutos e, em seguida, muda para o próximo ponto de distribuição no grupo de limites. Agrupamento do cliente de localizações de origem de conteúdo válida inclui DP_A1 e DP_A2.  

- Se o cliente não conseguir localizar o conteúdo a partir de seus *atual* grupo de limites depois de procurar por 10 minutos, em seguida, adiciona os pontos de distribuição do grupo de limites de BG_B à sua pesquisa. Em seguida, continua a pesquisar conteúdo de um ponto de distribuição no respetivo conjunto combinado de servidores. Este conjunto inclui agora os servidores a partir de grupos de limites BG_A tanto BG_B. O cliente continua a contactar cada ponto de distribuição durante dois minutos e, em seguida, muda para o próximo servidor em seu pool. Agrupamento do cliente de localizações de origem de conteúdo válida inclui DP_A1, DP_A2, DP_B1 e DP_B2.  

- Após um adicionais 10 minutos (total de 20 minutos), se o cliente ainda não foi encontrado um ponto de distribuição com conteúdo, ele se expande seu pool para incluir servidores disponíveis da segunda *vizinho* de grupo, o grupo de limites BG_C. O cliente tem agora seis pontos de distribuição para procurar: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2. Ele continua mudando para um novo ponto de distribuição até encontrar conteúdo a cada dois minutos.  

- Se o cliente não foi encontrado conteúdo depois de um total de 120 minutos, retrocede para incluir o *grupo de limite de site predefinido* como parte da sua pesquisa contínua. Agora o conjunto inclui todos os pontos de distribuição de três grupos de limites configurados e o ponto de distribuição final localizado no servidor do site. O cliente, em seguida, continua a pesquisa de conteúdo, a alteração de pontos de distribuição a cada dois minutos até que o conteúdo é encontrado.  

Ao configurar os grupos de vizinho diferentes para estar disponível em momentos diferentes, pode controlar quando os pontos de distribuição específicos são adicionados como uma localização de origem de conteúdo. O cliente utiliza a contingência para o grupo de limites de site padrão como uma rede de segurança para o conteúdo que não está disponível a partir de qualquer outra localização.



## <a name="changes-from-prior-versions"></a>Alterações das versões anteriores

Seguem-se as principais alterações de grupos de limites e como os clientes localizam o conteúdo no ramo atual do Configuration Manager. Muitas destas alterações e conceitos funcionam em conjunto.


### <a name="configurations-for-fast-or-slow-are-removed"></a>Configurações para rápida ou lenta são removidas

Já não está a configurar pontos de distribuição individuais para ser rápido ou lento. Em vez disso, cada sistema de sites associado a um grupo de limites é Tratado da mesma. Por causa dessa alteração, o **referências** separador de propriedades do grupo de limites já não suporta a configuração de rápida ou lenta.  


### <a name="new-default-boundary-group-at-each-site"></a>Novo grupo de limite predefinido em cada site

Cada site primário tem um novo grupo de limites de padrão com o nome **predefinição---grupo de limite Site&lt;sitecode >**. Quando um cliente não está numa localização de rede atribuído a um grupo de limites, ele usa os sistemas de sites associados ao grupo predefinido do seu site atribuído. Recomendamos que utilize este grupo de limites como uma substituição para o conceito de localização de conteúdo de contingência.     

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>**Permitir que as localizações de origem de contingência para conteúdo** é removido
Já não é explicitamente a configurar um ponto de distribuição para ser utilizado para contingência. As opções para configurar esta definição são removidas da consola.

Além disso, o resultado da definição **permitir que os clientes utilizem uma localização de origem de contingência para conteúdo** numa implementação foi alterado o tipo para aplicações. Esta definição num tipo de implementação agora permite que um cliente utilizar o grupo de limites de site padrão como uma localização de origem de conteúdo.

#### <a name="boundary-groups-relationships"></a>Relações de grupos de limites
Pode associar cada grupo de limites a um ou mais grupos de limites adicionais. Estas ligações formam relações que configura no novo separador de propriedades de grupo limites com o nome **relações**:  

- Cada grupo de limites que um cliente é diretamente associado é chamado um **atual** grupo de limites.  

- Nenhum grupo de limites um cliente pode utilizar devido a uma associação entre esse cliente *atual* grupo de limites e outro grupo é chamado um **vizinho** grupo de limites.  

- Sobre o **relações** separador, adicionar grupos de limites para utilizar como um *vizinho* grupo de limites. Também configure um período de tempo em minutos para contingência. Quando um cliente não conseguir localizar o conteúdo de um ponto de distribuição no *atual* grupo, desta vez, é quando o cliente começa a pesquisar localizações de conteúdo de *vizinho* grupos de limites.  

    Quando adicionar ou alterar a configuração de um grupo de limites, pode bloquear a contingência para esse grupo de limites específicos do grupo atual que está a configurar.  

Para utilizar a nova configuração, defina explícitas associações (links) de um grupo de limites para outro. Configure todos os pontos de distribuição nesse grupo associado com o mesmo tempo em minutos. Quando um cliente não conseguir encontrar uma origem de conteúdo do respetivo *atual* grupo de limites, o tempo que configurar determina quando começa a procurar a fontes de conteúdo do seu grupo de limite vizinho.

Além dos grupos de limites que configure explicitamente, cada grupo de limites tem uma ligação implícita para o grupo de limites de site padrão. Esta ligação é ativada após 120 minutos. Em seguida, o grupo de limites de site predefinido torna-se um grupo de limite vizinho. Este comportamento permite que os clientes utilizar como localizações de origem de conteúdo os pontos de distribuição associados a esse grupo de limites.

Este comportamento substitui o que era anteriormente chamado de contingência para conteúdo. Substituir este comportamento predefinido de 120 minutos associando explicitamente o grupo de limites de site predefinido para um *atual* grupo. Definir uma hora específica em minutos, ou bloquear contingência inteiramente para impedir a sua utilização.


### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Os clientes tentam obter o conteúdo de cada ponto de distribuição para até dois minutos

Quando um cliente procura de uma localização de origem de conteúdo, este tenta aceder a cada ponto de distribuição durante dois minutos antes de, em seguida, tentar outro ponto de distribuição. Este comportamento é uma alteração de versões anteriores em que os clientes tentaram ligar a um ponto de distribuição para até duas horas.

- Os clientes selecionam aleatoriamente o primeiro ponto de distribuição a partir do agrupamento de servidores disponíveis no cliente do *atual* grupo de limites (ou grupos).  

- Depois de dois minutos, se o cliente ainda não foi encontrado o conteúdo, ele muda para um novo ponto de distribuição e tenta obter conteúdo a partir desse servidor. O processo se repete a cada dois minutos até que o cliente encontra o conteúdo ou alcança o último servidor no seu conjunto.  

- Se um cliente não conseguir encontrar uma localização de origem de conteúdo válida a partir do respetivo *atual* agrupamento antes de atingir o período de contingência para um *vizinho* grupo de limites, o cliente, em seguida, adiciona os pontos de distribuição do que *vizinho* grupo ao final da lista atual. Ele pesquisa, em seguida, o grupo expandida das localizações de origem, que inclui os pontos de distribuição a partir de ambos os grupos de limites.  

    > [!TIP]  
    > Quando criar uma ligação explícita do grupo de limites atual para o grupo de limites de site padrão e define um tempo de contingência que é menor que o tempo de contingência para um link para um grupo de limite vizinho, os clientes começam a pesquisar localizações de origem a partir do site predefinido grupo de limites antes de incluir o grupo de vizinho.  

- Quando o cliente não consegue obter o conteúdo do último servidor no agrupamento, ele começa novamente o processo.  



## <a name="see-also"></a>Consulte também

- [Procedimentos para grupos de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures)  

- [Sobre limites](/sccm/core/servers/deploy/configure/boundaries)  

- [Conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  
