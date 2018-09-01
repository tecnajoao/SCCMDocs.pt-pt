---
title: Configurar a deteção
titleSuffix: Configuration Manager
description: Configure métodos de deteção para localizar recursos para gerir a partir de sua rede, Active Directory e Azure Active Directory.
ms.date: 08/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e232875aab086dea04261abc4d83df8d5d03e6c8
ms.sourcegitcommit: aca62bd3d267b1dbea46d4db6f32d797c5f6263c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/31/2018
ms.locfileid: "43347975"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Configurar métodos de deteção do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Configure métodos de deteção para localizar recursos para gerir a partir de sua rede, Active Directory e Azure Active Directory (Azure AD). Ativar primeiro e, em seguida, configurar cada método que deseja usar para pesquisar seu ambiente. Também pode desativar um método usando o mesmo procedimento que utiliza para ativá-la. As únicas exceções a este processo são de deteção de Heartbeat e deteção de servidores:  

-   Por predefinição, **deteção de Heartbeat** já está ativada quando instala um site primário do Configuration Manager. Ele é configurado para executar com base numa agenda básica. Mantenha a deteção de Heartbeat ativada. Torna-se de que os registos de dados de deteção (DDR) para os dispositivos estão atualizados. Para obter mais informações sobre a deteção de Heartbeat, consulte [acerca da deteção de Heartbeat](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

-   **Deteção de servidores** é um método de deteção automática. Ele localiza os computadores que utilizam como sistemas de sites. Não é possível configurar ou desativá-la.  

### <a name="enable-a-configurable-discovery-method"></a>Ativar um método de deteção configuráveis  
 > [!NOTE]  
 > As seguintes informações não se aplica a deteção de utilizador do Azure AD. Em vez disso, veja [configurar o Azure AD User Discovery](#azureaadisc) mais adiante neste artigo.

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração da hierarquia**e, em seguida, selecione **métodos de deteção**.  

2.  Selecione o método de deteção para o site onde pretende ativar a deteção.  

3.  Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**. Em seguida, na **gerais** separador, selecione a opção de **ativar &lt;método de deteção\>**.  

     Se esta opção já estiver ativada, pode desativar o método de deteção por desmarcando a caixa de verificação.  

4.  Selecione **OK** para guardar a configuração.  



##  <a name="BKMK_ConfigADForestDisc"></a> Configurar a deteção de florestas do Active Directory  

Para concluir a configuração da deteção de florestas do Active Directory, configure as definições nas seguintes localizações da consola do Configuration Manager:  

- Na **métodos de deteção** nó:

    - Ative este método de deteção.  

    - Defina uma agenda de consulta.  

    - Selecione se a deteção automática cria limites para os sites do Active Directory e sub-redes que Deteta.  

- Na **florestas do Active Directory** nó:

    - Adicione florestas que pretende detetar.  

    - Ative a deteção de sites e sub-redes nessa floresta do Active Directory.  

    - Configure as definições que permitem a sites do Configuration Manager publicar as suas informações de site na floresta.  

    - Atribua uma conta a utilizar como conta de floresta do Active Directory para cada floresta.  

Utilize os procedimentos seguintes para ativar a deteção de floresta do Active Directory e configurar florestas individuais para utilização com deteção de floresta do Active Directory.  


### <a name="enable-active-directory-forest-discovery"></a>Deteção de floresta de diretório do Active Directory de ativar  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração da hierarquia**e selecione o **métodos de deteção** nó.  

2.  Selecione o método de deteção de floresta do Active Directory para o site onde pretende configurar a deteção.  

3.  Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**.  

4.  Sobre o **gerais** separador, selecione a caixa de verificação para ativar a deteção. Ou pode configurar a deteção agora e, em seguida, volte para ativar a deteção mais tarde.  

5.  Especifique as opções para criar limites de sites para localizações detetadas.  

6.  Especifique uma agenda para a execução da deteção.  

7.  Selecione **OK** para guardar a configuração.  


### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Configurar uma floresta para deteção de floresta do Active Directory  

1.  Na **Administration** área de trabalho, expanda **configuração da hierarquia**e selecione o **florestas do Active Directory** nó. Se a Deteção de Florestas do Active Directory tiver sido executada anteriormente, as florestas detetadas serão apresentadas no painel de resultados. A floresta local e quaisquer florestas fidedignas são detetadas quando a Deteção de Florestas do Active Directory é executada. Apenas terá de adicionar manualmente as florestas não fidedignas.  

    -   Para configurar uma floresta detetada anteriormente, selecione uma floresta no painel de resultados. Em seguida, na **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades** para abrir as propriedades da floresta. Continue com o passo 3.  

    -   Para configurar uma nova floresta que não está listada, no **home page** separador do Friso, no **Create** grupo, selecione **adicionar floresta**. Esta ação abre o **adicionar florestas** caixa de diálogo. Continue com o passo 3.  

2.  Sobre o **gerais** separador, termine as configurações da floresta que pretende detetar e especifique a **conta de floresta do Active Directory**. Para obter mais informações sobre esta conta, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#active-directory-forest-account).  

    > [!NOTE]  
    >  A Deteção de Florestas do Active Directory requer uma conta global para detetar e publicar em florestas não fidedignas. Se não usar a conta de computador do servidor do site, pode selecionar apenas uma conta global.  

3.  Se pretende permitir que os sites publiquem dados do site nesta floresta no **publicação** separador, termine as configurações para publicação nesta floresta.  

    > [!NOTE]  
    >  Se permitir que os sites publiquem numa floresta, expanda o esquema do Active Directory dessa floresta para o Configuration Manager. A conta de floresta do Active Directory tem de ter permissões de controlo total ao contentor do sistema dessa floresta.  

4.  Selecione **OK** para guardar a configuração.  



##  <a name="BKMK_ConfigADDiscGeneral"></a> Configurar a deteção do Active Directory para computadores, utilizadores ou grupos  

Para configurar a deteção de computadores, utilizadores ou grupos, comece com estes passos comuns:

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração da hierarquia**e selecione o **métodos de deteção** nó.  

2.  Selecione o método para o site onde pretende configurar a deteção.  

3.  Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**.  

4.  Sobre o **gerais** separador, selecione a caixa de verificação para ativar a deteção. Ou pode configurar a deteção agora e, em seguida, volte para ativar a deteção mais tarde.  

Em seguida, utilize as informações nas secções seguintes para configurar os métodos de deteção específicas:  

- [Deteção de grupos do Active Directory](#bkmk_config-adgd)  

- [Deteção de sistemas do Active Directory](#bkmk_config-adgd)  

- [Deteção de utilizadores do Active Directory](#bkmk_config-adud)  

> [!NOTE]  
>  As informações nesta secção não se aplica a deteção de floresta do Active Directory.  

 Embora cada um destes métodos de deteção seja independente dos outros, partilham opções semelhantes. Para obter mais informações sobre estas opções de configuração, consulte [partilhados opções para a deteção de grupo, o sistema e o utilizador](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_shared).  

> [!WARNING]  
>  A consulta do Active Directory por cada um destes métodos de deteção pode gerar tráfego de rede significativo. Considere o agendamento de cada método de deteção para ser executado num período de tempo quando este tráfego de rede não afete negativamente utilizações empresariais da sua rede.  


### <a name="bkmk_config-adgd"></a> Configurar a deteção de grupos do Active Directory  

1. Sobre o **gerais** separador da janela de propriedades de deteção de grupo do Active Directory, selecione **Add** para configurar um âmbito de deteção. Selecione **grupos** ou **localização**. Em seguida, concluir as seguintes configurações na **adicionar grupos** ou **adicionar localização do Active Directory** caixa de diálogo:  

    1.  Especifique um **nome** para este âmbito de deteção.  

    2.  Especifique um **domínio do Active Directory** ou **localização** para procurar:  

        -   Se escolheu **grupos**, especifique um ou mais grupos do Active Directory para detetar.  

        -   Se escolheu **localização**, especifique um contentor do Active Directory como uma localização a detetar. Também pode ativar uma pesquisa recursiva dos contentores subordinados do Active Directory para esta localização.  

    3.  Especifique a **conta de deteção de grupo do Active Directory** que o site utiliza para procurar este âmbito de deteção. Para obter mais informações, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#active-directory-group-discovery-account).  

    4.  Selecione **OK** para guardar a configuração de âmbito de deteção.  

2.  Repita os passos anteriores para cada âmbito de deteção adicionais que pretende definir.  

3.  Sobre o **agenda de consulta** separador, configure os dois a consulta de deteção completa deteção diferenciais e agenda.  

4.  Sobre o **opções** separador, configure definições para filtrar ou excluir os registos de computadores obsoletos da deteção. Também configure a deteção da associação de grupos de distribuição.  

    > [!NOTE]  
    >  Por predefinição, a deteção de grupo do Active Directory Deteta apenas a associação de grupos de segurança.  

5. Selecione **OK** para guardar a configuração.  


### <a name="bkmk_config-adsd"></a> Configurar a deteção de sistemas do Active Directory  

1. Na **gerais** separador da janela de propriedades de deteção de sistema do Active Directory, selecione a **New** ícone ![novo ícone](media/Disc_new_Icon.gif) para especificar um novo contentor do Active Directory. Na **contentor do Active Directory** diálogo caixa, conclua as seguintes configurações:  

    1.  Escreva ou procure para uma localização para o **caminho**. Este valor é um caminho LDAP válido para um contentor ou unidade organizacional (UO). O site de consulta este caminho para os recursos. Por exemplo, `LDAP://CN=Computers,DC=contoso,DC=com`  

    2.  Especifique as opções que alterar o comportamento de procura:  

        - **Detetar objetos dentro de grupos do Active Directory**: O site também analisa a associação de grupos neste caminho.  

        - **Contentores subordinados do Active Directory de Pesquisar recursivamente**: Se ativar esta opção, o site de pesquisa quaisquer contentores adicionais ou UOs no caminho acima. Se desativar esta opção, o site de procura apenas para recursos no caminho específico.  

            A partir da versão 1806, selecione os subcontentores para impedir que esta pesquisa recursiva. Esta opção ajuda a reduzir o número de objetos detetados. Selecione **adicionar** para escolher os contentores no caminho acima. Na caixa de diálogo Selecionar novo contentor, selecione um contentor de subordinados para excluir. Selecione **OK** para fechar a caixa de diálogo Selecionar novo contentor.<!--1358143-->

            > [!Tip]  
            > A lista de contentores do Active Directory na janela de propriedades de deteção de sistema do Active Directory inclui uma coluna **tem exclusões**. Ao selecionar contentores para excluir, este valor é **Sim**.  

    3.  Para cada localização, especifique a conta a utilizar como a **conta de deteção do Active Directory**. Para obter mais informações, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#active-directory-system-discovery-account).  

        > [!TIP]  
        >  Para cada localização especificada, pode configurar um conjunto de opções de deteção e uma conta de deteção do Active Directory exclusiva.  

    4.  Selecione **OK** para guardar a configuração de contentor do Active Directory.  

2.  Sobre o **agenda de consulta** separador, configure os dois a consulta de deteção completa deteção diferenciais e agenda.  

3.  Sobre o **atributos do Active Directory** separador, configurar atributos adicionais do Active Directory para computadores que pretende detetar. Este separador lista os atributos de objeto do padrão.  

     > [!Tip]  
     > Por exemplo, a sua organização utiliza o **Descrição** atributo na conta de computador no Active Directory. Selecione **personalizados**e adicione `Description` como um atributo personalizado. Depois deste método de deteção é executado, esse atributo mostra no separador de propriedades do dispositivo na consola do Configuration Manager.<!--513948-->  

4.  Sobre o **opções** separador, configure definições para filtrar ou excluir os registos de computadores obsoletos da deteção.  

5. Selecione **OK** para guardar a configuração.  


### <a name="bkmk_config-adud"></a> Configurar a deteção de utilizadores do Active Directory  

1.  Na **gerais** separador da janela de propriedades de deteção de utilizador do Active Directory, selecione a **New** ícone ![novo ícone](media/Disc_new_Icon.gif) para especificar um novo contentor do Active Directory. Na **contentor do Active Directory** diálogo caixa, conclua as seguintes configurações:  

    1.  Especifique um ou mais localizações para procurar.  

    2.  Para cada localização, especifique as opções que alteram o comportamento de procura.  

    3.  Para cada localização, especifique a conta a utilizar como a **conta de deteção do Active Directory**. Para obter mais informações, consulte [contas](/sccm/core/plan-design/hierarchy/accounts#active-directory-user-discovery-account).  

        > [!NOTE]  
        >  Para cada localização especificada, pode configurar um conjunto exclusivo de opções de deteção e uma conta de deteção do Active Directory exclusiva.  

    4.  Selecione **OK** para guardar a configuração de contentor do Active Directory.  

6.  Sobre o **agenda de consulta** separador, configure os dois a consulta de deteção completa deteção diferenciais e agenda.  

7.  Sobre o **atributos do Active Directory** separador, configurar atributos adicionais do Active Directory para computadores que pretende detetar. Este separador lista os atributos de objeto do padrão.  

8.  Selecione **OK** para guardar a configuração.  



## <a name="azureaadisc"></a> Configurar a deteção de utilizador do Azure AD

O Azure AD User Discovery não está ativada ou configurado da mesma forma que outros métodos de deteção. Configurá-lo quando integrar o Gestor de configuração do site para o Azure AD. Quando [configurar os serviços do Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para **gestão de Cloud**, também pode ativar e configurar este método de deteção. 

Quando configurar o **gestão na Cloud** o serviço do Azure: 
- Sobre o **deteção** página do assistente, selecione a opção para **ativar o Azure Active Directory deteção de utilizadores**. 
- Selecione **definições**. 
- Na caixa de diálogo de definições de deteção de utilizador do Azure AD, configure uma agenda para quando ocorre a deteção. Também pode ativar a deteção de diferenças, que só verifica a existência de contas novas ou alteradas no Azure AD. 

Para obter mais informações, consulte [do Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

 > [!Important]  
 > Antes de *importar* a aplicação do Azure AD para o Configuration Manager, tem de conceder a permissão da aplicação de servidor para ler dados do diretório do Azure AD. 
 >  - Na [portal do Azure](https://portal.azure.com), aceda ao **Azure Active Directory** painel. 
 >  - Selecione **registos de aplicações**e troque para **todas as aplicações** se necessário. 
 >  - Selecione a aplicação de servidor do tipo *aplicação Web / API*e, em seguida, selecione **definições**. 
 >  - Selecione **permissões obrigatórias**e, em seguida, selecione **conceder permissões**.
 >  
 > Se *criar* a aplicação de servidor do Configuration Manager, do Azure AD cria automaticamente as permissões com a aplicação. Ainda tem de dar consentimento para a aplicação no portal do Azure.

 > [!Note]  
 > Se o utilizador é uma identidade federada ou sincronizada, tem de utilizar o Configuration Manager [deteção de utilizadores do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) , bem como a deteção de utilizadores do Azure AD. Para obter mais informações sobre identidades híbridas, consulte [definir uma estratégia de adoção de identidade híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->



##  <a name="BKMK_ConfigHBDisc"></a> Configurar a deteção de Heartbeat  

O Configuration Manager permite que o método de deteção de Heartbeat, quando instala um site primário. Se pretender utilizar a agenda predefinida de cada sete dias, há mais nada a configurar. Caso contrário, apenas tem de configurar a agenda para saber como muitas vezes, os dados de deteção de Heartbeat para um ponto de gestão de registos de envio de clientes.  

> [!NOTE]  
>  Se ativar a instalação push do cliente e a tarefa de manutenção do site para **Limpar sinalizador de instalação** no mesmo site, defina a agenda da deteção de Heartbeat para ser inferior à **período de Redeteção do cliente** de o **Limpar sinalizador de instalação** tarefa de manutenção do site. Para obter mais informações sobre tarefas de manutenção do site, consulte [tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks).  


### <a name="configure-the-heartbeat-discovery-schedule"></a>Configurar a agenda da deteção de Heartbeat  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração da hierarquia**e selecione o **métodos de deteção** nó.  

2.  Selecione o **deteção de Heartbeat** método para o site onde pretende configurar a deteção de Heartbeat.  

3.  Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**.  

4.  Configure a frequência com que os clientes enviam um registo de dados de deteção de Heartbeat. Em seguida, selecione **OK** para guardar a configuração.  



<a name="BKMK_AboutConfigNetworkDisc"></a>

##  <a name="BKMK_ConfigNetworkDisc"></a> Configurar a deteção de rede  

 Antes de configurar a deteção de rede, compreenda os seguintes tópicos:  

-   Níveis disponíveis de deteção de rede  

-   Opções de deteção de rede disponíveis  

-   Limitar a deteção de rede na rede  

Para obter mais informações, consulte [acerca da deteção de rede](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutNetwork).  

As secções seguintes fornecem informações sobre configurações comuns para a deteção de rede. Pode configurar uma ou mais destas configurações para utilização durante a deteção mesmo executam. Se utilizar várias configurações, planeie as interações que podem afetar os resultados de deteção.  

Por exemplo, descobre todos os dispositivos Simple Network Management Protocol (SNMP) que utilizam um nome de Comunidade SNMP específico. Para a mesma deteção a executar, desativar a deteção numa sub-rede específica. Quando a deteção é executada, a deteção de rede não detetar os dispositivos SNMP com o nome de Comunidade especificado na sub-rede que depois de ter desabilitado.  


###  <a name="BKMK_DetermineNetTopology"></a> Determinar a topologia de rede  

 Pode utilizar uma deteção só de topologia para mapear a rede. Este tipo de deteção não Deteta potenciais clientes. A deteção de rede só de topologia depende do SNMP.  

 Quando estiver a mapear a topologia de rede, configurar o **saltos máximos** no **SNMP** separador o **propriedades da deteção de rede** caixa de diálogo. Apenas alguns saltos podem ajudar a controlar a largura de banda de rede que é utilizada quando a deteção é executada. Como detetar mais de sua rede, aumente o número de saltos para obter uma melhor compreensão da topologia da rede.  

 Depois de compreender a topologia de rede, configure propriedades adicionais para a deteção de rede. Estas propriedades ajudam a detetar potenciais clientes e os respetivos sistemas operativos. Também configure a deteção de rede para limitar os segmentos de rede pode procurar.  

 Para obter mais informações, consulte [como determinar a topologia de rede](#bkmk_proc-top)


### <a name="network-discovery-search-options"></a>Opções de pesquisa de deteção de rede

O Configuration Manager suporta os seguintes métodos para pesquisar na rede:
- [Limitar pesquisas através da utilização de sub-redes](#BKMK_LimitBySubnet)
- [Procurar num domínio específico](#BKMK_SearchByDomain)
- [Limitar procuras utilizando nomes de comunidades SNMP](#BKMK_LimitBySNMPname)
- [Procurar num servidor DHCP específico](#BKMK_SearchByDHCP)

####  <a name="BKMK_LimitBySubnet"></a> Limitar pesquisas através da utilização de sub-redes  

 Pode configurar a deteção de rede para procurar sub-redes específicas durante uma deteção. Por predefinição, a deteção de rede procura a sub-rede do servidor que executa a deteção. As sub-redes adicionais que forem configuradas e ativadas aplicam-se apenas ao SNMP e DHCP opções de pesquisa. Quando a deteção de rede procura domínios, não é limitado por configurações para sub-redes.  

 Se especificar uma ou mais sub-redes no **sub-redes** separador a **propriedades da deteção de rede** caixa de diálogo, este procura apenas as sub-redes que marcar como **ativado**.  

 Quando desativa uma sub-rede, o site a exclui da deteção e são aplicáveis as seguintes condições:  

-   As consultas baseadas em SNMP não são executados na sub-rede.  

-   Servidores DHCP não respondem com uma lista de recursos localizados na sub-rede.  

-   As consultas baseadas em domínio podem detetar recursos que estão localizados na sub-rede.  


####  <a name="BKMK_SearchByDomain"></a> Procurar num domínio específico  

 Pode configurar a deteção de rede para pesquisar um domínio específico ou um conjunto de domínios durante a execução da deteção. Por predefinição, a deteção de rede pesquisa o domínio local do servidor que executa a deteção.  

 Se especificar um ou mais domínios na **domínios** separador a **propriedades da deteção de rede** caixa de diálogo, este procura apenas os domínios marcados como **ativado**.  

 Quando desativa um domínio, o site a exclui da deteção e são aplicáveis as seguintes condições:  

-   Deteção de rede não consulta controladores de domínio nesse domínio.  

-   As consultas baseadas em SNMP ainda podem executar em sub-redes do domínio.  

-   Servidores DHCP podem responder com uma lista de recursos localizados no domínio.  


#### <a name="BKMK_LimitBySNMPname"></a> Limitar procuras utilizando nomes de comunidades SNMP  

 Configurar a deteção de rede para pesquisar uma Comunidade SNMP específico ou de um conjunto de Comunidades durante a execução da deteção. Por predefinição, o método configura a **público** nome de Comunidade.  

 Deteção de rede utiliza nomes de Comunidades para obter acesso a routers que sejam dispositivos SNMP. Um router pode fornecer a deteção de rede com informações sobre outros routers e sub-redes que estejam ligadas ao primeiro router.  

> [!NOTE]  
>  Nomes de comunidades SNMP assemelham-se as palavras-passe. Deteção de rede pode obter informações apenas a partir de um dispositivo SNMP, para que tiver especificado um nome de Comunidade. Cada dispositivo SNMP pode ter seu próprio nome de Comunidade, mas, muitas vezes, o mesmo nome de Comunidade é partilhado por vários dispositivos. Além disso, a maioria dos dispositivos SNMP tem um nome de Comunidade predefinido de **público**. Mas algumas organizações eliminam o **público** nome de Comunidade a partir dos seus dispositivos como precaução de segurança.  

 Se incluir mais do que uma Comunidade SNMP no **SNMP** separador a **propriedades da deteção de rede** caixa de diálogo, ele pesquisará as mesmas pela ordem em que estão apresentadas. Certifique-se de que os nomes de utilizadas com mais frequência são na parte superior da lista. Esta configuração ajuda a minimizar o tráfego de rede que o site gera ao tentar contactar um dispositivo utilizando diferentes nomes.

> [!NOTE]  
>  Juntamente com a utilizar o nome de Comunidade SNMP, pode especificar o endereço IP ou nome resolúvel de um dispositivo SNMP específico. Execute esta ação no **dispositivos SNMP** separador a **propriedades da deteção de rede** caixa de diálogo.  


####  <a name="BKMK_SearchByDHCP"></a> Procurar num servidor DHCP específico  

 Pode configurar a deteção de rede para utilizar um servidor DHCP específico ou vários servidores para detetar clientes DHCP durante uma deteção.  

 Deteção de rede pesquisa cada servidor DHCP que especificar no **DHCP** separador a **propriedades da deteção de rede** caixa de diálogo. Se o servidor que executa a deteção obtiver a concessão dos seus endereços IP a partir de um servidor DHCP, pode configurar a deteção para pesquisar esse servidor DHCP. Habilitar esse comportamento com a opção para **incluem o servidor DHCP que o servidor do site está configurado para utilizar**.  

> [!NOTE]  
>  Para configurar com êxito um servidor DHCP na deteção de rede, o seu ambiente tem de suportar IPv4. Não é possível configurar a deteção de rede para utilizar um servidor DHCP num ambiente IPv6 nativo.  


###  <a name="BKMK_HowToConfigNetDisc"></a> Como configurar a deteção de rede  

 Utilize os procedimentos seguintes para começar por detetar apenas a topologia de rede e, em seguida, para configurar a deteção de rede para detetar potenciais clientes, utilizando um ou mais das opções de deteção de rede disponíveis.  

#### <a name="bkmk_proc-top"></a> Como determinar a topologia de rede  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração da hierarquia**e selecione o **métodos de deteção** nó.  

2.  Selecione o **deteção de rede** método para o site onde pretende detetar recursos de rede.  

3.  Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**.  

    -   Sobre o **gerais** separador, selecione a opção de **Ativar deteção de rede**. Em seguida, selecione **topologia** partir a **tipo de deteção** opções.  

    -   Sobre o **sub-redes** separador, selecione a **procurar sub-redes locais** opção.  

        > [!TIP]  
        >  Se conhecer as sub-redes específicas que constituem a sua rede, desmarque a **procurar sub-redes locais** caixa de verificação. Em seguida, selecione o **New** ícone ![novo ícone](media/Disc_new_Icon.gif)e adicionar as sub-redes específicas que pretende procurar. Redes de grandes dimensões, pesquise apenas uma ou duas sub-redes por vez para minimizar a utilização de largura de banda de rede.  

    -   Sobre o **domínios** separador, selecione a opção de **Procurar domínio local**.  

    -   Sobre o **SNMP** separador, selecione a opção da **saltos máximos** na lista pendente. Esta opção especifica quantos saltos de router a deteção de rede pode demorar mapear a topologia.  

        > [!TIP]  
        >  Quando mapear a topologia de rede pela primeira vez, configure apenas alguns saltos de router para minimizar a utilização de largura de banda de rede.  

4.  Na **agenda** separador, selecione a **New** ícone ![novo ícone](media/Disc_new_Icon.gif)e defina uma agenda a execução da deteção.  

    > [!NOTE]  
    >  Não é possível atribuir uma configuração de deteção diferentes para separar as agendas de deteção de rede. Sempre que for executada a deteção de rede, ele usa a configuração de deteção atual.  

5.  Selecione **OK** para aceitar as configurações. Deteção de rede é executada à hora agendada.  


#### <a name="bkmk_proc-config"></a> Como configurar a deteção de rede  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração da hierarquia**e selecione o **métodos de deteção** nó.  

2.  Selecione o **deteção de rede** método para o site onde pretende detetar recursos de rede.  

3.  Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**.  

4.  Sobre o **gerais** separador, selecione a opção de **Ativar deteção de rede**.  

    - Selecione entre as **tipo de deteção** opções do tipo de deteção que pretende executar.  

    - Ativar a **rede lenta** opção para o Configuration Manager para fazer ajustes automáticos para redes de largura de banda baixa.  

5.  Para configurar a deteção para pesquisar sub-redes, mude para o **sub-redes** separador. Em seguida, configure uma ou mais das seguintes opções:  

    -   Para executar a deteção em sub-redes locais no computador que executa a deteção, ative a opção para **procurar sub-redes locais**.  

    -   Para pesquisar uma sub-rede específica, certifique-se de que a sub-rede está listada na **sub-redes para pesquisar** e tem um **pesquisa** valor de **ativado**:  

        1.  Se a sub-rede não estiver listada, selecione o **New** ícone ![novo ícone](media/Disc_new_Icon.gif). Na **nova atribuição de sub-rede** caixa de diálogo, introduza o **sub-rede** e **máscara** informações e, em seguida, selecione **OK**. Por predefinição, uma nova sub-rede está ativada para pesquisa.  

        2.  Para alterar o **pesquisa** valor para uma sub-rede listada, selecione-o na lista. Em seguida, selecione o **alternância** ícone para alternar o valor entre **desativada** e **ativado**.  

6.  Para configurar a deteção para pesquisar domínios, mude para o **domínios** separador. Em seguida, configure uma ou mais das seguintes opções:  

    -   Para executar a deteção no domínio do computador que executa a deteção, ative a opção para **Procurar domínio local**.  

    -   Para pesquisar um domínio específico, certifique-se de que o domínio está listado na **domínios** e tem um **pesquisa** valor de **ativado**:  

        1.  Se o domínio não estiver listado, selecione o **New** ícone ![novo ícone](media/Disc_new_Icon.gif). Na **propriedades do domínio** caixa de diálogo, introduza o **domínio** informações e, em seguida, selecione **OK**. Por predefinição, um novo domínio está ativado para pesquisa.  

        2.  Para alterar o **pesquisa** valor para um domínio listado, selecione-o na lista. Em seguida, selecione o **alternância** ícone para alternar o valor entre **desativada** e **ativado**.  

7.  Para configurar a deteção para pesquisar nomes de comunidades SNMP específicos para dispositivos SNMP, mude para o **SNMP** separador. Em seguida, configure uma ou mais das seguintes opções:  

    - Para adicionar um nome de Comunidade SNMP à lista de **nomes da Comunidade SNMP**, selecione a **New** ícone ![novo ícone](media/Disc_new_Icon.gif). Na **novo nome de Comunidade SNMP** caixa de diálogo caixa, especifique a **nome** da Comunidade SNMP e, em seguida, selecione **OK**.  

    - Para remover um nome de Comunidade SNMP, selecione o nome de Comunidade e, em seguida, selecione o **elimine** ícone ![ícone Eliminar](media/Disc_delete_Icon.gif).  

    - Para ajustar a ordem de pesquisa de nomes de comunidades SNMP, selecione um nome de Comunidade na lista. Em seguida, selecione o **Mover Item para cima** ícone ![mover até o ícone](media/Disc_moveUp_Icon.gif) ou o **Mover Item para baixo** ícone ![mover o ícone](media/Disc_moveDown_Icon.gif). Quando a deteção é executada, os nomes de Comunidades são pesquisados numa ordem de cima para baixo. 

    - Para configurar o número máximo de saltos de routers para utilização pelas pesquisas de SNMP, selecione o número de saltos do **saltos máximos** na lista pendente.  

8. Para configurar um dispositivo SNMP, mude para o **dispositivos SNMP** separador. Se o dispositivo não estiver listado, selecione o **New** ícone ![novo ícone](media/Disc_new_Icon.gif). Na **novo dispositivo SNMP** caixa de diálogo, especifique o nome de dispositivo ou endereço IP do dispositivo SNMP e, em seguida, selecione **OK**.  

    > [!NOTE]  
    >  Se especificar um nome de dispositivo, tem de ser capaz de resolver o nome NetBIOS para um endereço IP do Configuration Manager.  

9. Para configurar a deteção para consultar servidores DHCP específicos, mude para o **DHCP** separador. Em seguida, configure uma ou mais das seguintes opções:  

    -   Para consultar o servidor DHCP no computador que executa a deteção, ative a opção para **utilizam sempre o servidor DHCP do servidor de site**.  

        > [!NOTE]  
        >  Para utilizar esta opção, o servidor deve obter concessões de seu endereço IP de um servidor DHCP e não é possível utilizar um endereço IP estático.  

    -   Para consultar um servidor DHCP específico, selecione o **New** ícone ![novo ícone](media/Disc_new_Icon.gif). Na **novo servidor DHCP** caixa de diálogo, especifique o nome de servidor ou endereço IP do servidor DHCP e, em seguida, selecione **OK**.  

        > [!NOTE]  
        >  Se especificar um nome de servidor, tem de ser capaz de resolver o nome NetBIOS para um endereço IP do Configuration Manager.  

10. Para configurar a execução da deteção, mude para o **agenda** separador. Em seguida, selecione o **New** ícone ![novo ícone](media/Disc_new_Icon.gif) para agendar a execução da deteção de rede. Pode configurar vários agendamentos periódicos e vários agendamentos sem periodicidade.  

    > [!NOTE]  
    >  Se o **agenda** separador mostra mais do que uma agenda ao mesmo tempo, a deteção de rede é executada para todas as agendas porque esta está configurada à hora indicada na agenda. Esse comportamento também é verdade para agendamentos periódicos.  

11. Selecione **OK** para guardar as configurações.  


###  <a name="BKMK_HowToVerifyNetDisc"></a> Como verificar se a deteção de rede foi concluída  

 O tempo que a deteção de rede necessita para concluir pode variar dependendo um ou mais dos seguintes fatores:  

-   O tamanho da sua rede  

-   A topologia da rede  

-   O número máximo de saltos configurados para localizar routers na rede  

-   O tipo de deteção que está a ser executado  

Deteção de rede não cria mensagens para o alertar quando for concluído. Utilize o procedimento seguinte para verificar quando a deteção foi concluída:  

1.  Na consola do Configuration Manager, vá para o **monitorização** área de trabalho. Expanda **estado do sistema**e, em seguida, selecione a **consultas de mensagens de estado** nó.  

2.  Selecione o **todas as mensagens de estado** consulta.  

3.  Sobre o **home page** separador do Friso, no **consultas de mensagens de estado** grupo, selecione **Mostrar mensagens**.  

4.  Na janela de todas as mensagens de estado, selecione um valor de **selecione a data e hora** na lista pendente que inclua há quanto tempo a deteção foi iniciada. Em seguida, selecione **OK** para abrir o **Configuration Manager Status Message Viewer**.  

    > [!TIP]  
    >  Também pode utilizar o **especificar a data e hora** opção de selecionar uma data e hora a que tenha executado a deteção. Esta opção é útil quando executado a deteção de rede numa determinada data e pretender obter mensagens apenas dessa data.  

5.  Para validar que a deteção de rede foi concluída, procure uma mensagem de estado que tem os seguintes detalhes:  

    -   ID da mensagem: **502**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrição: **Este componente parada**  

    Se esta mensagem de estado não estiver presente, a deteção de rede não foi concluída.  

7.  Para validar quando iniciado a deteção de rede, procure uma mensagem de estado que tem os seguintes detalhes:  

    -   ID da mensagem: **500**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrição: **Este componente foi iniciado**  

    Esta informação confirma que a deteção de rede foi iniciada. Se esta informação não estiver presente, reagende a deteção de rede.  
