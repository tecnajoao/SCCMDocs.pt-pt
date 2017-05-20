---
title: "Gerir pontos de distribuição | Documentos do Microsoft"
description: "Aloje o conteúdo (ficheiros e software) que implemente nos dispositivos e utilizadores através da utilização de pontos de distribuição. Eis como instalar e configurá-los."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 8728d9f2ae63282a8f58b20105e488fb1a5ef55b
ms.openlocfilehash: 4c94e4de5bbfe621492e8682c9424a48eb38196d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>Instalar e configurar pontos de distribuição para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*
 
Instalar pontos de distribuição do System Center Configuration Manager para alojar o conteúdo (ficheiros e software) que pode implementar em dispositivos e utilizadores. Também pode criar distribuição grupos de pontos que simplificam como gerir pontos de distribuição e, como distribuir os conteúdos aos pontos de distribuição.  

 Quando lhe *instalar um novo ponto de distribuição* (utilizando o Assistente de instalação) ou *gerir as propriedades do ponto de distribuição pré-existente* (editando as propriedades do ponto de distribuição), pode configurar a maior parte das definições de ponto de distribuição. Algumas definições estão disponíveis apenas quando estiver a instalar ou editar, mas não ambos:  

-   Definições que estão disponíveis apenas quando estiver a instalar um ponto de distribuição:  

    -   **Permitir que o Configuration Manager para instalar o IIS no computador do ponto de distribuição**

    -   **Configurar definições de espaço de unidade para o ponto de distribuição**  

-   Definições que estão disponíveis apenas quando estiver a editar as propriedades de um ponto de distribuição:  

    -   **Gerir relações de grupo de ponto de distribuição**  

    -   **Visualização de conteúdo implementada no ponto de distribuição**  

    -   **Configurar limites de velocidade para transferências de dados para pontos de distribuição**  

    -   **Configurar as agendas para as transferências de dados para pontos de distribuição**  

##  <a name="bkmk_install"></a>Instalar um ponto de distribuição  
 Tem de designar um servidor de sistema de sites como um ponto de distribuição antes do conteúdo pode ser disponibilizado a computadores cliente. Pode adicionar a função de site do ponto de distribuição para um novo servidor de sistema de sites ou adicionar a função de site a um servidor de sistema de sites existente.  

 Quando instala um novo ponto de distribuição, pode utilizar um Assistente de instalação que explica-lhe como as definições disponíveis. Antes de começar, considere o seguinte:  

-   Tem de ter as seguintes permissões de segurança para criar e configurar um ponto de distribuição:  

    -   **Leitura** para o **ponto de distribuição** objeto  

    -   **Copiar para ponto de distribuição** para o **ponto de distribuição** objeto  

    -   **Modificar** para o **Site** objeto  

    -   **Gerir certificados para a implementação do sistema operativo** para o **Site** objeto  

-   Serviços de informação Internet (IIS) tem de ser instalado no servidor que irá alojar o ponto de distribuição. Ao instalar a função de sistema de sites, o Configuration Manager pode instalar e configurar o IIS para si.  

Utilize os seguintes procedimentos básicos para instalar ou alterar um ponto de distribuição. Para obter detalhes sobre as opções de configuração disponíveis, consulte o [configurar um ponto de distribuição](#bkmk_configs) secção deste tópico.  

#### <a name="to-install-a-distribution-point"></a>Para instalar um ponto de distribuição  

1.  Na consola do Configuration Manager, escolha **administração** >  **configuração do Site** > **servidores e funções de sistema de sites**.  

2.  Adicione a função de sistema de sites de ponto de distribuição a um servidor de sistema de sites novo ou existente:  

    -   **Novo servidor de sistema de sites**: No **base** separador o **criar** grupo, selecione **criar servidor do sistema de sites**. Abre o Assistente para Criar Servidor do Sistema de Sites.  

    -   **Servidor de sistema de sites existente**: Selecione o servidor no qual pretende instalar a função de sistema de sites de ponto de distribuição. Quando escolher um servidor, é apresentada uma lista das funções de sistema de sites que já estão instaladas no servidor no painel de resultados.  

         No **base** separador o **servidor** grupo, selecione **Adicionar função de sistema de sites**. Abre o Assistente para Adicionar Funções ao Sistema de Sites.  

3.  Na página **Geral** , especifique as definições gerais para o servidor de sistema de sites. Quando adiciona o ponto de distribuição a um servidor de sistema de sites existente, verifique os valores que foram anteriormente configurados.  

4.  No **seleção da função do sistema** página, selecione **ponto de distribuição** da lista de funções disponíveis e, em seguida, escolha **seguinte**.  

5.  Para as páginas subsequentes do assistente, consulte as informações de [configurar um ponto de distribuição](#bkmk_configs) secção.  

     Por exemplo, se pretender instalar o ponto de distribuição como um ponto de distribuição de solicitação, escolher **ativar este ponto de distribuição para obter conteúdo a partir de outros pontos de distribuição** e, em seguida, efetue as configurações adicionais que necessitam de pontos de distribuição de solicitação.  

6.  Depois de concluir o assistente, a função de site do ponto de distribuição é adicionada ao servidor de sistema do site.  

#### <a name="to-change-a-distribution-point"></a>Para alterar um ponto de distribuição  

1.  Na consola do Configuration Manager, escolha **administração** >  **pontos de distribuição**e, em seguida, selecione o ponto de distribuição que pretende configurar.  

2.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

3.  Utilize as informações de [configurar um ponto de distribuição](#bkmk_configs) secção quando está a editar as propriedades do ponto de distribuição.  

4.  Depois de efetuar as alterações que pretende, guarde as suas definições e fechar as propriedades do ponto de distribuição.  

##  <a name="bkmk_manage"></a>Gerir grupos de pontos de distribuição  
 Grupos de pontos de distribuição permitem um agrupamento lógico de pontos de distribuição para distribuição de conteúdos. Pode utilizar estes grupos para gerir e monitorizar conteúdos a partir de uma localização central de pontos de distribuição que abranjam vários sites. Tenha em atenção o seguinte:

-   Pode adicionar um ou mais pontos de distribuição a partir de qualquer site na hierarquia para um grupo de pontos de distribuição.  

-   Pode adicionar um ponto de distribuição a mais do que um grupo de pontos de distribuição.  

-   Quando distribui conteúdo a um grupo de pontos de distribuição, o Configuration Manager distribui o conteúdo por todos os pontos de distribuição que são membros do grupo de pontos de distribuição.  

-   Se adicionar um ponto de distribuição para o grupo de pontos de distribuição após uma distribuição de conteúdo inicial, o Configuration Manager distribui automaticamente o conteúdo para o novo membro do ponto de distribuição.  

-   Pode associar uma coleção um grupo de pontos de distribuição. Quando distribui conteúdo a essa coleção, o Configuration Manager determina que grupos de pontos de distribuição estão associados à coleção. Os conteúdos são posteriormente distribuídos a todos os pontos de distribuição que sejam membros desses grupos de pontos de distribuição.  

    > [!NOTE]  
    >  Após distribuir conteúdos a uma coleção, se, em seguida, associar a coleção de um novo grupo de pontos de distribuição, necessitará de redistribuir os conteúdos à coleção antes do conteúdo é distribuído para o novo grupo de pontos de distribuição.  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>Para criar e configurar um novo grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, escolha **administração** > **grupos de pontos de distribuição**.  

2.  No **base** separador o **criar** grupo, selecione **criar grupo**.  

3.  Introduza o nome e descrição para o grupo de pontos de distribuição.  

4.  No **coleções** separador, escolha **adicionar**, selecione as coleções que pretende associar o grupo de pontos de distribuição e, em seguida, escolha **OK**.  

5.  No **membros** separador, escolha **adicionar**, selecione os pontos de distribuição que pretende adicionar como membros do grupo de pontos de distribuição e, em seguida, escolha **OK**.  

6.  Escolher **OK** para criar o grupo de pontos de distribuição.  

#### <a name="to-add-distribution-points-and-associate-collections-with-an-existing-distribution-point-group"></a>Para adicionar pontos de distribuição e associar coleções a um grupo de pontos de distribuição existente  

1.  Na consola do Configuration Manager, escolha **administração** > **grupos de pontos de distribuição**.  

2.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

3.  No **coleções** separador, escolha **adicionar** para selecionar as coleções que pretende associar o grupo de pontos de distribuição e, em seguida, escolha **OK**.  

4.  No **membros** separador, escolha **adicionar** para selecionar os pontos de distribuição que pretende adicionar como membros do grupo de pontos de distribuição e, em seguida, selecione **OK**.  

5.  Escolher **OK** para guardar as alterações ao grupo de pontos de distribuição.  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>Para adicionar distribuição selecionados aponta para um novo grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, escolha **administração** > **pontos de distribuição**e, em seguida, selecione os pontos de distribuição que pretende adicionar ao novo grupo de pontos de distribuição.  

2.  No **base** separador o **ponto de distribuição** grupo, expanda **adicionar itens selecionados**e, em seguida, escolha **adicionar itens selecionados ao novo grupo de pontos de distribuição**.  

3.  Introduza o nome e descrição para o grupo de pontos de distribuição.  

4.  No **coleções** separador, escolha **adicionar** para selecionar as coleções que pretende associar o grupo de pontos de distribuição e, em seguida, escolha **OK**.  

5.  No **membros** separador, certifique-se de que pretende que o Configuration Manager para adicionar os pontos de distribuição listados como membros do grupo de pontos de distribuição. Escolher **adicionar** para adicionar os pontos de distribuição e, em seguida, escolha **OK**.  

6.  Escolher **OK** para criar o grupo de pontos de distribuição.  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>Para adicionar distribuição selecionados pontos a grupos de pontos de distribuição existentes  

1.  Na consola do Configuration Manager, escolha **administração** > **pontos de distribuição**e, em seguida, selecione os pontos de distribuição que pretende adicionar ao novo grupo de pontos de distribuição.  

2.  No **base** separador o **ponto de distribuição** grupo, expanda **adicionar itens selecionados**e, em seguida, escolha **adicionar itens selecionados a grupos de pontos de distribuição existentes**.  

3.  No **grupos de pontos de distribuição disponíveis**, selecione os grupos de pontos de distribuição aos quais os pontos de distribuição selecionados são adicionados como membros e, em seguida, selecione **OK**.  

##  <a name="bkmk_configs"></a>Configurar um ponto de distribuição  
 Pontos de distribuição individuais suportam uma variedade de configurações diferentes. No entanto, nem todos os tipos de pontos de distribuição suportam todas as configurações. Por exemplo, pontos de distribuição baseado na nuvem não suportarem implementações de conteúdos que estejam ativadas para o PXE ou multicast. Pode encontrar informações sobre as limitações específicas nos seguintes tópicos:  

-   [Utilizar um ponto de distribuição baseado na nuvem com o System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [Utilizar um ponto de distribuição de solicitação com o System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

As secções seguintes descrevem as configurações que pode selecionar quando está a instalar um novo ponto de distribuição ou editando as propriedades de um ponto de distribuição existente.  

### <a name="general"></a>Geral  
 Configure as definições de ponto de distribuição gerais:  

-   **Instalar e configurar o IIS se exigido pelo Configuration Manager**: Escolha esta definição para permitir que o Configuration Manager instalar e configurar o IIS no servidor se não estiver já instalado. O IIS tem de ser instalado em todos os pontos de distribuição. Se o IIS não está instalado no servidor e não Escolha esta definição, deve instalar o IIS antes do ponto de distribuição pode ser instalado com êxito.  

    > [!NOTE]  
    >  Esta opção só está disponível quando estiver a instalar um novo ponto de distribuição.  

- **Ativar e configurar o BranchCache para este ponto de distribuição**: Escolha esta definição para permitir ao configurar o Windows BranchCache no servidor de ponto de distribuição do Configuration Manager. Para obter mais informações sobre como utilizar o Windows BranchCache com o System Center Configuration Manager, consulte o artigo [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#a-namebkmkbranchcachea-branchcache) no *funcionalidades de suporte para Windows e as redes no System Center Configuration Manager*.

-   **Configurar a forma como os dispositivos cliente comunicam com o ponto de distribuição**: Existem vantagens e desvantagens para utilização de HTTP e HTTPS. Para obter mais informações, consulte "Melhores práticas de segurança para gestão de conteúdo" em [os conceitos fundamentais para gestão de conteúdo no System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   **Permitir a ligação anónima dos clientes**: Esta definição especifica se o ponto de distribuição irá permitir ligações anónimas dos clientes do Configuration Manager para a biblioteca de conteúdos.  

    > [!IMPORTANT]  
    >  Reparação de uma aplicação do Windows Installer pode falhar num cliente quando utiliza esta definição.  
    >   
    >  Quando implementa uma aplicação do Windows Installer num cliente do Configuration Manager, o Configuration Manager transfere o ficheiro para a cache local no cliente. Os ficheiros são eventualmente removidos depois da conclusão da instalação.
    >  
    >  O cliente do Configuration Manager atualiza a lista de origem do Windows Installer para as aplicações do Windows Installer instaladas com o caminho de conteúdo da biblioteca de conteúdos em pontos de distribuição associados. Mais tarde, se iniciar a ação de reparação a partir de adicionar ou remover programas num cliente do Configuration Manager, o MSIExec tenta aceder ao caminho de conteúdo utilizando um utilizador anónimo.  
    >   
    >  No entanto, pode instalar a atualização descrita no artigo da Base de dados de Conhecimento Microsoft [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) e, em seguida, modificar uma chave de registo para alterar este comportamento.  
    >   
    >  Após a atualização é instalada nos clientes, o MSIExec acederá ao caminho de conteúdo utilizando a conta de utilizador com sessão iniciada quando não optar o **permitir a ligação anónima dos clientes** definição.  

-   **Criar um certificado autoassinado ou importar um certificado de cliente de infraestrutura de chaves públicas (PKI) para o ponto de distribuição**: O certificado tem os seguintes fins:  

    -   Autentica o ponto de distribuição para um ponto de gestão antes do ponto de distribuição envia mensagens de estado.  

    -   Quando seleciona o **ativar suporte PXE para clientes** caixa o **definições do PXE** página, o certificado é enviado para computadores que realizam um arranque PXE para que se possam ligar a um ponto de gestão durante a implementação do sistema operativo.  

    Quando todos os pontos de gestão no site estão configurados para HTTP, crie um certificado autoassinado. Quando os pontos de gestão estiverem configurados para HTTPS, importe um certificado PKI de cliente.  

    Para importar o certificado, navegue para um ficheiro de Public Key Cryptography Standard (PKCS #12) que tenha um certificado PKI com os seguintes requisitos para o Configuration Manager:  

    -   A utilização prevista deve incluir a autenticação de cliente.  

    -   A chave privada tem de ser ativada para ser exportada.  

    > [!TIP]  
    >  Não não existem requisitos específicos para o requerente do certificado ou nome alternativo do requerente (SAN), e pode utilizar o mesmo certificado para vários pontos de distribuição.  

     Para obter mais informações sobre os requisitos de certificado, veja [Requisitos de certificado PKI para o System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     Para um exemplo de implementação deste certificado, consulte a secção "Implementar o cliente certificado para pontos de distribuição" [exemplo passo a passo de implementação de PKI certificados para o System Center Configuration Manager: Autoridade de certificação do Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

-   **Ativar conteúdo pré-configurado para este ponto de distribuição**: Escolha esta definição para ativar o ponto de distribuição para conteúdo pré-configurado. Quando esta definição está selecionada, pode configurar o comportamento de distribuição quando distribuir conteúdos. Pode optar por sempre efetue um dos seguintes procedimentos:

 - Pré-configurar o conteúdo no ponto de distribuição.
 - Pré-configurar o conteúdo inicial para o pacote, mas utilize o processo normal de distribuição de conteúdo caso existam atualizações ao conteúdo.
 - Utilize o processo normal de distribuição de conteúdo para o conteúdo no pacote.  

### <a name="drive-settings"></a>Definições de unidade  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando estiver a instalar um novo ponto de distribuição.  

Especifique as definições de unidade para o ponto de distribuição. Pode configurar até duas unidades de disco para a biblioteca de conteúdos e duas unidades de disco para a partilha de pacote. O Configuration Manager possa utilizar unidades adicionais quando as duas primeiras atingem a reserva do espaço na unidade configurada. O **definições de unidade** página configura a prioridade para as unidades de disco e a quantidade de espaço livre em disco que sobra em cada unidade de disco.  

-   **(MB) de reserva do espaço na unidade**: O valor que configurar para esta definição determina a quantidade de espaço livre numa unidade antes do Configuration Manager escolher uma unidade diferente e continuar o processo de cópia para essa unidade. Ficheiros de conteúdo podem abranger várias unidades.  

-   **Localizações de conteúdo**: Especifique as localizações de conteúdos para a partilha de biblioteca e do pacote de conteúdo. O Configuration Manager copia conteúdo para a localização de conteúdos primária até a quantidade de espaço livre atingir o valor especificado para **reserva de espaço na unidade (MB)**. Por predefinição, as localizações de conteúdo estão definidas como **automática**. A localização de conteúdo principal está definida para a unidade de disco que tem mais espaço de disco durante a instalação e a localização secundária é atribuída à unidade de disco que tem a maioria do segundo espaço livre em disco. Quando as unidades principais e secundárias atingem a reserva do espaço na unidade, o Configuration Manager seleciona uma outra unidade disponível com mais disco espaço livre e continua o processo de cópia.  

> [!NOTE]  
>  Para impedir que o Configuration Manager instalar numa unidade específica, crie um ficheiro vazio designado **no_sms_on_drive** e copie-o para a pasta de raiz da unidade antes de instalar o ponto de distribuição.  

### <a name="pull-distribution-point"></a>Ponto de distribuição de solicitação  
Quando escolher **ativar este ponto de distribuição para obter conteúdo a partir de outros pontos de distribuição**, alterar o comportamento da forma como esse computador obtém os conteúdos distribuir ao ponto de distribuição. Torna-se um ponto de distribuição de solicitação.  

Para cada ponto de distribuição de solicitação que configurar, tem de especificar um ou mais pontos de distribuição origem a partir do qual o ponto de distribuição de solicitação obtém o conteúdo:  

-   Escolher **adicionar**e, em seguida, selecione um ou mais dos pontos de distribuição disponíveis para serem pontos de distribuição de origem.  

-   Escolher **remover** para remover o ponto de distribuição selecionado como um ponto de distribuição de origem.  

-   Utilize os botões de seta para ajustar a ordem na qual a distribuição de solicitação aponte contactos quando o ponto de distribuição de solicitação tenta transferir conteúdo de pontos de distribuição de origem. Pontos de distribuição com o valor mais baixo são contactados pela primeira vez.  

### <a name="pxe"></a>PXE  
Especifique se pretende ativar o PXE no ponto de distribuição. Quando ativa o PXE, Configuration Manager instala os serviços de implementação do Windows no servidor, se necessário. Serviços de implementação do Windows é o serviço que efetua o arranque PXE para instalar sistemas operativos. Depois de concluir o Assistente para criar o ponto de distribuição, o Configuration Manager instala um fornecedor nos serviços de implementação do Windows que utiliza as funções de arranque PXE.  

Quando escolher **ativar suporte PXE para clientes**, configure as seguintes definições:  

-   **Permitir que este ponto de distribuição responder a pedidos PXE recebidos**: Especifique se pretende ativar os serviços de implementação do Windows, de modo a que responda a pedidos de serviço PXE. Utilize esta caixa para ativar e desativar o serviço sem remover a funcionalidade PXE a partir do ponto de distribuição.  

-   **Ativar suporte para computadores desconhecidos**: Especifique se pretende ativar o suporte para computadores que não gere a Configuration Manager.  

-   **Exigir uma palavra-passe quando os computadores utilizam PXE**: Para fornecer segurança adicional para as implementações de PXE, especifique uma palavra-passe.  

-   **Afinidade dispositivo / utilizador**: Especifique como pretende que o ponto de distribuição associe utilizadores ao computador de destino para implementações de PXE. Escolha uma das seguintes opções:  

    -   **Permitir afinidade de dispositivo / utilizador com aprovação automática**: Escolha esta definição para associar automaticamente os utilizadores ao computador de destino sem aguardar aprovação.  

    -   **Permitir afinidade de dispositivo / utilizador com aprovação do administrador pendente**: Escolha esta definição para aguardar a aprovação de um utilizador administrativo antes dos utilizadores estão associados ao computador de destino.  

    -   **Não permitir afinidade dispositivo / utilizador**: Escolha esta definição para especificar que os utilizadores não estão associados ao computador de destino.  

     Para obter mais informações sobre a afinidade de dispositivo de utilizador, veja [Associar utilizadores e dispositivos à afinidade de dispositivo do utilizador no System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Interfaces de rede**: Especifique que o ponto de distribuição responde a pedidos PXE de todas as interfaces de rede ou de interfaces de rede específicas. Se o ponto de distribuição responde a interfaces de rede específico, tem de fornecer o endereço MAC para cada interface de rede.  

-   **Especificar o atraso da resposta do servidor PXE (segundos)**: Especifique em segundos o tempo de atraso do ponto de distribuição antes de responder a pedidos do computador quando são utilizados vários pontos de distribuição preparados para PXE. Por predefinição, o ponto de serviço do Configuration Manager PXE responde primeiro a pedidos PXE.  

> [!NOTE]  
>  Pode utilizar o protocolo PXE para iniciar as implementações do sistema operativo para computadores de cliente do Configuration Manager. Configuration Manager utiliza a função de site do ponto de distribuição com PXE ativado para iniciar o processo de implementação do sistema operativo. O ponto de distribuição com PXE ativado deve ser configurado para:
>
> 1. Responda a pedidos de arranque PXE, que facilitam a clientes do Configuration Manager na rede.
> 2. Interagir com a infraestrutura do Configuration Manager para determinar as ações de implementação adequadas.  

### <a name="multicast"></a>Multicast  
Especifique se pretende ativar o multicast no ponto de distribuição. Quando ativa o multicast, Configuration Manager instala os serviços de implementação do Windows no servidor, se necessário.  

Quando seleciona o **ativar o multicast para enviar dados em simultâneo a múltiplos clientes** caixa, configure as seguintes definições:  

-   **Conta de ligação de multicast**: Especifique a conta a utilizar quando configurar ligações de base de dados do Configuration Manager para multicast.  

-   **Definições de endereço multicast**: Especifique os endereços IP para enviar dados para os computadores de destino. Por predefinição, o endereço IP é obtido a partir de um servidor DHCP que se encontra ativado para distribuir endereços multicast. Dependendo do ambiente de rede, pode especificar um intervalo de endereços IP a partir do 239.0.0.0 através de 239.255.255.255.  

    > [!IMPORTANT]  
    >  Os endereços IP que configura tem de ser acessíveis aos computadores de destino que pedem a imagem do sistema operativo. Certifique-se de que os routers e firewalls permitem tráfego multicast entre o computador de destino e o servidor do site.  

-   **Intervalo de portas UDP para multicast**: Especifica as portas do intervalo do utilizador datagrama Protocol (UDP) que são utilizadas para enviar dados para os computadores de destino.  

    > [!IMPORTANT]  
    >  As portas UDP devem ser acessíveis aos computadores de destino que pedem a imagem do sistema operativo. Certifique-se de que os routers e firewalls permitem tráfego multicast entre o computador de destino e o servidor do site.  

-   **Velocidade de transferência do cliente**: Selecione a velocidade de transferência que é utilizada para transferir dados para os computadores de destino.  

-   **Máximo de clientes**: Especifique o número máximo de computadores de destino que pode transferir o sistema operativo a partir deste ponto de distribuição.  

-   **Ativar multicast agendado**: Especifique como do Configuration Manager controla quando iniciar a implementação de sistemas operativos em computadores de destino. Configure as seguintes opções:  

    -   **Atraso (minutos) de início de sessão**: Especifique o número de minutos que o Configuration Manager aguarda antes de ter responde ao primeiro pedido de implementação.  

    -   **Tamanho mínimo da sessão (clientes)**: Especifique o número de pedidos deve ser recebido antes de iniciar o Configuration Manager implementar o sistema operativo.  

> [!NOTE]  
>  As implementações multicast conservam a largura de banda de rede ao enviarem dados simultaneamente para vários clientes do Configuration Manager em vez de enviarem uma cópia dos dados a cada cliente através de uma ligação separada. Para mais informações sobre a utilização de multicast para implementação do sistema operativo, consulte o artigo [utilize o multicast para implementar o Windows através da rede com o System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="group-relationships"></a>Relações de grupo  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando está a editar as propriedades de um ponto de distribuição previamente instalado.  

Gerir os grupos de pontos de distribuição nos quais este ponto de distribuição é um membro.  

Para adicionar este ponto de distribuição como membro a um grupo de pontos de distribuição existente, selecione **adicionar**. Selecione um grupo de pontos de distribuição existente na lista de **adicionar a grupos de pontos de distribuição** diálogo caixa e, em seguida, selecione **OK**.  

Para remover este ponto de distribuição a partir de um grupo de pontos de distribuição, selecione o grupo de pontos de distribuição na lista e, em seguida, selecione **remover**.  

### <a name="content"></a>Conteúdo  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando está a editar as propriedades de um ponto de distribuição previamente instalado.  

Gerir o conteúdo que tenha sido distribuído ao ponto de distribuição. O **pacotes de implementação** secção fornece uma lista dos pacotes distribuídos a este ponto de distribuição. Pode selecionar um pacote a partir da lista e efetuar as seguintes ações:  

-   **Validar**: Inicia o processo para validar a integridade dos ficheiros de conteúdo no pacote. Para ver os resultados do processo de validação de conteúdo, no **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, escolha o **estado do conteúdo** nó.  

-   **Redistribuir**: Copia todos os ficheiros de conteúdo no pacote para o ponto de distribuição e substitui os ficheiros existentes. Normalmente, utilize esta ação para reparar ficheiros de conteúdo no pacote.  

-   **Remover**: Remove os ficheiros de conteúdo do ponto de distribuição para o pacote.  

### <a name="content-validation"></a>Validação de conteúdos  
Especifique se pretende definir uma agenda para validar a integridade dos ficheiros de conteúdo no ponto de distribuição. Quando ativa a validação de conteúdos com base numa agenda, Configuration Manager inicia o processo à hora agendada e todo o conteúdo no ponto de distribuição é verificado. Também pode configurar a prioridade da validação de conteúdo. Por predefinição, a prioridade é definida como **mais baixa**.  

Para ver os resultados do processo de validação de conteúdo, no **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, escolha o **estado do conteúdo** nó. É apresentado o conteúdo de cada tipo de pacote (por exemplo, aplicação, pacote de atualização de software e imagem de arranque).  

> [!WARNING]  
>  Apesar de especificar a agenda de validação de conteúdo utilizando a hora local para o computador, a consola do Configuration Manager mostra a agenda em UTC.  

### <a name="boundary-group"></a>Grupo de limites  
Gira os grupos de limites para os quais é atribuído este ponto de distribuição. Pode associar grupos de limites um ponto de distribuição. Durante a implementação de conteúdos, os clientes devem estar no grupo de limites com o ponto de distribuição para utilizar como localização de origem para o conteúdo.

Além disso,

- Antes de versão 1610, pode verificar o **permitir que os clientes utilizam este sistema de sites como localização de origem de contingência para conteúdo** caixa para permitir que os clientes fora destes limites grupos revertam e utilizem o ponto de distribuição como localização de origem de conteúdo quando não houver outros pontos de distribuição estão disponíveis. Para mais informações sobre grupos de limites, consulte o artigo [grupos de limites para versões 1511, 1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606). Para pontos de distribuição preferenciais, consulte o artigo [os conceitos fundamentais para gestão de conteúdo no System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).

- Com a versão 1610 ou posterior, pode configura o grupo de limites *relações* que definam os grupos de limites e quando um cliente pode reverter para localizar conteúdo. Para obter mais informações, consulte o artigo [grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


### <a name="schedule"></a>Agenda  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando está a editar as propriedades de um ponto de distribuição previamente instalado.  

> [!TIP]  
>  Este separador só está disponível quando edita as propriedades de um ponto de distribuição que seja remoto do computador do servidor do site.  

 Especifique se pretende configurar uma agenda que restringe quando o Configuration Manager pode transferir dados para o ponto de distribuição.  

> [!IMPORTANT]  
>  A agenda baseia-se no fuso horário do site de envio, não o ponto de distribuição.  

Para restringir dados, selecione o período de tempo e, em seguida, escolha uma das seguintes definições para **disponibilidade**:  

-   **Aberto para todas as prioridades**: Especifica que o Configuration Manager envia dados para o ponto de distribuição sem restrições.  

-   **Permitir média e alta prioridade**: Especifica que o Configuration Manager envia apenas dados de prioridade média e alta prioridade para o ponto de distribuição.  

-   **Permitir alta prioridade apenas**: Especifica que o Configuration Manager envia dados de apenas alta prioridade para o ponto de distribuição.  

-   **Fechado**: Especifica que o Configuration Manager não envia quaisquer dados para o ponto de distribuição.  

Pode restringir os dados por prioridade ou fechar a ligação para períodos de tempo selecionados.  

### <a name="rate-limits"></a>Limites de velocidade  

> [!NOTE]  
>  Estas opções estão disponíveis apenas quando está a editar as propriedades de um ponto de distribuição previamente instalado.  

> [!TIP]  
>  Este separador só está disponível quando edita as propriedades de um ponto de distribuição que seja remoto do computador do servidor do site.  

Especifique se pretende configurar limites de velocidade para controlar a largura de banda de rede que está a ser utilizado ao Configuration Manager está a transferir conteúdo para o ponto de distribuição. Pode selecionar de entre as seguintes opções:  

-   **Ilimitado quando envia para este destino**: Esta opção especifica que o Configuration Manager envia dados para o ponto de distribuição sem restrições de limite de velocidade.  

-   **Modo de impulso**: Esta opção especifica o tamanho dos blocos de dados que são enviadas para o ponto de distribuição. Também pode especificar um atraso de tempo entre o envio de cada bloco de dados. Utilize esta opção quando tiver de enviar dados através de uma ligação de rede de muito baixa largura de banda para o ponto de distribuição. Por exemplo, poderá ter limitações para enviar 1 KB de dados a cada cinco segundos, independentemente da velocidade da ligação ou da sua utilização num determinado momento.  

-   **Limitado a velocidades de transferência máximas especificadas por hora**: Especifique esta definição para que um site envie dados para um ponto de distribuição utilizando apenas a percentagem de tempo que configurar. Quando utilizar esta opção, o Configuration Manager não identifica a largura de banda disponível da rede, mas em vez disso, divide o tempo que pode enviar dados. Em seguida, os dados são enviados por um curto bloco de tempo, o que é seguido de blocos de tempo quando não são enviados dados. Por exemplo, se a velocidade máxima for definida **50%**, Configuration Manager transmite dados durante um período de tempo seguido por um período de tempo quando são enviados sem dados igual. A quantidade real de dados ou o tamanho do bloco de dados não são geridos. Em vez disso, apenas é gerida a quantidade de tempo durante a qual são enviados dados.  

