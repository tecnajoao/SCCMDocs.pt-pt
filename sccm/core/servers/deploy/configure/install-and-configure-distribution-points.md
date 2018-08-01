---
title: Gerir pontos de distribuição
titleSuffix: Configuration Manager
description: Utilize pontos de distribuição para alojar o conteúdo que implementar em dispositivos e utilizadores.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bca3e0857ed40d2e2b3f9d739b4c0411e0213d09
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385376"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Instalar e configurar pontos de distribuição no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Instale pontos de distribuição do Configuration Manager para alojar os ficheiros de conteúdo que implementar em dispositivos e utilizadores. Crie grupos de pontos para simplificar a forma como gerir pontos de distribuição e, como distribuir o conteúdo para pontos de distribuição de distribuição.  

*Instalar um novo ponto de distribuição* utilizando o Assistente de instalação. Para obter mais informações, consulte [instale um ponto de distribuição](#bkmk_install). Para *gerir as propriedades de um ponto de distribuição existente*, editar as propriedades do ponto de distribuição. Para obter mais informações, consulte [configurar um ponto de distribuição](#bkmk_configs). 

Configure a maioria das definições de ponto de distribuição com qualquer um dos métodos. Algumas definições estão disponíveis apenas quando estiver a instalar ou editar, mas não ambos:  

-   Definições que estão disponíveis apenas quando estiver a instalar um ponto de distribuição:  

    -   **Permitir Gestor de configuração para instalar o IIS no computador do ponto de distribuição**

    -   **Configurar definições de espaço da unidade para o ponto de distribuição**  

-   Definições que estão disponíveis apenas quando está editando as propriedades de um ponto de distribuição:  

    -   **Gerir relações de grupo de ponto de distribuição**  

    -   **Ver conteúdo implementado no ponto de distribuição**  

    -   **Configurar limites de velocidade para transferências de dados para pontos de distribuição**  

    -   **Configurar agendamentos para transferências de dados para pontos de distribuição**  



##  <a name="bkmk_install"></a> Instalar um ponto de distribuição  

Escolha um servidor de sistema de sites como ponto de distribuição antes de conteúdo pode ser disponibilizado para os computadores cliente. Atribuir um ponto de distribuição a, pelo menos, um [grupo de limites](/sccm/core/servers/deploy/configure/boundary-groups#distribution-points) antes no local, computadores cliente podem utilizar esse ponto de distribuição como localização de origem de conteúdo. Adicione a função de ponto de distribuição a um servidor de sistema de sites novo ou adicioná-lo a um servidor de sistema de sites existente.


### <a name="bkmk_install-prereq"></a> Pré-requisitos

Ao instalar um novo ponto de distribuição, use um Assistente de instalação que explica-lhe as definições disponíveis. Antes de começar, considere os seguintes pré-requisitos:  

-   Tem de ter as seguintes permissões de segurança para criar e configurar um ponto de distribuição:  

    -   **Leia** para o **ponto de distribuição** objeto  

    -   **Copiar para ponto de distribuição** para o **ponto de distribuição** objeto  

    -   **Modificar** para o **Site** objeto  

    -   **Gerir certificados para implementação do sistema operativo** para o **Site** objeto  

-   Instale serviços de informação Internet (IIS) no servidor do Windows que aloja o ponto de distribuição. Em alternativa, ao instalar a função de sistema de sites, o Configuration Manager pode instalar e configurar o IIS para.  


### <a name="bkmk_install-procedure"></a> Procedimento para instalar um ponto de distribuição  

Utilize este procedimento para adicionar um novo ponto de distribuição. Para alterar a configuração de um ponto de distribuição existente, consulte a [configurar um ponto de distribuição](#bkmk_configs) secção.  

Começar com o procedimento geral para [instalar funções do sistema de sites](/sccm/core/servers/deploy/configure/install-site-system-roles). Selecione o **ponto de distribuição** função no **seleção da função do sistema** página do Assistente para criar servidor do sistema de sites. Esta ação adiciona as seguintes páginas para o assistente:  
- [Ponto de distribuição](#bkmk_config-general)
- [Definições de unidade](#bkmk_config-drive)
- [Ponto de distribuição de extração](#bkmk_config-pull)
- [Definições do PXE](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Validação de conteúdos](#bkmk_config-valid)
- [Grupos de limites](#bkmk_config-boundary)

> [!Important]  
> As seguintes definições estão disponíveis apenas quando estiver a instalar um ponto de distribuição:  
> 
> - **Permitir Gestor de configuração para instalar o IIS no computador do ponto de distribuição**  
> 
> - **Configurar definições de espaço da unidade para o ponto de distribuição**  

Para obter mais informações sobre as páginas do assistente específica para a função de ponto de distribuição, consulte a [configurar um ponto de distribuição](#bkmk_configs) secção. Por exemplo, se pretende instalar o ponto de distribuição como uma [ponto de distribuição de solicitação](#bkmk_config-pull), escolha a opção de **ativar este ponto de distribuição extrair conteúdo de outros pontos de distribuição**. Em seguida, faça as configurações adicionais que necessitam de pontos de distribuição de extração.  

Depois de concluir o Assistente para criar servidor do sistema de sites, o site adiciona a função de ponto de distribuição para o servidor de sistema de sites.  



##  <a name="bkmk_manage"></a> Gerir grupos de pontos de distribuição  

Grupos de pontos de distribuição permitem um agrupamento lógico de pontos de distribuição para distribuição de conteúdos. Utilize estes grupos para gerir e monitorizar conteúdos a partir de um local central para pontos de distribuição que abranjam vários sites. Considere o seguinte ponto:

-   Adicione um ou mais pontos de distribuição a partir de qualquer site na hierarquia para um grupo de pontos de distribuição.  

-   Adicione um ponto de distribuição a mais do que um grupo de pontos de distribuição.  

-   Quando distribui conteúdo a um grupo de pontos de distribuição, o Configuration Manager distribui o conteúdo por todos os pontos de distribuição que são membros do grupo.  

-   Se adicionar um ponto de distribuição ao grupo após uma distribuição de conteúdo inicial, o Configuration Manager distribui automaticamente o conteúdo para o novo membro do ponto de distribuição.  

-   Associe uma coleção com um grupo de pontos de distribuição. Quando distribui conteúdo por essa coleção, o Configuration Manager determina quais os grupos são associados à coleção. Em seguida, distribui o conteúdo por todos os pontos de distribuição que são membros desses grupos.  

    > [!NOTE]  
    >  Após distribuir conteúdos a uma coleção, se, em seguida, associar a coleção com um novo grupo de pontos de distribuição, tem de redistribuir os conteúdos à coleção antes do conteúdo é distribuído para o novo grupo de pontos de distribuição.  

As secções seguintes listam os procedimentos para as seguintes ações gerir grupos de pontos de distribuição:  
- [Criar e configurar um novo grupo de pontos de distribuição](#bkmk_dpgroup-create)
- [Modificar um grupo de pontos de distribuição existente](#bkmk_dpgroup-modify)
- [Adicionar pontos de distribuição selecionados a grupos de pontos de distribuição existentes](#bkmk_dpgroup-addexist)


### <a name="bkmk_dpgroup-create"></a> Procedimento para criar e configurar um novo grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **grupos de pontos de distribuição** nó.  

2.  No Friso, clique em **criar grupo**.  

3.  Na janela Criar grupo de pontos de distribuição nova, introduza o **Name** e, opcionalmente, uma **Descrição** para o grupo.  

4.  Sobre o **membros** separador, clique em **Add**.  

5.  Na janela de pontos de distribuição de adicionar, selecione um ou mais pontos de distribuição para adicionar como membros do grupo. Em seguida, clique em **OK**.  

6.  Se necessário, mude para o **coleções** separador da janela Criar grupo de pontos de distribuição nova e clique em **Add**.  

7.  Na janela selecionar coleções, selecione as coleções a associar ao grupo de ponto de distribuição e, em seguida, clique em **OK**.  

8.  Na janela Criar grupo de pontos de distribuição nova, clique em **OK** para criar o grupo.  


#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Criar um novo grupo a partir de um ponto de distribuição existente

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **pontos de distribuição** nó. Selecione um ou mais pontos de distribuição para adicionar a uma distribuição do novo grupo de pontos.  

2.  No Friso, clique em **adicionar itens selecionados**e, em seguida, clique em **adicionar itens selecionados ao novo grupo de pontos de distribuição**.  

Este processo povoa automaticamente a **membros** separador da janela Criar grupo de pontos de distribuição novo com os servidores selecionados.


### <a name="bkmk_dpgroup-modify"></a> Procedimento para modificar um grupo de pontos de distribuição existente  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **grupos de pontos de distribuição** nó.  

2.  Selecione um grupo de pontos de distribuição existente para modificar. No Friso, clique em **Propriedades**.  

3.  Para associar novas coleções este grupo, mude para o **coleções** separador e clique em **Add**. Selecione as coleções e, em seguida, clique em **OK**.  

4.  Para adicionar novos pontos de distribuição para este grupo, mude para o **membros** separador e clique em **Add**. Selecione os pontos de distribuição e, em seguida, clique em **OK**.  

5.  Escolher **OK** para guardar as alterações para o grupo de pontos de distribuição.  


### <a name="bkmk_dpgroup-addexist"></a> Procedimento para adicionar pontos de distribuição selecionados a grupos de pontos de distribuição existentes  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **pontos de distribuição** nó. Selecione um ou mais pontos de distribuição para adicionar a um grupo existente.  

2.  No Friso, clique em **adicionar itens selecionados**e, em seguida, clique em **adicionar itens selecionados a grupos de pontos de distribuição existentes**.  

3.  Na **grupos de pontos de distribuição disponíveis**, selecione os grupos a que, pontos de distribuição selecionados são adicionados como membros. Em seguida, clique em **OK**.  



## <a name="bkmk_reassign"></a> Reatribuir um ponto de distribuição
<!-- 1306937 --> Muitos clientes têm de grandes infra-estruturas de Configuration Manager e reduzindo os sites primários ou secundários para simplificar o seu ambiente. Eles ainda precisam manter os pontos de distribuição nas localizações das sucursais para servir de conteúdo para clientes gerenciados. Esses pontos de distribuição geralmente contêm vários terabytes, ou mais dos conteúdos. Este conteúdo é dispendioso em termos de largura de banda de rede e de tempo para distribuir a estes servidores remotos. 

A partir da versão 1802, esta funcionalidade permite-lhe reatribuir um ponto de distribuição para outro site principal sem redistribuir o conteúdo. Esta ação atualiza a atribuição de sistema do site e a persistência de todo o conteúdo no servidor. Se precisa de reatribuir vários pontos de distribuição, primeiro efetue esta ação num único ponto de distribuição. Em seguida, continue com servidores adicionais, um por vez.

> [!IMPORTANT]  
> O servidor de destino apenas pode alojar a função de ponto de distribuição. Se o servidor de sistema de sites aloja outra função de servidor do Configuration Manager, tais como o ponto de migração de estado, não é possível reatribuir o ponto de distribuição. Não é possível reatribuir um ponto de distribuição de nuvem. 

Antes de reatribuir um ponto de distribuição, adicione a conta de computador do servidor do site de destino para o grupo de administradores local no servidor de ponto de distribuição de destino. 

Siga estes passos para reatribuir um ponto de distribuição:

1. Na consola do Configuration Manager, ligue-se ao site de administração central.  

2. Vá para o **Administration** área de trabalho e selecione o **pontos de distribuição** nó.  

3. O ponto de distribuição de destino com o botão direito e selecione **reatribuir ponto de distribuição**.  

4. Selecione o destino server e o site de código do site ao qual pretende reatribuir este ponto de distribuição.  

Monitorize a reatribuição da mesma forma como quando adiciona uma nova função. O método mais simples é atualizar a vista de consola após alguns minutos. Adicione a coluna de código do site para o modo de exibição. Este valor é alterado quando o Configuration Manager reatribui o servidor. Se tentar realizar outra ação no servidor de destino antes de atualizar a vista da consola, ocorre um erro "objeto não encontrado". Certifique-se de que o processo estiver concluído e atualize a consola antes de iniciar quaisquer outras ações no servidor.

Depois de reatribuir um ponto de distribuição, atualize o certificado do servidor. O novo servidor de site precisa criptografar novamente este certificado utilizando a respetiva chave pública e armazená-la na base de dados do site. Para obter mais informações, consulte a **criar um certificado autoassinado ou importar um certificado de cliente de infraestrutura de chaves públicas (PKI) para o ponto de distribuição** definir o [geral](#general) separador do Propriedades do ponto de distribuição. 

- Para certificados PKI, não terá de criar um novo certificado. Importe o mesmo. PFX e introduza a palavra-passe.  

- Para certificados autoassinados, ajuste a expiração de data ou hora para atualizá-lo.  

- Se não atualizar o certificado, o ponto de distribuição ainda serve conteúdo, mas falharem as seguintes funções:  

    - Mensagens de validação de conteúdos (o distmgr mostra que ele não é possível desencriptar o certificado)  

    - Suporte PXE para clientes  


### <a name="tips"></a>Sugestões 

- Efetue esta ação do site de administração central. Essa prática ajuda com a replicação para sites primários.  

- Não distribuir conteúdo para o servidor de destino e, em seguida, tente reatribuí-lo. Distribuir conteúdo tarefas que estão em curso podem falhar durante o processo de reatribuição, mas tentar novamente por normal.  

- Se o servidor também é um cliente do Configuration Manager, lembre-se de que também reatribuir o cliente para o novo site primário. Este passo é essencial sobretudo para pontos de distribuição de solicitação, o que utilizam componentes de cliente para transferir conteúdo.  

- Este processo remove o ponto de distribuição do grupo de limite predefinido do site antigo. Terá de adicioná-la manualmente ao grupo de limite predefinido do novo site, se necessário. Todas as outras atribuições de grupo de limites permanecem os mesmos.  



##  <a name="bkmk_configs"></a> Configurar um ponto de distribuição  

Pontos de distribuição individuais suportam uma variedade de configurações diferentes. No entanto, nem todos os tipos de ponto de distribuição suportam todas as configurações. Por exemplo, pontos de distribuição na nuvem não suportam implementações de capacidade de PXE ou multicast. Para obter mais informações sobre limitações específicas, consulte os artigos seguintes:  

-   [Utilizar um ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

-   [Utilizar um ponto de distribuição de extração](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

As secções seguintes descrevem as configurações de ponto de distribuição quando estiver [instalar um novo](#bkmk_install-procedure) ou [editar uma existente](#bkmk_change-procedure):  
- [Definições gerais](#bkmk_config-general)
- [Definições de unidade](#bkmk_config-drive)
- [Ponto de distribuição de extração](#bkmk_config-pull)
- [Definições do PXE](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Validação de conteúdos](#bkmk_config-valid)
- [Grupos de limites](#bkmk_config-boundary)


#### <a name="bkmk_change-procedure"></a> Procedimento para alterar um ponto de distribuição  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho e selecione o **pontos de distribuição** nó.  

2.  Selecione o ponto de distribuição para configurar. No Friso, clique em **Propriedades**.  

3.  Utilize as informações nas secções seguintes quando estiver a editar as propriedades do ponto de distribuição.  

4.  Depois de efetuar as alterações que pretende, clique em **OK** para guardar as definições e fechar as propriedades do ponto de distribuição.  


### <a name="bkmk_config-general"></a> Geral  

As seguintes definições estão no **ponto de distribuição** página do Assistente para criar servidor do sistema de sites e o **geral** separador da janela de propriedades do ponto de distribuição:  

-   **Instalar e configurar o IIS se exigido pelo Configuration Manager**: Se o IIS já não está instalado no servidor, o Configuration Manager instala e configura-o. O Configuration Manager requer o IIS em todos os pontos de distribuição. Se não escolher esta definição e o IIS não está instalado no servidor, instale primeiro o IIS antes do Configuration Manager possa instalar o ponto de distribuição.  

    > [!NOTE]  
    >  Esta opção está apenas nos **ponto de distribuição** página do Assistente para criar servidor do sistema de sites. Está disponível apenas quando estiver [instalar um novo ponto de distribuição](#bkmk_install-procedure).  

- **Ativar e configurar a BranchCache deste ponto de distribuição**: Escolha esta definição para permitir que configurar o Windows BranchCache no servidor do ponto de distribuição do Configuration Manager. Para obter mais informações, consulte [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache).  

- **Ajustar a velocidade de transferência para utilizar a largura de banda de rede não utilizadas (Windows LEDBAT)**<!--1358112-->: A partir da versão 1806, ative os pontos de distribuição para utilizar o controlo de congestionamento de rede. Para obter mais informações, consulte [Windows LEDBAT](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat). O ponto de distribuição deve executar o Windows Server, versão 1709. Não há nenhum pré-requisito do cliente.  

- **Descrição**: Uma descrição opcional para esta função de ponto de distribuição.  

-   **Configurar a forma como os dispositivos cliente comunicam com o ponto de distribuição**: Existem vantagens e desvantagens para usando **HTTP** ou **HTTPS**. Para obter mais informações, consulte [melhores práticas de segurança para gestão de conteúdos](/sccm/core/plan-design/hierarchy/security-and-privacy-for-content-management#BKMK_Security_ContentManagement).  

-   **Permitir a ligação anónima dos clientes**: Esta definição especifica se o ponto de distribuição permite ligações anónimas de clientes do Configuration Manager para a biblioteca de conteúdos.  

    > [!Important]  
    > Se não utilizar esta definição, aplicar as alterações descritas no artigo da Base de dados de conhecimento da Microsoft [2619572](https://support.microsoft.com/help/2619572/) nos clientes do Windows 7. Caso contrário a reparação de aplicações do Windows Installer pode falhar.  
    >   
    >  Quando implementa uma aplicação do Windows Installer, o cliente do Configuration Manager transfere o ficheiro para a respetiva cache local. O cliente, por fim, remove os ficheiros após a conclusão da instalação. O cliente do Configuration Manager atualiza a lista de origem do Windows Installer para a aplicação. Define o caminho de conteúdo à biblioteca de conteúdos nos pontos de distribuição associados. Mais tarde, se tentar reparar a aplicação no dispositivo, o MSIExec tenta aceder ao caminho de conteúdo com um utilizador anónimo.  
    >   
    >  Depois de instalar a atualização nos clientes e modificar a chave de registo documentada, o MSIExec acessa o caminho de conteúdo utilizando a conta de utilizador com sessão iniciada.  

-   **Criar um certificado autoassinado ou importar um certificado de cliente PKI**: O Configuration Manager utiliza este certificado para os seguintes fins:  

    -   Autentica o ponto de distribuição para um ponto de gestão antes do ponto de distribuição envia mensagens de estado.  

    -   Quando **ativar suporte PXE para clientes** sobre o **definições do PXE** página, o ponto de distribuição envia-os para computadores com arranque PXE. Estes computadores, em seguida, utilizá-lo para ligar a um ponto de gestão durante o processo de implementação do sistema operacional.  

    Quando configura todos os pontos de gestão no site para HTTP, selecione a opção para **Criar certificado autoassinado**. Quando configurar os pontos de gestão para HTTPS, utilize a opção para **importar certificado** de PKI.  

    Para importar o certificado, navegue para um ficheiro de Public Key Cryptography Standard (PKCS #12) válido. Este ficheiro PFX ou CER tem o certificado PKI com os seguintes requisitos para o Configuration Manager:  

    -   A utilização pretendida inclui autenticação de cliente  

    -   Ativar a chave privada seja exportada  

    > [!TIP]  
    >  Não existem não requisitos específicos para o requerente do certificado ou nome alternativo do requerente (SAN). Se necessário, utilize o mesmo certificado para vários pontos de distribuição.  

     Para obter mais informações sobre os requisitos de certificado, consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

     Para um exemplo de implementação deste certificado, consulte [implementar o certificado de cliente para pontos de distribuição](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

-   **Ativar conteúdo pré-configurado para este ponto de distribuição**: Esta definição permite-lhe adicionar conteúdo para o servidor antes de distribuir software. Uma vez que os ficheiros de conteúdo já estão na biblioteca de conteúdos, eles não transferem através da rede quando distribuir o software. Para obter mais informações, consulte [conteúdo pré-configurado](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  


### <a name="bkmk_config-drive"></a> Definições de unidade  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando estiver a instalar um novo ponto de distribuição.  

Especifique as definições de unidade para o ponto de distribuição. Configure até duas unidades de disco para a biblioteca de conteúdos e duas unidades de disco para a partilha de pacote. O Configuration Manager possa utilizar unidades adicionais quando as duas primeiras atingem a reserva do espaço na unidade configurada. O **definições de unidade** página configura a prioridade para as unidades de disco e a quantidade de espaço livre em disco que permanece em cada unidade de disco.  

-   **(MB) de reserva de espaço na unidade**: Este valor determina a quantidade de espaço livre numa unidade antes do Configuration Manager escolher uma unidade diferente e continuar o processo de cópia para essa unidade. Ficheiros de conteúdo podem abranger várias unidades.  

-   **Localizações de conteúdo**: Especifica as localizações para a partilha de biblioteca e o pacote de conteúdo deste ponto de distribuição. Por predefinição, todas as localizações de conteúdo estão definidas como **automática**. O Configuration Manager copia os conteúdos para localização de conteúdos primária até a quantidade de espaço livre atingir o valor especificado para **reserva de espaço na unidade (MB)**. Quando seleciona **automática**, Configuration Manager define as localizações de conteúdos primárias para a unidade de disco com mais espaço em disco durante a instalação. Ele define as localizações secundárias para a unidade de disco com o segundo mais espaço livre em disco. Quando as localizações primárias e secundárias atingem a reserva de espaço da unidade, o Configuration Manager seleciona outra unidade disponível com mais disco espaço livre para continuar o processo de cópia.  

> [!Tip]  
>  Para impedir que o Configuration Manager instale numa unidade específica, crie um ficheiro vazio designado **no_sms_on_drive** e copie-o para a pasta raiz da unidade antes de instalar o ponto de distribuição.  

Para obter mais informações, consulte [a biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library).


### <a name="bkmk_config-pull"></a> Ponto de distribuição de extração  

Quando **ativar este ponto de distribuição para extrair conteúdo de outros pontos de distribuição**, torna-se um ponto de distribuição de extração. Alterar o comportamento de como o ponto de distribuição obtém o conteúdo que distribui a ele. Para obter mais informações, consulte [utilizar um ponto de distribuição de extração](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

Para cada ponto de distribuição de extração que configurar, especifique um ou mais pontos de distribuição origem do qual ele obtém o conteúdo:  

-   Clique em **adicionar**e, em seguida, selecione uma ou mais dos pontos de distribuição disponível para ser origens.  

-   Utilize os botões de seta para ajustar a prioridade. Quando o ponto de distribuição de solicitação tenta transferir conteúdo, a prioridade é a ordem em que ele entra em contacto com os pontos de distribuição de origem. Contacta-lo pela primeira vez, pontos de distribuição com o valor mais baixo.  


### <a name="bkmk_config-pxe"></a> PXE  

Especifique se pretende ativar o PXE no ponto de distribuição. Utilize o PXE para iniciar implementações de sistema operacional nos clientes. Para obter mais informações sobre como utilizar o PXE no Configuration Manager, consulte [utilizar o PXE para implementar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).

Quando ativar o PXE, o Configuration Manager instala os serviços de implementação do Windows (WDS) no servidor, se necessário. O WDS é o serviço que efetua o arranque PXE para instalar sistemas operacionais. Depois de concluir o Assistente para criar o ponto de distribuição, o Configuration Manager instala um fornecedor no WDS que utiliza as funções de arranque PXE. 

A partir da versão 1806, pode ativar o PXE num ponto de distribuição sem WDS. 

Selecione a opção para **ativar suporte PXE para clientes**e, em seguida, configure as seguintes definições:  

 > [!Note]  
 > Clique em **Sim** no **analisar as portas necessárias para PXE** caixa de diálogo para confirmar que pretende ativar o PXE. O Configuration Manager configura automaticamente as portas predefinidas na firewall do Windows. Se utilizar uma firewall diferente, configure manualmente as portas.  
 >   
 > Se instalar o WDS e DHCP no mesmo servidor, configure o WDS para escutar numa porta diferente. Por predefinição, o DHCP escuta na mesma porta. Para obter mais informações, veja [Considerações sobre quando tiver o WDS e DHCP no mesmo servidor](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#BKMK_WDSandDHCP).  

- **Permitir que este ponto de distribuição responder a pedidos PXE recebidos**: Especifique se pretende ativar o WDS responder a pedidos de serviço PXE. Utilize esta definição para ativar e desativar o serviço sem remover a funcionalidade PXE do ponto de distribuição.  

- **Ativar suporte para computadores desconhecidos**: Especifique se pretende ativar o suporte para computadores que não gere o Configuration Manager. Para obter mais informações, consulte [preparar implementações de computadores desconhecidos](/sccm/osd/get-started/prepare-for-unknown-computer-deployments).  

- **Ativar o dispositivo de resposta PXE sem o serviço de implementação do Windows**: A partir da versão 1806, esta opção permite que um dispositivo de resposta do PXE no ponto de distribuição, o que não exige o WDS. Este dispositivo de resposta do PXE oferece suporte a redes IPv6. Se ativar esta opção num ponto de distribuição que já está preparado para PXE, o Configuration Manager suspende o serviço WDS. Se desativar esta opção, mas ainda **ativar suporte PXE para clientes**, em seguida, o ponto de distribuição permite que o WDS novamente.<!--1357580-->  

- **Exigir uma palavra-passe quando os computadores utilizam PXE**: Para fornecer segurança adicional às implementações PXE, especifique uma palavra-passe segura.  

- **Afinidade dispositivo / utilizador**: Especifique como pretende que o ponto de distribuição associe os utilizadores ao computador de destino para implementações de PXE. Escolha uma das seguintes opções:  

    - **Permitir afinidade de dispositivo / utilizador com aprovação automática**: Escolha esta definição para associar automaticamente os utilizadores ao computador de destino sem aguardar aprovação.  

    - **Permitir afinidade de dispositivo / utilizador com aprovação de administrador pendente**: Escolha esta definição para aguardar a aprovação de um utilizador administrativo antes dos utilizadores estão associados ao computador de destino.  

    - **Não permitir afinidade dispositivo / utilizador**: Escolha esta definição para especificar que os utilizadores não são associados ao computador de destino. Esta é a predefinição.  

     Para obter mais informações sobre a afinidade de dispositivo do utilizador, consulte [associar utilizadores e dispositivos à afinidade dispositivo / utilizador](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

- **Interfaces de rede**: Especifique que o ponto de distribuição responde a pedidos PXE de todas as interfaces de rede ou de interfaces de rede específicas. Se o ponto de distribuição responde a interfaces de rede específicas, em seguida, forneça o endereço MAC para cada interface de rede.  

    > [!Note]  
    > Quando alterar a interface de rede, reinicie o serviço WDS para se certificar de que guarda corretamente a configuração. A partir da versão 1806, ao utilizar o serviço de resposta do PXE, reinicie o **serviço de resposta do PXE do ConfigMgr** (SccmPxe).<!--SCCMDocs issue 642-->  

- **Especificar o atraso da resposta do servidor PXE (segundos)**: Ao utilizar múltiplos servidores PXE, especifique o tempo em que este ponto de distribuição com PXE ativado deve aguardar antes de responder a pedidos do computador. Por predefinição, o ponto de distribuição ativado por PXE do Configuration Manager responde imediatamente.  


### <a name="bkmk_config-multicast"></a> Multicast  

Especifique se pretende ativar o multicast no ponto de distribuição. As implementações multicast poupam a largura de banda de rede ao enviarem dados simultaneamente para vários clientes do Configuration Manager. Sem multicast, o servidor envia uma cópia dos dados para cada cliente através de uma ligação separada. Para obter mais informações sobre como utilizar multicast para implantação de sistema operacional, consulte [utilizar multicast para implementar o Windows através da rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).

Quando ativa o multicast, o Configuration Manager instala os serviços de implementação do Windows (WDS) no servidor, se necessário.  

Selecione a opção para **ativar multicast para enviar dados em simultâneo a múltiplos clientes**e, em seguida, configure as seguintes definições:  

- **Conta de ligação de multicast**: Especifique a conta a utilizar quando configurar ligações de base de dados do Configuration Manager para multicast. Para obter mais informações, consulte a [conta de ligação de Multicast](/sccm/core/plan-design/hierarchy/accounts#multicast-connection-account).  

- **Definições de endereço multicast**: Especifique os endereços IP para enviar dados para os computadores de destino. Por padrão, ele obtém o endereço IP de um servidor DHCP que tenha ativado para distribuir endereços multicast. Dependendo do ambiente de rede, pode especificar um intervalo de endereços IP do 239.0.0.0 por meio de 239.255.255.255.  

    > [!IMPORTANT]  
    >  Os endereços IP que configurar tem de ser acessíveis aos computadores de destino que pedem a imagem de sistema operacional. Certifique-se de que os routers e firewalls permitem tráfego multicast entre o computador de destino e o ponto de distribuição.  

- **Intervalo de portas UDP para multicast**: Especifique o intervalo de portas UDP que é utilizados para enviar dados para os computadores de destino.  

    > [!IMPORTANT]  
    >  As portas UDP devem ser acessíveis aos computadores de destino que pedem a imagem do SO. Certifique-se de que os routers e firewalls permitem tráfego multicast entre o computador de destino e o servidor do site.  

- **Máximo de clientes**: Especifique o número máximo de computadores de destino que pode transferir a imagem do SO a partir deste ponto de distribuição.  

- **Ativar multicast agendado**: Especifique como o Configuration Manager controla quando iniciar a implementação de sistemas operativos em computadores de destino. Configure as seguintes opções:  

    - **Atraso (minutos) de início de sessão**: Especifique o número de minutos que o Configuration Manager aguarda antes de ele responde ao primeiro pedido de implementação.  

    - **Tamanho mínimo de sessão (clientes)**: Especifique o número de pedidos têm de ser recebido antes do Configuration Manager começa a implementar o sistema operativo.  


> [!IMPORTANT]  
> A partir da versão 1806, para ativar e configurar o multicast no **Multicast** separador Propriedades do ponto de distribuição, o ponto de distribuição tem de utilizar o serviço de implementação do Windows.  
> - Se **ativar suporte PXE para clientes** e **ativar multicast para enviar dados em simultâneo a múltiplos clientes**, em seguida, não pode **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows** .  
> - Se **ativar suporte PXE para clientes** e **ativar um dispositivo de resposta PXE sem o serviço de implementação do Windows**, em seguida, não pode **ativar multicast para enviar dados em simultâneo a múltiplos clientes**  


### <a name="bkmk_config-group"></a> Relações de grupo  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando estiver a editar as propriedades de um ponto de distribuição anteriormente instalado.  

Gerir os grupos de pontos de distribuição em que este ponto de distribuição é membro.  

Para adicionar este ponto de distribuição como um membro a um grupo de pontos de distribuição existente, clique em **adicionar**. O adicionar à janela de grupos de pontos de distribuição, selecione um grupo existente e, em seguida, clique em **OK**.  

Para remover este ponto de distribuição de um grupo de pontos de distribuição, selecione o grupo na lista e, em seguida, clique em **remover**.  


### <a name="bkmk_config-content"></a> Conteúdo  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando estiver a editar as propriedades de um ponto de distribuição anteriormente instalado.  

Gerir o conteúdo distribuído ao ponto de distribuição. Selecione na lista de pacotes de implementação e efetuar as seguintes ações:  

- **Validar**: Inicie o processo para validar a integridade dos ficheiros de conteúdo para o software. Para ver os resultados do processo de validação de conteúdo, na **monitorização** área de trabalho, expanda **estado de distribuição**e, em seguida, selecione o **estado do conteúdo** nó. Para obter mais informações, consulte [validar os conteúdos](/sccm/core/servers/deploy/configure/deploy-and-manage-content#validate-content).   

- **Redistribuir**: Copia todos os ficheiros de conteúdo para o software selecionado para o ponto de distribuição e substitui os ficheiros existentes. Esta ação é normalmente utilizada para reparar ficheiros de conteúdo. Para obter mais informações, consulte [redistribuir conteúdos](/sccm/core/servers/deploy/configure/deploy-and-manage-content#redistribute-content).  

-   **Remover**: Remove os ficheiros de conteúdo para o software a partir do ponto de distribuição. Para obter mais informações, consulte [remover conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#remove-content).    


### <a name="bkmk_config-valid"></a> Validação de conteúdos  

Defina uma agenda para validar a integridade dos ficheiros de conteúdo no ponto de distribuição. Quando ativa a validação de conteúdos com base numa agenda, o Configuration Manager inicia o processo à hora agendada. Ele verifica todo o conteúdo no ponto de distribuição. Também pode configurar a prioridade de validação de conteúdos. Por predefinição, a prioridade é definida como **menor**. Aumentar a prioridade pode aumentar o processador e a utilização do disco no servidor durante o processo de validação, mas deverá ser concluída com mais rapidez. 

Para ver os resultados do processo de validação de conteúdo, na **monitorização** área de trabalho, expanda **estado de distribuição**e, em seguida, selecione o **estado do conteúdo** nó. Mostra o conteúdo para cada tipo de software, por exemplo, aplicativos, o pacote de atualização de software e de imagem de arranque.  

> [!WARNING]  
>  Embora especificar a agenda de validação de conteúdo utilizando a hora local para o computador, a consola do Configuration Manager mostra a agenda em UTC.  

Para obter mais informações, consulte [validar os conteúdos](/sccm/core/servers/deploy/configure/deploy-and-manage-content#validate-content).


### <a name="bkmk_config-boundary"></a> Grupos de limites  

Gerir os grupos de limites aos quais atribuir este ponto de distribuição. Adicione o ponto de distribuição para, pelo menos, um grupo de limites. Durante a implementação de conteúdos, os clientes devem ser num grupo de limites associado a um ponto de distribuição a utilizar esse ponto de distribuição como localização de origem para o conteúdo.

Configurar grupo de limites *relações* que definir quando e a quais grupos de limites um cliente pode reverter para encontrar o conteúdo. Para obter mais informações, consulte [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

Clique em **adicionar** e selecione um grupo de limites existentes na lista.

Para criar um novo grupo de limites para este ponto de distribuição, clique em **criar**. Para obter mais informações sobre como criar e configurar um grupo de limites, consulte [procedimentos para grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#procedures-for-boundary-groups).

Quando estiver a editar as propriedades de um ponto de distribuição anteriormente instalado, gerir a opção para **ativar para distribuição a pedido**. Esta opção permite ao Configuration Manager para distribuir automaticamente o conteúdo para este servidor quando um cliente solicita-lo. Para obter mais informações, consulte [distribuição de conteúdo a pedido](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).


### <a name="bkmk_config-sched"></a> agenda  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando estiver a editar as propriedades de um ponto de distribuição anteriormente instalado. 
> 
>  Este separador só está disponível quando edita as propriedades para um ponto de distribuição que seja remoto do servidor do site.  

Configure uma agenda que restringe quando o Configuration Manager podem transferir dados para o ponto de distribuição. Restringir os dados por prioridade ou fechar a ligação para períodos de tempo selecionado.   

Para restringir dados, selecione o período de tempo na grade e, em seguida, escolha uma das seguintes definições para **disponibilidade**:  

- **Aberto para todas as prioridades**: O Configuration Manager envia dados para o ponto de distribuição sem restrições. Esta definição é a predefinição para todos os períodos de tempo.  

- **Permitir média e alta prioridade**: O Configuration Manager envia dados de apenas média e alta prioridade para o ponto de distribuição.  

- **Permitir apenas alta prioridade**: O Configuration Manager envia apenas dados de alta prioridade para o ponto de distribuição.  

- **Fechado**: O Configuration Manager não envia quaisquer dados para o ponto de distribuição.  

Configurar o **prioridade de distribuição** de software no **definições de distribuição** separador de propriedades do software. 

> [!IMPORTANT]  
>  O agendamento baseia-se no fuso horário do site de envio, não é o ponto de distribuição.  


### <a name="bkmk_config-rate"></a> Limites de velocidade  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando estiver a editar as propriedades de um ponto de distribuição anteriormente instalado.  
>   
>  Este separador só está disponível quando edita as propriedades para um ponto de distribuição que seja remoto do servidor do site.  

Configure limites de velocidade para controlar a largura de banda de rede utilizadas pelo Configuration Manager para transferir conteúdo para o ponto de distribuição. Pode escolher uma das seguintes opções:  

- **Ilimitada ao enviar para este destino**: O Gestor de configuração envia conteúdo ao ponto de distribuição sem restrições de limite de taxa. Esta é a predefinição.  

- **Modo de impulso**: Esta opção especifica o tamanho dos blocos de dados que o servidor do site envia para o ponto de distribuição. Também pode especificar um atraso de tempo entre o envio de cada bloco de dados. Utilize esta opção quando tiver de enviar dados através de uma ligação de rede muito pouca largura de banda para o ponto de distribuição. Por exemplo, tem limitações para enviar 1 KB de dados a cada cinco segundos, independentemente da velocidade da ligação ou da respetiva utilização num determinado momento.  

- **Limitado a velocidades de transferência máximas especificadas por hora**: Especifique esta definição para que um site envie dados para um ponto de distribuição utilizando apenas a percentagem de tempo que configurar. Quando utiliza esta opção, o Configuration Manager não identifica a largura de banda disponível da rede. Em vez disso, ele divide o tempo que pode enviar dados. O servidor envia dados para um curto período de tempo, o que é seguido por períodos de tempo quando os dados não são enviados. Por exemplo, se definir **largura de banda disponível do limite** ao **50%**, Configuration Manager transmite dados durante um período de tempo seguido por um período de tempo quando não são enviados dados igual. A quantidade real de dados ou o tamanho do bloco de dados, não é gerido. Ele gerencia apenas a quantidade de tempo durante o qual são enviados dados.  
