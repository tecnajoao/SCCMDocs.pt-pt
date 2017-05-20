---
title: "Planear funções do sistema de sites | Documentos do Microsoft"
description: "Considere servidores do sistema de sites e funções de sistema de sites como planear a hierarquia do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: a93ea730c39cce9dc46036f5aa6ece4a62679d0f
ms.openlocfilehash: 0d16d362b798c194645f987088ba8a95a7be3f19
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Planear os servidores do sistema de sites e as funções do sistema de sites para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Cada site do System Center Configuration Manager instalar inclui um servidor de site que seja um **servidor do sistema de site**. O site também pode incluir servidores do sistema de sites adicionais em computadores que são remotos em relação ao servidor do site. Os servidores do sistema de sites (o servidor do site ou um servidor do sistema de sites remoto) suportam **funções do sistema de sites**.


##  <a name="bkmk_siteservers"></a> Servidores do sistema de sites  
 Quando instala uma função de sistema de sites num computador, esse computador torna-se um servidor de sistema de sites. Em cada site, pode instalar um ou mais servidores de sistema de sites adicionais. Pode também optar por não instalar servidores do sistema de sites adicionais e executar todas as funções de sistema de sites diretamente no computador do servidor de site. Cada servidor de sistema de sites suporta uma ou mais funções de sistema de sites. Servidores adicionais podem ajudar a expandir as capacidades e a capacidade de um site através da partilha a carga de processamento de CPU colocar as funções do sistema de site num servidor.  

 Ao considerar a adição de um servidor de sistema de sites, certifique-se de que o servidor cumpre os pré-requisitos para a utilização pretendida. É também uma boa ideia para adicioná-lo numa localização de rede com largura de banda suficiente para comunicar com pontos finais esperados, incluindo o servidor do site, recursos de domínio, numa localização baseado na nuvem, servidores do sistema de sites e clientes).  

 Se configurar o servidor de sistema de sites com um proxy para utilização por funções de sistema de sites, consulte o artigo [funções do sistema que podem utilizar um servidor proxy do Site](#bkmk_proxy).  

##  <a name="bkmk_planroles"></a> Site system roles  
 As funções do sistema de sites são instaladas num computador para fornecer capacidades adicionais ao site. Alguns exemplos:  

-   Pontos de gestão adicionais para que o site pode suportar mais dispositivos, até capacidade suportados do site.  

-   Pontos de distribuição adicionais para expandir a infraestrutura de conteúdo, melhorar o desempenho das distribuições de conteúdo em dispositivos e utilizadores.  

-   Um ou mais funções de sistema de sites de funcionalidades específicas. Por exemplo, um ponto de atualização de software permite-lhe gerir atualizações de software para dispositivos geridos ou um ponto do reporting services permite-lhe executar relatórios para monitorizar e compreender ou partilhar informações sobre a implementação.  


Diferentes sites do Configuration Manager podem suportar diferentes conjuntos de funções do sistema de sites. O conjunto de funções do sistema de sites suportado depende do tipo de site (um site de administração central, site primário ou site secundário). A topologia da hierarquia pode limitar a colocação de algumas funções em determinados tipos de site. Por exemplo, o ponto de ligação de serviço só é suportado no site de nível superior da hierarquia, que poderá ser um site de administração central ou um site primário autónomo. Esta função não é suportada num site primário subordinado nem em sites secundários.  

Após a instalação de um site, pode mover a localização de algumas funções de sistema de sites a partir da localização predefinida no servidor do site para outro servidor. Por exemplo, isto acontece do ponto de gestão ou ponto de distribuição, que instalar por predefinição num servidor de site primário ou secundário. Também pode instalar instâncias adicionais de algumas funções de sistema de sites para expandir as capacidades do seu site (fornecer mais serviços aos clientes) e para cumprir os requisitos de negócio. Algumas funções são necessárias, enquanto outros são opcionais.  

-   **Servidor de sites do Configuration Manager.** Esta função identifica o servidor em que a configuração do Configuration Manager é executada para instalar um site ou o servidor no qual instala um site secundário. Esta função não pode ser movida ou desinstalada até o site ser desinstalado.  

-   **Sistema de sites do Configuration Manager.** Esta função é atribuída a qualquer computador no qual pode instala um site ou instala uma função de sistema de sites. Esta função não pode ser movida ou desinstalada até que a última função do sistema de sites seja removida do computador.  

-   **Função de sistema de sites de componente do Configuration Manager.** Esta função identifica o sistema de sites que execute uma instância do serviço SMS Executive e é necessário para suportar outras funções, como os pontos de gestão. Esta função não pode ser movida ou desinstalada até que a última função do sistema de sites aplicável seja removida do computador.  

-   **Servidor de base de dados de sites do Configuration Manager.** Esta função é atribuída para servidores de sistema de sites que contenha uma instância de base de dados do site para um site. Esta função só pode ser movida para um novo servidor, modificando o site para utilizar uma instância diferente do SQL Server para alojar a base de dados do site.  

-   **Fornecedor de SMS.** A função do fornecedor de SMS é atribuída a cada computador que aloje uma instância do fornecedor de SMS, a interface entre uma consola do Configuration Manager e a base de dados do site. Por predefinição, esta função instala automaticamente no servidor do site de um site de administração central e sites primários. Pode instalar instâncias adicionais em cada site para fornecer acesso a utilizadores administrativos adicionais.  

     Para instalar fornecedores adicionais, tem de executar o programa de configuração do Configuration Manager para [gerir o fornecedor de SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Em seguida, instalar fornecedores adicionais em computadores adicionais. Só pode instalar uma instância do fornecedor de SMS num computador e, nesse computador tem de estar no mesmo domínio que o servidor do site.  

-   **Ponto de serviço de web de catálogo de aplicações.** Uma função do sistema de sites que fornece informações sobre software ao Web site do Catálogo de Aplicações a partir da Biblioteca de Software. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

-   **Ponto de Web site do catálogo de aplicações.** Uma função do sistema de sites que fornece aos utilizadores uma lista de software disponível a partir do Catálogo de Aplicações. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

     Se o catálogo de aplicações suportar computadores cliente na Internet, é uma melhor prática de segurança para instalar o ponto de Web site do catálogo de aplicações numa rede de perímetro para segurança e para instalar o ponto de serviço web do catálogo de aplicações na intranet.  

-   **Ponto de sincronização do Asset Intelligence.** Uma função de sistema de sites que se liga à Microsoft para transferir informações de catálogo do Asset Intelligence. Esta função também carregamentos títulos não categorizados, para que possam ser contemplados para inclusão futura no catálogo. Uma hierarquia suporta apenas uma única instância desta função, e que tem de ser no site de nível superior da hierarquia (site de administração central ou site primário autónomo). Se expandir um site primário autónomo para uma hierarquia maior, tem de desinstalar esta função do site primário e, em seguida, instalá-lo no site de administração central.   Para obter mais informações, veja [Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Ponto de registo de certificados.** Uma função de sistema de sites que comunica com um servidor que executa o serviço de inscrição de dispositivos de rede. Esta função gere pedidos de certificado de dispositivo que utilizam o certificado de inscrição de protocolo SCEP (Simple). Esta função só é suportada em sites primários e no site de administração central.

     Embora um ponto de registo único de certificados pode conferir funcionalidade a uma hierarquia completa, pode querer instalar várias instâncias desta função de um site e em vários sites na mesma hierarquia. Isto pode ajudar com balanceamento de carga. Quando existem várias instâncias numa hierarquia, os clientes são atribuídos aleatoriamente a um dos pontos de registo de certificados.  

     Cada ponto de registo de certificados necessita de acesso a uma instância separada do serviço de registo de dispositivos de rede. Não é possível configurar dois ou mais pontos de registo de certificados para utilizarem o mesmo serviço de registo de dispositivos de rede. Além disso, o ponto de registo de certificados não pode ser instalado no mesmo servidor que executa o Serviço de Inscrição de Dispositivos de Rede.  

- **Ponto de gestão de conector de gateway da nuvem.** Uma função de sistema de sites para comunicação com o [gateway de gestão da nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway).

-   **Ponto de distribuição.** Uma função do sistema de sites que contém ficheiros de origem para os clientes transferirem, como por exemplo, o conteúdo da aplicação, pacotes de software, atualizações de software, imagens do sistema operativo e imagens de arranque. Por predefinição, esta função é instalada no computador do servidor do site de novos sites primários e secundários quando o site é instalado. Esta função não é suportada num site de administração central. Pode instalar várias instâncias desta função num site suportado e em vários sites na mesma hierarquia. Para obter mais informações, veja [Conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) e [Gerir conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Ponto de estado de contingência.** Uma função de sistema de sites que o ajuda a monitorizar a instalação de cliente e identificar os clientes que não são geridos porque não conseguem comunicar com o respetivo ponto de gestão. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site e em vários sites na mesma hierarquia. Para obter mais informações, veja [Cenários de localização da origem de conteúdo](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).


-   **Ponto de Endpoint Protection.** Uma função de sistema de sites do Configuration Manager utiliza para aceitar os termos de licenciamento do Endpoint Protection e para configurar a associação predefinida para o serviço de proteção de nuvem. Uma hierarquia suporta apenas uma única instância desta função, e que tem de ser no site de nível superior da hierarquia (site de administração central ou site primário autónomo). Se expandir um site primário autónomo para uma hierarquia maior, tem de desinstalar esta função do site primário e, em seguida, instalá-lo no site de administração central. Para obter mais informações, consulte o artigo [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Ponto de inscrição.** Uma função de sistema de sites que utiliza certificados PKI para o Configuration Manager para inscrever dispositivos móveis e computadores Mac. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

     Se um utilizador inscreve dispositivos móveis utilizando o Gestor de configuração e a conta de utilizador do Active Directory estiver localizada numa floresta que não é fidedigna pela floresta do servidor de site, tem de instalar um ponto de registo na floresta do utilizador. O utilizador, em seguida, pode ser autenticado.  

-   **Ponto de proxy de registo.** Uma função de sistema de sites que gere os pedidos de inscrição do Gestor de configuração de dispositivos móveis e computadores Mac. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

     Se forem suportados dispositivos móveis na Internet, instale o ponto de proxy de registo numa rede de perímetro para segurança e instalar o ponto de registo na intranet.  

-   **Conector do Exchange Server.** Para obter informações sobre esta função, consulte o artigo [gerir dispositivos móveis com o System Center Configuration Manager e do Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **Ponto de gestão.** Uma função de sistema de sites que fornece informações de localização de serviços e políticas a clientes e recebe dados de configuração a partir de clientes.  

    Por predefinição, esta função é instalada no computador do servidor do site de novos sites primários e secundários quando o site é instalado. Sites primários suportam várias instâncias desta função. Os sites secundários suportam um único ponto de gestão fornecer um ponto local de contacto para os clientes obterem o computador e utilizador políticas (um ponto de gestão num site secundário é referido como um ponto de gestão do proxy).  

     Pontos de gestão podem ser configurados para suportar HTTP ou HTTPs, bem como para suportar dispositivos móveis que gere com gestão de dispositivos móveis no local do System Center Configuration Manager. Pode utilizar o tópico [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) para ajudar a reduzir a carga da CPU colocada no servidor da base de dados do site por pontos de gestão à medida que atendem pedidos de clientes.  

-   **Ponto do Reporting services.** Uma função de sistema de sites que se integra no SQL Server Reporting Services para criar e gerir relatórios para o Configuration Manager. Esta função é suportada em sites primários e o site de administração central e pode instalar várias instâncias desta função de um site suportado. Para obter mais informações, veja [Planeamento de relatórios no System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Ponto de ligação de serviço.** Uma função de sistema de sites que utiliza para gerir dispositivos móveis com o Microsoft Intune e no local MDM. Esta função também carregamentos de dados de utilização do seu site e é necessário para disponibilizar as atualizações para o Configuration Manager na consola do Configuration Manager. Uma hierarquia suporta apenas uma única instância desta função, e que tem de ser no site de nível superior da hierarquia (site de administração central ou site primário autónomo). Se expandir um site primário autónomo para uma hierarquia maior, tem de desinstalar esta função do site primário e, em seguida, instalá-lo no site de administração central. Para obter mais informações, veja [Sobre o ponto de ligação de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Ponto de atualização de software.** Uma função de sistema de sites que se integra com o Windows Server Update Services (WSUS) para fornecer atualizações de software a clientes do Configuration Manager. Esta função é suportada em todos os sites:  

    -   Instale este sistema de sites no site de administração central para sincronizar com o WSUS.  

    -   Configure cada instância desta função em sites primários subordinados para sincronizar com o site de administração central.  

    -   Considere a instalação de um ponto de atualização de software em sites secundários, quando a transferência de dados através da rede for lenta.  

    Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Ponto de migração de estado.** Uma função do sistema de sites que armazena dados de estado dos utilizadores quando um computador é migrado para um novo sistema operativo. Esta função é suportada em sites primários e em sites secundários. Pode instalar várias instâncias desta função de um site e em vários sites na mesma hierarquia. Para obter mais informações sobre o armazenamento do estado do utilizador ao implementar sistemas operativos, veja [Gerir o estado do utilizador no System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Ponto do validador de estado de funcionamento do sistema.** Embora esta função do sistema de sites permanece visível na consola do Configuration Manager, já não é utilizado.  

###  <a name="bkmk_proxy"></a> Funções do sistema de sites que podem utilizar um servidor proxy  
 Algumas funções de sistema de sites do Configuration Manager necessitam de ligações à Internet e utilizarão um servidor proxy quando o servidor de sistema de sites que aloja a função está configurado para um. Normalmente, esta ligação é efetuada no **sistema** contexto do computador onde está instalada a função de sistema de sites. A ligação não é possível utilizar uma configuração de proxy para contas de utilizador normais. Quando é necessário um servidor proxy para estabelecer uma ligação à Internet, tem de configurar o computador para utilizar um servidor proxy:  

-   Pode configurar um servidor proxy ao instalar uma função de sistema de sites.  

-   Pode adicionar ou modificar uma configuração de servidor proxy quando utilizar a consola do Configuration Manager.  

-   A mesma configuração de servidor proxy é utilizada para todas as funções de sistema de sites num servidor de sistema de sites que pode utilizar uma configuração de servidor proxy. Se necessitar de funções de sistema de sites diferentes para utilizar diferentes servidores proxy, tem de instalar as funções de sistema de sites em computadores de servidor do sistema de sites diferentes.  

-   Se modificar a configuração do servidor proxy ou instalar uma nova função de sistema de sites num computador que já tenha uma configuração de servidor proxy, a configuração original é substituída pela nova configuração.  


Para obter procedimentos sobre como configurar o servidor proxy para funções do sistema de sites, consulte o [adicionar funções do sistema de sites para o System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md) tópico.  

A seguir, são indicadas as funções do sistema de sites que podem utilizar um servidor proxy:  

-   **Ponto de sincronização do Asset Intelligence.** Esta função do sistema de sites liga à Microsoft, utiliza uma configuração de servidor proxy no computador que aloja o ponto de sincronização do Asset Intelligence.  

-   **Ponto de distribuição baseado na nuvem.** Quando utiliza um ponto de distribuição baseado na nuvem, o site primário que gere o ponto de distribuição baseado na nuvem tem de ser capaz de ligar ao Microsoft Azure para aprovisionar, monitorizar e distribuir conteúdo ao ponto de distribuição. Se um servidor proxy for necessário para esta ligação, tem de configurar o servidor de proxy no servidor do site primário. Não é possível configurar um servidor proxy no ponto de distribuição em nuvem com base no Azure. Para obter mais informações, consulte o [configurar definições de proxy para sites primários que gerem serviços em nuvem](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) secção a [instalar pontos de distribuição baseado na nuvem no Microsoft Azure para o System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) tópico.  

-   **Conector do Exchange Server.** Esta função do sistema de sites liga a um Exchange Server e utiliza uma configuração de servidor proxy no computador que aloja o conector do Exchange Server.  

-   **Ponto de atualizações de software.** Esta função do sistema de sites pode necessitar de ligações ao Microsoft Update, para transferir patches e sincronizar informações sobre atualizações. Normalmente, quando configurar o servidor proxy, cada função do sistema de sites nesse computador que suporta a utilização do servidor proxy utiliza o servidor proxy. Não é necessária nenhuma configuração adicional. Uma exceção a isto é o ponto de atualizações de software. Por predefinição, um ponto de atualizações de software não utiliza um servidor proxy disponível, exceto se também ativar as seguintes opções quando configura o ponto de atualizações de software:  

    -   **Utilizar um servidor proxy para sincronizar atualizações de software**  

    -   **Utilizar um servidor proxy quando transferir conteúdo usando regras de implementação automática**  

    > [!TIP]  
    >  Antes de poder selecionar qualquer uma das opções, um servidor proxy tem de ser configurado no servidor do sistema de sites que aloja o ponto de atualizações de software. O servidor proxy só é utilizado para as opções específicas que selecionar.  

 Para mais informações sobre servidores proxy para pontos de atualização de software, consulte a secção "Definições do servidor Proxy" [instalar um ponto de atualização de software](../../../sum/get-started/install-a-software-update-point.md) tópico.  

-   **Ponto de ligação de serviço.** Quando configurar a estar online (não offline), esta função do sistema de sites liga-se ao Microsoft Intune e o serviço de nuvem da Microsoft.  
