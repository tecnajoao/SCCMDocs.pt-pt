---
title: "Planejar funções do sistema de site | Microsoft Docs"
description: "Considere a possibilidade de servidores do sistema de site e funções do sistema de site como planejar sua hierarquia do System Center Configuration Manager."
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
ms.sourcegitcommit: 0ebda27c0f3848615346c2ecf1ab8b9bb9ab6f0d
ms.openlocfilehash: 0a3704a2d3b75ed7e0a7f718b681448ab6fc078d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/26/2017


---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Planear os servidores do sistema de sites e as funções do sistema de sites para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Cada site do System Center Configuration Manager que você instala inclui um servidor de site que seja um **servidor do sistema de site**. O site também pode incluir servidores do sistema de sites adicionais em computadores que são remotos em relação ao servidor do site. Os servidores do sistema de sites (o servidor do site ou um servidor do sistema de sites remoto) suportam **funções do sistema de sites**.


##  <a name="bkmk_siteservers"></a> Servidores do sistema de sites  
 Quando você instala uma função de sistema de site em um computador, esse computador torna-se um servidor de sistema de site. Em cada site, você pode instalar um ou mais servidores de sistema de site adicionais. Você também pode escolher para não instalar servidores de sistema de site adicionais e executar todas as funções de sistema de site diretamente no computador servidor do site. Cada servidor do sistema de site oferece suporte a uma ou mais funções de sistema de site. Servidores adicionais podem ajudar a expandir os recursos e a capacidade de uma site compartilhando a carga de processamento da CPU que colocar funções do sistema de site em um servidor.  

 Ao considerar a adição de um servidor de sistema de site, certifique-se de que o servidor atende aos pré-requisitos para o uso pretendido. Ele também é uma boa ideia para adicioná-lo em um local de rede que tem largura de banda suficiente para se comunicar com pontos de extremidade esperados, incluindo o servidor do site, recursos de domínio, um local baseado em nuvem, servidores de sistema de site e clientes).  

 Se você configurar o servidor do sistema de site com um proxy para uso por funções do sistema de site, consulte [Site funções do sistema que podem usar um servidor proxy](#bkmk_proxy).  

##  <a name="bkmk_planroles"></a> Site system roles  
 As funções do sistema de sites são instaladas num computador para fornecer capacidades adicionais ao site. Alguns exemplos:  

-   Pontos de gerenciamento adicionais para que o site pode dar suporte a mais dispositivos, até a capacidade de suporte do site.  

-   Pontos de distribuição adicionais para expandir sua infraestrutura de conteúdo, melhorando o desempenho de distribuições de conteúdo para usuários e dispositivos.  

-   Uma ou mais funções do sistema de sites específicas do recurso. Por exemplo, um ponto de atualização de software permite que você gerencie atualizações de software para dispositivos gerenciados, ou um ponto do reporting services permite que você execute relatórios para monitorar e compreender ou compartilhar informações sobre a implantação.  


Diferentes sites do Configuration Manager podem dar suporte a diferentes conjuntos de funções do sistema de site. O conjunto com suporte de funções do sistema de site depende do tipo de site (um site de administração central, site primário ou site secundário). A topologia da sua hierarquia pode limitar o posicionamento de algumas funções em determinados tipos de site. Por exemplo, o ponto de ligação de serviço só é suportado no site de nível superior da hierarquia, que poderá ser um site de administração central ou um site primário autónomo. Esta função não é suportada num site primário subordinado nem em sites secundários.  

Depois de instalar um site, você pode mover o local de algumas funções do sistema de sites do respectivo local padrão no servidor do site para outro servidor. Por exemplo, isso é verdadeiro para o ponto de gerenciamento ou ponto de distribuição, que são instalados por padrão em um servidor de site primário ou secundário. Você também pode instalar instâncias adicionais de algumas funções do sistema de sites para expandir os recursos do seu site (fornecer mais serviços aos clientes) e para atender aos requisitos de negócios. Algumas funções são obrigatórias, enquanto outros são opcionais.  

-   **Servidor de site do Configuration Manager.** Essa função identifica o servidor em que a instalação do Configuration Manager é executada para instalar um site ou o servidor no qual você instalar um site secundário. Esta função não pode ser movida ou desinstalada até o site ser desinstalado.  

-   **Sistema de site do Configuration Manager.** Essa função é atribuída a qualquer computador no qual você instala um site ou instala uma função de sistema de site. Esta função não pode ser movida ou desinstalada até que a última função do sistema de sites seja removida do computador.  

-   **Função de sistema de site do componente do Configuration Manager.** Essa função identifica um sistema de site que executa uma instância do serviço SMS Executive e é necessário para dar suporte a outras funções, como pontos de gerenciamento. Esta função não pode ser movida ou desinstalada até que a última função do sistema de sites aplicável seja removida do computador.  

-   **Servidor de banco de dados do site do Configuration Manager.** Essa função é atribuída a servidores de sistema de sites que mantêm uma instância do banco de dados de site para um site. Essa função pode ser movida apenas para um novo servidor ao modificar o site para usar uma instância diferente do SQL Server para hospedar o banco de dados do site.  

-   **Provedor de SMS.** A função de provedor de SMS é atribuída a cada computador que hospeda uma instância do provedor de SMS, a interface entre um console do Configuration Manager e o banco de dados do site. Por padrão, essa função é instalada automaticamente no servidor do site de um site de administração central e sites primários. Você pode instalar instâncias adicionais em cada site para fornecer acesso a usuários administrativos adicionais.  

     Para instalar provedores adicionais, você deve executar a instalação do Configuration Manager para [gerenciar o provedor de SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Em seguida, instalar provedores adicionais em computadores adicionais. Você só pode instalar uma instância do provedor de SMS em um computador e esse computador deve estar no mesmo domínio que o servidor do site.  

-   **Ponto do serviço da web do catálogo de aplicativos.** Uma função do sistema de sites que fornece informações sobre software ao Web site do Catálogo de Aplicações a partir da Biblioteca de Software. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

-   **Ponto de site do catálogo de aplicativos.** Uma função do sistema de sites que fornece aos utilizadores uma lista de software disponível a partir do Catálogo de Aplicações. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

     Quando o catálogo de aplicativos dá suporte a computadores cliente na Internet, é uma prática recomendada de segurança para instalar o ponto de site do catálogo de aplicativos em uma rede de perímetro de segurança e para instalar o ponto de serviço da web de catálogo de aplicativos na intranet.  

-   **Ponto de sincronização do Asset Intelligence.** Uma função de sistema de site que se conecta à Microsoft para baixar informações do catálogo do Asset Intelligence. Essa função também carrega os títulos não categorizados, para que eles possam ser considerados para futura inclusão no catálogo. Uma hierarquia permite apenas uma única instância dessa função, e esta deve estar no site de nível superior da hierarquia (um site de administração central ou site primário autônomo). Se você expandir um site primário autônomo em uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, instale-o no site de administração central.   Para obter mais informações, veja [Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Ponto de registro de certificado.** Uma função de sistema de site que se comunica com um servidor que executa o serviço de registro de dispositivo de rede. Essa função gerencia solicitações de certificado de dispositivos que usam o protocolo de registro de certificado simples (SCEP). Esta função só é suportada em sites primários e no site de administração central.

     Embora um ponto de registro de certificado único possa fornecer funcionalidade a uma hierarquia inteira, convém instalar várias instâncias dessa função em um site e em vários sites na mesma hierarquia. Isso pode ajudar com balanceamento de carga. Quando existem várias instâncias numa hierarquia, os clientes são atribuídos aleatoriamente a um dos pontos de registo de certificados.  

     Cada ponto de registo de certificados necessita de acesso a uma instância separada do serviço de registo de dispositivos de rede. Não é possível configurar dois ou mais pontos de registo de certificados para utilizarem o mesmo serviço de registo de dispositivos de rede. Além disso, o ponto de registo de certificados não pode ser instalado no mesmo servidor que executa o Serviço de Inscrição de Dispositivos de Rede.  

- **Ponto de conector de gateway de gerenciamento de nuvem.** Uma função de sistema de site para se comunicar com o [gateway de gerenciamento de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway).

-   **Ponto de distribuição.** Uma função do sistema de sites que contém ficheiros de origem para os clientes transferirem, como por exemplo, o conteúdo da aplicação, pacotes de software, atualizações de software, imagens do sistema operativo e imagens de arranque. Por predefinição, esta função é instalada no computador do servidor do site de novos sites primários e secundários quando o site é instalado. Não há suporte para essa função em um site de administração central. Pode instalar várias instâncias desta função num site suportado e em vários sites na mesma hierarquia. Para obter mais informações, veja [Conceitos fundamentais da gestão de conteúdos no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) e [Gerir conteúdo e a infraestrutura de conteúdo do System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Ponto de status de fallback.** Uma função de sistema de site que ajuda você a monitorar a instalação do cliente e identificar os clientes que não são gerenciados porque eles não podem se comunicar com seu ponto de gerenciamento. Embora essa função é permitida apenas em sites primários, você pode instalar várias instâncias dessa função em um site e em vários sites na mesma hierarquia.     


-   **Ponto do Endpoint Protection.** Uma função de sistema de site do Configuration Manager usa para aceitar os termos de licença do Endpoint Protection e configurar a associação padrão para o serviço de proteção de nuvem. Uma hierarquia permite apenas uma única instância dessa função, e esta deve estar no site de nível superior da hierarquia (um site de administração central ou site primário autônomo). Se você expandir um site primário autônomo em uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, instale-o no site de administração central. Para obter mais informações, consulte [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Ponto de registro.** Uma função de sistema de site que usa certificados PKI para o Configuration Manager para registrar dispositivos móveis e computadores Mac. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

     Se um usuário registrar dispositivos móveis usando o Gerenciador de configuração e a conta do usuário do Active Directory está em uma floresta não confiável para floresta do servidor do site, você deve instalar um ponto de registro na floresta do usuário. O usuário pode ser autenticado.  

-   **Ponto proxy do registro.** Uma função de sistema de site que gerencia as solicitações de registro do Gerenciador de configuração de dispositivos móveis e computadores Mac. Embora esta função só seja suportada em sites primários, pode instalar várias instâncias desta função num site ou em vários sites na mesma hierarquia.  

     Quando você oferece suporte a dispositivos móveis na Internet, instale o ponto proxy do registro em uma rede de perímetro de segurança e instalar o ponto de registro na intranet.  

-   **Conector do Exchange Server.** Para obter informações sobre essa função, consulte [gerenciar dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **Ponto de gerenciamento.** Uma função de sistema de site que fornece informações de localização de serviço e a política para clientes e recebe dados de configuração de clientes.  

    Por predefinição, esta função é instalada no computador do servidor do site de novos sites primários e secundários quando o site é instalado. Sites primários dão suporte a várias instâncias dessa função. Sites secundários oferecem suporte a um único ponto de gerenciamento fornecer um ponto de contato para os clientes obtenham o computador e usuário local políticas (um ponto de gerenciamento em um site secundário é conhecido como um ponto de gerenciamento proxy).  

     Podem configurar pontos de gerenciamento para oferecer suporte a HTTP ou HTTPs, bem como para dar suporte a dispositivos móveis gerenciados com o gerenciamento de dispositivo móvel local do System Center Configuration Manager. Pode utilizar o tópico [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) para ajudar a reduzir a carga da CPU colocada no servidor da base de dados do site por pontos de gestão à medida que atendem pedidos de clientes.  

-   **Ponto do Reporting services.** Uma função de sistema de site que se integra ao SQL Server Reporting Services para criar e gerenciar relatórios do Configuration Manager. Essa função tem suporte em sites primários e o site de administração central, e você pode instalar várias instâncias dessa função em um site com suporte. Para obter mais informações, veja [Planeamento de relatórios no System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Ponto de conexão de serviço.** Uma função de sistema de site que você usa para gerenciar dispositivos móveis com Microsoft Intune e o local de MDM Essa função também carrega dados de uso do seu site e é necessária para disponibilizar as atualizações para o Configuration Manager no console do Configuration Manager. Uma hierarquia permite apenas uma única instância dessa função, e esta deve estar no site de nível superior da hierarquia (um site de administração central ou site primário autônomo). Se você expandir um site primário autônomo em uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, instale-o no site de administração central. Para obter mais informações, veja [Sobre o ponto de ligação de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Ponto de atualização de software.** Uma função de sistema de site que se integra com o Windows Server Update Services (WSUS) para fornecer atualizações de software a clientes do Configuration Manager. Essa função tem suporte em todos os sites:  

    -   Instale este sistema de site no site de administração central para sincronizar com o WSUS.  

    -   Configure cada instância dessa função em sites primários filho para sincronizar com o site de administração central.  

    -   Considere a instalação de um ponto de atualização de software em sites secundários, quando a transferência de dados através da rede for lenta.  

    Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Ponto de migração de estado.** Uma função do sistema de sites que armazena dados de estado dos utilizadores quando um computador é migrado para um novo sistema operativo. Essa função tem suporte em sites primários e em sites secundários. Você pode instalar várias instâncias dessa função em um site e em vários sites na mesma hierarquia. Para obter mais informações sobre o armazenamento do estado do utilizador ao implementar sistemas operativos, veja [Gerir o estado do utilizador no System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Ponto do validador de integridade do sistema.** Embora essa função do sistema de site permanece visível no console do Configuration Manager, ele não é mais usado.  

###  <a name="bkmk_proxy"></a> Funções do sistema de sites que podem utilizar um servidor proxy  
 Algumas funções do sistema de site do Configuration Manager requerem conexões à Internet e usam um servidor proxy quando o servidor do sistema de site que hospeda a função é configurado para um. Normalmente, essa conexão é feita na **sistema** contexto do computador em que a função de sistema de site está instalada. A conexão não pode usar uma configuração de proxy para contas de usuário típicas. Quando um servidor proxy é necessário para concluir uma conexão à Internet, você deve configurar o computador para usar um servidor proxy:  

-   Você pode configurar um servidor proxy ao instalar uma função de sistema de site.  

-   Você pode adicionar ou modificar uma configuração de servidor proxy quando você usar o console do Configuration Manager.  

-   A mesma configuração de servidor proxy é usada para todas as funções de sistema de site em um servidor de sistema de site que pode usar uma configuração de servidor proxy. Se você precisar de funções do sistema de site diferente para usar diferentes servidores proxy, você deve instalar as funções do sistema de site em computadores do servidor de sistema de site diferente.  

-   Se modificar a configuração do servidor proxy ou instalar uma nova função de sistema de sites num computador que já tenha uma configuração de servidor proxy, a configuração original é substituída pela nova configuração.  


Para obter procedimentos sobre como configurar o servidor proxy para funções do sistema de site, consulte o [adicionar funções do sistema de site para o System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md) tópico.  

A seguir, são indicadas as funções do sistema de sites que podem utilizar um servidor proxy:  

-   **Ponto de sincronização do Asset Intelligence.** Essa função do sistema de site se conecta à Microsoft, usa uma configuração de servidor proxy no computador que hospeda o ponto de sincronização do Asset Intelligence.  

-   **Ponto de distribuição baseado em nuvem.** Quando você usa um ponto de distribuição baseado em nuvem, o site primário que gerencia o ponto de distribuição baseado em nuvem deve ser capaz de se conectar ao Microsoft Azure para provisionar, monitorar e distribuir conteúdo ao ponto de distribuição. Se um servidor proxy é necessário para esta conexão, você deve configurar o servidor proxy no servidor do site primário. Você não pode configurar um servidor proxy no ponto de distribuição baseado em nuvem no Azure. Para obter mais informações, consulte o [definir configurações de proxy para sites primários que gerenciam serviços de nuvem](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) seção o [instalar pontos de distribuição baseado em nuvem no Microsoft Azure para o System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) tópico.  

-   **Conector do Exchange Server.** Essa função do sistema de site se conecta a um Exchange Server e usa uma configuração de servidor proxy no computador que hospeda o conector do Exchange Server.  

-   **Ponto de atualização de software.** Essa função do sistema de site pode exigir conexões com o Microsoft Update para baixar patches e sincronizar informações sobre atualizações. Normalmente, quando você configura o servidor proxy, cada função de sistema de site naquele computador que oferece suporte ao uso do servidor proxy usa o servidor proxy. Nenhuma configuração adicional é necessária. Uma exceção a isso é o ponto de atualizações de software. Por padrão, um ponto de atualizações de software não usa um servidor proxy disponível, a menos que você também habilitar as opções a seguir quando você configura o ponto de atualização de software:  

    -   **Utilizar um servidor proxy para sincronizar atualizações de software**  

    -   **Utilizar um servidor proxy quando transferir conteúdo usando regras de implementação automática**  

    > [!TIP]  
    >  Antes de selecionar qualquer opção, um servidor proxy deve ser definido no servidor do sistema de site que hospeda o ponto de atualizações de software. O servidor proxy só é utilizado para as opções específicas que selecionar.  

 Para obter mais informações sobre servidores proxy para pontos de atualização de software, consulte a seção "Configurações do servidor Proxy" [instalar um ponto de atualização de software](../../../sum/get-started/install-a-software-update-point.md) tópico.  

-   **Ponto de conexão de serviço.** Quando configurado para estar online (não offline), essa função do sistema de site conecta-se ao Microsoft Intune e o serviço de nuvem da Microsoft.  

