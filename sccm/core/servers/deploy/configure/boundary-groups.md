---
title: Configurar grupos de limites
titleSuffix: Configuration Manager
description: Ajudar os clientes a localizar os sistemas de sites através de grupos de limites para organizar logicamente as localizações de rede relacionadas chamadas limites
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 297f4a5ecb7650a4ea643fff00dd67b6580256de
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurar grupos de limites para o System Center Configuration Manager


*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizar grupos de limites no Configuration Manager para organizar logicamente as localizações de rede relacionadas ([limites](/sccm/core/servers/deploy/configure/boundaries)) torna mais fácil de gerir a sua infraestrutura. Atribua os limites a grupos de limites antes de utilizar o grupo de limites.

Por predefinição, o Configuration Manager cria um grupo de limites de site predefinido em cada site.

Para configurar grupos de limites, associar limites (localizações de rede) e funções de sistema de sites, como pontos de distribuição, para o grupo de limites. Esta configuração ajuda a associar clientes para servidores do sistema de sites como perto de pontos de distribuição que estão localizados os clientes na rede.

Para aumentar a disponibilidade dos sistemas de sites servidores, como pontos de distribuição, para uma vasta gama de localizações de rede, atribuir o mesmo limite e o mesmo servidor a vários grupos de limites.

Os clientes utilizam um grupo de limites para:  

-   Atribuição automática de site  
-   Para localizar um servidor de sistema de sites que pode fornecer um serviço, incluindo:
    - Pontos de distribuição para localização de conteúdo
    -   Pontos de atualização de software
    - Pontos de migração de estado
    - Pontos de gestão preferenciais (se utilizar pontos de gestão preferidos, tem de ativar esta opção para a hierarquia e não a partir da configuração do grupo de limites. Consulte [para ativar a utilização de pontos de gestão preferenciais](#to-enable-use-of-preferred-management-points) neste tópico.)

##  <a name="boundary-groups-and-relationships"></a>Grupos de limites e relações
Para cada grupo de limites na hierarquia, pode atribuir:

-  Um ou mais limites. Um cliente **atual** grupo de limites for uma localização de rede que está definida como um limite atribuído a um grupo de limites específico. Um cliente pode ter mais do que um grupo de limites atuais.
- Uma ou mais funções de sistema de sites. Os clientes podem sempre utilizar funções de sistema de sites associadas com o respetivo grupo de limites atuais. Dependendo das configurações adicionais, poderá seria capazes de utilizar as funções do sistema de sites em grupos de limites adicionais.  

Para cada grupo de limites que cria, pode configurar uma ligação unidirecional para outro grupo de limites. A ligação é chamada um **relação**. Os grupos de limites a associar ao são denominados **vizinho** grupos de limites. Um grupo de limites pode ter várias relações, cada um com um grupo de limites de vizinho específico.

Quando um cliente não consegue localizar um servidor de sistema de sites disponíveis no seu grupo de limites atual, a configuração de cada relação determina quando começa a um grupo de limites de vizinho de pesquisa. Esta pesquisa de grupos adicionais denomina **contingência**.

## <a name="fallback"></a>Contingência
Para evitar problemas quando os clientes não é possível localizar um sistema de sites disponíveis no respetivo grupo de limites atual, defina a relação entre grupos de limites para o comportamento de contingência. Contingência permite que um cliente expandir a sua pesquisa para grupos de limites adicionais para localizar um sistema de sites disponíveis.

As relações estão configuradas em Propriedades do grupo de limites **relações** separador. Quando configurar uma relação, é possível definir uma ligação a um grupo de limites de vizinho. Para cada tipo de função do sistema de sites suportados, configure definições independentes de contingência para o grupo de limites de vizinho. Por exemplo, quando configurar uma relação a um grupo de limites específico, defina contingência para pontos de distribuição para ocorrer após 20 minutos, em vez da predefinição de 120. Para obter um exemplo mais extenso, consulte [exemplo de como utilizar grupos de limites](#example-of-using-boundary-groups).

Se um cliente não conseguir localizar uma função de sistema de sites disponíveis no seu grupo de limites atual, o cliente utiliza o contingência tempo em minutos. Neste momento contingência determina quando o cliente começa para procurar um sistema de sites disponíveis associado ao grupo de limites de vizinho.  

Quando um cliente não é possível localizar um sistema de sites disponíveis e começa a procurar nas localizações dos grupos de limites de vizinho, aumenta o conjunto de sistemas de sites disponíveis. A configuração de grupos de limites e relações define a utilização do cliente deste conjunto de sistemas de sites disponíveis.

- Um grupo de limites pode ter mais de uma relação. Com várias relações, pode configurar a contingência para cada tipo de sistema de sites para diferentes vizinhos para ocorrer após os períodos de tempo diferentes.    
- Clientes só contingência para um grupo de limites que é um vizinho direto do respetivo grupo de limites atuais.
- Quando um cliente é um membro de vários grupos de limites, o grupo de limites atual está definido como uma União do cliente grupos de limites. O cliente retrocede para vizinhos de qualquer um desses grupos de limites original.

### <a name="the-default-site-boundary-group"></a>O grupo de limites de site predefinido
Para além dos grupos de limites que cria, cada site tem um grupo de limites de site predefinido que é criado pelo Configuration Manager. Este grupo é designado ***predefinição-Site-limite-grupo&lt;sitecode >***. Por exemplo, o grupo para o site ABC seria possível designado *predefinição-Site-limite-grupo&lt;ABC >.*

Para cada grupo de limites que cria, o Configuration Manager cria automaticamente uma ligação implícita para cada grupo de limites de site predefinido na hierarquia.
-   A hiperligação implícita é uma opção de contingência de predefinido de um grupo de limites atuais ao grupo de limites de sites predefinido, que tem um tempo de contingência da predefinição de 120 minutos.
-   Para clientes não num limite associado a nenhum grupo de limites: para identificar funções do sistema de site válido, utilize o grupo de limites de site predefinido do seu site atribuído.

Para gerir a contingência para o grupo de limites de site predefinido:
- Abra as propriedades do grupo de limites do site predefinido e alterar os valores no **comportamento predefinido** separador. Alterações efetuadas aqui aplicam-se a *todos os* implícito ligações a este grupo de limites. Estas definições podem ser substituídas quando configurar a ligação explícita para este grupo de limites de site predefinido do outro grupo de limites.
- Abra as propriedades de um grupo de limites personalizado. Altere os valores para a ligação explícita para um grupo de limites de site predefinido. Quando definir um novo período de tempo em minutos para contingência ou bloco de contingência, essa alteração afeta apenas a ligação que está a configurar. Configuração da ligação explícita substitui as definições no **comportamento predefinido** separador de um grupo de limites de site predefinido.


## <a name="site-assignment"></a>Atribuição de site  
 É possível configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recentemente instalado que utilize a atribuição automática de site é associado ao site atribuído de um grupo de limites que contém a localização de rede atual do cliente.  
-   Depois da atribuição a um site, um cliente não altera a sua atribuição de site ao alterar a respetiva localização de rede. Por exemplo, se o cliente fizer roaming para uma nova localização de rede representada por um limite num grupo de limites com uma atribuição de site diferente, não altere permanece de site atribuído do cliente.  
-   Quando a Deteção de Sistemas do Active Directory deteta um novo recurso, as informações de rede do recurso detetado são comparadas com os limites dos grupos de limites. Este processo associa o novo recurso a um site atribuído que será utilizado pelo método de instalação push do cliente.  
-   Quando um limite é um membro de vários grupos de limites que possuem diferentes sites atribuídos, os clientes aleatoriamente selecionam um dos sites.  
-   As alterações efetuadas a um site atribuído de um grupo de limites apenas são aplicáveis a novas ações de atribuição de site. Os clientes atribuídos anteriormente a um site não reevaluate a atribuição do site com base nas alterações à configuração de um grupo de limites (ou para sua própria localização de rede).  

Para obter mais informações sobre a atribuição de sites do cliente, consulte [utilizando a atribuição de Site automática para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) no [como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Pontos de distribuição

Quando um cliente solicita a localização de um ponto de distribuição, o Configuration Manager envia ao cliente uma lista dos sistemas de sites. Estes sistemas de sites são do tipo adequado associado a cada grupo de limites que inclui a localização de rede atual:

-   **Durante a distribuição de software**, os clientes solicitam uma localização para o conteúdo de implementação que está disponível a partir de um ponto de distribuição ou outra origem de conteúdo válida (por exemplo, um cliente configurado para a Cache ponto a ponto).

-   **Durante a implementação do sistema operativo**, os clientes solicitam uma localização para enviar ou receber as respetivas informações de migração de estado.  

Durante a implementação de conteúdos, se um cliente solicita conteúdo que não está disponível de uma origem no seu grupo de limites atual, o cliente continua a pedir esse conteúdo. O cliente tenta diferentes origens de conteúdo no seu grupo de limites atuais até atingir o período de contingência para um grupo de limites de vizinho ou o grupo de limites de site predefinido. Se o cliente ainda não encontrar o conteúdo, em seguida, expandir a pesquisa de origens de conteúdo incluir os grupos de limites de vizinho.

Se o conteúdo é distribuído a pedido e não está disponível num ponto de distribuição quando solicitado por um cliente, iniciar o processo para transferir o conteúdo para esse ponto de distribuição. É possível que o cliente localiza nesse servidor como uma origem de conteúdo antes de reverter para utilizar um grupo de limites de vizinho.

## <a name="software-update-points"></a>Pontos de atualização de software
Os clientes utilizam grupos de limites para localizar um novo ponto de atualização de software. Para controlar quais os servidores de um cliente pode localizar, adicione pontos de atualização de individual software para diferentes grupos de limites.

Se atualizar a partir de uma versão antes de 1702, cada site adiciona todos os pontos de atualização de software existente para o grupo de limites de site predefinido. Este comportamento da atualização de site mantém o comportamento do cliente anterior para selecionar um ponto de atualização de software do agrupamento de servidores disponíveis. Este comportamento é mantido até optar por adicionar pontos de atualização de individual software para diferentes grupos de limites para seleção controlada e o comportamento de contingência.

Se instalar um novo site, os pontos de atualização de software não foram adicionados ao grupo de limites de site predefinido. Atribua os pontos de atualização de software a um grupo de limites para que os clientes possam localizar e utilizá-los.

### <a name="fallback-for-software-update-points"></a>Contingência para pontos de atualização de software
Contingência para pontos de atualização de software está configurada como outras funções de sistema de sites, mas tem os seguintes avisos:
- **Novos clientes utilizam grupos de limites para selecionar pontos de atualização de software.** Os clientes novos que instalar selecionam um ponto de atualização de software nesses servidores associados os grupos de limites que configura. Este comportamento substitui o anterior comportamento onde os clientes selecionam um ponto de atualização de software aleatoriamente entre uma lista de servidores que partilham na floresta do cliente.

- **Os clientes continuam a utilizar um ponto de atualização de software boa último conhecido até que a contingência para localizar um novo.** Clientes que já tenham um ponto de atualização de software continuam a utilizá-lo até que este não é possível aceder. Este comportamento inclui contínua de utilização de um ponto de atualização de software que não está associada ao grupo de limites atual do cliente.

  A utilização contínua de um ponto de atualização de software existente, mesmo quando nesse servidor não está no grupo de limites atual do cliente é intencional. Quando as alterações de ponto de atualização de software, o cliente sincroniza os dados com o novo servidor, o que faz com que a utilização de rede significativo. Se todos os clientes para um novo servidor ao mesmo tempo, o atraso em transição ajuda a evitar saturating a sua rede.

- **Um cliente tenta sempre alcançar o último ponto de atualização de software boa conhecida para 120 minutos antes de começar contingência.** Depois de 120 minutos, se o cliente não tenha estabelecido contacte, em seguida, começa contingência. Quando inicia a reversão, o cliente recebe uma lista de todos os pontos de atualização de software do respetivo grupo de limites atuais. Pontos de vizinho e site limites de predefinição estão disponíveis grupos com base nas configurações de contingência de atualização de software adicional.

### <a name="fallback-configurations-for-software-update-points"></a>Configurações de contingência para pontos de atualização de software
#### <a name="beginning-with-version-1706"></a>A partir da versão 1706   
Pode configurar **contingência exceder o tempo (em minutos)** para atualização de software pontos para ser inferior a 120 minutos. No entanto, o cliente continua a tentar contactar o respetivo ponto de atualização de software original para 120 minutos. Em seguida, expande a pesquisa para servidores adicionais. Horas de contingência de grupo de limites iniciar quando o cliente primeiro não consegue contactar o respetivo servidor original. Quando o cliente expande a pesquisa, o site fornece quaisquer grupos de limites configurados para menos de 120 minutos.

Para bloquear a contingência para um ponto de atualização de software a um grupo de limites de vizinho, configurar a definição para **nunca contingência**.

Depois de conseguir contactar o respetivo servidor original de duas horas, o cliente utiliza um ciclo mais curto para estabelecer uma ligação para um novo ponto de atualização de software. Este comportamento permite que o cliente rapidamente procurar a lista de expansão de potenciais pontos de atualização de software.

 -  **Exemplo de contingência:**  
    Grupo de limites atuais de um cliente tem de contingência para pontos de atualização de software que está configurado como *10* minutos para o grupo de limites *A*, e *130* minutos para o grupo de limites *B*. Quando o cliente não conseguir alcançar o último ponto de atualização de software boas:
    -   O cliente tenta aceder apenas o servidor original para os seguintes 120 minutos. Após 10 minutos, o software de pontos de atualização do grupo de limites A são adicionados ao agrupamento de servidores disponíveis. No entanto, o cliente não é possível tentar contactá-los ou qualquer outro servidor, enquanto tiver decorrido o período inicial de 120 minutos para restabelecer a ligação com o servidor original.
    -   Após a tentar localizar esse ponto de atualização de software original para 120 minutos, o cliente, em seguida, pode expandir a pesquisa. Nessa altura, o cliente adiciona servidores para o conjunto de pontos de atualização de software que estão no mesmo disponível do atual e quaisquer grupos de limites de vizinho configurado para 120 minutos ou menos. Este agrupamento inclui os servidores do grupo de limites A que tenham sido previamente adicionados ao agrupamento de servidores disponíveis.
    -       Depois de 10 minutos (130 minutos tempo total após o cliente primeiro não conseguiu contactar o último ponto de atualização de software boas), o cliente expande a pesquisa para incluir os pontos de atualização de software do grupo de limites B.  

#### <a name="prior-to-version-1706"></a>Antes de versão 1706
Antes de versão 1706, configurações de contingência para pontos de atualização de software não suportam um período de tempo configurável em minutos. Em vez disso, o comportamento de contingência está limitado a:

  - **Tempos de contingência (em minutos):** Esta opção está desativada para pontos de atualização de software e não pode ser configurada. Está definido para 120 minutos.
  -     **Nunca contingência:** Pode bloquear a contingência para um ponto de atualização de software a um grupo de limites de vizinho quando utiliza esta configuração.

Quando um cliente que já tem um ponto de atualização de software não consegue contactar, o cliente, em seguida, retrocede para localizar outro. Quando utiliza a contingência, o cliente recebe uma lista de todos os pontos de atualização de software do respetivo grupo de limites atuais. Se não conseguir encontrar um servidor disponível para 120 minutos,-lo, em seguida, retrocede para os grupos de limites de vizinho e o grupo de limites de site predefinido. Ocorre a contingência para ambos os grupos de limites ao mesmo tempo. Tempo de contingência do ponto de atualização de software para os grupos de elementos vizinhos está definido para 120 minutos. Não é possível alterar este período de tempo de contingência. 120 minutos também é o período predefinido utilizado para contingência para o grupo de limites de site predefinido. Quando um cliente retrocede para ambos os um vizinho e grupo de limites de site predefinido, o cliente tenta contactar os pontos de atualização de software do grupo de limites de vizinho antes de tentar utilizar um grupo de limites de site predefinido.

### <a name="manually-switch-to-a-new-software-update-point"></a>Mudar manualmente para um novo ponto de atualização de software
Além da utilização de contingência, pode utilizar *notificação do cliente* para forçar manualmente um dispositivo para mudar para um novo ponto de atualização de software.

Quando mudar para um novo servidor, os dispositivos utilizam contingência localizar esse servidor novo. Reveja as configurações do grupo de limites. Certifique-se de que os seus pontos de atualização de software estão nos grupos de limites correto antes de começar esta alteração.

Para obter mais informações, consulte [mudar manualmente os clientes para um novo ponto de atualização de software](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Pontos de gestão
<!-- 1324594 -->
A partir de versão 1802, configure as relações de contingência para pontos de gestão entre grupos de limites. Este comportamento proporciona maior controlo para os pontos de gestão que os clientes utilizam. No **relações** separador das propriedades do grupo de limites, é uma coluna para o ponto de gestão. Quando adiciona um novo grupo de limites de contingência, o tempo de contingência para o ponto de gestão é atualmente sempre zero (0). Este comportamento é o mesmo para o **comportamento predefinido** no grupo de limites de site predefinido.

Anteriormente, um problema comum ocorre quando tiver um protegido ponto de gestão numa rede segura. Os clientes na rede empresarial principal recebem a política que inclui este ponto de gestão protegidos, apesar de não conseguirem comunicar com o mesmo através de uma firewall. Para resolver este problema, utilize o **nunca contingência** opção para garantir que apenas contingência para gestão de clientes aponta com que possam comunicar.

Ao atualizar o site para a versão 1802, o Configuration Manager adiciona todos os pontos de gestão de não-acesso à internet para o grupo de limites do site predefinido. Este comportamento atualização assegura que as versões cliente anteriores continuam a comunicar com pontos de gestão. Para tirar partido desta funcionalidade, mova os pontos de gestão para os grupos de limites pretendido.

Reversão de grupo de limites de ponto de gestão não altera o comportamento durante a instalação de cliente (ccmsetup.exe). Se a linha de comandos não especificar o ponto de gestão inicial com o parâmetro /MP, o novo cliente recebe a lista completa dos pontos de gestão disponíveis. Para o seu processo de arranque de configuração inicial, o cliente utiliza o primeiro ponto de gestão que possa aceder. Depois do cliente regista com o site, este recebe a lista de pontos de gestão ordenada corretamente com este novo comportamento. 

Para os clientes utilizar esta capacidade, ative a definição seguinte: **Os clientes preferem utilizar pontos de gestão especificados em grupos de limites** no **definições de hierarquia**. 

> [!Note]
> Processos de implementação do sistema operativo não têm conhecimento dos grupos de limites.

### <a name="troubleshooting"></a>Resolução de Problemas
Novas entradas são apresentados no **LocationServices.log**. O **Localidade** atributo identifica um dos seguintes Estados:
- 0: Desconhecido
- 1: O ponto de gestão especificado é apenas no grupo de limites de site predefinido para contingência
- 2: O ponto de gestão especificado está num grupo de limites de vizinhança ou remoto. Quando o ponto de gestão está num vizinho e os grupos de limites do site predefinido, a Localidade é 2.
- 3: O ponto de gestão especificado está no grupo de limites local ou atual. Quando o ponto de gestão está no grupo de limites atuais, bem como um vizinho ou o grupo de limites do site predefinido, a Localidade é 3. Se não ativar os pontos de gestão preferenciais definição nas definições de hierarquia, a Localidade é sempre 3, independentemente dos limites do ponto de gestão de grupo está a ser.

Os clientes utilizam pontos de gestão local primeiro (Localidade 3), segundo remoto (Localidade 2) e contingência (Localidade 1). 

Quando um cliente recebe erros de cinco dentro de 10 minutos e não consegue comunicar com um ponto de gestão no respetivo grupo de limites atual, este tenta contactar um ponto de gestão de um vizinho ou o grupo de limites do site predefinido. Se o ponto de gestão atual grupo de limites mais tarde voltar a ficar online, o cliente irá devolver ao ponto de gestão local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando o serviço de agente do Configuration Manager for reiniciado.




## <a name="preferred-management-points"></a>Pontos de gestão preferenciais

 > [!Note]
 > O comportamento desta definição, da hierarquia **os clientes preferem utilizar pontos de gestão especificados em grupos de limites**, as alterações a partir de versão 1802. Quando ativa esta definição, o Configuration Manager utiliza a funcionalidade de grupo de limites para o ponto de gestão atribuído. Para obter mais informações, consulte [pontos de gestão](#management-points). 

 Os pontos de gestão preferenciais permitem a um cliente identificar um ponto de gestão que esteja associado à sua localização de rede atual (limite).  

-   Um cliente tenta utilizar um ponto de gestão preferidos do respetivo site atribuído antes de utilizar um não configurado como preferencial do seu site atribuído.  
-   Para utilizar esta opção, ativar **os clientes preferem utilizar pontos de gestão especificados em grupos de limites** no **definições de hierarquia**. Em seguida, configure grupos de limites em sites primários individuais. Inclua os pontos de gestão que devem ser associados aos limites associados do grupo de limites.
-   Quando configurar pontos de gestão preferenciais e um cliente organiza a respetiva lista de pontos de gestão, o cliente coloca os pontos de gestão preferenciais no topo da lista. Esta lista inclui todos os pontos de gestão do site atribuído do cliente.  

> [!NOTE]  
>  Cliente de roaming significa alterar as localizações de rede. Por exemplo, quando um computador portátil circula para uma localização de escritório remoto. Quando um cliente faz roaming, poderá utilizar um ponto de gestão ou ponto de gestão do proxy de site local na nova localização antes de tentar utilizar um servidor do site atribuído. Esta lista de servidores a partir do respetivo site atribuído inclui os pontos de gestão preferenciais. Para obter mais informações, consulte [compreender a forma como os clientes localizam os recursos de site e os serviços](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Sobreposição de limites  
 O Configuration Manager suporta configurações de limites sobrepostos para localização de conteúdo. Quando a localização de rede do cliente pertence a vários grupos de limites:

-   Quando um cliente solicita conteúdo, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que possuem o conteúdo.  
-   Quando um cliente solicita a um servidor para enviar ou receber as informações de migração de estado, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado associados um grupo de limites que inclui a localização de rede atual do cliente.  

Este comportamento permite que o cliente selecione o servidor mais próximo para transferir o conteúdo ou as informações de migração de estado.  



## <a name="example-of-using-boundary-groups"></a>Exemplo de como utilizar grupos de limites
O exemplo seguinte utiliza um cliente procurar conteúdo a partir de um ponto de distribuição. Este exemplo pode ser aplicado a outras funções de sistema de sites que utilizam grupos de limites. Tenha em atenção que os pontos de atualização de software não suporta a configuração de contingência para um grupo de vizinho e utilize sempre um período de 120 minutos.

Crie três grupos de limites que não partilham limites ou servidores de sistema de sites:
-   Grupo BG_A com pontos de distribuição DP_A1 e DP_A2 associados ao grupo
-   Grupo BG_B com pontos de distribuição DP_B1 e DP_B2 associados ao grupo
-   Grupo BG_C com pontos de distribuição DP_C1 e DP_C2 associados ao grupo

Adicione as localizações de rede dos clientes como limites ao apenas BG_A grupo de limites. Em seguida, configure as relações desse grupo de limites para os outros dois grupos de limites:
-   Configurar pontos de distribuição para o primeiro *vizinho* grupo (BG_B) a ser utilizada após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos são boas ligações para as localizações de limites de grupos primeiro.
-   Configurar a segunda *vizinho* grupo (BG_C) a ser utilizada após 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos são através de uma WAN dos outros grupos de limites de dois.
-   Também adicione ao grupo de limites de site de sites predefinido outro ponto de distribuição que se encontra no servidor do site. Este servidor é a localização de origem de conteúdo menos preferencial, mas está centralmente localizado para todos os grupos de limites.

    Exemplo de grupos de limites e tempos de contingência:

     ![Exemplo de grupos de limites e tempos de contingência](media/BG_Fallback.png)


Com esta configuração:
-   O cliente começa a procurar conteúdo dos pontos de distribuição no respetivo *atual* grupo de limites (BG_A). Procura cada ponto de distribuição de dois minutos e, em seguida, muda para o próximo ponto de distribuição no grupo de limites. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1 e DP_A2.
-   Se o cliente não conseguir localizar o conteúdo do respetivo *atual* grupo de limites depois de procurar durante 10 minutos, em seguida, adiciona os pontos de distribuição do grupo de limites BG_B para a sua pesquisa. Em seguida, continua a pesquisar conteúdo a partir de um ponto de distribuição no respetivo conjunto combinado de servidores. Este agrupamento inclui agora servidores a partir de grupos de limites BG_A tanto BG_B. O cliente continua a contactar cada ponto de distribuição de dois minutos e, em seguida, muda para o servidor seguinte no seu conjunto. O conjunto de clientes de localizações de origem de conteúdo válida inclui DP_A1, DP_A2, DP_B1 e DP_B2.
-   Após um adicionais 10 minutos (total de 20 minutos), se o cliente ainda não encontrou um ponto de distribuição com conteúdo, que expande o conjunto para incluir servidores disponíveis a partir do segundo *vizinho* grupo, o grupo de limites BG_C. O cliente tem agora seis pontos de distribuição para pesquisa (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2). Continua a alteração cada dois minutos até encontrar conteúdo para um novo ponto de distribuição.
-   Se o cliente não foi encontrado conteúdo depois de um total de 120 minutos, fica novamente para incluir o *grupo de limites de site predefinido* como parte da sua pesquisa contínua. O conjunto inclui agora todos os pontos de distribuição dos três grupos de limites configurado e o ponto de distribuição final localizado no servidor do site. O cliente, em seguida, continua a pesquisa de conteúdo, alterar a cada dois minutos até ser encontrado conteúdo de pontos de distribuição.

Ao configurar os grupos de vizinho diferentes para estar disponível em alturas diferentes, pode controlar quando são adicionados como uma localização de origem de conteúdo pontos de distribuição específico. O cliente utiliza a contingência para o grupo de limites de site predefinido como uma rede de segurança para o conteúdo que não está disponível a partir de qualquer outra localização.





<!--
### Update existing boundary groups to the new model
When you update to version prior to 1610, the following configurations are automatically made. This behavior ensures your current fallback behavior remains available until you configure new boundary groups and relationships.

-   Each primary site creates a default site boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***.
  - The primary site adds to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group any state migration points and distribution points configured to **Allow fallback source location for content**.
  - The site adds software update points to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group.
-   The site makes a copy of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***&lt;original boundary group name>-&lt;original boundary group ID>***:  
    -   Site systems that have a fast connection are left in the original boundary group.
    -   A copy of site systems (distribution points, management points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
    - This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - If a secondary site has at least one state migration point or distribution point enabled to **Allow fallback source location for content**, Configuration Manager creates a boundary group named ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>***. 
  - All distribution points enabled to **Allow fallback source location for content** and state migration points are added to this secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group. The fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients do not fallback to that group.    
Not selected | Selected     |   **Normal fallback** - Use distribution points in current boundary group, then servers from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  
-->



## <a name="changes-from-prior-versions"></a>Alterações das versões anteriores
Seguem-se as alterações principais grupos de limites e como os clientes localizam os conteúdos no Configuration Manager atual ramo. Muitas destas alterações e conceitos funcionam em conjunto.


-   Configurações para rápida ou lenta são removidas: Já não está a configurar pontos de distribuição individuais para serem rápida ou lenta. Em vez disso, cada sistema de sites associado a um grupo de limites é Tratado da mesma. Devido a esta alteração, o **referências** separador das propriedades do grupo de limites já não suporta a configuração rápida ou lenta.
- Novo grupo de limites de predefinição em cada site: Cada site primário tem um novo grupo de limites de predefinição com o nome ***predefinição-Site-limite-grupo&lt;sitecode >***. Quando um cliente não está numa localização de rede atribuída a um grupo de limites, utiliza os sistemas de sites associados ao grupo predefinido do seu site atribuído. Planear a utilização deste grupo de limites como uma substituição para o conceito de localização de conteúdo de contingência.   
 -  **Permitir que as localizações de origem de contingência para conteúdo** for removido: Já não está explicitamente a configurar um ponto de distribuição para ser utilizado para contingência. As opções para configurar esta definição são removidas da consola.

    Além disso, o resultado da definição **permitir que os clientes utilizem uma localização de origem de contingência para conteúdo** numa implementação tipo para aplicações foi alterada. Esta definição num tipo de implementação agora permite que um cliente para utilizar o grupo de limites de site predefinido como uma localização de origem de conteúdo.

 -  Relações de grupos de limites: Cada grupo de limites pode ser associado a um ou mais grupos de limites adicionais. Estas ligações formam relações que estão configuradas no novo limite grupo separador de propriedades com o nome **relações**:
    -   Cada grupo de limites que um cliente é diretamente associado é chamado um **atual** grupo de limites.  
    -   Nenhum grupo de limites pode utilizar um cliente devido a uma associação entre esse cliente *atual* grupo de limites e outro grupo é chamado um **vizinho** grupo de limites.
    -  No **relações** separador, adicione os grupos de limites para utilizar como um *vizinho* grupo de limites. Também configure um período de tempo em minutos para contingência. Quando um cliente não conseguir localizar conteúdo a partir de um ponto de distribuição no *atual* grupo, desta vez, é quando o cliente começa a procurar nas localizações de conteúdo de *vizinho* grupos de limites.

        Quando adicionar ou alterar uma configuração do grupo de limites, tem a opção para o bloco de contingência para esse grupo de limites específico do grupo atual que estiver a configurar.

    Para utilizar a nova configuração, defina explícitas associações (ligações) de um grupo de limites para outro. Configure todos os pontos de distribuição nesse grupo associados com o mesmo tempo em minutos. Quando um cliente não conseguir localizar uma origem de conteúdo do respetivo *atual* grupo de limites, o tempo que configura determina quando começa a pesquisar origens de conteúdo do respetivo grupo de limites de vizinho.

    Além dos grupos de limites que configurar explicitamente, cada grupo de limites tem uma ligação implícita para o grupo de limites de site predefinido. Esta ligação fica ativa depois de 120 minutos. Em seguida, o grupo de limites de site predefinido torna-se um grupo de limites de vizinho. Este comportamento permite que os clientes utilizar como localizações de origem de conteúdo os pontos de distribuição associados a esse grupo de limites.

    Este comportamento substitui que anteriormente foi referido como contingência para conteúdo. Substituir este comportamento predefinido de 120 minutos associando explicitamente o grupo de limites de site predefinido para um *atual* grupo. Definir uma hora específica em minutos, ou bloquear contingência inteiramente para impedir a sua utilização.


-   Os clientes tentam obter conteúdos de cada ponto de distribuição de dois minutos: Quando um cliente procura de uma localização de origem de conteúdo, este tenta aceder a cada ponto de distribuição de dois minutos antes de, em seguida, tentar outro ponto de distribuição. Este comportamento é uma alteração de versões anteriores onde os clientes tentaram ligar a um ponto de distribuição para até duas horas.

    - Os clientes selecionam aleatoriamente o primeiro ponto de distribuição do agrupamento de servidores disponíveis no cliente do *atual* grupo de limites (ou grupos).

    - Depois de dois minutos, se o cliente não foi encontrado o conteúdo, muda para um novo ponto de distribuição e tenta obter conteúdo a partir desse servidor. Este processo repete-se a cada dois minutos até que o cliente localiza o conteúdo ou atinge o último servidor no seu conjunto.

    - Se um cliente não é possível encontrar uma localização de origem de conteúdo válida a partir do respetivo *atual* agrupamento antes de atingir o período de contingência para um *vizinho* grupo de limites, o cliente, em seguida, adiciona os pontos de distribuição do que *vizinho* grupo até ao fim da respetiva lista atual. Este, em seguida, procura o grupo expandido das localizações de origem que inclua os pontos de distribuição a partir de ambos os grupos de limites.

        > [!TIP]  
        > Quando criar uma ligação explícita do grupo de limites atuais para o grupo de limites de site predefinido e definir uma hora de contingência que é inferior à hora de contingência para uma ligação a um grupo de limites de vizinho, os clientes começam a pesquisar localizações de origem do site predefinido grupo de limites antes, incluindo o grupo de vizinho.

    - Quando o cliente não consegue obter conteúdos do último servidor no agrupamento, começar o processo de novo.


## <a name="procedures-for-boundary-groups"></a>Procedimentos para grupos de limites

### <a name="to-create-a-boundary-group"></a>Para criar um grupo de limites  
1.  Na consola do Configuration Manager, clique em **administração** > **configuração da hierarquia** >  **grupos de limites**.  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Grupo de Limites**.  

3.  No **criar grupo de limites** caixa de diálogo, selecione o **geral** separador e especifique um **nome** para este grupo de limites.  

4.  Clique em **OK** para guardar o novo grupo de limites.  


### <a name="to-configure-a-boundary-group"></a>Para configurar um grupo de limites  
 1.  Na consola do Configuration Manager, clique em **administração** > **configuração da hierarquia** >  **grupos de limites**.  

 2.  Selecione o grupo de limites que pretende modificar.  

 3.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  

 4.  Na caixa de diálogo **Propriedades** do grupo de limites, selecione o separador **Geral** para modificar os limites que são membros deste grupo de limites:  

     -   Para adicionar limites, clique em **Adicionar**, selecione a caixa de verificação de um ou mais limites e clique em **OK**.  

     -   Para remover limites, selecione o limite e clique em **Remover**.  

 5.  Selecione o separador **Referências** para modificar a atribuição de sites e a configuração do servidor do sistema de sites associada:  

     -   Para ativar este grupo de limites para utilização pelos clientes para atribuição de sites, selecione **utilizar este grupo de limites para atribuição de site**. Em seguida, selecione um site a partir de **site atribuído** na lista pendente.  

     -   Para configurar que servidores do sistema de sites disponíveis estão associados a este grupo de limites:  

     1.  Clique em **Adicionar**e, em seguida, selecione a caixa de verificação de um ou mais servidores. Os servidores são adicionados como servidores do sistema de sites associados a este grupo de limites. Só estão disponíveis os servidores que têm a função de sistema de sites instalada.  

         > [!NOTE]  
         >  Pode selecionar uma combinação de sistemas de sites disponíveis a partir de qualquer site na hierarquia. Os sistemas de sites selecionados são listados no separador **Sistemas de Sites** nas propriedades de cada limite que seja membro deste grupo de limites.  

     2.  Para remover um servidor deste grupo de limites, selecione o servidor e, em seguida, clique em **Remover**.  

         > [!NOTE]  
         >  Para parar a utilização deste grupo de limites para associar sistemas de sites, remova todos os servidores listados como servidores de sistema de sites associados.  

 6.  Para configurar o comportamento de contingência, selecione o **relações** separador:  

     - Clique em **adicionar**e, em seguida, selecione o grupo de limites que pretende configurar.

     - Defina uma hora para pontos de distribuição de contingência. Após este período de tempo, os clientes num grupo de limites que está a configurar relações, será possível iniciar a pesquisa de conteúdo dos pontos de distribuição do grupo de limites que está a adicionar.

     - Para impedir a contingência para um grupo de limites específico, incluindo o *grupo de limites de site predefinido* que está configurado por predefinição, selecione o grupo de limites e, em seguida, selecione a caixa para **nunca contingência**.   

 7.  Clique em **OK** para fechar as propriedades do grupo de limites e guardar a configuração.  

#### <a name="to-associate-a-site-system-server-with-a-boundary-group"></a>Para associar um servidor de sistema de sites um grupo de limites  
 1.  Na consola do Configuration Manager, clique em **administração** > **configuração da hierarquia** >  **grupos de limites**.  

 2.  Selecione o grupo de limites que pretende modificar.  

 3.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  

 4.  Na caixa de diálogo **Propriedades** do grupo de limites, selecione o separador **Referências** .  

 5.  Em **selecionar servidores de sistema de sites**, clique em **adicionar**. Selecionar os servidores de sistema de sites para associar este grupo de limites e, em seguida, clique em **OK**.  

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
