---
title: Procedimentos para grupos de limites
titleSuffix: Configuration Manager
description: Configure grupos de limites para organizar logicamente as localizações de rede relacionados chamadas limites.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d4aa1c044c8ea68b934a6dad4f1f85cbe43ec19b
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458311"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Como configurar grupos de limites para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo inclui procedimentos sobre como configurar grupos de limites. Antes de começar, certifique-se de que compreende os conceitos de grupo de limites. Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="bkmk_create"></a> Criar um grupo de limites  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração da hierarquia**e selecione o **grupos de limites** nó.  

2.  Sobre o **home page** separador a **Create** grupo, selecione **criar grupo de limites**.  

3.  Na **criar grupo de limites** caixa de diálogo a **gerais** separador, especifique um **nome** para este grupo de limites. Opcionalmente, incluir uma **Descrição**.  

4.  Selecione **OK** para guardar o novo grupo de limites, ou para continuar para a secção seguinte para configurar o grupo de limites.  


## <a name="bkmk_config"></a> Configurar um grupo de limites  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração da hierarquia**e selecione o **grupos de limites** nó.  

2.  Selecione o grupo de limites que pretende modificar e selecione **propriedades** na faixa de opções. Esta ação abre a janela de propriedades do grupo de limites.  

Configure as seguintes definições:  
- [Adicionar ou remover limites](#bkmk_add)  
- [Configurar a atribuição de site e selecionar servidores do sistema de sites](#bkmk_references)  
- [Configurar o comportamento de contingência](#bkmk_bg-fallback)  
- [Configurar opções de grupos de limites](#bkmk_options)  


### <a name="bkmk_add"></a> Adicionar ou remover limites

Na janela de propriedades do grupo de limites, utilize o **gerais** separador para modificar os limites que são membros deste grupo de limites:  

- Para adicionar limites, selecione **adicionar**. Na janela Adicionar limites, selecione a caixa de verificação para um ou mais limites e selecione **OK**.  

- Para remover limites, selecione o limite da lista e selecione **remover**.  


### <a name="bkmk_references"></a> Configurar a atribuição de site e selecionar servidores do sistema de sites

Para modificar a atribuição de site e a configuração do servidor de sistema de sites associados, mude para o **referências** separador na janela de propriedades do grupo de limites.  

- Para ativar este grupo seja utilizado pelos clientes para atribuição de site, selecione **utilizar este grupo de limites para atribuição de site**. Em seguida, selecione um site a partir da **site atribuído** lista suspensa. Para obter mais informações, consulte [atribuição de Site](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment).  

- Para associar servidores de sistema de sites disponíveis este grupo de limites, selecione **adicionar**. A janela de adicionar sistemas de sites apenas apresenta uma lista de servidores que têm as funções do sistema de sites suportadas. Selecione a caixa de verificação para um ou mais servidores e selecione **OK**. Ele as adiciona como servidores de sistema de sites associados para este grupo de limites.  

    > [!NOTE]  
    >  Pode selecionar uma combinação de sistemas de sites disponíveis a partir de qualquer site na hierarquia. Sistemas de sites selecionados são listados os **sistemas de sites** separador nas propriedades de cada limite que seja membro deste grupo de limites.  

- Para remover um servidor deste grupo de limites, selecione o servidor e, em seguida, selecione **remover**.  

    > [!NOTE]  
    >  Para parar a utilização deste grupo de limites para associar sistemas de sites, remova todos os servidores listados como servidores de sistema de sites associados.  


### <a name="bkmk_bg-fallback"></a> Configurar o comportamento de contingência

Para configurar o comportamento de contingência, mude para o **relações** separador na janela de propriedades do grupo de limites.  

- Para criar uma relação com outro grupo de limites:  

    - Selecione **adicionar**. Na janela de grupos de limites de contingência, selecione o grupo de limites para configurar.  

    - Defina um tempo de contingência para o site seguinte funções do sistema:  
        - Ponto de distribuição  
        - Ponto de atualização de software  
        - Ponto de gestão  

        > [!Note]  
        > Por exemplo, abrir a janela de propriedades para o grupo de limites de sucursal. Na janela de grupos de limites de contingência, selecione o grupo de limites do Office principal. Definir o tempo de contingência de ponto de distribuição `20`. Quando guardar esta configuração, os clientes no grupo de limites de sucursal serão para começar a procurar conteúdo a partir de pontos de distribuição no grupo de limites de Main Office após 20 minutos.  

    - Para evitar a contingência para um grupo de limites específicos, selecione o grupo de limites e, em seguida, selecione **Never contingência** para o tipo de função do sistema de sites. Esta ação pode incluir a *grupo de limite de site predefinido*.  

- Para modificar a configuração de uma relação existente, selecione o grupo de limites na lista e selecione **alteração**. Esta ação abre a janela de grupos de limites de contingência para apenas esse grupo de limites.  
 
- Para remover uma relação, selecione o grupo de limites na lista e selecione **remover**.  

Para obter mais informações, consulte [contingência](/sccm/core/servers/deploy/configure/boundary-groups#fallback). 


### <a name="bkmk_options"></a> Configurar opções de grupos de limites
<!--1356193--> A partir da versão 1806, para configurar opções adicionais para os clientes neste grupo de limites, mude para o **opções** separador. Para obter mais informações, consulte [opções de grupos de limites para as transferências de ponto a ponto](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).

- **Permitir transferências de ponto a ponto neste grupo de limites**: Por predefinição, esta opção encontra-se ativada. O ponto de gestão fornece aos clientes uma lista de localizações de conteúdo que inclui a origens de ponto a ponto.  

    - **Durante downloads de ponto a ponto, utilize apenas colegas dentro da mesma sub-rede**: Esta definição é dependente de um acima. Se ativar esta opção, o ponto de gestão inclui apenas nas fontes de mesmo nível de lista de localização de conteúdo que estão na mesma sub-rede que o cliente.  


## <a name="bkmk_site-fallback"></a> Configurar um site de contingência para atribuição automática de site  

Se os clientes não estão num grupo de limites com um site atribuído, atribuí-las a este site quando são instaladas.

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2.  Sobre o **home page** separador do Friso, no **Sites** grupo, selecione **definições de hierarquia**.  

3.  Sobre o **gerais** separador, selecione a caixa de verificação **utilizar um site de contingência**. Em seguida, selecione um site a partir da **site de contingência** na lista pendente.  

4.  Selecione **OK** para guardar a configuração.  

Para obter mais informações, consulte [atribuição de Site](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment).


## <a name="bkmk_proc-prefer"></a> Ativar a utilização de pontos de gestão preferenciais  

Para obter mais informações, consulte [pontos de gestão preferenciais](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_preferred).

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2. Sobre o **home page** separador do Friso, no **Sites** grupo, selecione **definições de hierarquia**.  

3. Sobre o **gerais** separador, selecione **os clientes preferem utilizar pontos de gestão especificados em grupos de limites**.  

4. Selecione **OK** para guardar a configuração.  

