---
title: Definir grupos de limites | Microsoft Docs
description: "Compreenda os grupos de limites com ligação de clientes para sistemas de sites no System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 5debc6559f4b1c213e8ca513d685941c9e669063
ms.contentlocale: pt-pt
ms.lasthandoff: 07/29/2017

---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurar grupos de limites para o System Center Configuration Manager


*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizar grupos de limites no System Center Configuration Manager para agrupar logicamente relacionadas com as localizações de rede ([limites](/sccm/core/servers/deploy/configure/boundaries)) torna mais fácil de gerir a sua infraestrutura. Limites devem ser atribuídos a grupos de limites, antes de poder utilizar o grupo de limites.

Por predefinição, o Configuration Manager cria um grupo de limites de site predefinido em cada site.

> [!IMPORTANT]  
>  **As informações nesta secção de grupos de limites e respetivas secções subordinado aplica-se a versão 1610 ou posterior.** Este conteúdo tiver sido revisto para ser específico a alterações estruturais introduzidas para grupos de limites com esta versão de atualização.
>
> **Se utilizar versões anteriores à 1610**, consulte [grupos de limites para as versões do System Center Configuration Manager versão 1511, 1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) para obter informações sobre como utilizar e configurar grupos de limites com essas versões de produto.

Para configurar grupos de limites, associar limites (localizações de rede) e funções de sistema de sites, como pontos de distribuição, para o grupo de limites. Isto ajuda a associar clientes para servidores do sistema de sites como perto de pontos de distribuição que estão localizados os clientes na rede.

Ao atribuir o mesmo limite a vários grupos de limites e atribuir o mesmo site servidores do sistema, como pontos de distribuição a vários grupos de limites, aumentar a disponibilidade dos sistemas de sites para uma vasta gama de localizações de rede.

Os clientes utilizam um grupo de limites para:  

-   Atribuição automática de site  
-   Para localizar um servidor de sistema de sites que pode fornecer um serviço, incluindo:
    - Pontos de distribuição para localização de conteúdo
    -   Pontos de atualização de software (início com a versão 1702)
    - Pontos de migração de estado
    - Pontos de gestão preferenciais (se utilizar pontos de gestão preferidos, tem de ativar esta opção para a hierarquia e não a partir da configuração do grupo de limites. Consulte [para ativar a utilização de pontos de gestão preferenciais](#to-enable-use-of-preferred-management-points) neste tópico.)

##  <a name="boundary-groups-and-relationships"></a>Grupos de limites e relações
Para cada grupo de limites na hierarquia, pode atribuir:

-  Um ou mais limites. Quando um cliente estiver numa localização de rede que está definida como um limite atribuído a um grupo de limites específico, que é chamado o **atual** grupo de limites. Um cliente pode ter mais do que um grupo de limites atuais.
- Uma ou mais funções de sistema de sites.  Os clientes podem sempre utilizar funções de sistema de sites associadas com o respetivo grupo de limites atuais. Dependendo das configurações adicionais, poderá seria capazes de utilizar as funções do sistema de sites em grupos de limites adicionais.  

Para cada grupo de limites que cria, pode configurar uma ligação unidirecional para outro grupo de limites. A ligação é chamada um **relação**. Os grupos de limites a associar ao são denominados **vizinho** grupos de limites. Um grupo de limites pode ter várias relações, cada um com um grupo de limites de vizinho específico.

A configuração de cada relação determina quando um cliente que não consegue localizar que um servidor do sistema de sites disponíveis no seu grupo de limites atual pode começar a pesquisar um grupo de limites de vizinho para localizar um sistema de sites disponíveis. Esta pesquisa de grupos adicionais denomina **contingência**.

## <a name="fallback"></a>Contingência
Para evitar problemas para clientes quando estes não é possível localizar um sistema de sites disponíveis no respetivo grupo de limites atual, é possível definir a relação entre grupos de limites que define o comportamento de contingência. Contingência permite que um cliente expandir a sua pesquisa para grupos de limites adicionais para localizar um sistema de sites disponíveis.

As relações estão configuradas em Propriedades do grupo de limites **relações** separador. Quando configurar uma relação, é possível definir uma ligação a um grupo de limites de vizinho. Para cada tipo de função de sistema de sites que é suportada, pode configurar definições independentes para reversão para esse grupo de limites de vizinho. Por exemplo, quando configurar uma relação a um grupo de limites específico pode definir contingência para pontos de distribuição para ocorrer após 20 minutos, em vez da predefinição de 120. Consulte [exemplo de como utilizar grupos de limites](#example-of-using-boundary-groups) para obter um exemplo mais extenso.

Se um cliente não conseguir localizar uma função de sistema de sites disponíveis no seu grupo de limites atual, o cliente utiliza o contingência tempo em minutos para determinar após o período de tempo pode começar a pesquisar um sistema de sites disponíveis que está associado esse grupo de limites de vizinho.  

Quando um cliente não é possível localizar um sistema de sites disponíveis e começa a procurar nas localizações dos grupos de limites de vizinho, aumenta o conjunto de sistemas de sites disponíveis que pode utilizar de forma que é definida pela sua configuração de grupos de limites e relações.

- Um grupo de limites pode ter mais de uma relação. As relações de múltiplos pode configurar a contingência para cada tipo de sistema de sites para diferentes vizinhos para ocorrer após os períodos de tempo diferentes.    
- Clientes só contingência para um grupo de limites que é um vizinho direto do respetivo grupo de limites atuais.
- Quando um cliente é um membro de vários grupos de limites, o grupo de limites atual está definido como uma União de tudo o que os grupos de limites do cliente. Que o cliente pode, em seguida, contingência para vizinhos de qualquer um desses grupos de limites original.

### <a name="the-default-site-boundary-group"></a>O grupo de limites de site predefinido
Para além dos grupos de limites que cria, cada site tem um grupo de limites de site predefinido que é criado pelo Configuration Manager. Este grupo é designado ***predefinição-Site-limite-grupo&lt;sitecode >***. Por exemplo, o grupo para o site ABC seria possível designado *predefinição-Site-limite-grupo&lt;ABC >.*

Para cada grupo de limites que cria, o Configuration Manager cria automaticamente uma ligação implícita para cada grupo de limites de site predefinido na hierarquia.
-   A hiperligação implícita é uma opção de contingência de predefinido de um grupo de limites atuais ao grupo de limites de sites predefinido, que tem um tempo de contingência da predefinição de 120 minutos.
-   Os clientes que não estão num limite associado a nenhum grupo de limites na hierarquia utilizam o grupo de limites de site predefinido do respetivo site atribuído para identificar funções do sistema de sites válidos podem utilizar.

Para gerir a contingência para o grupo de limites de site predefinido:
- Pode aceder às propriedades do site predefinido limites do grupo e alterar os valores no **comportamento predefinido** separador. Alterações efetuadas aqui aplicam-se a *todos os* implícito ligações a este grupo de limites. Estas definições podem ser substituídas quando configurar a ligação explícita para este grupo de limites de site predefinido do outro grupo de limites.
- Pode aceder às propriedades de um grupo de limites que criou e alterar os valores para a ligação explícita que passa para um grupo de limites de site predefinido. Quando definir um novo período de tempo em minutos para contingência ou bloco de contingência, essa alteração afeta apenas a ligação que está a configurar. Configurações da ligação explícita substituem as que no **comportamento predefinido** separador de um grupo de limites de site predefinido.


## <a name="site-assignment"></a>Atribuição de site  
 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recentemente instalado que utilize a atribuição automática de site é associado ao site atribuído de um grupo de limites que contém a localização de rede atual do cliente.  
-   Depois da atribuição a um site, um cliente não altera a sua atribuição de site ao alterar a respetiva localização de rede. Por exemplo, se o cliente fizer roaming para uma nova localização de rede que é representada por um limite num grupo de limites com uma atribuição de site diferente, não altere permanece de site atribuído do cliente.  
-   Quando a Deteção de Sistemas do Active Directory deteta um novo recurso, as informações de rede do recurso detetado são comparadas com os limites dos grupos de limites. Este processo associa o novo recurso a um site atribuído que será utilizado pelo método de instalação push do cliente.  
-   Quando um limite é um membro de vários grupos de limites que possuem diferentes sites atribuídos, os clientes aleatoriamente selecionam um dos sites.  
-   As alterações efetuadas a um site atribuído de um grupo de limites apenas são aplicáveis a novas ações de atribuição de site. Os clientes atribuídos anteriormente a um site, não reevaluate a atribuição do site com base nas alterações à configuração de um grupo de limites (ou para sua própria localização de rede).  

Para obter mais informações sobre a atribuição de sites do cliente, consulte [utilizando a atribuição de Site automática para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) no [como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Pontos de distribuição

Quando um cliente solicita a localização de um ponto de distribuição, o Configuration Manager envia ao cliente uma lista que inclui os sistemas de sites do tipo adequado que estão associados a cada grupo de limites que inclui a localização de rede atual:

-   **Durante a distribuição de software**, os clientes solicitam uma localização para o conteúdo de implementação que está disponível a partir de um ponto de distribuição ou outra origem de conteúdo válida (por exemplo, um cliente configurado para a Cache ponto a ponto).

-   **Durante a implementação do sistema operativo**, os clientes solicitam uma localização para enviar ou receber as respetivas informações de migração de estado.  

Durante a implementação de conteúdos, se um cliente solicita conteúdo que não está disponível de uma origem no seu grupo de limites atual, o cliente continua a pedir esse conteúdo tentar diferentes origens de conteúdo no seu grupo de limites atual até que o período de contingência para um grupo de limites de vizinho ou o grupo de limites de site predefinido for atingido. Se o cliente ainda não encontrar o conteúdo, em seguida, expandir a pesquisa de origens de conteúdo incluir os grupos de limites de vizinho.

No entanto, se o conteúdo é distribuído a pedido e não está disponível num ponto de distribuição quando solicitado por um cliente, o processo para transferir o conteúdo para esse ponto de distribuição começa e é possível que o cliente irá encontrar este servidor como uma origem de conteúdo antes de reverter para utilizar um grupo de limites de vizinho.

## <a name="software-update-points"></a>Pontos de atualização de software
A partir da versão 1702, os clientes utilizam grupos de limites para localizar um novo ponto de atualização de software. Pode adicionar pontos de atualização de individual software para diferentes grupos de limites para controlar quais os servidores de um cliente pode localizar.

Se atualizar a partir de uma versão antes de 1702, todos os pontos de atualização de software existentes são adicionados ao grupo de limites do site predefinido em cada site. Isto mantém o comportamento de pré-atualização onde os clientes selecionam um ponto de atualização de software do agrupamento de pontos de atualização de software disponíveis que configurou para a sua hierarquia.  Este comportamento é mantido até optar por adicionar pontos de atualização de individual software para diferentes grupos de limites para seleção controlada e o comportamento de contingência.

Se instalar um novo site que executa a versão 1702 ou posterior, os pontos de atualização de software não foram adicionados ao grupo de limites de site predefinido. Atribua os pontos de atualização de software a um grupo de limites para que os clientes possam localizar e utilizá-los.

### <a name="fallback-for-software-update-points"></a>Contingência para pontos de atualização de software
Contingência para pontos de atualização de software está configurada como outras funções de sistema de sites, mas tem os seguintes avisos:
- **Novos clientes utilizam grupos de limites para selecionar pontos de atualização de software.** Depois de instalar a versão 1702, os clientes novos que instalar selecionam um ponto de atualização de software encontram associadas os grupos de limites que configurou. Esta ação substitui o anterior comportamento onde os clientes selecionam um ponto de atualização de software aleatoriamente uma lista dos partilhar na floresta do cliente.

- **Os clientes continuam a utilizar um ponto de atualização de software boa último conhecido até que a contingência para localizar um novo.** Clientes que já tenham um ponto de atualização de software continuam a utilizar esse ponto de atualização de software até que o servidor não é possível aceder.  Isto inclui a utilização contínua de um ponto de atualização de software que não está associada ao grupo de limites atual do cliente.

  A utilização contínua de um ponto de atualização de software existente, mesmo quando nesse servidor não está no grupo de limites atual do cliente é intencional. Isto acontece porque uma alteração de ponto de atualização de software pode resultar numa grande utilização de largura de banda de rede, como o cliente sincroniza os dados com o novo ponto de atualização de software. O atraso em transição pode ajudar a evitar saturating a sua rede, se todos os seus clientes mudarem para um novo software de um ponto de atualização em simultâneo.

- **Um cliente tenta sempre alcançar o último ponto de atualização de software boa conhecida para 120 minutos antes de começar contingência.** Depois de 120 minutos, se o cliente não tenha estabelecido contacte, em seguida, começa contingência. Quando inicia a reversão, o cliente recebe uma lista de todos os pontos de atualização de software do respetivo grupo de limites atuais. Pontos de atualização de software adicionais de grupos de limites de vizinho e grupo de limites do site predefinido estão disponíveis com base nas configurações de contingência.

### <a name="fallback-configurations-for-software-update-points"></a>Configurações de contingência para pontos de atualização de software
#### <a name="beginning-with-version-1706"></a>A partir da versão 1706   
Pode configurar **contingência exceder o tempo (em minutos)** para atualização de software pontos para ser inferior a 120 minutos. No entanto, o cliente tem continuam a tentar contactar o respetivo ponto de atualização de software original para 120 minutos antes que expande-pesquisa para servidores adicionais. Porque os tempos de contingência de grupo de limites iniciar quando o cliente primeiro não consegue contactar o respetivo servidor original, quaisquer grupos de limites que estão configurados para menos de 120 minutos são fornecidos para o cliente, quando expandir a pesquisa depois de conseguir contactar o respetivo servidor original para 120 minutos.

Pode configurar **nunca contingência** para o bloco de contingência para o software de um ponto de atualização para um grupo de limites de vizinho.

Depois de conseguir contactar o respetivo servidor original de duas horas, o cliente utiliza um ciclo mais curto para estabelecer uma ligação para um novo ponto de atualização de software. Isto permite ao cliente procurar rapidamente a lista de expansão de potenciais pontos de atualização de software.

 -  **Exemplo de contingência:**  
    Grupo de limites atuais de um cliente tem de contingência para pontos de atualização de software que está configurado como *10* minutos para o grupo de limites *A*, e *130* minutos para o grupo de limites *B*. Quando o cliente não conseguir alcançar o último ponto de atualização de software boas:
    -   O cliente tenta aceder apenas o servidor original para os seguintes 120 minutos.  Após 10 minutos, o software de pontos de atualização do grupo de limites A são adicionados ao agrupamento de servidores disponíveis. No entanto, o cliente não é possível tentar contactá-los ou qualquer outro servidor, enquanto tiver decorrido o período inicial de 120 minutos para restabelecer a ligação com o servidor original.
    -   Após a tentar localizar esse ponto de atualização de software original para 120 minutos, o cliente, em seguida, pode expandir a pesquisa. Nessa altura, foram adicionados servidores no grupo de limites atual do cliente e quaisquer grupos de limites de vizinho que estão configuradas para 120 minutos ou menos, para o conjunto de pontos de atualização de software disponível. Isto inclui os servidores do grupo de limites A que tenham sido previamente adicionados ao agrupamento de servidores disponíveis.
    -       Depois de 10 minutos (130 minutos tempo total após o cliente primeiro não conseguiu contactar o último ponto de atualização de software boas), o cliente expande a pesquisa para incluir os pontos de atualização de software do grupo de limites B.  

#### <a name="prior-to-version-1706"></a>Antes de versão 1706
Antes de versão 1706, configurações de contingência para pontos de atualização de software não suportam um período de tempo configurável em minutos. Em vez disso, o comportamento de contingência está limitado a:

  - **Tempos de contingência (em minutos):**  Esta opção está desativada para pontos de atualização de software e não pode ser configurada. Está definido para 120 minutos.
  -     **Nunca contingência:** Pode bloquear a contingência para um ponto de atualização de software a um grupo de limites de vizinho quando utiliza esta configuração.

Quando um cliente que já tem um ponto de atualização de software não consegue contactar, o cliente pode contingência, em seguida, para localizar outro. Quando utiliza a contingência, o cliente recebe uma lista de todos os pontos de atualização de software do respetivo grupo de limites atuais. Se não conseguir encontrar um servidor disponível para 120 minutos, irá, em seguida, contingência respetivos grupos de limites de vizinho e o grupo de limites de site predefinido. Acontece contingência para ambos os grupos de limites ao mesmo tempo, porque o software de atualizar os pontos de tempo de contingência para grupos de elementos vizinhos está definido para 120 minutos e não pode ser alterado. 120 minutos também é o período predefinido utilizado para contingência para o grupo de limites de site predefinido. Quando um cliente retrocede para ambos os um vizinho e grupo de limites de site predefinido, o cliente tenta contactar os pontos de atualização de software do grupo de limites de vizinho antes de tentar utilizar um grupo de limites de site predefinido.

### <a name="manually-switch-to-a-new-software-update-point"></a>Mudar manualmente para um novo ponto de atualização de software
Além da utilização de contingência, pode utilizar *notificação do cliente* para forçar manualmente um dispositivo para mudar para um novo ponto de atualização de software.

Quando mudar para um novo servidor, os dispositivos utilizam contingência localizar esse servidor novo. Por conseguinte, reveja as configurações do grupo de limites e certifique-se de que os seus pontos de atualização de software estão nos grupos de limites correto antes de começar esta alteração.

Para obter mais informações, consulte [mudar manualmente os clientes para um novo ponto de atualização de software](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).


## <a name="preferred-management-points"></a>Pontos de gestão preferenciais

 Os pontos de gestão preferenciais permitem a um cliente identificar um ponto de gestão que esteja associado à sua localização de rede atual (limite).  

-   Um cliente tenta utilizar um ponto de gestão preferidos do respetivo site atribuído antes de utilizar um ponto de gestão do respetivo site atribuído que não está configurado como preferencial.  
-   Para utilizar esta opção, tem de ativá-la para a hierarquia e, em seguida, configurar grupos de limites em sites primários individuais para incluir os pontos de gestão que devem ser associados aos limites associados do grupo de limites.  
-   Quando os pontos de gestão preferenciais são configurados e um cliente organiza a respetiva lista de pontos de gestão, o cliente coloca os pontos de gestão preferenciais no topo da lista de pontos de gestão atribuídos (que inclui todos os pontos de gestão do site atribuído do cliente).  

> [!NOTE]  
>  Quando um cliente fizer roaming (o que significa alterar as respetivas localizações de rede, tais como quando um computador portátil circula para uma localização de escritório remoto), poderá utilizar um ponto de gestão (ou ponto de gestão do proxy) a partir do site local na nova localização antes de tentar utilizar um ponto de gestão a partir do respetivo site atribuído (que inclui os pontos de gestão preferenciais).  Consulte [compreender a forma como os clientes localizam os recursos de site e os serviços do System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para obter mais informações.  

### <a name="overlapping-boundaries"></a>Sobreposição de limites  
 O Configuration Manager suporta configurações de limites sobrepostos para localização de conteúdo:  

-   **Quando um cliente solicita conteúdo**e a localização de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que possuem o conteúdo.  
-   **Quando um cliente solicita a um servidor para enviar ou receber as informações de migração de estado**e a localização de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado que estão associados um grupo de limites que inclui a localização de rede atual do cliente.  

Este comportamento permite que o cliente selecione o servidor mais próximo para transferir o conteúdo ou as informações de migração de estado.  



## <a name="example-of-using-boundary-groups"></a>Exemplo de como utilizar grupos de limites
O exemplo seguinte utiliza um cliente procurar conteúdo a partir de um ponto de distribuição. Este exemplo pode ser aplicado a outras funções de sistema de sites que utilizam grupos de limites. No entanto, como se aplica aos pontos de atualização de software, tenha em atenção que os pontos de atualização de software não suporta a configuração de um período de tempo em minutos para contingência para um grupo de vizinho e utilize sempre um período de 120 minutos.

Crie três grupos de limites que não partilham limites ou servidores de sistema de sites:
-   Grupo BG_A com pontos de distribuição DP_A1 e DP_A2 associados ao grupo
-   Grupo BG_B com pontos de distribuição DP_B1 e DP_B2 associados ao grupo
-   Grupo BG_C com pontos de distribuição DP_C1 e DP_C2 associados ao grupo

A adicionar as localizações de rede dos clientes como limites para apenas o grupo de limites BG_A e, em seguida, configurar relações desse grupo de limites para os outros dois grupos de limites:
-   Configurar pontos de distribuição para o primeiro *vizinho* grupo (BG_B) a ser utilizada após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos são boas ligações para as localizações de limites de grupos primeiro.
-   Configurar a segunda *vizinho* grupo (BG_C) a ser utilizada após 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos são através de uma WAN dos outros grupos de limites de dois.
-   Pode também adiciona um ponto de distribuição adicionais que está localizado no servidor do site ao grupo de limites de site de sites predefinido. Esta é a localização de origem de conteúdo menos preferencial, mas está centralmente localizado para todos os grupos de limites.

    Exemplo de grupos de limites e tempos de contingência:

     ![BG_Fallack](media/BG_Fallback.png)


Com esta configuração:
-   O cliente começa a procurar conteúdo dos pontos de distribuição no respetivo *atual* pesquisar a distribuição de cada grupo de limites (BG_A), para que aponte do dois minutos antes de mudar para o próximo ponto de distribuição no grupo de limites. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1 e DP_A2.
-   Se o cliente não conseguir localizar o conteúdo do respetivo *atual* grupo de limites depois de procurar durante 10 minutos, em seguida, adiciona os pontos de distribuição do grupo de limites BG_B para a sua pesquisa. Em seguida, continua a pesquisar conteúdo a partir de um ponto de distribuição no respetivo conjunto combinado de pontos de distribuição que inclui os grupos de limites BG_A tanto BG_B agora. O cliente continua a contactar cada ponto de distribuição de dois minutos antes de mudar para o próximo ponto de distribuição do seu conjunto. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1, DP_A2, DP_B1 e DP_B2.
-   Após um adicionais de 10 minutos (totais de 20 minutos) se o cliente ainda não encontrou um ponto de distribuição com conteúdo, que expande o conjunto de pontos de distribuição disponíveis para incluir as da segunda *vizinho* grupo, o grupo de limites BG_C. O cliente agora tem 6 pontos de distribuição para pesquisa (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua a alteração cada dois minutos até ser encontrado conteúdo para um novo ponto de distribuição.
-   Se o cliente não foi encontrado conteúdo depois de um total de 120 minutos, fica novamente para incluir o *grupo de limites de site predefinido* como parte da sua pesquisa contínua. O conjunto de pontos de distribuição inclui agora todos os pontos de distribuição dos três grupos de limites configurado e o ponto de distribuição final localizado no computador do servidor do site.  O cliente, em seguida, continua a pesquisa de conteúdo, alterar a cada dois minutos até ser encontrado conteúdo de pontos de distribuição.

Ao configurar os grupos de vizinho diferentes para estar disponível em alturas diferentes, pode controlar quando são adicionados como uma localização de origem de conteúdo, pontos de distribuição específico e quando, ou se, o cliente utiliza a contingência para o grupo de limites de site predefinido como uma rede de segurança para o conteúdo que não está disponível a partir de qualquer outra localização.






### <a name="update-existing-boundary-groups-to-the-new-model"></a>Atualizar os grupos de limites existentes para o novo modelo
Quando atualizar para versão antes de 1610, as seguintes configurações são efetuadas automaticamente. Estes são concebidas para Certifique-se de que o comportamento de contingência atual permanece disponível até configurar novos grupos de limites e relações.

-   É criado um grupo de limites de site predefinido para cada site primário, o nome é ***predefinição-Site-limite-grupo&lt;sitecode >.***
  - Pontos de distribuição com *permitir a localização de origem de contingência para conteúdo* marcada e pontos de migração de estado em sites primários são adicionados para o *grupo-de-Site-limites-predefinição&lt;sitecode >* grupo de limites desse site.
  - A partir da versão 1702, pontos de atualização de software são adicionados para cada sites *predefinição-Site-limite-grupo&lt;sitecode >*.
-   É efetuada uma cópia de cada grupo de limites existentes, que inclui um servidor de site configurado com uma ligação lenta. O nome do novo grupo é *** &lt;nome original do grupo de limites >-&lt;ID do grupo de limites original >***:  
    -   Sistemas de sites que tenham uma ligação rápida são mantidos no grupo de limites original.
    -   Uma cópia dos sistemas de sites (pontos de distribuição, pontos de gestão) que tenham uma ligação lenta são adicionadas para a cópia do grupo de limites. Os sistemas de site original configurados como lenta permanecem no respetivos original grupos de limites para compatibilidade com versões anteriores, mas não são utilizados a partir desses grupos de limites.
    - Esta cópia do grupo de limites não tem limites associados à mesma. No entanto, é criada uma ligação de contingência entre o grupo original e a nova cópia do grupo de limites com o tempo de contingência definido como zero.  


- **Sites específicos para secundário:**
  - É criado um grupo de limites, se um site secundário tem, pelo menos, um ponto com de distribuição *permitir a localização de origem de contingência para conteúdo* ponto de migração de estado ou marcada. O nome do grupo de limites é ***secundária-Site-vizinho – Tmp&lt;Sitecode >.***
  - Pontos de distribuição de todos os com *permitir a localização de origem de contingência para conteúdo* marcado e os pontos de migração de estado são adicionados a este grupo de limites de site secundário recentemente criado.
  - É criada uma ligação de contingência entre o grupo de limites original e o grupo de limites de vizinho recentemente criado e a hora de contingência está definida para zero.


 A tabela seguinte identifica o novo comportamento contingência pode esperar da combinação de definições de implementação original e a distribuição de configurações de pontos:

Configuração de implementação original "não executaram" na rede lenta  |Configuração para "Permitir ao utilizar uma localização de origem de contingência para conteúdo de cliente" do ponto de distribuição original  |Novo comportamento de contingência  
---------|---------|---------
Selecionado     |  Selecionado    |  **Não existem contingência** -utilizar apenas os pontos de distribuição no grupo de limites atual       
Selecionado     |  Não selecionada|  **Não existem contingência** -utilizar apenas os pontos de distribuição no grupo de limites atual       
Não selecionada |  Não selecionada|  **Contingência para vizinho** - utilizar os pontos de distribuição no grupo de limites atual e, em seguida, adicione os pontos de distribuição do grupo de limites de vizinho. A menos que uma ligação explícita para o grupo de limites de site predefinido está configurada, os clientes irão não contingência a esse grupo.    
Não selecionada | Selecionado     |   **Contingência normal** -utilizar pontos de distribuição no grupo de limites atual, em seguida, os do site e vizinho predefinido de grupos de limites

 Todas as outras configurações de implementação resultam em **contingência Normal**.  




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Alterações de versões anteriores para a IU e o comportamento para localizações de conteúdo
Seguem-se as alterações principais grupos de limites e a forma como os clientes localizam os conteúdos. Estas alterações são introduzidas com a versão 1610. Muitas destas alterações e conceitos funcionam em conjunto.


-   **Configurações para rápida ou lenta são removidas:** Já não está a configurar pontos de distribuição individuais para serem rápida ou lenta.  Em vez disso, cada sistema de sites associado a um grupo de limites é Tratado da mesma. Devido a esta alteração, o **referências** separador das propriedades do grupo de limites já não suporta a configuração rápida ou lenta.
-   **Novo grupo de limites de predefinição em cada site:**  Cada site primário tem um novo grupo de limites de predefinição com o nome ***predefinição-Site-limite-grupo&lt;sitecode >***.  Quando um cliente não está numa localização de rede que está atribuída a um grupo de limites, esse cliente utilizará os sistemas de sites associados ao grupo predefinido do seu site atribuído. Planear a utilização deste grupo de limites como uma substituição para o conceito de localização de conteúdo de contingência.      
 -  **'Permitir que as localizações de origem de contingência para conteúdo'** for removido: Já não está explicitamente a configurar um ponto de distribuição para ser utilizado para contingência e as opções para configurar esta são removidas da IU.

    Além disso, o resultado da definição **permitir que os clientes utilizem uma localização de origem de contingência para conteúdo** numa implementação tipo para aplicações foi alterada. Esta definição num tipo de implementação agora permite que um cliente para utilizar o grupo de limites de site predefinido como uma localização de origem de conteúdo.

 -  **Relações de grupos de limites:** Cada grupo de limites pode ser associado a um ou mais grupos de limites adicionais. Estas ligações formam relações que estão configuradas no novo limite grupo separador de propriedades com o nome **relações**:
    -   Cada grupo de limites que um cliente é diretamente associado é chamado um **atual** grupo de limites.  
    -   Nenhum grupo de limites pode utilizar um cliente devido a uma associação entre esse cliente *atual* grupo de limites e outro grupo é chamado um **vizinho** grupo de limites.
    -  É o **relações** separador adicionar grupos de limites que podem ser utilizados como um *vizinho* grupo de limites. Também pode configurar um período de tempo em minutos que determina quando um cliente que não consegue localizar o conteúdo a partir de um ponto de distribuição no *atual* grupo irá começar a procurar nas localizações de conteúdo das *vizinho* grupos de limites.

        Quando adicionar ou alterar uma configuração do grupo de limites, terá a opção para o bloco de contingência para esse grupo de limites específico do grupo atual que estiver a configurar.

    Para utilizar a nova configuração, pode define associações explícitas (ligações) a partir de um grupo de limites para outro e configura todos os pontos de distribuição nesse grupo associados com o mesmo tempo em minutos. O tempo que configura determina quando um cliente que não consegue encontrar uma origem de conteúdo do respetivo *atual* grupo de limites pode começar a pesquisar origens de conteúdo desse grupo de limites de vizinho.

    Além dos grupos de limites que configurar explicitamente, cada grupo de limites tem uma ligação implícita para o grupo de limites de site predefinido. Esta ligação fica ativa depois de 120 minutos em que momento o grupo de limites de site predefinido torna-se um grupo de limites de vizinho que permite que os clientes utilizar os pontos de distribuição associados esse grupo de limites como localizações de origem de conteúdo.

    Este comportamento substitui que anteriormente foi referido como contingência para conteúdo.  Pode substituir este comportamento predefinido de 120 minutos associando explicitamente o grupo de limites de site predefinido para um *atual* grupo e definir uma hora específica em minutos ou bloquear contingência inteiramente para impedir a sua utilização.


-   **Os clientes tentam obter conteúdos de cada ponto de distribuição para 2 minutos:** Quando um cliente procura de uma localização de origem de conteúdo, este tenta aceder a cada ponto de distribuição para 2 minutos antes de, em seguida, tentar outro ponto de distribuição. Esta é uma alteração de versões anteriores onde os clientes tentaram ligar a um ponto de distribuição de até 2 horas.

    - O primeiro ponto de distribuição que um cliente tenta utilizar aleatoriamente está selecionado do agrupamento de pontos de distribuição disponíveis do cliente *atual* grupo de limites (ou grupos).

    - Depois de dois minutos, se o cliente não foi encontrado o conteúdo, muda para um novo ponto de distribuição e tenta obter conteúdo a partir desse servidor. Este processo repete-se a cada dois minutos até que o cliente localiza o conteúdo ou atinge o último servidor no seu conjunto.

    - Se um cliente não é possível encontrar uma localização de origem de conteúdo válida a partir do respetivo *atual* agrupamento antes do período de contingência para um *vizinho* for atingido o grupo de limites, o cliente, em seguida, adiciona os pontos de distribuição do *vizinho* até ao fim da respetiva lista atual de grupo e, em seguida, irá procurar o grupo expandido das localizações de origem que inclua os pontos de distribuição a partir de ambos os grupos de limites.

        > [!TIP]  
        > Quando criar uma ligação explícita do grupo de limites atuais para o grupo de limites de site predefinido e definir uma hora de contingência que é inferior à hora de contingência para uma ligação a um grupo de limites de vizinho, os clientes começam a pesquisar localizações de origem do grupo de limites de site predefinido antes, incluindo o grupo de vizinho.

    - Quando o cliente não consegue obter conteúdos do último servidor no agrupamento, começar o processo de novo.


## <a name="procedures-for-boundary-groups"></a>Procedimentos para grupos de limites
Os procedimentos seguintes aplicam-se à versão 1610 ou posterior. Se utilizar a versão antes de 1610, consulte os procedimentos [grupos de limites para as versões do System Center Configuration Manager versão 1511, 1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


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

 6.  Selecione o **relações** separador para configurar o comportamento de contingência:  

     - Clique em **adicionar**e, em seguida, selecione o grupo de limites que pretende configurar.

     - Defina uma hora para pontos de distribuição de contingência. Após este período de tempo, os clientes num grupo de limites que está a configurar relações, será possível iniciar a pesquisa de conteúdo dos pontos de distribuição do grupo de limites que está a adicionar.

     - Para impedir a contingência para um grupo de limites específico, incluindo o *grupo de limites de site predefinido* que está configurado por predefinição, selecione o grupo de limites e, em seguida, selecione a caixa para **nunca contingência**.   

 7.  Clique em **OK** para fechar as propriedades do grupo de limites e guardar a configuração.  

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>Para associar um servidor de sistema de sites um grupo de limites  
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

 1.  Na consola do Configuration Manager, clique em **administração** > **configuração do Site** > **Sites**e, em seguida, no **home page** separador selecione **definições de hierarquia**.  

 2.  No separador **Geral** das Definições de Hierarquia, selecione **Os clientes preferem utilizar pontos de gestão especificados em grupos de limites**.  

 3.  Clique em **OK** para fechar a caixa de diálogo e guardar a configuração.  

