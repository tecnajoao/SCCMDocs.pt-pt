---
title: Definir grupos de limites | Documentos do Microsoft
description: "Compreenda os grupos de limites com ligação de clientes para sistemas de sites no System Center Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d940fd1bbf96767d44f8c55315e814be55a83897
ms.openlocfilehash: 5684fd4fbfd0ffb8f3ffbcfa122eef3dafd77327
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurar grupos de limites para o System Center Configuration Manager


*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizar grupos de limites no System Center Configuration Manager para logicamente grupo relacionado com localizações de rede ([limites](/sccm/core/servers/deploy/configure/boundaries)) para facilitar a gerir a sua infraestrutura. Para poder utilizar o grupo de limites, tem de atribuir os limites a grupos de limites.

Por predefinição, o Configuration Manager cria um grupo de limites de site predefinido em cada site.

> [!IMPORTANT]  
>  **As informações nesta secção de grupos de limites e as secções de subordinados aplica-se a versão 1610 ou posterior.** Este conteúdo tiver sido revisto para ser específicas alterações estruturais introduzidas para grupos de limites com esta versão de atualização.
>
> **Se utilizar versões anteriores ao 1610**, consulte o artigo [grupos de limites para versões do System Center Configuration Manager 1511, 1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) para obter informações sobre como utilizar e configurar grupos de limites com essas versões de produto.

Para configurar grupos de limites, associe limites (localizações de rede) e funções de sistema de sites, como os pontos de distribuição, ao grupo de limites. Isto ajuda a associar os clientes nos servidores do sistema de sites, como pontos de distribuição que estão localizados junto de clientes na rede.

Quando atribuir o mesmo limite a vários grupos de limites e atribuir o mesmo site servidores do sistema, como pontos de distribuição, a vários grupos de limites, aumentar a disponibilidade de sistemas de site para uma vasta gama de localizações de rede.

Os clientes utilizam um grupo de limites para:  

-   Atribuição automática de site  
-   Para localizar um servidor de sistema de sites que pode fornecer um serviço, incluindo:
    - Pontos de distribuição para localização de conteúdo
    -    Pontos de atualização de software (início com a versão 1702)
    - Pontos de migração de estado
    - Pontos de gestão de preferência (se pretender utilizar pontos de gestão preferencial, tem de ativar esta opção para a hierarquia e não a partir da configuração do grupo de limites. Consulte o artigo [para ativar a utilização de pontos de gestão preferencial](#to-enable-use-of-preferred-management-points) neste tópico.)

##  <a name="boundary-groups-and-relationships"></a>Grupos de limites e relações
Para cada grupo de limites na hierarquia, pode atribuir:

-  Um ou mais limites. Quando um cliente se encontre numa localização de rede que está definida como um limite atribuído a um grupo de limites específicos, que é denominada a **atual** grupo de limites. Um cliente pode ter mais do que um grupo de limites atual.
- Uma ou mais funções de sistema de sites.  Os clientes podem sempre utilizar funções de sistema de sites associadas com o atual grupo de limites. Dependendo das configurações adicionais, poderá poderão utilizar funções do sistema de sites em grupos de limites adicionais.  

Para cada grupo de limites que cria, pode configurar uma ligação unidirecional para outro grupo de limites. A ligação é designado por um **relação**. Ligação para os grupos de limites são denominados **vizinho** grupos de limites. Um grupo de limites pode ter várias relações, cada uma com um grupo de limites de vizinho específico.

A configuração de cada relação determina quando um cliente que não consegue localizar que um servidor de sistema de sites disponíveis no respetivo grupo de limites atual pode começar a procurar um grupo de limites de vizinho para localizar um sistema de sites disponíveis. Esta pesquisa de grupos adicionais chama **contingência**.

## <a name="fallback"></a>Contingência
Para impedir problemas para os clientes não conseguem encontrar um sistema de sites disponíveis no respetivo grupo de limites atual, pode define relações entre os grupos de limites que define o comportamento de contingência. Contingência permite que um cliente expandir a sua pesquisa para grupos de limites adicionais para localizar um sistema de sites disponíveis.

As relações são configuradas num propriedades do grupo de limites **relações** separador. Quando configura uma relação, definir uma ligação a um grupo de limites de vizinho. Para cada tipo de função de sistema de sites que é suportado, pode configurar as definições de independentes de contingência a esse grupo de limites de vizinho. Por exemplo, quando configurar uma relação com um grupo de limites específicos pode definir contingência pontos de distribuição para ocorrer, passados 20 minutos em vez da predefinição de 120. Consulte o artigo [exemplo de utilização de grupos de limites](#example-of-using-boundary-groups) por um exemplo mais extenso.

Se um cliente não conseguir localizar uma função do sistema de sites disponíveis no respetivo grupo de limites atual, o cliente utiliza o tempo de contingência em minutos para determinar após quanto pode começar a procurar um sistema de sites disponíveis que está associado esse grupo de limites de vizinho.  

Quando um cliente não é possível localizar um sistema de sites disponíveis e começa a procurar nas localizações a partir de grupos de limites de vizinho, aumenta o conjunto de sistemas de sites disponíveis que pode utilizar de forma que é definido pela sua configuração de grupos de limites e as respetivas relações.

- Um grupo de limites pode ter mais de uma relação. Isto permite-lhe configurar reversão para cada tipo de sistema de sites para neighbors diferentes para ocorrer depois diferentes períodos de tempo.    
- Os clientes serão contingência apenas a um grupo de limites que é um vizinho direto do respetivo grupo de limites atual.
- Quando um cliente for membro de vários grupos de limites, o grupo de limites atual está definido como uma União muito do cliente grupos de limites. Que o cliente pode em seguida, reversão para neighbors de qualquer um desses grupos de limites original.

### <a name="the-default-site-boundary-group"></a>O grupo de limites de site predefinidos
Para além de criar os grupos de limites, cada site tem um grupo de limites de site predefinido que é criado pelo Configuration Manager. Este grupo com o nome ***limites-grupo de predefinido-Site&lt;sitecode >***. Por exemplo, o grupo para o site ABC seria chamado *limites-grupo de predefinido-Site&lt;ABC >.*

Para cada grupo de limites que cria, Configuration Manager cria automaticamente uma ligação de implícita para cada grupo de limites de site predefinidos na hierarquia.
-    A hiperligação implícita é uma opção de contingência de predefinição de um grupo de limites atual para o grupo de limites predefinidos de sites que tem uma hora de contingência predefinida de 120 minutos.
-    Clientes que não estejam num limite de associado a nenhum grupo de limites na hierarquia de utilizam o grupo de limites de site predefinidos a partir do respetivo site atribuído para identificar podem utilizar funções do sistema de site válido.

Para gerir contingência para o grupo de limites de site predefinido:
- Pode aceder às propriedades de site predefinidos limites do grupo e alterar os valores no **comportamento predefinido** separador. Alterações que efetuar aqui aplicam-se a *todos os* implícito ligações a este grupo de limites. Estas definições podem ser substituídas quando configurou a ligação explícita para este grupo de limites de site predefinidos a partir de outro grupo de limites.
- Pode aceder às propriedades de um grupo de limites que criou e alterar os valores para a ligação explícito que vai para um grupo de limites de sites predefinido. Quando definir uma nova hora em minutos para contingência ou bloco de contingência, essa alteração afeta apenas a ligação que está a configurar. Configurações da ligação explícita substituem as no **comportamento predefinido** separador de um grupo de limites de site predefinido.


## <a name="site-assignment"></a>Atribuição de site  
 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recentemente instalado que utiliza a atribuição automática de site irá aderir ao site atribuído de um grupo de limites que contém a localização de rede atual do cliente.  
-   Depois da atribuição a um site, um cliente não altera a sua atribuição de site ao alterar a respetiva localização de rede. Por exemplo, se o cliente fizer roaming para uma nova localização de rede que é representada por um limite num grupo de limites com uma atribuição de site diferente, site atribuído do cliente permanecerá inalterado.  
-   Quando a Deteção de Sistemas do Active Directory deteta um novo recurso, as informações de rede do recurso detetado são comparadas com os limites dos grupos de limites. Este processo associa o novo recurso a um site atribuído que será utilizado pelo método de instalação push do cliente.  
-   Quando um limite for membro de vários grupos de limites que tenham diferentes sites atribuídos, os clientes selecionam um dos sites de forma aleatória.  
-   As alterações efetuadas a um site atribuído de um grupo de limites apenas são aplicáveis a novas ações de atribuição de site. Os clientes atribuídos anteriormente a um site não reavaliam a respetiva atribuição de site com base nas alterações à configuração de um grupo de limites (ou à própria localização de rede).  

Para obter mais informações sobre a atribuição de site do cliente, consulte o artigo [atribuição automática de sites a utilizar para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) no [como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Pontos de distribuição

Quando um cliente solicita a localização de um ponto de distribuição, o Configuration Manager envia ao cliente uma lista que inclui os sistemas de sites do tipo adequado que estão associados a cada grupo de limites que inclui a localização de rede atual de clientes:

-   **Durante a distribuição de software**, os clientes solicitam uma localização de conteúdo de implementação que está disponível a partir de um ponto de distribuição ou outra origem de conteúdo válida (por exemplo, um cliente configurado para a cache de elementos da).

-   **Durante a implementação do sistema operativo**, os clientes solicitam uma localização para enviar ou receber as suas informações de migração de estado.  

Durante a implementação de conteúdos, se um cliente solicita conteúdo que não está disponível a partir de uma origem no respetivo grupo de limites atual, o cliente continua a pedir que o conteúdo tentar diferentes origens de conteúdo no respetivo grupo de limites atual até que seja atingido o período de contingência para um grupo de limites de vizinho ou o grupo de limites de site predefinido. Se o cliente ainda não encontrar o conteúdo, em seguida, expande a pesquisa para origens de conteúdo a incluir os grupos de limites de vizinho.

No entanto, se o conteúdo é distribuído a pedido e não está disponível num ponto de distribuição quando solicitado por um cliente, iniciar o processo para transferir o conteúdo para esse ponto de distribuição e é possível que o cliente irá encontrar esse servidor como uma origem de conteúdo antes de reverter para utilizar um grupo de limites de vizinho.

## <a name="software-update-points"></a>Pontos de atualização de software
A partir da versão 1702, os clientes utilizam os grupos de limites para localizar um novo ponto de atualização de software. Pode adicionar pontos de atualização de individual software a grupos de limites diferentes para controlar quais os servidores de um cliente pode encontrar.

Ao atualizar a partir de uma versão anterior ao 1702, todos os pontos de atualização de software existente são adicionados ao grupo de limites de site predefinido em cada site. Esta ação mantém o comportamento de pré-atualização em que os clientes selecionam um ponto de atualização de software a partir do conjunto de pontos de atualização de software disponíveis que tiver configurado para a hierarquia.  Este comportamento é mantido até optar por adicionar pontos de atualização de individual software para grupos de limites diferentes para seleção controlada e o comportamento de contingência.

Se instalar um novo site que é executada versão 1702 ou posterior, tem de atribuir os pontos de atualização de software a um grupo de limites antes dos clientes podem localizar e utilizá-los.


Contingência de pontos de atualização de software está configurada como outras funções de sistema de sites, mas tem as seguintes advertências:
- **Os novos clientes utilizam grupos de limites para selecionar pontos de atualização de software.** Depois de instalar a versão 1702, os clientes novos que instalar selecionam um ponto de atualização de software associada aos grupos de limites que tiver configurado.

  Esta ação substitui o anterior comportamento onde os clientes selecionam um ponto de atualização de software aleatoriamente a partir de uma lista das pessoas que partilham na floresta do cliente.

- **Anteriormente instalados os clientes continuam a utilizar o respetivo ponto de atualização de software atual até que contingência para localizar um novo.** Os clientes que tiverem sido instaladas e que já tenham um ponto de atualização de software irão continuar a utilizar esse ponto de atualização de software até que o servidor não é possível aceder. Isto inclui a utilização contínua de um ponto de atualização de software que não esteja associado com o grupo de limites atual do cliente.

  Quando um cliente que já tenha um ponto de atualização de software falhar para contactá-lo, o cliente pode reversão em seguida, para localizar outra. Ao utilizar a reversão, o cliente recebe uma lista de todos os pontos de atualização de software a partir do respetivo grupo de limites atual. Se não conseguir localizar um servidor disponível para 120 minutos, irá, em seguida, contingência respetivos grupos de limites de vizinho e o grupo de limites de site predefinido. Contingência a ambos os grupos de limites acontece ao mesmo tempo porque o software de atualizar os pontos de contingência tempo para grupos de vizinho está definido para 120 minutos e não pode ser alterado. 120 minutos também é o período predefinido utilizado para contingência para o grupo de limites de site predefinido. Quando um cliente reverterá para ambos os um vizinho e grupo de limites de site predefinidos, o cliente tenta contactar os pontos de atualização de software a partir do grupo de limites de vizinho antes de tentar utilizar um grupo de limites de site predefinido.

  A utilização contínua de um ponto de atualização de software existente, mesmo quando esse servidor não está no grupo de limites atual do cliente é intencional. Isto acontece porque uma alteração de ponto de atualização de software pode implicar uma utilização de largura de banda de rede grande como o cliente sincroniza os dados com o novo ponto de atualização de software. O atraso em transição pode ajudar a evitar saturating rede devem todos os seus clientes mudarem para um novo software de ponto de atualização ao mesmo tempo.

- **Configurações para tempo de contingência:**  Ao contrário das configurações de contingência para outras funções de sistema de sites, os pontos de atualização de software ainda não suportam um período de tempo configurável em minutos. Em vez disso, o comportamento de contingência é limitado ao seguinte:  
  - **Tempos de contingência (em minutos):**  Esta opção a cinzento para pontos de atualização de software e não pode ser configurada. Está definido para 120 minutos.
  -     **Nunca contingência:** Pode bloquear reversão para um ponto de atualização de software a um grupo de limites de vizinho quando utiliza esta configuração.

## <a name="preferred-management-points"></a>Pontos de gestão preferenciais

 Os pontos de gestão preferenciais permitem a um cliente identificar um ponto de gestão que esteja associado à sua localização de rede atual (limite).  

-   Um cliente tenta utilizar um ponto de gestão preferencial do respetivo site atribuído antes de utilizar um ponto de gestão a partir do respetivo site atribuído que não esteja configurado como preferencial.  
-   Para utilizar esta opção, tem de ativá-lo para a hierarquia e, em seguida, configurar grupos de limites em sites primários individuais a incluir os pontos de gestão que devem ser associados com limites associado do grupo de limites.  
-   Quando são configurados pontos de gestão preferenciais e um cliente organiza respetiva lista de pontos de gestão, o cliente coloca os pontos de gestão preferencial na parte superior da respetiva lista de pontos de gestão atribuído (que inclui todos os pontos de gestão a partir do site atribuído do cliente).  

> [!NOTE]  
>  Quando um cliente fizer roaming (o que significa alterar as respetivas localizações de rede, tais como quando um computador portátil circula para uma localização de escritório remoto), poderá utilizar um ponto de gestão (ou ponto de gestão do proxy) a partir do site local na nova localização antes de tentar utilizar um ponto de gestão a partir do respetivo site atribuído (que inclui os pontos de gestão preferenciais).  Consulte o artigo [compreender como os clientes localizam os recursos do site e os serviços do System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para obter mais informações.  

### <a name="overlapping-boundaries"></a>Sobreposição de limites  
 O Configuration Manager suporta configurações de limites sobrepostos para localização de conteúdo:  

-   **Quando um cliente solicita conteúdo**e a localização de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que possuem o conteúdo.  
-   **Quando um cliente solicita a um servidor para enviar ou receber as informações de migração de estado**e a localização de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado que estão associados um grupo de limites que inclui a localização de rede atual do cliente.  

Este comportamento permite que o cliente selecione o servidor mais próximo para transferir o conteúdo ou as informações de migração de estado.  



## <a name="example-of-using-boundary-groups"></a>Exemplo de utilização de grupos de limites
O exemplo seguinte utiliza um cliente procurar conteúdo num ponto de distribuição. Este exemplo pode ser aplicado a outras funções de sistema de sites que utilizam grupos de limites. No entanto, como aplica-se para pontos de atualização de software, tenha em atenção que os pontos de atualização de software não suporta a configuração de um período de tempo em minutos para contingência a um grupo de vizinho e utilize sempre um período de 120 minutos.

Crie três grupos de limites que não partilham limites ou servidores do sistema de sites:
-    Grupo BG_A com pontos de distribuição DP_A1 e DP_A2 associado ao grupo de
-    Grupo BG_B com pontos de distribuição DP_B1 e DP_B2 associado ao grupo de
-    Grupo BG_C com pontos de distribuição DP_C1 e DP_C2 associado ao grupo de

Pode adiciona as localizações de rede dos clientes como limites ao apenas o grupo de limites BG_A e, em seguida, configurar relações desse grupo de limites para os outros dois grupos de limites:
-    Configurar pontos de distribuição para o primeiro *vizinho* grupo (BG_B) para ser utilizado após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos são com boas ligações para as localizações de limite de grupos primeiro.
-    Configurar o segundo *vizinho* grupo (BG_C) para ser utilizado, passados 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos são através de uma WAN a partir de outros dois grupos de limites.
-    Pode também adiciona um ponto de distribuição adicionais que esteja localizado no servidor do site ao grupo de limites de site de sites predefinido. Esta é a localização de origem de conteúdo menos preferencial, mas se centralmente encontra todos os grupos de limites.

    Exemplo de grupos de limites e tempos de contingência:

     ![BG_Fallack](media/BG_Fallback.png)


Com esta configuração:
-    O cliente começa procurar conteúdo a partir de pontos de distribuição no respetivo *atual* procurar distribuição de cada grupo de limites (BG_A), aponte para dois minutos antes de mudar para o próximo ponto de distribuição no grupo de limites. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1 e DP_A2.
-    Se o cliente não conseguir encontrar o conteúdo a partir do respetivo *atual* grupo de limites após à procura de 10 minutos, em seguida, adiciona os pontos de distribuição a partir do grupo de limites BG_B à sua pesquisa. Em seguida, continua a pesquisar conteúdo num ponto de distribuição no seu conjunto combinado de pontos de distribuição que inclui agora as do BG_A tanto BG_B grupos de limites. O cliente continua a contactar cada ponto de distribuição para dois minutos antes de mudar para o próximo ponto de distribuição a partir do seu conjunto. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1, DP_A2, DP_B1 e DP_B2.
-    Após 10 minutos (total de 20 minutos) adicionais se o cliente ainda não encontrou um ponto de distribuição com conteúdo, expande o conjunto de pontos de distribuição disponíveis para incluir os da segunda *vizinho* agrupar, grupo de limites BG_C. Agora, o cliente tem 6 pontos de distribuição para pesquisa (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua a alterar para um novo ponto de distribuição de todos os dois minutos até é encontrado conteúdo.
-    Se o cliente não foi encontrado conteúdo após um total de 120 minutos,-reverterá para incluir o *grupo de limites de site predefinidos* como parte da sua pesquisa contínua. O conjunto de pontos de distribuição inclui agora todos os pontos de distribuição a partir de grupos de limites configurados três e o ponto de distribuição final localizado no computador do servidor do site.  O cliente, em seguida, continua a pesquisa de conteúdo, alterar cada dois minutos até é encontrado conteúdo a pontos de distribuição.

Ao configurar os grupos de vizinho diferentes para estar disponível em alturas diferentes, pode controlar quando são adicionados como uma localização de origem de conteúdo, pontos de distribuição específico e quando, ou se, o cliente utiliza contingência para o grupo de limites de site predefinidos como uma rede de segurança de conteúdo que não está disponível a partir de qualquer outra localização.






### <a name="update-existing-boundary-groups-to-the-new-model"></a>Atualizar os grupos de limites existentes para o novo modelo
Quando atualizar para versão anterior ao 1610, as seguintes configurações são efetuadas automaticamente. Estes se destinam a certifique-se de que o comportamento de contingência atual permanece disponível até configurar novos grupos de limites e relações.

-    É criado um grupo de limites de site predefinido para cada site primário, o nome é ***limites-grupo de predefinido-Site&lt;sitecode >.***
  -    Pontos de distribuição com *permitir a localização de origem de contingência para conteúdo* dada e pontos de migração de estado em sites primários são adicionados ao *limites-grupo de predefinido-Site&lt;sitecode >* grupo de limites desse site.
  -    A partir da versão 1702, pontos de atualização de software são adicionados a cada sites *limites-grupo de predefinido-Site&lt;sitecode >*.
-    É efetuada uma cópia de cada grupo de limites existentes que inclua um servidor de sites configurado com uma ligação lenta. O nome do novo grupo é *** &lt;nome original do grupo de limites >-&lt;ID do grupo de limites original >***:  
    -    Sistemas de sites que tenham uma ligação rápida são mantidos no grupo de limites original.
    -    Uma cópia dos sistemas de sites (pontos de distribuição, pontos de gestão) que tenham uma ligação lenta são adicionados à cópia do grupo de limites. Os sistemas de sites original configurados como lenta permanecem nos respetivos grupos de limites original para compatibilidade com versões anteriores, mas não são utilizados a partir desses grupos de limites.
    - Esta cópia do grupo de limites não tiverem limites associados à mesma. No entanto, é criada uma ligação de contingência entre o grupo original e a nova cópia do grupo de limites que tenha o tempo de contingência definido como zero.  


- **Sites específicos para o secundário:**
  - É criado um grupo de limites se um site secundário tem, pelo menos, um ponto com de distribuição *permitir a localização de origem de contingência para conteúdo* ponto de migração de estado ou dada. O nome do grupo de limites for ***secundária-Site-vizinho - Tmp&lt;Sitecode >.***
  - Pontos de distribuição de todos os com *permitir a localização de origem de contingência para conteúdo* dada e pontos de migração de estado são adicionados a este grupo de limites de site secundário recentemente criado.
  - É criada uma ligação de contingência entre o grupo de limites original e o grupo de limites de vizinho criado recentemente e a hora de contingência está definida para zero.


 A tabela seguinte identifica o novo comportamento de contingência que poderá esperar da combinação de original definições de implementação e pontos de distribuição configurações:

Configuração de implementação original para "Não executar o programa" numa rede lenta  |Configuração para "Permitir a utilizar uma localização de origem de contingência para conteúdo de cliente" do ponto de distribuição original  |Novo comportamento de contingência  
---------|---------|---------
Selecionada     |  Selecionada    |  **Nenhum contingência** -utilize apenas os pontos de distribuição num grupo de limites atual       
Selecionada     |  Não selecionado|  **Nenhum contingência** -utilize apenas os pontos de distribuição num grupo de limites atual       
Não selecionado |  Não selecionado|  **Contingência para vizinho** - utilizar pontos de distribuição num grupo de limites atual e, em seguida, adicione os pontos de distribuição a partir do grupo de limites de vizinho. A menos que é configurada uma ligação de explícita para o grupo de limites de site predefinidos, os clientes não poderá contingência a esse grupo.    
Não selecionado | Selecionada        |   **Contingência normal** -utilizar pontos de distribuição num grupo de limites atual, em seguida, as do vizinho e o site predefinido de grupos de limites

 Todas as outras configurações de implementação resultam em **contingência Normal**.  




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Alterações a partir de versões anteriores para a IU do e comportamento para localizações de conteúdo
Seguem-se as alterações chave para grupos de limites e como os clientes localizarem conteúdo. Estas alterações são introduzidas com a versão 1610. Muitas destas alterações e conceitos trabalhar em conjunto.


-    **Configurações para rápida ou lenta são removidas:** Já não configurar pontos de distribuição individuais para serem rápida ou lenta.  Em vez disso, cada sistema de sites associado a um grupo de limites é Tratado da mesma. Devido a esta alteração, o **referências** separador da folha de propriedades do grupo de limites já não suporta a configuração rápida ou lenta.
-     **Novo grupo de limites predefinidos em cada site:**  Cada site primário tem um novo grupo de limites predefinidos, com o nome ***limites-grupo de predefinido-Site&lt;sitecode >***.  Quando um cliente não se encontre numa localização de rede que está atribuída a um grupo de limites, esse cliente utilizará os sistemas de sites associados ao grupo predefinido do site atribuído. Planear a utilização deste grupo de limites como uma substituição para o conceito de localização de conteúdo de contingência.      
 -    **'Permitir localizações de origem de contingência para conteúdo'** é removido: Configurar um ponto de distribuição para ser utilizado para contingência já não explicitamente, e as opções para configurar estas são removidas da IU.

    Além disso, o resultado da definição **permitir que os clientes utilizem uma localização de origem de contingência para conteúdo** numa implementação tipo para aplicações foi alterado. Esta definição agora num tipo de implementação permite que um cliente para utilizar o grupo de limites de site predefinidos como uma localização de origem de conteúdo.

 -    **Relações de grupos de limites:** Cada grupo de limites pode ser associado a um ou mais grupos de limites adicionais. Estas ligações formam relações que são configuradas no separador de propriedades do grupo de limites novo com o nome **relações**:
     -    Cada grupo de limites que está diretamente associado um cliente é designado por um **atual** grupo de limites.  
    -     Nenhum grupo de limites um cliente pode utilizar devido a uma associação entre esse cliente *atual* grupo de limites e outro grupo chama-se um **vizinho** grupo de limites.
    -  É o **relações** separador que adicionar grupos de limites que podem ser utilizados como um *vizinho* grupo de limites. Também pode configurar um período de tempo em minutos que determina quando um cliente que não consegue localizar conteúdo num ponto de distribuição no *atual* grupo irá começar a procurar em localizações de conteúdo das *vizinho* grupos de limites.

        Quando adicionar ou alterar uma configuração do grupo de limites, terá a opção para bloquear contingência a esse grupo de limites específicos do grupo atual que estiver a configurar.

    Para utilizar a nova configuração, define associações explícitas (ligações) a partir de um grupo de limites para outro e configurar todos os pontos de distribuição nesse grupo associado com o mesmo tempo em minutos. Determina o tempo que configura quando um cliente que não consegue localizar uma origem de conteúdo a partir do respetivo *atual* grupo de limites, pode começar a procurar fontes de conteúdo a partir desse grupo de limites de vizinho.

    Para além dos grupos de limites que configurar explicitamente, cada grupo de limites tem uma ligação de implícita para o grupo de limites de site predefinido. Esta ligação fica ativa depois de 120 minutos em que momento o grupo de limites de site predefinidos torna-se um grupo de limites de vizinho que permite que os clientes utilizar os pontos de distribuição associados esse grupo de limites como localizações de origem de conteúdo.

    Este comportamento substitui o que foi anteriormente designado contingência para conteúdo.  Pode substituir este comportamento predefinido de 120 minutos associando explicitamente o grupo de limites de site predefinido para um *atual* grupo e definir uma hora específica em minutos ou bloquear contingência completamente para impedir a sua utilização.


-     **Os clientes tentam obter conteúdo a partir de cada ponto de distribuição para até 2 minutos:** Quando um cliente procura de uma localização de origem de conteúdo, este tenta aceder a cada ponto de distribuição para 2 minutos antes de, em seguida, tentar outro ponto de distribuição. Esta é uma mudança de versões anteriores onde os clientes tentaram ligar a um ponto de distribuição até 2 horas.

    - O primeiro ponto de distribuição que um cliente tenta utilizar aleatoriamente está selecionado o conjunto de pontos de distribuição disponíveis no cliente do *atual* grupo de limites (ou grupos).

    - Depois de dois minutos, se o cliente não foi encontrado o conteúdo, este muda para um novo ponto de distribuição e tenta obter conteúdo a partir desse servidor. Este processo repete-se em dois minutos até o cliente localiza o conteúdo ou atinge o último servidor no seu conjunto.

    - Se um cliente não é possível encontrar uma localização de origem de conteúdo válida a partir do respetivo *atual* conjunto antes que o período de contingência para um *vizinho* grupo de limites for atingido, o cliente, em seguida, adiciona os pontos de distribuição que *vizinho* grupo para o fim da respetiva lista atual e, em seguida, irá pesquisar o grupo expandido das localizações de origem que inclua os pontos de distribuição a partir de ambos os grupos de limites.

        > [!TIP]  
        > Quando criar uma ligação explícita o atual grupo de limites para o grupo de limites de site predefinidos e definir uma hora de contingência que é menor do que o tempo de contingência para uma ligação para um grupo de limites de vizinho, os clientes irão começar a procurar localizações de origem a partir do grupo de limites de site predefinidos antes incluindo o grupo de vizinho.

    - Quando o cliente não consegue obter conteúdo a partir do servidor do último no agrupamento de, inicia o processo novamente.


## <a name="procedures-for-boundary-groups"></a>Procedimentos para grupos de limites
Os procedimentos seguintes aplicam-se à versão 1610 ou posterior. Se utilizar a versão anterior ao 1610, consulte os procedimentos em [grupos de limites para versões do System Center Configuration Manager 1511, 1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


### <a name="to-create-a-boundary-group"></a>Para criar um grupo de limites  
1.  Na consola do Configuration Manager, clique em **administração** > **configuração da hierarquia** >  **grupos de limites**.  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Grupo de Limites**.  

3.  Na caixa de diálogo **Criar Grupo de Limites** , selecione o separador **Geral** e especifique um **Nome** para este grupo de limites.  

4.  Clique em **OK** para guardar o novo grupo de limites.  


### <a name="to-configure-a-boundary-group"></a>Para configurar um grupo de limites  
 1.  Na consola do Configuration Manager, clique em **administração** > **configuração da hierarquia** >  **grupos de limites**.  

 2.  Selecione o grupo de limites que pretende modificar.  

 3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

 4.  Na caixa de diálogo **Propriedades** do grupo de limites, selecione o separador **Geral** para modificar os limites que são membros deste grupo de limites:  

     -   Para adicionar limites, clique em **Adicionar**, selecione a caixa de verificação de um ou mais limites e clique em **OK**.  

     -   Para remover limites, selecione o limite e clique em **Remover**.  

 5.  Selecione o separador **Referências** para modificar a atribuição de sites e a configuração do servidor do sistema de sites associada:  

     -   Para permitir que este grupo seja utilizado pelos clientes para atribuição de site, selecione a caixa de verificação **Utilizar este grupo de limites para atribuição de site**e, em seguida, selecione um site na caixa pendente **Site atribuído** .  

     -   Para configurar que servidores do sistema de sites disponíveis estão associados a este grupo de limites:  

     1.  Clique em **Adicionar**e, em seguida, selecione a caixa de verificação de um ou mais servidores. Os servidores são adicionados como servidores do sistema de sites associados a este grupo de limites. Só estão disponíveis os servidores que têm a função de sistema de sites instalada.  

         > [!NOTE]  
         >  Pode selecionar uma combinação de sistemas de sites disponíveis a partir de qualquer site na hierarquia. Os sistemas de sites selecionados são listados no separador **Sistemas de Sites** nas propriedades de cada limite que seja membro deste grupo de limites.  

     2.  Para remover um servidor deste grupo de limites, selecione o servidor e, em seguida, clique em **Remover**.  

         > [!NOTE]  
         >  Para parar a utilização deste grupo de limites para associar sistemas de sites, tem de remover todos os servidores listados como servidores do sistema de sites associados.  

 6.  Selecione o **relações** tecla de tabulação para configurar o comportamento de contingência:  

     - Clique em **adicionar**e, em seguida, selecione o grupo de limites que pretende configurar.

     - Defina uma hora de contingência para pontos de distribuição. Após este período de tempo, os clientes no grupo de limites que está a configurar relações, será possível começar a procurar conteúdo a partir de pontos de distribuição do grupo de limites que está a adicionar.

     - Para impedir a reversão para um grupo de limites específico, incluindo o *grupo de limites de site predefinidos* que está configurada por predefinição, selecione o grupo de limites e, em seguida, selecione a caixa do **nunca contingência**.   

 7.  Clique em **OK** para fechar as propriedades do grupo de limites e guardar a configuração.  

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>Para associar um servidor do site systme um grupo de limites  
 1.  Na consola do Configuration Manager, clique em **administração** > **configuração da hierarquia** >  **grupos de limites**.  

 2.  Selecione o grupo de limites que pretende modificar.  

 3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

 4.  Na caixa de diálogo **Propriedades** do grupo de limites, selecione o separador **Referências** .  

 5.  Em **Selecionar servidores do sistema de sites**, clique em **Adicionar**, selecione a caixa de verificação dos servidores do sistema de sites que pretende associar a este grupo de limites e, em seguida, clique em **OK**.  

 6.  Clique em **OK** para fechar a caixa de diálogo e guardar a configuração do grupo de limites.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Para configurar um site de contingência para atribuição automática de sites  

  1.  Na consola do Configuration Manager, clique em **administração** > **configuração do Site** >  **Sites**.  

  2.  No separador **Home Page** , no grupo **Sites** , clique em **Definições de Hierarquia**.  

  3.  No separador **Geral** , selecione a caixa de verificação para **Utilizar um site de contingência**e selecione um site na lista pendente **Site de contingência** .  

  4.  Clique em **OK** para guardar a configuração.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Para ativar a utilização de pontos de gestão preferenciais  

 1.  Na consola do Configuration Manager, clique em **administração** > **configuração do Site** > **Sites**e, em seguida, no **base** separador selecione **definições de hierarquia**.  

 2.  No separador **Geral** das Definições de Hierarquia, selecione **Os clientes preferem utilizar pontos de gestão especificados em grupos de limites**.  

 3.  Clique em **OK** para fechar a caixa de diálogo e guardar a configuração.  

