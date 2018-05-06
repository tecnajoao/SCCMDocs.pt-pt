---
title: Configurar a deteção
titleSuffix: Configuration Manager
description: Configure métodos de deteção para localizar recursos para gerir a partir da sua rede, o Active Directory e o Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e7ac10fdc08569e519468633f30548c5c76b5838
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>Configurar métodos de deteção para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Configure métodos de deteção para localizar recursos para gerir a partir da sua rede, o Active Directory e o Azure Active Directory (Azure AD). Ative o primeiro e, em seguida, configurar cada método que pretende utilizar para pesquisar o seu ambiente. Também pode desativar um método utilizando o mesmo procedimento utilizado para o ativar. São as únicas exceções a este processo de deteção de Heartbeat e deteção de servidores:  

-   Por predefinição, **deteção de Heartbeat** já está ativada quando instala um site primário do Configuration Manager. Este é configurado para ser executada com base numa agenda básico. Mantenha a deteção de Heartbeat ativada. Garante que os registos de dados de deteção (DDR) para os dispositivos estão atualizados. Para obter mais informações sobre a deteção de Heartbeat, consulte [sobre a deteção de Heartbeat](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

-   **Deteção de servidores** é um método de deteção automática. Encontra computadores que utilizam como sistemas de sites. Não é possível configurar ou desativá-lo.  

### <a name="enable-a-configurable-discovery-method"></a>Ativar um método de deteção configuráveis  
 > [!NOTE]  
 > As seguintes informações não se aplicam ao Azure AD User Discovery. Em vez disso, consulte [configurar o Azure AD User Discovery](#azureaadisc) posteriormente neste artigo.

1.  Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **configuração da hierarquia**e, em seguida, selecione **métodos de deteção**.  

2.  Selecione o método de deteção para o site onde pretende ativar a deteção.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**. Em seguida, no **geral** separador, verifique o **ativar &lt;método de deteção\>**  caixa.  

     Se esta caixa já está selecionada, pode desativar o método de deteção desmarcando a caixa.  

4.  Escolha **OK** para guardar a configuração.  



##  <a name="BKMK_ConfigADForestDisc"></a> Configurar a deteção de florestas do Active Directory  
Para concluir a configuração da deteção de floresta do Active Directory, tem de configurar as definições em duas localizações:  

-   No **métodos de deteção** nós, pode:

    - Ative este método de deteção.
    - Defina uma agenda de consulta.
    - Selecione se a deteção automática cria limites para os sites do Active Directory e sub-redes que Deteta.  

-   No **florestas do Active Directory** nós, pode:

    - Adicione florestas que pretenda detetar.
    - Ative a deteção de sites e sub-redes nessa floresta do Active Directory.
    - Configure as definições que permitem sites do Configuration Manager publicar as suas informações de site na floresta.
    - Atribua uma conta a utilizar como conta de floresta do Active Directory para cada floresta.  

Utilize os procedimentos seguintes para ativar a deteção de floresta do Active Directory e configurar florestas individuais para utilização com deteção de floresta do Active Directory.  

#### <a name="to-enable-active-directory-forest-discovery"></a>Para ativar a deteção de floresta do Active Directory  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração da hierarquia**e, em seguida, escolha **métodos de deteção**.  

2.  Selecione o método de deteção de floresta do Active Directory para o site onde pretende configurar a deteção.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

4.  No **geral** separador, selecione a caixa para ativar a deteção. Ou pode configurar a deteção agora e, em seguida, regressar para ativar a deteção mais tarde.  

5.  Especifique as opções para criar limites de sites para localizações detetadas.  

6.  Especifique uma agenda para quando a deteção é executada.  

7.  Quando concluir a configuração da deteção de floresta do Active Directory para este site, escolha **OK** para guardar a configuração.  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>Para configurar uma floresta para deteção de floresta do Active Directory  

1.  No **administração** área de trabalho, escolha **florestas do Active Directory**. Se a Deteção de Florestas do Active Directory tiver sido executada anteriormente, as florestas detetadas serão apresentadas no painel de resultados. A floresta local e quaisquer florestas fidedignas são detetadas quando a Deteção de Florestas do Active Directory é executada. Apenas é necessário adicionar manualmente as florestas não fidedignas.  

    -   Para configurar uma floresta detetada anteriormente, selecione uma floresta no painel de resultados. Em seguida, no **home page** separador o **propriedades** grupo, escolha **propriedades** para abrir as propriedades da floresta. Continue com o passo 3.  

    -   Para configurar uma nova floresta que não está listada, no **home page** separador o **criar** grupo, escolha **adicionar floresta** para abrir o **adicionar florestas** caixa de diálogo. Continue com o passo 3.  

2.  No **geral** separador, concluir as configurações da floresta que pretende detetar e especifique o **conta de floresta do Active Directory**.  

    > [!NOTE]  
    >  A Deteção de Florestas do Active Directory requer uma conta global para detetar e publicar em florestas não fidedignas. Se não utilizar a conta de computador do servidor do site, pode selecionar apenas uma conta global.  

3.  Se pretende permitir que os sites publiquem dados do site nesta floresta no **publicação** separador, concluir as configurações para publicação nesta floresta.  

    > [!NOTE]  
    >  Se permitir que os sites publiquem numa floresta, tem de expandir o esquema do Active Directory dessa floresta para o Configuration Manager. A conta de floresta do Active Directory tem de ter permissões de controlo total ao contentor do sistema dessa floresta.  

4.  Quando concluir a configuração desta floresta para utilização com deteção de floresta do Active Directory, escolha **OK** para guardar a configuração.  



##  <a name="BKMK_ConfigADDiscGeneral"></a> Configurar a deteção do Active Directory para computadores, utilizadores ou grupos  
 Para configurar a deteção de computadores, utilizadores ou grupos, utilize as informações nestas secções para os seguintes métodos de Deteção:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

> [!NOTE]  
>  As informações nesta secção não se aplica a deteção de floresta do Active Directory.  

 Embora cada um destes métodos de deteção seja independente dos outros, partilham opções semelhantes. Para obter mais informações sobre estas opções de configuração, consulte [partilhado opções para a deteção de grupo, o sistema e o utilizador](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
>  A consulta do Active Directory por cada um destes métodos de deteção pode gerar tráfego de rede significativo. Considere o agendamento de cada método de deteção para ser executada com um período de tempo quando este tráfego de rede não prejudique as utilizações empresariais da sua rede.  

#### <a name="to-configure-active-directory-group-discovery"></a>Para configurar a deteção de grupo do Active Directory  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração da hierarquia**e, em seguida, escolha **métodos de deteção**.  

2.  Escolha o **deteção de grupo do Active Directory** método para o site onde pretende configurar a deteção.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

4.  No **geral** separador, selecione a caixa para ativar a deteção. Ou pode configurar a deteção agora e, em seguida, regressar para ativar a deteção mais tarde.  

5.  Escolha **adicionar** para configurar um âmbito de deteção, escolha o **grupos** ou **localização**e concluir as seguintes configurações no **adicionar grupos** ou **adicionar localização do Active Directory** caixa de diálogo:  

    1.  Especifique um **nome** para este âmbito de deteção.  

    2.  Especifique um **domínio do Active Directory** ou **localização** para procurar:  

        -   Se tiver escolhido **grupos**, especifique um ou mais grupos do Active Directory a detetar.  

        -   Se tiver escolhido **localização**, especifique um contentor do Active Directory como uma localização a detetar. Também pode ativar uma pesquisa recursiva dos contentores subordinados do Active Directory para esta localização.  

    3.  Especifique o **conta de deteção de grupo do Active Directory** que é utilizada para procurar este âmbito de deteção.  

    4.  Escolha **OK** para guardar a configuração de âmbito de deteção.  

6.  Repita o passo 6 para cada âmbito de deteção adicionais que pretenda definir.  

7.  No **agenda de consulta** separador, configure a deteção completa deteção agenda e diferenças de consulta.  

8.  Opcionalmente, no **opção** separador Configurar opções para filtrar ou excluir os registos de computadores obsoletos da deteção. Também configure a deteção de associação de grupos de distribuição.  

    > [!NOTE]  
    >  Por predefinição, a deteção de grupo do Active Directory Deteta apenas a associação dos grupos de segurança.  

9. Quando tiver concluído a configuração da deteção de grupo do Active Directory para este site, escolha **OK** para guardar a configuração.  

#### <a name="to-configure-active-directory-system-discovery"></a>Para configurar a deteção de sistema do Active Directory  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração da hierarquia**e, em seguida, escolha **métodos de deteção**.  

2.  Selecione o método para o site onde pretende configurar a deteção.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

4.  No **geral** separador, selecione a caixa para ativar a deteção. Ou pode configurar a deteção agora e, em seguida, regressar para ativar a deteção mais tarde.  

5.  Escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif) para especificar um novo contentor do Active Directory. No **contentor do Active Directory** diálogo caixa, conclua as configurações seguintes:  

    1.  Especifique um ou mais localizações para procurar.  

    2.  Para cada localização, especifique as opções que se alterar o comportamento de procura.  

    3.  Para cada localização, especifique a conta a utilizar como o **conta de deteção do Active Directory**.  

        > [!TIP]  
        >  Para cada localização especificada, pode configurar um conjunto de opções de deteção e uma conta de deteção do Active Directory exclusiva.  

    4.  Escolha **OK** para guardar a configuração do contentor do Active Directory.  

6.  No **agenda de consulta** separador, configure a deteção completa deteção agenda e diferenças de consulta.  

7.  Opcionalmente, no **atributos do Active Directory** separador, pode configurar atributos adicionais do Active Directory para computadores que pretende detetar. Os atributos de objetos predefinidos também são listados.  

     > [!Tip]  
     > Por exemplo, a sua organização utiliza o **Descrição** atributo na conta de computador no Active Directory. Clique em **personalizado**e adicione `Description` como um atributo personalizado. Depois deste método de deteção é executado, este atributo mostra no separador de propriedades do dispositivo na consola do Configuration Manager.<!--513948-->

8.  Opcionalmente, no **opção** separador, pode configurar opções para filtrar ou excluir os registos de computadores obsoletos da deteção.  

9. Quando tiver concluído a configuração da deteção de sistema do Active Directory para este site, escolha **OK** para guardar a configuração.  

#### <a name="to-configure-active-directory-user-discovery"></a>Para configurar a deteção de utilizador do Active Directory  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração da hierarquia**e, em seguida, escolha **métodos de deteção**.  

2.  Escolha o **deteção de utilizador do Active Directory** método para o site onde pretende configurar a deteção.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

4.  No **geral** separador, selecione a caixa para ativar a deteção. Ou pode configurar a deteção agora e, em seguida, regressar para ativar a deteção mais tarde.  

5.  Escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif) para especificar um novo contentor do Active Directory. No **contentor do Active Directory** diálogo caixa, conclua as configurações seguintes:  

    1.  Especifique um ou mais localizações para procurar.  

    2.  Para cada localização, especifique as opções que se alterar o comportamento de procura.  

    3.  Para cada localização, especifique a conta a utilizar como o **conta de deteção do Active Directory**.  

        > [!NOTE]  
        >  Para cada localização especificada, pode configurar um conjunto exclusivo de opções de deteção e uma conta de deteção do Active Directory exclusiva.  

    4.  Escolha **OK** para guardar a configuração do contentor do Active Directory.  

6.  No **agenda de consulta** separador, configure a deteção completa deteção agenda e diferenças de consulta.  

7.  Opcionalmente, no **atributos do Active Directory** separador, pode configurar atributos adicionais do Active Directory para computadores que pretende detetar. Os atributos de objetos predefinidos também são listados.  

8.  Quando tiver concluído a configuração da deteção de utilizador do Active Directory para este site, escolha **OK** para guardar a configuração.  



## <a name="azureaadisc"></a> Configurar a deteção de utilizador do Azure AD
Azure AD User Discovery não está ativada ou configurada da mesma forma que outros métodos de deteção. Configure quando a carregar o Gestor de configuração do site para o Azure AD. Quando lhe [configurar os serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para **gestão de nuvem**, também pode ativar e configurar este método de deteção. 

Quando configurar o **gestão de nuvem** serviço do Azure: 
- No **deteção** página do assistente, clique em **ativar o Azure Active Directory deteção de utilizadores**. 
- Clique em **Definições**. 
- Na caixa de diálogo Definições de deteção de utilizador do Azure AD, configure uma agenda para quando ocorre a deteção. Também pode ativar a deteção de diferenças, que só verifica a existência de novas ou alteradas contas no Azure AD. 

Para obter mais informações, consulte [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

 > [!Important]  
 > Antes de *importar* a aplicação do Azure AD para o Configuration Manager, tem de conceder a permissão da aplicação de servidor para ler os dados de diretório do Azure AD. 
 >  - No [portal do Azure](https://portal.azure.com), vá para o **do Azure Active Directory** painel. 
 >  - Clique em **registos de aplicação**e mude para **todas as aplicações** se necessário. 
 >  - Selecione a aplicação de servidor do tipo *aplicação Web / API*e, em seguida, clique em **definições**. 
 >  - Clique em **as permissões necessárias**e, em seguida, clique em **conceder permissões**.
 >  
 > Se lhe *criar* a aplicação de servidor do Configuration Manager, do Azure AD cria automaticamente as permissões com a aplicação. Ainda tem de dar consentimento para a aplicação no portal do Azure.

 > [!Note]  
 > Se o utilizador é uma identidade federada ou sincronizada, tem de utilizar o Configuration Manager [deteção de utilizadores do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) , bem como a deteção de utilizadores do Azure AD. Para obter mais informações sobre as identidades híbridas, consulte [definir uma estratégia de adoção de identidade híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->



##  <a name="BKMK_ConfigHBDisc"></a> Configurar a deteção de Heartbeat  
 Por predefinição, a deteção de Heartbeat é ativada quando instala um site primário do Configuration Manager. Como resultado, só tem de configurar a agenda para como frequentemente de envio de clientes, registo de dados de deteção de Heartbeat para um ponto de gestão quando não quiser utilizar a predefinição de sete em sete dias.  

> [!NOTE]  
>  Se a tarefa de instalação push do cliente e a manutenção do site para **Limpar sinalizador de instalação** estão ativadas no mesmo site defina a agenda da deteção de Heartbeat para ser inferior à **período de Redeteção do cliente** do **Limpar sinalizador de instalação** tarefa de manutenção do site. Para obter mais informações sobre tarefas de manutenção do site, consulte [tarefas de manutenção do System Center Configuration Manager](../../../../core/servers/manage/maintenance-tasks.md).  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>Para configurar a agenda de deteção de Heartbeat  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração da hierarquia**e, em seguida, escolha **métodos de deteção**.  

2.  Escolha **deteção de Heartbeat** para o site onde pretende configurar a deteção de Heartbeat.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

4.  Configurar a frequência com que os clientes submeterem um registo de dados de deteção de Heartbeat e, em seguida, escolha **OK** para guardar a configuração.  



##  <a name="BKMK_ConfigNetworkDisc"></a> Configurar a deteção de rede  
 Para ajudar a configurar a deteção de rede, utilize as informações nestas secções.  

###  <a name="BKMK_AboutConfigNetworkDisc"></a> Sobre como configurar a deteção de rede  
 Antes de configurar a deteção de rede, tem de compreender os seguintes tópicos:  

-   Disponíveis níveis de deteção de rede  

-   Opções de deteção de rede disponíveis  

-   Limitar a deteção de rede na rede  

Para obter mais informações, consulte [sobre a deteção de rede](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork).  

 As secções seguintes fornecem informações sobre configurações comuns para a deteção de rede. Pode configurar um ou mais destas configurações para utilização durante a mesma deteção a executar. Se utilizar várias configurações, terá de planear as interações que podem afetar os resultados da deteção.  

 Por exemplo, pode querer detetar todos os dispositivos Simple Network Management Protocol (SNMP) que utilizam um nome de Comunidade SNMP específico. Além disso, para a mesma execução da deteção, poderá desativar a deteção numa sub-rede específica. Quando a deteção é executada, a deteção de rede não Deteta os dispositivos SNMP com o nome de Comunidade especificado na sub-rede que tiver desativado.  

####  <a name="BKMK_DetermineNetTopology"></a> Determinar a topologia de rede  
 Pode utilizar uma deteção só de topologia para mapear a rede. Este tipo de deteção não Deteta potenciais clientes. A deteção de rede só de topologia depende do SNMP.  

 Quando estiver a mapear a topologia de rede, tem de configurar o **saltos máximos** no **SNMP** separador o **propriedades da deteção de rede** caixa de diálogo. Apenas alguns saltos podem ajudar a controlar a largura de banda de rede que é utilizada quando a deteção é executada. Como descobrir mais da sua rede, pode aumentar o número de saltos para obter uma melhor compreensão da topologia de rede.  

 Depois de compreender a topologia de rede, pode configurar propriedades adicionais para deteção de rede para detetar potenciais clientes e os respetivos sistemas operativos enquanto estiver a utilizar configurações disponíveis para limitar os segmentos de rede nessa rede Pode procurar a deteção.  

####  <a name="BKMK_LimitBySubnet"></a> Limitar pesquisas através da utilização de sub-redes  
 Pode configurar a deteção de rede para pesquisar sub-redes específicas durante uma deteção. Por predefinição, a deteção de rede procura a sub-rede do servidor que executa a deteção. As sub-redes adicionais que forem configuradas e ativadas aplicam-se apenas ao SNMP e o protocolo de configuração dinâmica de anfitrião (DHCP) opções de pesquisa. Quando a deteção de rede procura domínios, não está limitada por configurações para sub-redes.  

 Se especificar uma ou mais sub-redes no **sub-redes** separador o **propriedades da deteção de rede** caixa de diálogo, apenas as sub-redes que estão marcados como **ativado** serão pesquisados.  

 Quando desativa uma sub-rede, este é excluído da deteção e são aplicáveis as seguintes condições:  

-   As consultas baseadas em SNMP não são executados na sub-rede.  

-   Servidores DHCP não respondem com uma lista de recursos localizados na sub-rede.  

-   As consultas baseadas em domínio podem detetar recursos que estão localizados na sub-rede.  

####  <a name="BKMK_SearchByDomain"></a> Procurar num domínio específico  
 Pode configurar a deteção de rede para pesquisar um domínio específico ou um conjunto de domínios durante a execução da deteção. Por predefinição, a deteção de rede pesquisa o domínio local do servidor que executa a deteção.  

 Se especificar um ou mais domínios no **domínios** separador o **propriedades da deteção de rede** caixa de diálogo, apenas os domínios que estão marcados como **ativado** serão pesquisados.  

 Quando desativa um domínio, este é excluído da deteção e são aplicáveis as seguintes condições:  

-   Deteção de rede não consulta controladores de domínio nesse domínio.  

-   As consultas baseadas em SNMP ainda podem executar em sub-redes do domínio.  

-   Servidores DHCP podem responder com uma lista de recursos localizados no domínio.  

####  <a name="BKMK_LimitBySNMPname"></a> Limitar procuras utilizando nomes de comunidades SNMP  
 Configurar a deteção de rede para pesquisar uma Comunidade SNMP específico ou um conjunto de Comunidades durante a execução da deteção. Por predefinição, o nome de Comunidade **pública** está configurada para utilização.  

 Deteção de rede utiliza nomes de Comunidades para obter acesso a routers que sejam dispositivos SNMP. Um router pode fornecer a deteção de rede com informações sobre outros routers e sub-redes que estejam ligadas ao primeiro router.  

> [!NOTE]  
>  Nomes de comunidades SNMP assemelham-se às palavras-passe. Deteção de rede pode obter informações apenas a partir de um dispositivo SNMP que tiver especificado um nome de Comunidade. Cada dispositivo SNMP pode ter o seu próprio nome de Comunidade, mas, muitas vezes, o mesmo nome de Comunidade é partilhado por vários dispositivos. Além disso, a maioria dos dispositivos SNMP tem um nome de Comunidade predefinido de **pública**. Mas algumas organizações eliminam o **pública** nome da Comunidade a partir dos seus dispositivos como precaução de segurança.  

 Se forem apresentadas várias comunidades SNMP no **SNMP** separador o **propriedades da deteção de rede** caixa de diálogo, a deteção de rede pesquisará as mesmas pela ordem em que estiver a apresentada. Para ajudar a minimizar o tráfego de rede que é gerado pelas tentativas de contacto com um dispositivo utilizando diferentes nomes, certifique-se de que os nomes mais frequentemente utilizados no topo da lista.  

> [!NOTE]  
>  Juntamente com a utilizar o nome de Comunidade SNMP, pode especificar o endereço IP ou nome resolúvel de um dispositivo SNMP específico. Execute esta ação no **dispositivos SNMP** separador o **propriedades da deteção de rede** caixa de diálogo.  

####  <a name="BKMK_SearchByDHCP"></a> Procurar um servidor DHCP específico  
 Pode configurar a deteção de rede para utilizar um servidor DHCP específico ou vários servidores para detetar clientes DHCP durante uma deteção.  

 Deteção de rede pesquisa cada servidor DHCP que especificar no **DHCP** separador o **propriedades da deteção de rede** caixa de diálogo. Se o servidor que executa a deteção obtiver a concessão dos seus endereços IP a partir de um servidor DHCP, pode configurar a deteção para pesquisar esse servidor DHCP, verificando o **incluem o servidor DHCP que o servidor do site está configurado para utilizar** caixa.  

> [!NOTE]  
>  Para configurar com êxito um servidor DHCP na deteção de rede, o seu ambiente tem de suportar IPv4. Não é possível configurar a deteção de rede para utilizar um servidor DHCP num ambiente IPv6 nativo.  

###  <a name="BKMK_HowToConfigNetDisc"></a> Como configurar a deteção de rede  
 Utilize os procedimentos seguintes para começar por detetar apenas a topologia de rede e, em seguida, para configurar a deteção de rede para detetar potenciais clientes utilizando um ou mais das opções de deteção de rede disponíveis.  

##### <a name="to-determine-your-network-topology"></a>Para determinar a topologia de rede  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração da hierarquia**e, em seguida, escolha **métodos de deteção**.  

2.  Escolha **deteção de rede** para o site onde pretende executar a deteção de rede.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

    -   No **geral** separador, verifique o **ativar a deteção de rede** caixa e, em seguida, escolha **topologia** do **tipo de deteção** opções.  

    -   No **sub-redes** separador, verifique o **procurar sub-redes locais** caixa.  

        > [!TIP]  
        >  Se conhecer as sub-redes específicas que constituem a sua rede, desmarque a **procurar sub-redes locais** caixa. Em seguida, utilize o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif) para adicionar as sub-redes específicas que pretende procurar. Para redes de grandes dimensões, muitas vezes, é melhor pesquisar apenas uma ou duas sub-redes de cada vez para minimizar a utilização de largura de banda de rede.  

    -   No **domínios** separador, verifique o **Procurar domínio local** caixa.  

    -   No **SNMP** separador, utilize o **saltos máximos** na lista pendente para especificar a deteção de rede de saltos de router quantos pode efetuar para mapear a topologia.  

        > [!TIP]  
        >  Quando mapear a topologia de rede pela primeira vez, configure apenas alguns saltos de router para minimizar a utilização de largura de banda de rede.  

4.  No **agenda** separador, escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif) para agendar a execução da deteção de rede.  

    > [!NOTE]  
    >  Não é possível atribuir uma configuração de deteção diferente a separar as agendas de deteção de rede. Sempre que a deteção de rede é executada, utiliza a configuração de deteção atual.  

5.  Escolha **OK** para guardar as configurações. Deteção de rede é executada na hora agendada.  

##### <a name="to-configure-network-discovery"></a>Para configurar a deteção de rede  

1.  Na consola do Configuration Manager, escolha **administração** > **configuração da hierarquia**e, em seguida, escolha **métodos de deteção**.  

2.  Escolha **deteção de rede** para o site onde pretende executar a deteção de rede.  

3.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

4.  No **geral** separador, verifique o **ativar a deteção de rede** caixa e, em seguida, selecione o tipo de deteção que pretende executar a partir de **tipo de deteção** opções.  

5.  Para configurar a deteção para pesquisar sub-redes, escolha o **sub-redes** separador e, em seguida, configure uma ou mais das seguintes opções:  

    -   Para executar a deteção em sub-redes locais no computador que executa a deteção, verifique o **procurar sub-redes locais** caixa.  

    -   Para pesquisar uma sub-rede específica, certifique-se de que a sub-rede está listada em **sub-rede a procurar** e tem um **pesquisa** valor **ativado**:  

        1.  Se a sub-rede não estiver listada, escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif). No **nova atribuição de sub-rede** caixa de diálogo, introduza o **sub-rede** e **máscara** informações e, em seguida, escolha **OK**. Por predefinição, uma nova sub-rede está ativada para pesquisa.  

        2.  Para alterar o **pesquisa** valor para uma sub-rede listada, selecione a sub-rede e, em seguida, escolha o **alternar** ícone para alternar o valor entre **desativado** e **ativado**.  

6.  Para configurar a deteção para pesquisar domínios, escolha o **domínios** separador e, em seguida, configure uma ou mais das seguintes opções:  

    -   Para executar a deteção no domínio do computador que executa a deteção, verifique o **Procurar domínio local** caixa.  

    -   Para pesquisar um domínio específico, certifique-se de que o domínio está listado em **domínios** e tem um **pesquisa** valor **ativado**:  

        1.  Se o domínio não estiver listado, escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif). No **domínio propriedades** caixa de diálogo, introduza o **domínio** informações e, em seguida, escolha **OK**. Por predefinição, um novo domínio está ativado para pesquisa.  

        2.  Para alterar o **pesquisa** valor para um domínio listado, selecione o domínio e, em seguida, escolha o **alternar** ícone para alternar o valor entre **desativado** e **ativado**.  

7.  Para configurar a deteção para pesquisar nomes de comunidades SNMP específicos para os dispositivos SNMP, escolha o **SNMP** separador e, em seguida, configure uma ou mais das seguintes opções:  

    -   Para adicionar um nome de Comunidade SNMP à lista de **nomes da Comunidade SNMP**, escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif). No **novo nome de Comunidade SNMP** diálogo caixa, especifique o **nome** da Comunidade SNMP e, em seguida, escolha **OK**.  

    -   Para remover um nome de Comunidade SNMP, selecione o nome de Comunidade e, em seguida, escolha o **eliminar** ícone ![ícone Eliminar](media/Disc_delete_Icon.gif).  

    -   Para ajustar a ordem de pesquisa dos nomes de comunidades SNMP, selecione um nome de Comunidade e, em seguida, escolha o **Mover Item para cima** ícone ![mover a cópia de segurança de ícone](media/Disc_moveUp_Icon.gif) ou **Mover Item para baixo** ícone ![mover o ícone](media/Disc_moveDown_Icon.gif). Quando a deteção é executada, nomes de Comunidades são pesquisados por uma ordem da parte superior para parte inferior. Tenha os seguintes pontos em mente.

        > [!NOTE]  
        >  Deteção de rede utiliza nomes de comunidades SNMP, para obter acesso a routers que sejam dispositivos SNMP. Um router pode informar a deteção de rede sobre outros routers e sub-redes ligadas ao primeiro router.  

        -   Nomes de comunidades SNMP assemelham-se às palavras-passe.  

        -   Deteção de rede pode obter informações apenas a partir de um dispositivo SNMP que especificou um nome de Comunidade.  

        -   Cada dispositivo SNMP pode ter o seu próprio nome de Comunidade, mas, muitas vezes, o mesmo nome de Comunidade é partilhado por vários dispositivos.  

        -   A maioria dos dispositivos SNMP tem um nome de Comunidade predefinido de **pública**. Pode utilizar que o se não souber outros nomes de Comunidade. No entanto, algumas organizações eliminam o **pública** nome da Comunidade a partir dos seus dispositivos como precaução de segurança.  

8.  Para configurar o número máximo de saltos de routers para utilização pelas pesquisas de SNMP, escolha o **SNMP** separador e, em seguida, selecione o número de saltos de **saltos máximos** na lista pendente.  

9. Para configurar um dispositivo SNMP, escolha o **dispositivos SNMP** separador. Se o dispositivo não estiver indicado não existe, escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif). No **novo dispositivo SNMP** caixa de diálogo, especifique o nome de dispositivo ou endereço IP do dispositivo SNMP e, em seguida, escolha **OK**.  

    > [!NOTE]  
    >  Se especificar um nome de dispositivo, o Configuration Manager tem de ser capaz de resolver o nome NetBIOS para um endereço IP.  

10. Para configurar a deteção para consultar servidores DHCP específicos sobre clientes DHCP, escolha o **DHCP** separador e, em seguida, configure uma ou mais das seguintes opções:  

    -   Para consultar o servidor DHCP no computador que executa a deteção, optar por **utilizar sempre o servidor DHCP do servidor de site**.  

        > [!NOTE]  
        >  Para utilizar esta opção, o servidor tem concessão o respetivo endereço IP de um servidor DHCP e não é possível utilizar um endereço IP estático.  

    -   Para consultar um servidor DHCP específico, escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif). No **novo servidor DHCP** caixa de diálogo, especifique o nome de servidor ou endereço IP do servidor DHCP e, em seguida, escolha **OK**.  

        > [!NOTE]  
        >  Se especificar um nome de servidor, tem de ser capaz de resolver o nome NetBIOS para um endereço IP do Configuration Manager.  

11. Para configurar quando a deteção é executada, escolha o **agenda** separador e, em seguida, escolha o **novo** ícone ![novo ícone](media/Disc_new_Icon.gif) para agendar a execução da deteção de rede.  

     Pode configurar vários agendamentos periódicos e vários agendamentos sem periodicidade.  

    > [!NOTE]  
    >  Se forem apresentadas várias agendas no **agenda** separador mesmo tempo, todos os agendamentos resultarão numa execução da deteção de rede conforme a configuração à hora indicada na agenda. Este comportamento também se verifica para agendamentos periódicos.  

12. Escolha **OK** para guardar as configurações.  

###  <a name="BKMK_HowToVerifyNetDisc"></a> Como verificar se a deteção de rede foi concluída  
 O tempo que a deteção de rede necessita para concluir pode variar consoante um ou mais dos seguintes fatores:  

-   O tamanho da sua rede  

-   A topologia da rede  

-   O número máximo de saltos configurados para localizar routers na rede  

-   O tipo de deteção que está a ser executado  

Porque a deteção de rede não cria mensagens para o alertar quando a deteção foi concluída, pode utilizar o procedimento seguinte para verificar se a deteção foi concluída.  

##### <a name="to-verify-that-network-discovery-has-finished"></a>Para verificar se a deteção de rede foi concluída  

1.  Na consola do Configuration Manager, escolha **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado do sistema**e, em seguida, escolha **consultas de mensagens de estado**.  

3.  Escolha **todas as mensagens de estado**.  

4.  No **home page** separador o **consultas de mensagens de estado** grupo, escolha **Mostrar mensagens**.  

5.  No **selecionar data e hora** na lista pendente, selecione um valor que inclua há quanto tempo a deteção foi iniciada e, em seguida, escolha **OK** para abrir o **Configuration Manager Status Message Viewer**.  

    > [!TIP]  
    >  Também pode utilizar o **especifique a data e hora** opção para selecionar uma determinada data e hora em que executou a deteção. Esta opção é útil quando executou a deteção de rede numa determinada data e pretender obter mensagens apenas dessa data.  

6.  Para validar que a deteção de rede foi concluída, procure uma mensagem de estado que tenha os seguintes detalhes:  

    -   ID da mensagem: **502**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrição: **Este componente parada**  

    Se esta mensagem de estado não estiver presente, a deteção de rede não foi concluída.  

7.  Para validar quando a deteção de rede iniciado, procure uma mensagem de estado que tenha os seguintes detalhes:  

    -   ID da mensagem: **500**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrição: **Este componente foi iniciado**  

    Esta informação confirma que a deteção de rede foi iniciada. Se esta informação não estiver presente, reagende a deteção de rede.  
