---
title: Métodos de deteção
titleSuffix: Configuration Manager
description: Saiba mais sobre os métodos de deteção disponíveis para localizar dispositivos na sua rede, a partir do Active Directory ou do Azure Active Directory.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
caps.latest.revision: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e53eb90b55034479ba3d278b4b19879f2ee1e4b7
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>Acerca dos métodos de deteção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Métodos de deteção do Configuration Manager localizar dispositivos diferentes na sua rede, dispositivos e utilizadores do Active Directory ou utilizadores do Azure Active Directory (Azure AD). Para utilizar eficazmente um método de deteção, deve compreender as respetivas configurações disponíveis e limitações.  



##  <a name="bkmk_aboutForest"></a> Deteção de florestas do Active Directory  
 **Configurável:** Sim  

 **Ativado por predefinição:** Não  

 **Contas** pode utilizar para executar este método:  

-   **Conta de deteção de floresta do Active Directory** (definido pelo utilizador)  

-   **Conta de computador** do servidor do site  

Ao contrário de outros métodos de deteção do Active Directory, a deteção de floresta do Active Directory não Deteta recursos que pode gerir. Em vez disso, este método Deteta localizações de rede que estão configuradas no Active Directory. Pode converter essas localizações em limites para utilização em toda a hierarquia.  

Quando este método é executado, este procura floresta do Active Directory local, cada floresta fidedigna e em cada floresta adicional configurada no **florestas do Active Directory** nós da consola do Configuration Manager.  

Deteção de floresta de diretório do Active Directory de utilização para:  

-   Detetar sub-redes e sites do Active Directory e, em seguida, criar limites do Configuration Manager com base nessas localizações de rede.  

-   Identifica supernets que estão atribuídos a um site do Active Directory. Converta cada Super-rede num limite de intervalo de endereços IP.  

-   Publicar nos serviços de domínio do Active Directory (AD DS) numa floresta quando a publicação nessa floresta está ativada. A conta de floresta do Active Directory especificado tem de ter permissões para essa floresta.  

Pode gerir a deteção de floresta do Active Directory na consola do Configuration Manager. Vá para o **administração** área de trabalho e expanda **configuração da hierarquia**.   

-   **Métodos de deteção**: Ative a deteção de floresta do Active Directory ser executada no site de nível superior da sua hierarquia. Também pode especificar uma agenda simples para executar a deteção. Configure-o para criar automaticamente limites a partir de sub-redes IP e sites do Active Directory que Deteta. Não é possível executar a deteção de florestas do Active Directory num site primário subordinado ou num site secundário.  

-   **Florestas do Active Directory**: Configurar as florestas adicionais para detetar, especificar a cada conta de floresta do Active Directory e configurar a publicação em cada floresta. Monitorize o processo de deteção. Adicione sub-redes IP e sites do Active Directory como limites do Configuration Manager e membros de grupos de limites.  

Para configurar a publicação para florestas do Active Directory para cada site na sua hierarquia, ligue a consola do Configuration Manager para o site de nível superior da hierarquia. O **publicação** separador um site do Active Directory **propriedades** caixa de diálogo pode mostrar apenas o site atual e os sites subordinados. Quando a publicação está ativada para uma floresta e o esquema dessa floresta está expandida para o Configuration Manager, são publicadas as seguintes informações para cada site que pode publicar nessa floresta do Active Directory:  

-    **SMS-Site -&lt;código do site >**

-   **SMS-MP -&lt;código do site >-&lt;nome de servidor do sistema de sites >**  

-   **SMS-SLP -&lt;código do site >-&lt;nome de servidor do sistema de sites >**  

-   **SMS -&lt;código do site >-&lt;nome de site do Active Directory ou sub-rede >**  

> [!NOTE]  
>  Os sites secundários utilizam sempre a conta de computador de servidor do site secundário para publicar no Active Directory. Se pretender que os sites secundários para publicar no Active Directory, certifique-se de que a conta de computador do servidor de site secundário tem permissões para publicar no Active Directory. Um site secundário não é possível publicar dados numa floresta não fidedigna.  

> [!CAUTION]  
>  Ao desmarcar a opção de publicar um site a uma floresta do Active Directory, todas as informações publicadas anteriormente para esse site, incluindo funções de sistema de sites disponíveis, são removidas do Active Directory.  

As ações de deteção de floresta do Active Directory são registadas nos seguintes registos:  

-   Todas as ações, exceto as ações relacionadas com publicação, são registadas no ficheiro de **ADForestDisc.Log** ficheiros o  **&lt;Caminhodeinstalação > \Logs** pasta no servidor do site.  

-   Deteção de florestas do Active Directory publicação ações são registadas no **hman.log** e **sitecomp.log** ficheiros no  **&lt;Caminhodeinstalação > \Logs** pasta no servidor do site.  

Para obter mais informações sobre como configurar este método de deteção, consulte [configurar métodos de deteção](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADForestDisc).  



##  <a name="bkmk_aboutGroup"></a> Deteção de grupos do Active Directory  
**Configurável:** Sim  

**Ativado por predefinição:** Não  

**Contas** pode utilizar para executar este método:  

-   **Conta de deteção de grupo do Active Directory** (definido pelo utilizador)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Para além das informações nesta secção, consulte [funcionalidades comuns de grupos do Active Directory, sistema e deteção de utilizadores](#bkmk_shared).  

Utilize este método para pesquisar os serviços de domínio do Active Directory para identificar:  

-   Grupos de segurança locais, globais e universais.  

-   A associação de grupos.  

-   Informações limitadas sobre utilizadores, mesmo quando outro método de deteção não foi anteriormente detetada esses computadores e utilizadores e computadores membros do grupo.  

Este método de deteção destina-se para identificar grupos e as relações de grupo dos membros dos grupos. Por predefinição, são detetados apenas os grupos de segurança. Se pretender também encontrar a associação dos grupos de distribuição, tem de selecionar a caixa para a opção **detetar a associação dos grupos de distribuição** no **opção** separador o **propriedades de deteção de grupo do Active Directory** caixa de diálogo.  

Deteção de grupos do Active Directory não suporta os atributos expandidos do Active Directory que podem ser identificados através de deteção de sistema do Active Directory ou a deteção de utilizador do Active Directory. Uma vez que este método de deteção não está otimizado para detetar recursos de computador e utilizador, considere executar este método de deteção depois de ter executado a deteção de sistema do Active Directory e deteção de utilizador do Active Directory. Este sugestão é porque este método cria um registo de dados de deteção completa (DDR) de grupos, mas apenas um DDR limitado de computadores e utilizadores que são membros dos grupos.  

Pode configurar os seguintes âmbitos de deteção que controlam a forma como este método procura informações:  

-   **Localização**: Utilize uma localização se pretender pesquisar um ou mais contentores do Active Directory. Esta opção de âmbito suporta uma pesquisa recursiva dos contentores do Active Directory especificados. Este processo pesquisa cada contentor subordinado no contentor que especificar. Continua até encontram-se não existem mais contentores subordinados.  

-   **Grupos**: Utilize grupos se pretender pesquisar um ou mais grupos do Active Directory específicos. Pode configurar **domínio do Active Directory** para utilizar o domínio predefinido e a floresta ou limitar a procura a um controlador de domínio individuais. Além disso, pode especificar um ou mais grupos a pesquisar. Se não especificar pelo menos um grupo, todos os grupos encontrados na especificado **domínio do Active Directory** localização serão pesquisados.  

> [!CAUTION]  
>  Quando configurar um âmbito de deteção, selecione apenas os grupos que tem de detetar. Esta recomendação é porque a deteção de grupo do Active Directory tentar detetar cada membro de cada grupo do âmbito de deteção. Deteção de grupos grandes pode necessitar de utilizar muita largura de banda e de recursos do Active Directory.  

> [!NOTE]  
>  Antes de poder criar coleções baseadas em atributos expandidos do Active Directory e, para garantir resultados de deteção exatos de computadores e utilizadores, executar a deteção de sistema do Active Directory ou a deteção de utilizador do Active Directory, consoante o que pretende detete.  

As ações de deteção de grupo do Active Directory são registadas no ficheiro **adsgdis.log** no  **&lt;Caminhodainstalação\>\LOGS** pasta no servidor do site.  

Para obter mais informações sobre como configurar este método de deteção, consulte [configurar métodos de deteção](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



##  <a name="bkmk_aboutSystem"></a> Deteção de sistemas do Active Directory  
**Configurável:** Sim  

**Ativado por predefinição:** Não  

**Contas** pode utilizar para executar este método:  

-   **Conta de deteção de sistema do Active Directory** (definido pelo utilizador)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Para além das informações nesta secção, consulte [funcionalidades comuns de grupos do Active Directory, sistema e deteção de utilizadores](#bkmk_shared).  

Utilize este método de deteção para pesquisar as serviços de domínio do Active Directory nas localizações especificadas de recursos de computador que podem ser utilizados para criar coleções e consultas. Também pode instalar o cliente do Configuration Manager num dispositivo detetado utilizando a instalação de push de cliente.  

Por predefinição, este método Deteta informações básicas sobre o computador, incluindo os seguintes atributos:  

-   Nome do computador  

-   Sistema operativo e versão  

-   Nome de contentor do Active Directory  

-   Endereço IP  

-   Site de Active Directory  

-   Carimbo de hora do último início de sessão  

Para criar com êxito um DDR para um computador, deteção de sistema do Active Directory tem de conseguir identificar a conta de computador e, em seguida, resolver o nome do computador com êxito para um endereço IP.  

No **propriedades de deteção de sistema do Active Directory** caixa de diálogo a **atributos do Active Directory** separador, pode ver a lista completa dos atributos de objetos predefinidos que Deteta. Também pode configurar o método para detetar adicionais atributos (expandidos).  

As ações de deteção de sistema do Active Directory são registadas no ficheiro **adsysdis.log** no  **&lt;Caminhodainstalação\>\LOGS** pasta no servidor do site.  

Para obter mais informações sobre como configurar este método de deteção, consulte [configurar métodos de deteção](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



##  <a name="bkmk_aboutUser"></a> Deteção de utilizadores do Active Directory  
**Configurável:** Sim  

**Ativado por predefinição:** Não  

**Contas** pode utilizar para executar este método:  

-   **Conta de deteção de utilizador do Active Directory** (definido pelo utilizador)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Para além das informações nesta secção, consulte [funcionalidades comuns de grupos do Active Directory, sistema e deteção de utilizadores](#bkmk_shared).  

Utilize este método de deteção para pesquisar os serviços de domínio do Active Directory e identificar contas de utilizador e atributos associados. Por predefinição, este método Deteta informações básicas sobre a conta de utilizador, incluindo os seguintes atributos:  

-   Nome de utilizador  

-   Nome de utilizador exclusivo (inclui o nome de domínio)  

-   Domain  

-   Nomes de contentor do Active Directory  

No **propriedades de deteção de utilizador do Active Directory** caixa de diálogo a **atributos do Active Directory** separador, pode ver a lista completa de atributos de objetos que Deteta. Também pode configurar o método para detetar adicionais atributos (expandidos).

As ações de deteção de utilizador do Active Directory são registadas no ficheiro **adusrdis.log** no  **&lt;Caminhodainstalação\>\LOGS** pasta no servidor do site.  

Para obter mais informações sobre como configurar este método de deteção, consulte [configurar métodos de deteção](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



## <a name="azureaddisc"></a> Deteção de utilizadores do Azure Active Directory
Utilize a deteção de utilizadores do Azure Active Directory (Azure AD) para procurar a sua subscrição do Azure AD para os utilizadores com uma identidade de nuvem modernas. Deteção de utilizadores do Azure AD pode encontrar os seguintes atributos:  
-   objectId
-   displayName
-   capacidade de correio
-   mailNickname
-   onPremisesSecurityIdentifier
-   userPrincipalName
-   TenantID do AAD

Este método suporta a sincronização completa e diferenças de atributos de utilizador do Azure AD. Estas informações, em seguida, podem estar recolher a partir de outros métodos de deteção de dados de deteção do juntamente lado utilizado.

As ações de deteção de utilizadores do Azure AD são registadas no ficheiro de **SMS_AZUREAD_DISCOVERY_AGENT.log** ficheiro no servidor do site de nível superior da hierarquia.

Para configurar a deteção de utilizadores do Azure AD, consulte [configurar os serviços do Azure](/sccm/core/servers/deploy/configure/Azure-services-wizard) para gestão de nuvem. Para obter informações sobre como configurar este método de deteção, consulte [configurar o Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).



##  <a name="bkmk_aboutHeartbeat"></a> Deteção de heartbeat  
**Configurável:** Sim  

**Ativado por predefinição:** Sim  

**Contas** pode utilizar para executar este método:  

-   **Conta de computador** do servidor do site  

Deteção de heartbeat difere de outros métodos de deteção do Configuration Manager. Está ativada por predefinição e é executada em cada computador cliente (em vez de num servidor do site) para criar um DDR. Para clientes de dispositivos móveis, este DDR é criado pelo ponto de gestão que está a utilizar o cliente do dispositivo móvel. Para ajudar a manter o registo da base de dados de clientes do Configuration Manager, não desative a deteção de Heartbeat. Para além de manter o registo da base de dados, este método pode forçar a deteção de um computador como um novo registo de recursos. Também se pode repovoar o registo da base de dados de um computador que tenha sido eliminado da base de dados.  

Deteção de heartbeat é executada segundo uma agenda configurada para todos os clientes na hierarquia. A agenda predefinida para a deteção de Heartbeat é definida para cada sete dias. Se alterar o intervalo de deteção de heartbeat, certifique-se de que é executada com maior frequência com que a tarefa de manutenção do site **eliminar dados de deteção desatualizados**. Esta tarefa elimina registos de clientes Inativos da base de dados do site. Pode configurar o **eliminar dados de deteção desatualizados** tarefa apenas para sites primários. 

Pode também manualmente invocar deteção de Heartbeat no cliente específico. Execute o **ciclo de recolha de dados de deteção** no **ação** separador do Configuration Manager de um cliente painel de controlo.  

Quando a deteção de Heartbeat é executada, cria um DDR que tem as informações do cliente atual. O cliente copia, em seguida, este ficheiro pequeno (cerca de 1 KB de tamanho) para um ponto de gestão para que um site primário pode processá-la. O ficheiro tem as seguintes informações:  

-   Localização de rede  

-   Nome NetBIOS  

-   Versão do agente cliente  

-   Detalhes do Estado operacional  

Deteção de heartbeat é o único método de deteção que fornece detalhes sobre o estado de instalação do cliente. Isto é feito ao atualizar o atributo de cliente de recursos do sistema para definir um valor igual a **Sim**.  

> [!NOTE]  
>  Mesmo quando a deteção de Heartbeat estiver desativada, o DDR ainda são criados e submetidos para clientes de dispositivos móveis ativos. Este comportamento garante que a tarefa **eliminar dados de deteção desatualizados** não afeta dispositivos móveis ativos. Quando o **eliminar dados de deteção desatualizados** tarefa elimina um registo de base de dados para um dispositivo móvel, revoga também o certificado do dispositivo. Esta ação impede o dispositivo móvel de estabelecer ligação a pontos de gestão.  

As ações de deteção de Heartbeat são registadas nas seguintes localizações:  

-   Para clientes de computador, as ações de deteção de Heartbeat são registadas no cliente no **InventoryAgent.log** ficheiros o *%Windir%\CCM\Logs* pasta.  

-   Para clientes de dispositivos móveis, as ações de deteção de Heartbeat são registadas no **DMPRP.log** ficheiros o *% programa Files%\CCM\Logs* pasta do ponto de gestão utilizado pelo cliente de dispositivo móvel.  

Para obter mais informações sobre como configurar este método de deteção, consulte [configurar métodos de deteção](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigHBDisc).  



##  <a name="bkmk_aboutNetwork"></a> Deteção de rede  
**Configurável:** Sim  

**Ativado por predefinição:** Não  

**Contas** pode utilizar para executar este método:  

-   **Conta de computador** do servidor do site  

Utilize este método para detetar a topologia da rede e para detetar dispositivos de rede que têm um endereço IP. Deteção de rede procura a sua rede para recursos IP ativados consultando as entidades seguintes: 
- Servidores que executam uma implementação Microsoft da DHCP
- Coloca em cache do protocolo ARP (Address Resolution Protocol) em routers de rede
- Dispositivos SNMP ativados
- Domínios do Active Directory  

Antes de poder utilizar a deteção de rede, tem de especificar o *nível* de deteção a executar. Também configurar um ou mais mecanismos de deteção que permitem a deteção de rede consultar segmentos de rede ou dispositivos. Também pode configurar as definições que ajudam a ações da deteção de controlo na rede. Finalmente, deverá definir uma ou mais agendas para execução da deteção de rede.  

Para que este método detetar com êxito um recurso, a deteção de rede tem de identificar o endereço IP e a máscara de sub-rede do recurso. Os métodos seguintes são utilizados para identificar a máscara de sub-rede de um objeto:  

-   **Cache ARP do router:** Deteção de rede consulta a cache ARP de um router para localizar as informações de sub-rede. Normalmente, os dados de uma ARP cache do router possuem um curto período de tempo-to-live. Por conseguinte, quando a deteção de rede consulta a cache ARP, a cache ARP poderá já não ter informações sobre o objeto pedido.  

-   **DHCP:** Deteção de rede consulta cada servidor DHCP que especificar para detetar os dispositivos para o qual o servidor DHCP forneceu uma concessão. Deteção de rede suporta apenas servidores DHCP que executem a implementação Microsoft da DHCP.  

-   **Dispositivo SNMP:** Deteção de rede pode consultar diretamente um dispositivo SNMP. Deteção de rede consultar um dispositivo, o dispositivo tem de ter um agente SNMP local instalado. Também configure a deteção de rede para utilizar o nome de Comunidade que está a utilizar o agente de SNMP.  

Quando a deteção identifica um objeto endereçável por IP e pode determinar a máscara de sub-rede do objeto, cria um DDR para esse objeto. Como diversos tipos de dispositivos ligar à rede, a deteção de rede Deteta recursos que não suportam o cliente do Configuration Manager. Por exemplo, os dispositivos que podem ser detetados mas não geridos incluem impressoras e routers.  

Deteção de rede poderá devolver vários atributos como parte do registo de deteção que cria. Estes atributos incluem:  

-   Nome NetBIOS  

-   Endereços IP  

-   Domínio de recurso  

-   Funções do sistema  

-   Nome de Comunidade SNMP  

-   Endereços MAC  

Atividade da deteção de rede é registada no **Netdisc.log** ficheiros  *&lt;Caminhodainstalação\>\Logs* no servidor do site que executa a deteção.  

 Para obter mais informações sobre como configurar este método de deteção, consulte [configurar métodos de deteção](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Redes complexas e ligações de largura de banda baixa podem fazer com que a deteção de rede para abrandar e gerar tráfego de rede significativo. Como melhor prática, execute a deteção de rede apenas quando os outros métodos de deteção não é possível localizar os recursos que tem de detetar. Por exemplo, utilize a deteção de rede se precisar de detetar computadores de grupo de trabalho. Outros métodos de deteção não detetar computadores de grupo de trabalho.  

###  <a name="BKMK_NetDiscLevels"></a> Níveis de deteção de rede  
Ao configurar a deteção de rede, tem de especificar um de três níveis de Deteção:  

|Nível de deteção|Detalhes|  
|------------------------|-------------|  
|Topologia|Este nível Deteta routers e sub-redes, mas não identifica uma máscara de sub-rede para objetos.|  
|Topologia e cliente|Além da topologia, este nível Deteta potenciais clientes, como computadores e recursos, como impressoras e routers. Este nível de deteção tenta identificar a máscara de sub-rede dos objetos que encontra.|  
|Sistema operativo topologia, cliente e cliente|Para além da topologia e potenciais clientes, este nível tenta detetar o nome de sistema operativo do computador e a versão. Este nível utiliza o Browser do Windows e chamadas de rede do Windows.|  

 Com cada nível incremental, a deteção de rede aumenta a sua atividade e a utilização de largura de banda de rede. Considere o tráfego de rede que pode ser gerado antes de ativar todos os aspetos da deteção de rede.  

 Por exemplo, quando utilizar a deteção de rede pela primeira vez, poderá começar com o nível de topologia para identificar a sua infraestrutura de rede. Em seguida, reconfigure a deteção de rede para detetar objetos e os respetivos sistemas operativos de dispositivos. Também pode configurar as definições que limitam a deteção de rede a um intervalo específico de segmentos de rede. Dessa forma, pode detetar os objetos em localizações de rede que necessite e evitar o tráfego de rede desnecessário. Este processo também permite-lhe detetar objetos de routers na margem ou a partir de fora da rede.  

###  <a name="BKMK_NetDiscOptions"></a> Opções de deteção de rede  
Para ativar a deteção de rede procurar dispositivos endereçáveis por IP, configure uma ou mais destas opções.  

> [!NOTE]  
>  Deteção de rede é executada no contexto da conta de computador do servidor do site que executa a deteção. Se a conta de computador não tem permissões para um domínio não fidedigno, o domínio e as configurações de servidor DHCP podem não conseguir detetar recursos.  

#### <a name="dhcp"></a>DHCP  

Especifique cada servidor DHCP que pretende que a deteção de rede para consulta. (A deteção de rede suporta apenas servidores DHCP que executem a implementação Microsoft da DHCP.)  

-   Deteção de rede obtém as informações utilizando chamadas de procedimento remoto para a base de dados no servidor DHCP.  

-   Deteção de rede pode consultar servidores DHCP de 32 bits e 64 bits para uma lista de dispositivos que estejam registados junto de cada servidor.  

-   Deteção de rede consultar com êxito um servidor DHCP, a conta de computador do servidor que executa a deteção tem de ser um membro do grupo utilizadores de DHCP no servidor DHCP. Por exemplo, este nível de acesso existe quando uma das instruções seguintes for verdadeira:  

    -   O servidor DHCP especificado é o servidor DHCP do servidor que executa a deteção.  

    -   O computador que executa a deteção e o servidor DHCP estão no mesmo domínio.  

    -   Existe uma fidedignidade bidirecional entre o computador que executa a deteção e o servidor DHCP.  

    -   O servidor do site é um membro do grupo de utilizadores de DHCP.  

-   Quando a deteção de rede enumera um servidor DHCP,-lo nem sempre Deteta endereços IP estáticos. Deteção de rede não encontra endereços IP que fazem parte de um excluídos intervalo de endereços IP no servidor DHCP. Também não Deteta endereços IP que estão reservados para atribuição manual.  

#### <a name="domains"></a>Domínios  

Especifique cada domínio que pretende que a deteção de rede para consulta.  

-   A conta de computador do servidor do site que executa a deteção tem de ter permissões para ler os controladores de domínio em cada domínio especificado.  

-   Para detetar computadores do domínio local, tem de ativar o serviço de Browser de computador em, pelo menos, um computador. Este computador tem de estar na mesma sub-rede que o servidor de site que executa a deteção de rede.  

-   Deteção de rede poderá detetar qualquer computador que pode ver a partir do seu servidor de site quando navega na rede.  

-   Deteção de rede obtém o endereço IP. Em seguida, utiliza um pedido de eco Internet Control Message Protocol (ICMP) para enviar um ping cada dispositivo que encontrar. O **ping** comando ajuda a determinar quais os computadores que se encontram atualmente ativos.  

#### <a name="snmp-devices"></a>Dispositivos SNMP  

Especifique cada dispositivo SNMP que pretende que a deteção de rede para consulta.  

-   Deteção de rede obtém o valor de ipNetToMediaTable de qualquer dispositivo SNMP que responda à consulta. Este valor devolve matrizes de endereços IP que sejam computadores cliente ou outros recursos, como impressoras, routers ou outros dispositivos endereçáveis por IP.  

-   Para consultar um dispositivo, tem de especificar o endereço IP ou nome NetBIOS do dispositivo.  

-   Configurar a deteção de rede para utilizar o nome de Comunidade do dispositivo ou o dispositivo rejeitará a consulta baseadas em SNMP.  


###  <a name="BKMK_LimitNetDisc"></a> Limitar a deteção de rede  
Quando a deteção de rede consultar um dispositivo SNMP na margem da rede, poderá identificar informações sobre sub-redes e dispositivos SNMP que estejam fora da rede imediata. Utilize as seguintes informações para limitar a deteção de rede, configurando os dispositivos SNMP que a deteção pode comunicar e especificando os segmentos de rede a consultar.  

#### <a name="subnets"></a>Sub-redes  

Configure as sub-redes que consultas de deteção de rede quando utiliza as opções de SNMP e DHCP. Estas duas opções de pesquisa apenas sub-redes ativadas.  

Por exemplo, um pedido DHCP poderá devolver dispositivos a partir de localizações em toda a rede. Se pretender detetar apenas os dispositivos numa sub-rede específica, especifique e ative essa sub-rede no **sub-redes** separador o **propriedades da deteção de rede** caixa de diálogo. Quando especificar e ativar sub-redes, limita tarefas futuras de deteção DHCP e SNMP a essas sub-redes.  

> [!NOTE]  
>  Configurações de sub-rede não limitam os objetos que o **domínios** opção de deteção Deteta.  

#### <a name="snmp-community-names"></a>Nomes de comunidades SNMP  

Para ativar a deteção de rede consultar com êxito um dispositivo SNMP, configure a deteção de rede com o nome de Comunidade do dispositivo. Se a deteção de rede não estiver configurada utilizando o nome de Comunidade do dispositivo SNMP, o dispositivo rejeitará a consulta.  

#### <a name="maximum-hops"></a>Saltos máximos  

Quando configurar o número máximo de saltos de routers, limita o número de segmentos de rede e routers que a deteção de rede pode consultar utilizando SNMP.  

O número de saltos que configura limita o número de dispositivos adicionais e segmentos de rede que a deteção de rede pode consultar.  

Por exemplo, uma deteção só de topologia com **0** (zero) saltos de routers Deteta a sub-rede onde reside o servidor de origem. Inclui todos os routers dessa sub-rede.  

O diagrama seguinte mostra o que uma topologia só de deteção de rede consulta encontra quando é executada no servidor 1 com 0 saltos de routers especificados: a sub-rede D e o Router 1.  

 ![Imagem de deteção com zero ir de router](media/Disc-0.gif)  

 O diagrama seguinte mostra que topologia e cliente encontra de consulta de deteção de rede quando é executada no servidor 1 com 0 saltos de routers especificados: a sub-rede D e o Router 1 e todos os potenciais clientes na sub-rede D.  

 ![Imagem de deteção com um router ir](media/Disc-1.gif)  

 Para obter uma ideia mais concreta do router adicional como saltos podem aumentar a quantidade de recursos de rede que são detetados, considere a rede seguinte:  

 ![Imagem de deteção com dois hiperligações de router](media/Disc-2.gif)  

 Executar uma deteção de rede só de topologia de servidor 1 com um salto de router Deteta as entidades seguintes:  

-   O router 1 e a sub-rede 10.1.10.0 (localizados com zero saltos)  

-   As sub-redes 10.1.20.0 e 10.1.30.0, a sub-rede d e Router 2 (localizados no primeiro salto)  

> [!WARNING]  
>  Cada aumento do número de saltos de router significativamente pode aumentar o número de recursos Detetáveis e aumentar a largura de banda de rede que utiliza a deteção de rede.  



##  <a name="bkmk_aboutServer"></a> Deteção de servidores  
**Configurável:** Não  

Para além dos métodos de deteção configuráveis de utilizador, o Configuration Manager utiliza um processo denominado **a deteção de servidores** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Este método de deteção cria registos de recursos para computadores que são os sistemas de sites, como um computador que está configurado como um ponto de gestão.  



##  <a name="bkmk_shared"></a> Funcionalidades comuns de deteção de grupo do Active Directory, a deteção de sistema e a deteção de utilizador  
Esta secção fornece informações sobre as funcionalidades que são comuns para os seguintes métodos de Deteção:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

> [!NOTE]  
>  As informações nesta secção não se aplica a deteção de floresta do Active Directory.  

Estes três métodos de deteção são semelhantes na configuração e a operação. Que estes possam detetar computadores, utilizadores e informações sobre associações a grupos de recursos que estão armazenadas nos serviços de domínio do Active Directory. O processo de deteção é gerido por um agente de deteção. O agente é executado no servidor do site em cada site em que a deteção está configurada para executar. Pode configurar cada um destes métodos de deteção para pesquisar um ou mais localizações do Active Directory como instâncias de localização na floresta local ou em florestas remotas.  

Quando a deteção procurar recursos numa floresta não fidedigna, o agente de deteção tem de ser capaz de resolver os seguintes seja concluída com êxito:  

-   Para detetar um recurso de computador através da utilização de deteção de sistema do Active Directory, o agente de deteção tem de conseguir resolver o FQDN do recurso. Se não conseguir resolver o FQDN, este tenta, em seguida resolver o recurso pelo respetivo nome NetBIOS.  

-   Para detetar um utilizador ou o recurso do grupo ao utilizar a deteção de utilizador do Active Directory ou a deteção de grupo do Active Directory, o agente de deteção tem de conseguir resolver o FQDN do nome de controlador de domínio que especificou para a localização do Active Directory.  

Para cada localização que especificar, pode configurar opções de pesquisa individuais, como ativar uma pesquisa recursiva dos contentores de subordinados a localização do Active Directory. Também pode configurar uma conta exclusiva para utilização quando pesquisar essa localização. Esta conta proporciona flexibilidade na configuração de um método de deteção num site para pesquisar várias localizações do Active Directory em várias florestas. Não tem de configurar uma conta única que tem permissões para todas as localizações.  

Quando cada um destes três métodos de deteção é executada num site específico, o servidor de site do Configuration Manager nesse site contacta o controlador de domínio mais próximo na floresta do Active Directory especificada para localizar recursos do Active Directory. O domínio e a floresta podem estar em qualquer modo suportado do Active Directory. A conta que atribuir a cada instância de localização deve ter **leitura** permissão às localizações especificadas do Active Directory de acesso.

Deteção de pesquisa de objetos nas localizações especificadas e, em seguida, tenta recolher informações sobre esses objetos. É criado um DDR quando podem ser identificadas informações suficientes sobre um recurso. As informações necessárias variam consoante o método de deteção que está a ser utilizado.  

Se configurar o mesmo método de deteção para ser executada em diferentes sites do Configuration Manager para tirar partido da consulta de servidores locais do Active Directory, pode configurar cada site com um conjunto exclusivo de opções de deteção. Porque os dados de deteção estão partilhados com cada site na hierarquia, evite a sobreposição destas configurações para detetar eficazmente cada recurso uma única vez.

Para ambientes menores, considere executar cada método de deteção apenas num site na sua hierarquia. Esta configuração reduz a sobrecarga administrativa e a possibilidade de múltiplas ações de deteção detetar novamente os mesmos recursos. Quando está a minimizar o número de sites que executar a deteção, pode reduzir a largura de banda de rede global que a deteção utiliza. Também pode reduzir o número global de DDRs que são criados e têm de ser processados pelos servidores do site.  

Muitas das configurações de método de deteção dispensam explicações. Utilize as secções seguintes para obter mais informações sobre as opções de deteção que poderão necessitar de informações adicionais antes de as configurar.  

As seguintes opções estão disponíveis para utilização com vários métodos de deteção do Active Directory:  

-   [Delta Discovery](#bkmk_delta)  

-   [Filtrar registos de computador obsoletos pelo início de sessão de domínio](#bkmk_stalelogon)  

-   [Filtrar registos obsoletos por palavra-passe de computador](#bkmk_stalepassword)  

-   [Procurar atributos personalizados do Active Directory](#bkmk_customAD)  


###  <a name="bkmk_delta"></a> Delta Discovery  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

A deteção de diferenças não é um método de deteção independentes, mas uma opção disponível para os métodos de deteção aplicável. A deteção de diferenças pesquisa atributos específicos do Active Directory para que as alterações efetuadas desde o último ciclo de deteção completa do método de deteção aplicável. As alterações de atributos são submetidas na base de dados do Configuration Manager para atualizar o registo de deteção do recurso.  

Por predefinição, a deteção de diferenças é executada num ciclo de cinco minutos. Esta agenda é muito mais frequente do que a agenda típica para um ciclo de deteção completa. Este ciclo frequente é possível porque a deteção de diferenças utiliza menos servidor do site e faz a recursos de rede que um ciclo de deteção completa. Quando utilizar a deteção de diferenças, pode reduzir a frequência do ciclo de deteção completa para esse método de deteção.  

Seguem-se as alterações mais comuns pela deteção de diferenças:  

-   Novos computadores ou utilizadores adicionados ao Active Directory  

-   Alterações às informações de computador e utilizador básicas  

-   Novos computadores ou utilizadores que são adicionados a um grupo  

-   Computadores ou utilizadores que são removidos de um grupo  

-   Alterações a objetos do grupo de sistema  

Embora a deteção de diferenças pode detetar novos recursos e as alterações à associação ao grupo, não consegue detetar quando um recurso foi eliminado do Active Directory. DDR criado pela deteção de diferenças é processado de forma semelhante aos DDR criados por um ciclo de deteção completa.  

Configurar a deteção de diferenças no **agenda de consulta** separador nas propriedades de cada método de deteção.  


###  <a name="bkmk_stalelogon"></a> Filtrar registos de computador obsoletos pelo início de sessão de domínio  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

Pode configurar a deteção para excluir computadores com um registo de computador obsoletos. Esta exclusão é baseado no último início de sessão de domínio do computador. Quando esta opção estiver ativada, a deteção de sistema do Active Directory avalia todos os computadores que identifica. Deteção de grupos do Active Directory avalia todos os computadores que seja um membro de um grupo que é detetado.  

Para utilizar esta opção:  

-   Computadores têm de ser configurados para atualizar o **lastLogonTimeStamp** atributo no Active Directory Domain Services.  

-   Tem de definir o nível funcional de domínio do Active Directory para o Windows Server 2003 ou posterior.  

Quando estiver a configurar o tempo após o último início de sessão que pretende utilizar para esta definição, considere o intervalo de replicação entre controladores de domínio.  

Configurar a filtragem de **opção** separador o **propriedades de deteção de sistema do Active Directory** e **propriedades de deteção de grupo do Active Directory** caixas de diálogo. Optar por **detetar apenas os computadores que iniciaram sessão domínio num determinado período de tempo**.  

> [!WARNING]  
>  Quando configura este filtro e **filtrar registos obsoletos por palavra-passe de computador**, deteção exclui os computadores que cumprem os critérios de um filtro.  


###  <a name="bkmk_stalepassword"></a> Filtrar registos obsoletos por palavra-passe de computador  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

Pode configurar a deteção para excluir computadores com um registo de computador obsoletos. Esta exclusão é baseado da última atualização de palavra-passe de conta de computador pelo computador. Quando esta opção estiver ativada, a deteção de sistema do Active Directory avalia todos os computadores que identifica. Deteção de grupos do Active Directory avalia todos os computadores que seja um membro de um grupo que é detetado.  

Para utilizar esta opção:  

-   Computadores têm de ser configurados para atualizar o **pwdLastSet** atributo no Active Directory Domain Services.  

Quando estiver a configurar esta opção, considere o intervalo das atualizações para este atributo. Também considere o intervalo de replicação entre controladores de domínio.  

Configurar a filtragem de **opção** separador o **propriedades de deteção de sistema do Active Directory** e **propriedades de deteção de grupo do Active Directory** caixas de diálogo. Optar por **detetar apenas os computadores que atualizaram a sua palavra-passe da conta de computador num determinado período de tempo**.  

> [!WARNING]  
>  Quando configura este filtro e **filtrar registos obsoletos pelo início de sessão de domínio**, deteção exclui os computadores que cumprem os critérios de um filtro.  


###  <a name="bkmk_customAD"></a> Procurar atributos personalizados do Active Directory  
 Disponível para:  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

Cada método de deteção suporta uma lista exclusiva de atributos do Active Directory que podem ser detetados.  

Pode ver e configurar a lista de atributos personalizados no **atributos do Active Directory** separador o **propriedades de deteção de sistema do Active Directory** e **propriedades de deteção de utilizador do Active Directory** caixas de diálogo.  
