---
title: "Métodos de deteção | Documentos do Microsoft"
ms.custom: na
ms.date: 2/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 81d7516b814d2db74d4d857871071c8911755754
ms.openlocfilehash: 6e53f501281e31f2b7df54b9740eac970f108257
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>Acerca dos métodos de deteção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Métodos de deteção do System Center Configuration Manager podem localizar dispositivos na sua rede ou dispositivos e utilizadores do Active Directory. Para utilizar eficazmente um método de deteção, deve compreender as respetivas configurações disponíveis e as limitações.  

##  <a name="bkmk_aboutForest"></a>Deteção de florestas do Active Directory  
 **Configurável:** Sim  

 **Ativado por predefinição:** Não  

 **Contas** pode utilizar para executar este método:  

-   **Conta de deteção de floresta do Active Directory** (definida pelo utilizador)  

-   **Conta de computador** do servidor do site  

Ao contrário de outros métodos de deteção do Active Directory, a deteção de floresta do Active Directory não Deteta recursos que pode gerir. Em vez disso, este método Deteta localizações de rede que estão configuradas no Active Directory e podem converter essas localizações em limites para utilização em toda a hierarquia.  

Quando este método é executada, este procura floresta do Active Directory local, cada fidedigna floresta e em cada floresta adicional configurada no **florestas do Active Directory** nó da consola do Configuration Manager.  

Deteção de florestas do Active Directory do utilizar para:  

-   Detetar sub-redes e sites do Active Directory e, em seguida, criar limites de Gestor de configuração baseados nessas localizações de rede.  

-   Identifica supernets que estão atribuídos a um site do Active Directory e converter cada Super-rede num limite de intervalo de endereços IP.  

-   Publica nos serviços de domínio do Active Directory (AD DS) numa floresta quando a publicação nessa floresta está ativada e a conta de floresta do Active Directory especificada tiver permissões para essa floresta.  

Pode gerir a deteção de floresta do Active Directory na consola do Configuration Manager a partir dos seguintes nós em **configuração da hierarquia** no **administração** área de trabalho:  

-   **Métodos de deteção**: Aqui, pode ativar a deteção de floresta do Active Directory para execução no site de nível superior da hierarquia. Também pode especificar uma agenda simples para executar a deteção e configurá-lo para criar automaticamente limites a partir de sub-redes IP e sites do Active Directory que Deteta. Não é possível executar a deteção de florestas do Active Directory num site primário subordinado ou num site secundário.  

-   **Florestas do Active Directory**: Aqui, pode configurar as florestas adicionais do Active Directory que pretende detetar, especificar a conta a utilizar como conta de floresta do Active Directory para cada floresta e configurar a publicação em cada floresta. Além disso, pode monitorizar o processo de deteção e adicionar as sub-redes IP e sites do Active Directory do Configuration Manager como limites e os membros de grupos de limites.  

Para configurar a publicação para florestas do Active Directory para cada site na sua hierarquia, ligue a consola do Configuration Manager para o site de nível superior da hierarquia. O **publicação** separador um site do Active Directory **propriedades** caixa de diálogo pode mostrar apenas o site atual e os sites subordinados. Quando a publicação está ativada para uma floresta e o esquema dessa floresta está expandida para o Configuration Manager, são publicadas as seguintes informações para cada site que está ativada para publicar nessa floresta do Active Directory:  

-    **SMS-Site -&lt;código do site >**

-   **SMS-MP -&lt;código do site >-&lt;nome de servidor do sistema de sites >**  

-   **SMS-SLP -&lt;código do site >-&lt;nome de servidor do sistema de sites >**  

-   **SMS -&lt;código do site >-&lt;nome do site do Active Directory ou sub-rede >**  

> [!NOTE]  
>  Os sites secundários utilizam sempre a conta de computador de servidor do site secundário para publicar no Active Directory. Se pretender que os sites secundários publiquem no Active Directory, certifique-se de que a conta de computador do servidor de site secundário tem permissões para publicar no Active Directory. Um site secundário não é possível publicar dados numa floresta não fidedigna.  

> [!CAUTION]  
>  Quando desmarcar a opção de publicar um site numa floresta do Active Directory, todas as informações publicadas anteriormente para esse site, incluindo as funções de sistema de sites disponíveis, serão removidas do Active Directory.  

Ações para a deteção de floresta do Active Directory são registadas nos seguintes registos:  

-   Todas as ações, com exceção das relacionadas com publicação, são registadas no **Adforestdisc** de ficheiros no  **&lt;Caminhodainstalação > \Logs** pasta no servidor do site.  

-   Deteção de florestas do Active Directory ações de publicação são registadas nos ficheiros de **hman** e **sitecomp. log** ficheiros no  **&lt;Caminhodainstalação > \Logs** pasta no servidor do site.  

Para obter mais informações sobre como configurar este método de deteção, consulte o artigo [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutGroup"></a>Deteção de grupos do Active Directory  
**Configurável:** Sim  

**Ativado por predefinição:** Não  

**Contas** pode utilizar para executar este método:  

-   **Conta de deteção de grupo do Active Directory** (definida pelo utilizador)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Para além das informações nesta secção, consulte o artigo [funcionalidades comuns do grupo do Active Directory, sistema e deteção de utilizadores](#bkmk_shared).  

Utilize este método para pesquisar os serviços de domínio do Active Directory para identificar:  

-   Grupos de segurança locais, globais e universais.  

-   A associação de grupos.  

-   Informações limitadas acerca dos utilizadores, mesmo quando outro método de deteção não foi anteriormente detetada esses computadores e utilizadores e computadores membros um grupo.  

Este método de deteção destina-se a identificar grupos e as relações de grupo dos membros dos grupos. Por predefinição, são detetados apenas os grupos de segurança. Se pretender também encontrar a associação dos grupos de distribuição, tem de verificar a caixa para a opção **detetar a associação dos grupos de distribuição** no **opção** separador o **propriedades de deteção de grupo do Active Directory** caixa de diálogo.  

Deteção de grupos do Active Directory não suporta os atributos expandidos do Active Directory que podem ser identificados utilizando a deteção de sistema do Active Directory ou a deteção de utilizador do Active Directory. Uma vez que este método de deteção não é otimizado para detetar recursos de computador e utilizador, considere executar este método de deteção depois de ter executado a deteção de sistema do Active Directory e deteção de utilizador do Active Directory. Isto acontece porque este método, cria um registo de dados (DDR) de deteção completa para grupos, mas apenas um DDR limitado de computadores e utilizadores que são membros dos grupos.  

Pode configurar os seguintes âmbitos de deteção que controlam a forma como este método se procura informações:  

-   **Localização**: Utilize uma localização se pretender pesquisar um ou mais contentores do Active Directory. Esta opção de âmbito suporta uma pesquisa recursiva dos contentores especificados do Active Directory que também pesquisa cada contentor subordinado no contentor que especificar. Este processo continua até não subordinado encontrados mais contentores são.  

-   **Grupos**: Utilize grupos se pretender pesquisar um ou mais grupos do Active Directory específicos. Pode configurar **domínio do Active Directory** para utilizar o domínio predefinido e a floresta, ou limitar a procura a um controlador de domínio individual. Além disso, pode especificar um ou mais grupos a pesquisar. Se não especificar pelo menos um grupo, todos os grupos encontrados na especificado **domínio do Active Directory** localização serão pesquisados.  

> [!CAUTION]  
>  Quando configurar um âmbito de deteção, selecione apenas os grupos que tem de detetar. Isto acontece porque a deteção de grupo do Active Directory tentar detetar cada membro de cada grupo de âmbito de deteção. Deteção de grupos grandes pode necessitar de utilizar muita largura de banda e de recursos do Active Directory.  

> [!NOTE]  
>  Antes de pode criar coleções baseadas em atributos expandidos do Active Directory (e certifique-se de deteção exatos resultados de computadores e utilizadores), executam a deteção de sistema do Active Directory ou a deteção de utilizador do Active Directory, dependendo daquilo pretende detetar.  

Ações de deteção de grupo do Active Directory são registadas no ficheiro **adsgdis.log** no  **&lt;Caminhodainstalação\>\LOGS** pasta no servidor do site.  

Para obter mais informações sobre como configurar este método de deteção, consulte o artigo [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutSystem"></a>Deteção de sistemas do Active Directory  
**Configurável:** Sim  

**Ativado por predefinição:** Não  

**Contas** pode utilizar para executar este método:  

-   **Conta de deteção de sistemas do Active Directory** (definida pelo utilizador)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Para além das informações nesta secção, consulte o artigo [funcionalidades comuns do grupo do Active Directory, sistema e deteção de utilizadores](#bkmk_shared).  

Utilize este método de deteção para pesquisar os serviços de domínio do Active Directory nas localizações especificadas nos recursos informáticos que podem ser utilizados para criar coleções e consultas. Também pode instalar o cliente do Configuration Manager num dispositivo detetado utilizando a instalação push do cliente.  

Por predefinição, este método Deteta informações básicas sobre o computador, incluindo as seguintes:  

-   Nome do computador  

-   Sistema operativo e versão  

-   Nome de contentor do Active Directory  

-   Endereço IP  

-   Site de Active Directory  

-   Carimbo de data / hora do último início de sessão  

Para criar com êxito um DDR para um computador, a deteção de sistema do Active Directory tem de ser capaz de identificar a conta de computador e, em seguida, resolver com êxito o nome do computador para um endereço IP.  

No **propriedades de deteção de sistema do Active Directory** caixa de diálogo no **atributos do Active Directory** separador, pode ver a lista completa de atributos de objetos predefinidos que devolveu a deteção de sistema do Active Directory. Também pode configurar o método para detetar atributos (expandidos) adicionais.  

Ações de deteção de sistema do Active Directory são registadas no ficheiro **adsysdis.log** no  **&lt;Caminhodainstalação\>\LOGS** pasta no servidor do site.  

Para obter mais informações sobre como configurar este método de deteção, consulte o artigo [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutUser"></a>Deteção de utilizadores do Active Directory  
**Configurável:** Sim  

**Ativado por predefinição:** Não  

**Contas** pode utilizar para executar este método:  

-   **Conta de deteção de utilizadores do Active Directory** (definida pelo utilizador)  

-   **Conta de computador** do servidor do site  

> [!TIP]  
>  Para além das informações nesta secção, consulte o artigo [funcionalidades comuns do grupo do Active Directory, sistema e deteção de utilizadores](#bkmk_shared).  

Utilize este método de deteção para pesquisar os serviços de domínio do Active Directory e identificar contas de utilizador e atributos associados. Por predefinição, este método Deteta informações básicas sobre a conta de utilizador, incluindo as seguintes:  

-   Nome de utilizador  

-   Nome de utilizador exclusivo (inclui o nome de domínio)  

-   Domain  

-   Nomes de contentor do Active Directory  

No **propriedades de deteção de utilizador do Active Directory** caixa de diálogo no **atributos do Active Directory** separador, pode ver a lista completa de atributos de objetos que devolveu a deteção de utilizador do Active Directory. Também pode configurar o método para detetar atributos (expandidos) adicionais.

Ações de deteção de utilizador do Active Directory são registadas no ficheiro **adusrdis.log** no  **&lt;Caminhodainstalação\>\LOGS** pasta no servidor do site.  

Para obter mais informações sobre como configurar este método de deteção, consulte o artigo [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutHeartbeat"></a>Deteção de heartbeat  
**Configurável:** Sim  

**Ativado por predefinição:** Sim  

**Contas** pode utilizar para executar este método:  

-   **Conta de computador** do servidor do site  

Deteção de heartbeat difere de outros métodos de deteção do Configuration Manager. É ativada por predefinição sendo executada em cada computador cliente (em vez de num servidor do site) criar um DDR. Para clientes de dispositivos móveis, este DDR é criado pelo ponto de gestão que está a utilizar o cliente do dispositivo móvel. Para ajudar a manter o registo de base de dados de clientes do Configuration Manager, não desative a deteção de Heartbeat. Para além de manter o registo de base de dados, este método pode forçar a deteção de um computador como um novo registo de recurso ou pode repovoar o registo de base de dados de um computador que tenha sido eliminado da base de dados.  

Deteção de heartbeat é executada segundo uma agenda configurada para todos os clientes na hierarquia, ou se invocada manualmente, num cliente específico, executando o **ciclo de recolha de dados de deteção** no **ação** separador no programa de um cliente do Configuration Manager. A agenda predefinida para a deteção de Heartbeat é definir a cada 7 dias. Se alterar o intervalo de deteção de heartbeat, certifique-se de que este é executado com mais frequência do que a tarefa de manutenção do site **eliminar dados de deteção desatualizados**, que elimina os registos de clientes Inativos da base de dados do site. Pode configurar o **eliminar dados de deteção desatualizados** tarefa apenas para sites primários.  

Quando a deteção de Heartbeat é executada, cria um DDR que tem as informações do cliente atual. O cliente copia, em seguida, este ficheiro pequeno (cerca de 1 KB de tamanho) para um ponto de gestão para que um site primário pode processá-lo. O ficheiro tem as seguintes informações:  

-   Localização de rede  

-   Nome NetBIOS  

-   Versão do agente do cliente  

-   Detalhes do Estado operacional  

Deteção de heartbeat é o único método de deteção que fornece detalhes sobre o estado de instalação do cliente. Isto é feito ao atualizar o atributo de cliente de recursos do sistema para definir um valor igual a **Sim**.  

> [!NOTE]  
>  Mesmo quando a deteção de Heartbeat estiver desativada, DDR ainda são criados e submetidos para clientes de dispositivos móveis ativos. Isto garante que o **eliminar dados de deteção desatualizados** tarefa não afeta dispositivos móveis ativos. Isto é feito porque quando o **eliminar dados de deteção desatualizados** tarefa elimina um registo de base de dados para um dispositivo móvel, revoga o certificado do dispositivo e impede o dispositivo móvel de estabelecer ligação a pontos de gestão também.  

Ações de deteção de Heartbeat são registadas nas seguintes localizações:  

-   Para clientes de computador, as ações de deteção de Heartbeat são registadas no cliente no **Inventoryagent** de ficheiros no *%Windir%\CCM\Logs* pasta.  

-   Para clientes de dispositivos móveis, as ações de deteção de Heartbeat são registadas no **DMPRP.log** de ficheiros no *% programa Files%\CCM\Logs* pasta do ponto de gestão que utiliza o cliente do dispositivo móvel.  

Para obter mais informações sobre como configurar este método de deteção, consulte o artigo [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutNetwork"></a>Deteção de rede  
**Configurável:** Sim  

**Ativado por predefinição:** Não  

**Contas** pode utilizar para executar este método:  

-   **Conta de computador** do servidor do site  

Utilize este método para detetar a topologia da rede e para detetar dispositivos de rede que tenham um endereço IP. Deteção de rede procura recursos IP ativados sua rede, consultando os servidores que executam uma implementação Microsoft de DHCP, caches de protocolo de resolução de endereço (ARP) em routers, dispositivos SNMP ativados e domínios do Active Directory.  

Antes de poder utilizar a deteção de rede, tem de especificar o *nível* de deteção a executar. Poderá também configurar um ou mais mecanismos de deteção que permitam a deteção de rede consulta para segmentos de rede ou dispositivos. Também pode configurar definições que ajudam a controlar as ações de deteção na rede. Finalmente, deverá definir uma ou mais agendas para a execução da deteção de rede.  

Para este método detetar um recurso com êxito, a deteção de rede tem de identificar o endereço IP e a máscara de sub-rede do recurso. Os métodos seguintes são utilizados para identificar a máscara de sub-rede de um objeto:  

-   **Cache ARP do router:** Deteção de rede consulta a cache ARP de um router para localizar informações de sub-rede. Normalmente, os dados na ARP cache de um router têm um curto período de tempo de vida. Por conseguinte, quando a deteção de rede consulta a cache ARP, a cache ARP já não pode ter informações sobre o objeto solicitado.  

-   **DHCP:** Deteção de rede consulta cada servidor DHCP que especificar para detetar os dispositivos para o qual o servidor DHCP forneceu uma concessão. Deteção de rede suporta apenas servidores DHCP que executem a implementação Microsoft de DHCP.  

-   **Dispositivo SNMP:** Deteção de rede pode consultar diretamente um dispositivo SNMP. Para a deteção de rede consultar um dispositivo, o dispositivo tem de ter um agente SNMP local instalado. Tem também de configurar a deteção de rede para utilizar o nome de Comunidade que está a utilizar o agente de SNMP.  

Quando a deteção identifica um objeto endereçável por IP e conseguir determinar a máscara de sub-rede de um objeto, cria um DDR para esse objeto. Como diversos tipos de dispositivos podem ligar à rede, a deteção de rede poderá detetar recursos que não suportem o software de cliente do Configuration Manager. Por exemplo, os dispositivos que podem ser detetados mas não geridos incluem impressoras e routers.  

Deteção de rede poderá devolver vários atributos como parte do registo de deteção que cria. Estas atualizações incluem:  

-   Nome NetBIOS  

-   Endereços IP  

-   Domínio de recurso  

-   Funções do sistema  

-   Nome de Comunidade SNMP  

-   Endereços MAC  

Atividade de deteção de rede é registada no **Netdisc.log** de ficheiros no  *&lt;Caminhodainstalação\>\Logs* no servidor do site que executa a deteção.  

 Para obter mais informações sobre como configurar este método de deteção, consulte o artigo [configurar métodos de deteção para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

> [!NOTE]  
>  Redes complexas e ligações de largura de banda reduzida podem fazer com que a deteção de rede para execução lenta e gerar tráfego de rede significativo. Como procedimento recomendado, execute a deteção de rede apenas quando os outros métodos de deteção não conseguirem localizar os recursos que tem de detetar. Por exemplo, utilize a deteção de rede se precisar de detetar computadores do grupo de trabalho. Outros métodos de deteção Deteta computadores de grupo de trabalho.  

###  <a name="BKMK_NetDiscLevels"></a>Níveis de deteção de rede  
Quando configurar a deteção de rede, tem de especificar um dos três níveis de Deteção:  

|Nível de deteção|Detalhes|  
|------------------------|-------------|  
|Topologia|Este nível Deteta routers e sub-redes, mas não identifica uma máscara de sub-rede para objetos.|  
|Topologia e cliente|Além da topologia, este nível Deteta potenciais clientes, como computadores e recursos como impressoras e routers. Este nível de deteção tentará identificar a máscara de sub-rede dos objetos que encontra.|  
|Topologia, cliente e cliente sistema operativo|Para além da topologia e de potenciais clientes, este nível tenta detetar o nome de sistema operativo do computador e a versão. Este nível utiliza o Browser do Windows e as chamadas de funcionamento em rede do Windows.|  

 Com cada nível de incremental, a deteção de rede aumenta a sua atividade e a utilização de largura de banda de rede. Considere o tráfego de rede que poderá ser gerado antes de ativar todos os aspetos da deteção de rede.  

 Por exemplo, quando utilizar a deteção de rede pela primeira vez, poderá começar com o nível de topologia para identificar a infraestrutura de rede. Em seguida, pode reconfigurar a deteção de rede para detetar objetos e os respetivos sistemas operativos de dispositivo. Também pode configurar as definições que limitam a deteção de rede a um intervalo específico de segmentos de rede. Dessa forma, pode detetar objetos em localizações de rede que necessite e evitar o tráfego de rede desnecessário e podem detetar objetos de routers na margem ou de fora da sua rede.  

###  <a name="BKMK_NetDiscOptions"></a>Opções de deteção de rede  
Para ativar a deteção de rede procurar dispositivos endereçáveis por IP, tem de configurar um ou mais das seguintes opções que especifiquem como consultar os dispositivos.  

> [!NOTE]  
>  Deteção de rede é executada no contexto da conta do computador do servidor do site que executa a deteção. Se a conta de computador não tem permissões para um domínio não fidedigno, o domínio e configurações de servidor DHCP poderão não conseguir detetar recursos.  

**DHCP:**  

Especifique cada servidor DHCP que pretende que a deteção de rede a consulta. (A deteção de rede suporta apenas servidores DHCP que executem a implementação Microsoft de DHCP.)  

-   Deteção de rede obtém as informações utilizando chamadas de procedimento remoto para a base de dados no servidor DHCP.  

-   Deteção de rede pode consultar servidores DHCP de 32 bits e 64 bits para obter uma lista de dispositivos que estejam registados junto de cada servidor.  

-   Para a deteção de rede poder consultar com êxito um servidor DHCP, a conta de computador do servidor que executa a deteção tem de ser um membro do grupo de utilizadores de DHCP no servidor DHCP. Por exemplo, este nível de acesso existe quando uma das seguintes opções for verdadeira:  

    -   O servidor DHCP especificado é o servidor DHCP do servidor que executa a deteção.  

    -   O computador que executa a deteção e o servidor DHCP estão no mesmo domínio.  

    -   Existe uma fidedignidade bidirecional entre o computador que executa a deteção e o servidor DHCP.  

    -   O servidor do site é um membro do grupo de utilizadores de DHCP.  

-   Quando a deteção de rede enumera um servidor DHCP, nem Deteta endereços IP estáticos sempre. Deteção de rede não encontra endereços IP que façam parte de um intervalo de endereços IP excluído no servidor DHCP. Também não Deteta endereços IP que estejam reservados para atribuição manual.  

**Domínios:**  

Especifique cada domínio que pretende que a deteção de rede a consulta.  

-   A conta de computador do servidor do site que executa a deteção tem de ter permissões para ler os controladores de domínio em cada domínio especificado.  

-   Para detetar computadores do domínio local, tem de ativar o serviço Browser de computador em pelo menos um computador que está na mesma sub-rede que o servidor do site que executa a deteção de rede.  

-   Deteção de rede poderá detetar qualquer computador que consiga visualizar a partir do seu servidor de site quando navega na rede.  

-   Deteção de rede obtém o endereço IP e, em seguida, utiliza um pedido de eco do protocolo de mensagem de controlo de Internet para efetuar ping a cada dispositivo que encontrar. O **ping** comando ajuda a determinar quais os computadores que se encontram atualmente ativos.  

**Dispositivos SNMP:**  

Especifique cada dispositivo SNMP que pretende que a deteção de rede a consulta.  

-   Deteção de rede obtém o valor de ipNetToMediaTable a partir de qualquer dispositivo SNMP que responda à consulta. Este valor devolve matrizes de endereços IP que sejam computadores cliente ou outros recursos, como de impressoras, routers ou outros dispositivos endereçáveis por IP.  

-   Para consultar um dispositivo, tem de especificar o endereço IP ou nome NetBIOS do dispositivo.  

-   Deve configurar a deteção de rede para utilizar o nome de Comunidade do dispositivo ou o dispositivo rejeitará a consulta baseada em SNMP.  

###  <a name="BKMK_LimitNetDisc"></a>Limitar a deteção de rede  
Quando a deteção de rede consultar um dispositivo SNMP na margem da rede, poderá identificar informações sobre sub-redes e dispositivos SNMP que estejam fora da rede imediata. Utilize as seguintes informações para limitar a deteção de rede, configurando os dispositivos SNMP que a deteção poderá comunicar e especificando os segmentos de rede a consultar.  

**Sub-redes:**  

Configure as sub-redes que a deteção de rede consulta ao utilizar as opções de SNMP e DHCP. Estas duas opções de pesquisa apenas sub-redes ativadas.  

Por exemplo, um pedido DHCP poderá devolver dispositivos de localizações em toda a rede. Se pretender detetar apenas os dispositivos numa sub-rede específica, especifique e ative essa sub-rede no **sub-redes** separador o **propriedades da deteção de rede** caixa de diálogo. Ao especificar e ativar sub-redes, estará a limitar tarefas futuras de deteção DHCP e SNMP a essas sub-redes.  

> [!NOTE]  
>  As configurações das sub-redes não limitam os objetos que o **domínios** opção de deteção Deteta.  

**Nomes de comunidades SNMP:**  

Para ativar a deteção de rede poder consultar com êxito um dispositivo SNMP, configure a deteção de rede com o nome de Comunidade do dispositivo. Se a deteção de rede não estiver configurada utilizando o nome da Comunidade do dispositivo SNMP, o dispositivo rejeitará a consulta.  

**Saltos máximos:**  

Quando configurar o número máximo de saltos de routers, limita o número de segmentos de rede e routers que a deteção de rede pode consultar utilizando SNMP.  

O número de saltos que configura limita o número de dispositivos e segmentos de rede que a deteção de rede pode consultar adicionais.  

Por exemplo, uma deteção só de topologia com **0** (zero) saltos de routers Deteta a sub-rede onde reside o servidor de origem. Inclui todos os routers dessa sub-rede.  

O diagrama seguinte mostra o que um só de topologia deteção de rede consulta encontra quando é executada no servidor 1 com 0 saltos de routers especificados: a sub-rede D e o Router 1.  

 ![Imagem de deteção com zero saltos de router](media/Disc-0.gif)  

 O diagrama seguinte mostra que uma topologia e cliente encontra de consulta de deteção de rede quando este é executado no servidor 1 com 0 saltos de routers especificados: a sub-rede D e o Router 1 e todos os potenciais clientes na sub-rede D.  

 ![Imagem de deteção com um router saltar](media/Disc-1.gif)  

 Para obter uma ideia mais concreta da forma como adicionais saltos de routers podem aumentar a quantidade de recursos de rede que são detetados, considere a rede seguinte:  

 ![Imagem de deteção com dois saltos de router](media/Disc-2.gif)  

 Executar uma deteção de rede só de topologia de servidor 1 com um salto de router Deteta o seguinte:  

-   O router 1 e a sub-rede 10.1.10.0 (localizados com zero saltos)  

-   As sub-redes 10.1.20.0 e 10.1.30.0, a sub-rede A e o Router 2 (localizados no primeiro salto)  

> [!WARNING]  
>  Cada aumento do número de saltos de router significativamente pode aumentar o número de recursos Detetáveis e aumentar a largura de banda de rede que a deteção de rede utiliza.  

##  <a name="bkmk_aboutServer"></a>Deteção do servidor  
**Configurável:** Não  

Para além de métodos de deteção configurável pelo utilizador, o Configuration Manager utiliza um processo denominado **deteção do servidor** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Este método de deteção cria registos de recursos para computadores que sejam sistemas de sites, como um computador que esteja configurado como um ponto de gestão.  

##  <a name="bkmk_shared"></a>Funcionalidades comuns de deteção de grupo do Active Directory, deteção de sistemas e deteção de utilizadores  
Esta secção fornece informações sobre as funcionalidades que são comuns para os seguintes métodos de Deteção:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

> [!NOTE]  
>  As informações nesta secção não se aplica a deteção de floresta do Active Directory.  

Estes três métodos de deteção são semelhantes na configuração e funcionamento. Que estes possam detetar computadores, utilizadores e informações sobre associações a grupos de recursos que estão armazenados nos serviços de domínio do Active Directory. O processo de deteção é gerido por um agente de deteção que é executado no servidor do site em cada site que esteja configurada deteção para ser executada. Pode configurar cada um destes métodos de deteção para pesquisar um ou mais localizações do Active Directory como instâncias de localização na floresta local ou em florestas remotas.  

Quando a deteção procurar recursos numa floresta não fidedigna, o agente de deteção tem de ser capaz de resolver os seguintes para ser concluída com êxito:  

-   Para detetar um recurso de computador utilizando a deteção de sistema do Active Directory, o agente de deteção tem de conseguir resolver o FQDN do recurso. Se não conseguir resolver o FQDN, em seguida, tentará resolver o recurso pelo respetivo nome NetBIOS.  

-   Para detetar um recurso de grupo ou utilizador utilizando a deteção de utilizador do Active Directory ou a deteção de grupo do Active Directory, o agente de deteção tem de conseguir resolver o FQDN do nome do controlador de domínio que especificou para a localização do Active Directory.  

Para cada localização que especificar, pode configurar opções de pesquisa individuais, como ativar uma pesquisa recursiva de contentores de subordinados a localização do Active Directory. Também pode configurar uma conta exclusiva para utilização quando pesquisar essa localização. Isto proporciona flexibilidade na configuração do método de deteção num site para pesquisar várias localizações do Active Directory em várias florestas sem ter de configurar uma conta única que tem permissões para todas as localizações.  

Quando cada um destes três métodos de deteção é executada num site específico, o servidor de site do Configuration Manager nesse site contacta o controlador de domínio mais próximo na floresta do Active Directory especificada para localizar recursos do Active Directory. O domínio e a floresta podem ser qualquer dos modos do Active Directory suportado. A conta que atribui a cada instância de localização deve ter **leitura** permissão para as localizações do Active Directory especificadas de acesso.

A deteção procura objetos nas localizações especificadas e, em seguida, tenta recolher informações sobre esses objetos. É criado um DDR quando são identificadas informações suficientes sobre um recurso. As informações necessárias variam consoante o método de deteção que está a ser utilizado.  

Se configurar o mesmo método de deteção para ser executada em diferentes sites do Configuration Manager para tirar partido da consulta de servidores locais do Active Directory, pode configurar cada site com um conjunto exclusivo de opções de deteção. Uma vez dados de deteção são partilhados por todos os sites da hierarquia, evite a sobreposição destas configurações para detetar eficazmente cada recurso uma vez. 

Para ambientes menores, poderá considerar executar cada método de deteção num site da hierarquia para reduzir a sobrecarga administrativa e a possibilidade de múltiplas ações de deteção para detetar novamente os mesmos recursos. Quando estará a minimizar o número de sites que executam a deteção, pode reduzir a largura de banda de rede global que a deteção está a utilizar. Também pode reduzir o número global de DDRs que são criados e têm de ser processados pelos servidores do site.  

Muitas das configurações de métodos de deteção dispensam explicações. Utilize as secções seguintes para obter mais informações sobre as opções de deteção que poderão necessitar de informações adicionais antes de as configurar.  

As seguintes opções estão disponíveis para utilização com vários métodos de deteção do Active Directory:  

-   [Deteção de diferenças](#bkmk_delta)  

-   [Filtrar os registos de computador obsoletos pelo início de sessão do domínio](#bkmk_stalelogon)  

-   [Filtrar registos obsoletos por palavra-passe de computador](#bkmk_stalepassword)  

-   [Procurar atributos personalizados do Active Directory](#bkmk_customAD)  

###  <a name="bkmk_delta"></a>Deteção de diferenças  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

A deteção de diferenças não é um método de deteção independente, mas uma opção disponível para os métodos de deteção aplicável. A deteção de diferenças pesquisa atributos específicos do Active Directory para que as alterações efetuadas desde o último ciclo de deteção completa do método de deteção aplicável. As alterações de atributo são submetidas na base de dados do Configuration Manager atualizar o registo de deteção do recurso.  

Por predefinição, a deteção de diferenças é executada num ciclo de cinco minutos. Isto é muito mais frequente do que a agenda típica para um ciclo de deteção completa.  Este ciclo frequente é possível porque a deteção de diferenças utiliza menos servidor do site e efetua a recursos de rede que um ciclo de deteção completa. Quando utiliza a deteção de diferenças, pode reduzir a frequência do ciclo de deteção completa para esse método de deteção.  

Seguem-se as alterações mais comuns que Deteta a deteção de diferenças:  

-   Novos computadores ou utilizadores adicionados ao Active Directory  

-   Alterações às informações básicas de computadores e utilizadores  

-   Novos computadores ou utilizadores que são adicionados a um grupo  

-   Computadores ou utilizadores que são removidos de um grupo  

-   Alterações aos objetos do grupo de sistema  

Embora a deteção de diferenças consiga detetar novos recursos e alterações às associações, não consegue detetar quando um recurso tiver sido eliminado do Active Directory. DDR criado pela deteção de diferenças é processado de forma semelhante aos DDR criado por um ciclo de deteção completa.  

Configurar a deteção de diferenças no **agenda de consulta** separador nas propriedades de cada método de deteção.  

###  <a name="bkmk_stalelogon"></a>Filtrar os registos de computador obsoletos pelo início de sessão do domínio  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

Pode configurar a deteção para excluir computadores com um registo de computador obsoletos com base no último início de sessão do domínio do computador. Quando esta opção estiver ativada, a deteção de sistema do Active Directory avalia todos os computadores que identifica. Deteção de grupos do Active Directory avalia todos os computadores que seja um membro de um grupo que é detetado.  

Para utilizar esta opção:  

-   Computadores têm de ser configurados para atualizar o **lastLogonTimeStamp** atributo no Active Directory Domain Services.  

-   O nível funcional de domínio do Active Directory deve estar definido para o Windows Server 2003 ou posterior.  

Quando estiver a configurar o tempo após o último início de sessão que pretende utilizar para esta definição, considere o intervalo de replicação entre controladores de domínio.  

Configurar a filtragem no **opção** separador o **propriedades de deteção de sistema do Active Directory** e **propriedades de deteção de grupo do Active Directory** caixas de diálogo. Escolha a opção **detetar apenas os computadores que iniciaram sessão num domínio num determinado período de tempo**.  

> [!WARNING]  
>  Ao configurar este filtro e **filtrar registos obsoletos por palavra-passe computador**, computadores que satisfaçam os critérios de qualquer um dos filtros serão excluídos da deteção.  

###  <a name="bkmk_stalepassword"></a>Filtrar registos obsoletos por palavra-passe de computador  
Disponível para:  

-   Deteção de Grupos do Active Directory  

-   Deteção de Sistemas do Active Directory  

Pode configurar a deteção para excluir computadores com um registo de computador obsoletos com base na última atualização de palavra-passe de conta de computador pelo computador. Quando esta opção estiver ativada, a deteção de sistema do Active Directory avalia todos os computadores que identifica. Deteção de grupos do Active Directory avalia todos os computadores que seja um membro de um grupo que é detetado.  

Para utilizar esta opção:  

-   Computadores têm de ser configurados para atualizar o **pwdLastSet** atributo no Active Directory Domain Services.  

Quando estiver a configurar esta opção, considere o intervalo das atualizações deste atributo, além do intervalo de replicação entre controladores de domínio.  

Configurar a filtragem no **opção** separador o **propriedades de deteção de sistema do Active Directory** e **propriedades de deteção de grupo do Active Directory** caixas de diálogo. Escolha a opção **detetar apenas os computadores que atualizaram a sua palavra-passe da conta de computador num determinado período de tempo**.  

> [!WARNING]  
>  Ao configurar este filtro e **filtrar registos obsoletos pelo início de sessão do domínio**, computadores que satisfaçam os critérios de qualquer um dos filtros serão excluídos da deteção.  

###  <a name="bkmk_customAD"></a>Procurar atributos personalizados do Active Directory  
 Disponível para:  

-   Deteção de Sistemas do Active Directory  

-   Deteção de Utilizadores do Active Directory  

Cada método de deteção suporta uma lista exclusiva de atributos do Active Directory que podem ser detetados.  

Pode ver e configurar a lista de atributos personalizados no **atributos do Active Directory** separador o **propriedades de deteção de sistema do Active Directory** e **propriedades de deteção de utilizador do Active Directory** caixas de diálogo.  

