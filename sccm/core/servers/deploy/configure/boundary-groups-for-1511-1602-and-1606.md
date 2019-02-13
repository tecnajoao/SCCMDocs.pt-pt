---
title: Grupos de limites para a versão 1511 e 1602 e 1606
titleSuffix: Configuration Manager
description: Utilize grupos de limites com versões do Configuration Manager versão 1511 e 1602 e 1606.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 04e212c2c1c24098e8260f9470aec81cb35a7cf9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156894"
---
# <a name="boundary-groups-for-system-center-configuration-manager-version-1511-1602-and-1606"></a>Grupos de limites para o System Center Configuration Manager versão 1511 e 1602 e 1606

*Aplica-se a: O System Center Configuration Manager (ramo atual)*
<!-- This topic drops from TOC with the release of version 1706 -->

As informações neste tópico são específicas para utilizar grupos de limites com versões 1511 e 1602 e 1606 do System Center Configuration Manager.
Se utilizar a versão 1610 ou posterior, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) para obter informações sobre como utilizar os grupos de limites redesenhada.  


##  <a name="BKMK_BoundaryGroups"></a> Boundary groups  
 Pode criar grupos de limites para agrupar logicamente as localizações de rede relacionadas (limites) para facilitar a gestão da sua infraestrutura. Para poder utilizar o grupo de limites, tem de atribuir os limites a grupos de limites. Os clientes utilizam a configuração do grupo de limites para:  

-   Atribuição automática de site  

-   Localização de conteúdo  

-   Pontos de gestão preferenciais

    Se pretender utilizar pontos de gestão preferidos, tem de ativar esta opção para a hierarquia e não a partir da configuração do grupo de limites. Consulte a *para ativar a utilização de pontos de gestão preferenciais* procedimento apresentado mais adiante neste tópico.  

Ao configurar grupos de limites, adicionar um ou mais limites ao grupo de limites. Em seguida, configure as definições adicionais para utilização por clientes localizados nesses limites.  

#### <a name="to-create-a-boundary-group"></a>Para criar um grupo de limites  

1.  Na consola do Configuration Manager, escolha **Administration** > **configuração da hierarquia** >  **grupos de limites**.  

2.  Sobre o **home page** separador a **criar** de grupo, escolha **criar grupo de limites**.  

3.  Na **criar grupo de limites** caixa de diálogo caixa, escolha a **gerais** separador e, em seguida, introduza um **nome** para este grupo de limites.  

4.  Escolher **OK** para guardar o novo grupo de limites.  

#### <a name="to-set-up-a-boundary-group"></a>Para configurar um grupo de limites  

1.  Na consola do Configuration Manager, escolha **Administration** > **configuração da hierarquia** >  **grupos de limites**.  

2.  Escolha o grupo de limites que pretende alterar.  

3.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

4.  Na **propriedades** caixa de diálogo para o grupo de limites, selecione a **geral** separador para alterar os limites que são membros deste grupo de limites:  

    -   Para adicionar limites, escolha **Add**, selecione a caixa de verificação para um ou mais limites e, em seguida, escolha **OK**.  

    -   Para remover limites, selecione o limite e, em seguida, escolha **remover**.  

5.  Escolha o **referências** separador para alterar a atribuição de site e a configuração de servidor de sistema de sites associada:  

    -   Para ativar este grupo seja utilizado pelos clientes para atribuição de site, marque a caixa de verificação **utilizar este grupo de limites para atribuição de sites**e, em seguida, selecione um site a partir do **site atribuído** na caixa pendente.  

    -   Para configurar os servidores de sistema de sites disponíveis que estão associados este grupo de limites:  

    1.  Escolher **adicionar**e, em seguida, selecione a caixa de verificação para um ou mais servidores. Os servidores são adicionados como servidores do sistema de sites associados a este grupo de limites. Só estão disponíveis os servidores que têm a função de sistema de sites instalada.  

        > [!NOTE]  
        >  Pode selecionar uma combinação de sistemas de sites disponíveis a partir de qualquer site na hierarquia. Os sistemas de sites selecionados são listados no separador **Sistemas de Sites** nas propriedades de cada limite que seja membro deste grupo de limites.  

    2.  Para remover um servidor deste grupo de limites, selecione o servidor e, em seguida, escolha **remover**.  

        > [!NOTE]  
        >  Para parar a utilização deste grupo de limites para associar sistemas de sites, tem de remover todos os servidores que estão listados como servidores de sistema de sites associados.  

    3.  Para alterar a velocidade da ligação de rede para um servidor de sistema de sites para este grupo de limites, selecione o servidor e, em seguida, escolha **Alterar ligação**.  

         Por predefinição, é a velocidade da ligação para cada sistema de sites **rapidamente**, mas pode alterar a velocidade **lenta**. A velocidade da ligação de rede e a configuração de uma implementação determinam se um cliente pode transferir conteúdo do servidor.  

6.  Escolher **OK** para fechar as propriedades do grupo de limites e guardar a configuração.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Para associar um servidor de implementação de conteúdo ou ponto de gestão a um grupo de limites  

1.  Na consola do Configuration Manager, escolha **Administration** > **configuração da hierarquia** >  **grupos de limites**.  

2.  Escolha o grupo de limites que pretende alterar.  

3.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

4.  Na **propriedades** caixa de diálogo para o grupo de limites, selecione a **referências** separador.  

5.  Sob **selecionar servidores do sistema de sites**, escolha **Add**, selecione a caixa de verificação para os servidores do sistema de sites que pretende associar este grupo de limites e, em seguida, escolha **OK**.  

6.  Escolher **OK** para fechar a caixa de diálogo e guardar a configuração do grupo de limites.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Para ativar a utilização de pontos de gestão preferenciais  

1.  Na consola do Configuration Manager, escolha **Administration** > **configuração do Site** > **Sites**e, em seguida, no **Home page** separador, escolha **definições de hierarquia**.  

2.  Sobre o **gerais** separador de **definições de hierarquia**, escolha **os clientes preferem utilizar pontos de gestão especificados em grupos de limites**.  

3.  Escolher **OK** para fechar a caixa de diálogo e guardar a configuração.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Para configurar um site de contingência para atribuição automática de site  

1. Na consola do Configuration Manager, escolha **Administration** > **configuração do Site** >  **Sites**.  

2. Sobre o **home page** separador a **Sites** de grupo, escolha **definições de hierarquia**.  

3. Na **gerais** separador, marque a caixa de verificação para **utilizar um site de contingência**e, em seguida, selecione um site a partir do **site de contingência** na lista pendente.  

4. Escolher **OK** para guardar a configuração.  

   As secções seguintes fornecem detalhes adicionais sobre as configurações de grupos de limites.  

###  <a name="BKMK_BoundarySiteAssignment"></a> Acerca da atribuição de sites  
 Pode configurar cada grupo de limites com um site atribuído para clientes.  

-   Um cliente recentemente instalado que utilize a atribuição automática de site será associado ao site atribuído de um grupo de limites que tem a localização de rede atual do cliente.  

-   Um cliente que está atribuído a um site não altera a sua atribuição de site quando o cliente é alterada a localização de rede. Por exemplo, se o cliente fizer roaming para uma nova localização de rede que é representada por um limite num grupo de limites que tenha uma atribuição de site diferente, site atribuído do cliente permanecerá inalterado.  

-   Quando a Deteção de Sistemas do Active Directory deteta um novo recurso, as informações de rede do recurso detetado são comparadas com os limites dos grupos de limites. Este processo associa o novo recurso a um site atribuído que será utilizado pelo método de instalação push do cliente.  

-   Quando um limite é um membro de vários grupos de limites que possuem diferentes sites atribuídos, os clientes selecionam aleatoriamente um dos sites.  

-   Alterações ao site atribuído de um grupo de limites aplicam-se apenas a novas ações de atribuição de site. Os clientes foram atribuídos anteriormente a um site não avaliam a atribuição do site novamente com base nas alterações à configuração de um grupo de limites (ou a sua própria localização de rede).  

Para obter mais informações sobre a atribuição de sites do cliente, consulte [através de atribuição de Site automática para computadores](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) na [como atribuir clientes a um site no System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="BKMK_BoundaryContentLocation"></a> Acerca da localização de conteúdo  
 Pode configurar cada grupo de limites com um ou mais pontos de distribuição e pontos de migração de estado, e pode associar os mesmos pontos de distribuição e pontos de migração de estado com vários grupos de limites.  

-   **Durante a distribuição de software**, os clientes solicitam uma localização para o conteúdo de implementação. O Configuration Manager envia ao cliente uma lista de pontos de distribuição que estão associados a cada grupo de limites que inclui a localização de rede atual do cliente.  

-   **Durante a implementação do sistema operativo**, os clientes solicitam uma localização para enviar ou receber as respetivas informações de migração de estado. O Configuration Manager envia ao cliente uma lista de pontos de migração de estado associados a cada grupo de limites que inclui a localização de rede atual do cliente.  

Este comportamento permite que o cliente selecione o servidor mais próximo para transferir o conteúdo ou informações de migração de estado.  

###  <a name="BKMK_PreferredMP"></a> Acerca dos pontos de gestão preferenciais  
 Pontos de gestão preferenciais permitem que um cliente identificar um ponto de gestão que está associado a respetiva localização de rede atual (limite).  

-   Um cliente tenta utilizar um ponto de gestão preferencial do seu site atribuído antes de utilizar um ponto de gestão do seu site atribuído que não está configurado como preferencial.  

-   Para utilizar esta opção, tem de ativá-la para a hierarquia e configurar grupos de limites em sites primários individuais para incluir os pontos de gestão que devem ser associados aos limites associados desse grupo de limites  

-   Quando são configurados os pontos de gestão preferenciais e de um cliente organiza a respetiva lista de pontos de gestão, os locais de cliente de pontos de gestão preferencial na parte superior da lista de atribuído gestão atribuídos pontos, que inclui todos os pontos de gestão a partir do cliente site.  

> [!NOTE]  
>  Quando um cliente fizer-roaming, como quando um computador portátil circula para uma localização de escritórios remotos e altera a localização de rede, ele poderá utilizar um ponto de gestão (ou ponto de gestão do proxy) do site local na nova localização antes de tentar utilizar um ponto de gestão através do respetivo atribuído site (que inclui os pontos de gestão preferenciais).  Ver [compreender como os clientes localizam os recursos de site e os serviços do System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) para obter mais informações.  

###  <a name="BKMK_BoundaryOverlap"></a> Acerca dos limites de sobreposição  
 O Configuration Manager suporta configurações de limites sobrepostos para localização de conteúdo:  

-   **Quando um cliente solicita conteúdo**e a localização de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de distribuição que possuem o conteúdo.  

-   **Quando um cliente solicita um servidor para enviar ou receber as respetivas informações de migração de estado**e a localização de rede do cliente pertence a vários grupos de limites, o Configuration Manager envia ao cliente uma lista de todos os pontos de migração de estado que estão associados com um grupo de limites que inclui a localização de rede atual do cliente.  

Este comportamento permite que o cliente selecione o servidor mais próximo para transferir o conteúdo ou informações de migração de estado.  

###  <a name="BKMK_BoudnaryNetworkSpeed"></a> Acerca da velocidade da ligação de rede  
 Pode definir a velocidade da ligação de rede para cada servidor de sistema de sites num grupo de limites. Esta definição aplica-se aos clientes que se ligam a um sistema de sites com base na configuração do grupo de limites. O mesmo servidor do sistema de sites pode ter uma velocidade de ligação diferente definida em diferentes grupos de limites.  

 Por predefinição, a velocidade da ligação de rede está definida como **rapidamente**, mas pode alterá-lo para **lenta**. A velocidade da ligação de rede e a configuração de implementação, verifique se um cliente pode transferir conteúdo de um ponto de distribuição quando o cliente está no grupo de limites associado.  

 Para obter mais informações sobre como a configuração de velocidade de ligação de rede afeta a forma como os clientes obtêm conteúdos, consulte [cenários de localização de origem de conteúdo](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
