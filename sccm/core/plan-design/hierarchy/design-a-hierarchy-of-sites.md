---
title: Criar uma hierarquia de site - Configuration Manager | Microsoft Docs
description: "Compreenda as topologias disponíveis e as opções de gerenciamento do System Center Configuration Manager para que possa planejar a hierarquia de sites."
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: 22
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: db673277d1cc2d24e8dba2439b2b1891c883ebd0
ms.openlocfilehash: 4710b1b89eb50cb7bcf4c4ee50c12a96b6561bc9
ms.contentlocale: pt-pt
ms.lasthandoff: 06/16/2017


---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>Estruturar uma hierarquia de sites do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Antes de instalar o primeiro site de uma nova hierarquia do System Center Configuration Manager, é uma boa ideia para entender as topologias disponíveis para o Configuration Manager, os tipos de sites disponíveis e suas relações entre si e o escopo de gerenciamento que cada tipo de site fornece.
Em seguida, após considerar as opções de gerenciamento de conteúdo que podem reduzir o número de sites que você precisa instalar, você pode planejar uma topologia que atenda suas necessidades de negócios atuais de maneira eficaz e posteriormente pode ser expandido para gerenciar o crescimento futuro.  

> [!NOTE]
> Ao planejar uma nova instalação do Configuration Manager, esteja atento a [notas de versão]( /sccm/core/servers/deploy/install/release-notes), que detalham problemas atuais nas versões do ativos. As notas de versão se aplicam a todas as ramificações do Configuration Manager.  No entanto, quando você usa o [ramificação de visualização técnica]( /sccm/core/get-started/technical-preview), você encontrará problemas específicos apenas para essa ramificação na documentação para cada versão de Technical Preview.  

##  <a name="bkmk_topology"></a>Topologia de hierarquia  
 Intervalo de topologias de hierarquia de um único site primário autônomo para um grupo de sites primários e secundários conectados com um site de administração central no site de nível superior (camada superior) da hierarquia.   O driver de chave do tipo e contagem de sites que você usa em uma hierarquia é normalmente o número e tipo de dispositivos, que você deve dar suporte, da seguinte maneira:   

 **Site primário autônomo:** Usar um site primário autônomo quando um único site primário pode dar suporte a gerenciamento de todos os seus dispositivos e usuários (consulte [números de dimensionamento e escala](/sccm/core/plan-design/configs/size-and-scale-numbers)). Essa topologia também tem êxito quando diferentes localizações geográficas de sua empresa podem ser atendidas com êxito por um único site primário.  Para ajudar a gerenciar o tráfego de rede, você pode usar pontos de gerenciamento preferenciais e uma infraestrutura de conteúdo cuidadosamente planejada (consulte [conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  

 As vantagens desta topologia incluem:  

-   Simplifica a sobrecarga administrativa.  

-   Atribuição de site do cliente simplificado e descoberta de recursos e serviços disponíveis.  

-   Eliminação de latência possível introduzida pela replicação de banco de dados entre sites.

-   Opção de expandir uma hierarquia primária autônoma em uma hierarquia maior com um site de administração central. o que lhe permite, depois, instalar novos sites primários para expandir a escala da implementação.  


**Site de administração central com um ou mais sites primários filho:** Use essa topologia quando precisar de mais de um site primário para dar suporte ao gerenciamento de todos os seus dispositivos e usuários.  É necessário quando você precisa usar mais de um único site primário. As vantagens desta topologia incluem:  


-   Ele dá suporte a até 25 sites primários que permitem que você estenda a escala de sua hierarquia.  

-   Você sempre usará o site de administração central (a menos que você reinstale seus sites). Essa é uma opção permanente. Não é possível desanexar um site primário filho para torná-lo um site primário autônomo.

 As secções seguintes podem ajudá-lo a compreender quando deve utilizar um site específico ou a opção de gestão de conteúdos em vez de um site adicional.  

##  <a name="BKMK_ChooseCAS"></a>Determinar quando usar um site de administração central  
 Use um site de administração central para definir as configurações de toda a hierarquia e monitorar todos os sites e objetos na hierarquia. Esse tipo de site não gerencia diretamente clientes mas coordena a replicação de dados entre sites, que inclui a configuração de sites e clientes em toda a hierarquia.  

**As informações a seguir podem ajudá-lo a decidir quando instalar um site de administração central:**  

-   O site de administração central é o site de nível superior em uma hierarquia.  

-   Quando você configura uma hierarquia que tem mais de um site primário, você deve instalar um site de administração central. Se você precisar imediatamente dois ou mais sites primários, instale primeiro o site de administração central. Quando você já tiver um site primário e, em seguida, instalar um site de administração central, você deve [expandir o site primário autônomo](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) para instalar o site de administração central. 

-   O site de administração central oferece suporte a apenas sites primários como sites filho.  

-   O site de administração central não pode ter clientes atribuídos a ele.  

-   O site de administração central não oferece suporte a funções de sistema de site que suporte diretamente aos clientes, como pontos de gerenciamento e pontos de distribuição.  

-   Você pode gerenciar todos os clientes na hierarquia e executar tarefas de gerenciamento do site para qualquer site filho, quando você usar um console do Configuration Manager que está conectado ao site de administração central. Isso pode incluir a instalação de pontos de gerenciamento ou outras funções de sistema de site em sites filho primários ou secundários.  

-   Quando utiliza um site de administração central, este é o único local onde pode ver os dados de todos os sites na hierarquia. Esses dados incluem informações como mensagens de status e dados de inventário.  

-   Você pode configurar operações de descoberta em toda a hierarquia do site de administração central ao atribuir métodos de descoberta para ser executado em sites individuais.  

-   Pode gerir a segurança em toda a hierarquia atribuindo diferentes funções de segurança, âmbitos de segurança e coleções a diferentes utilizadores administrativos. Essas configurações se aplicam a cada site na hierarquia.  

-   Pode configurar a replicação de ficheiros e a replicação de base de dados para controlar a comunicação entre sites na hierarquia. Isso inclui o agendamento de replicação de banco de dados para dados do site e gerenciar a largura de banda para a transferência de dados com base em arquivo entre sites.  

##  <a name="BKMK_ChoosePriimary"></a>Determinar quando usar um site primário  
 Utilize sites primários para gerir clientes. Pode instalar um site primário como site primário subordinado abaixo de um site de administração central ou como o primeiro site numa nova hierarquia. Um site primário que é instalado como o primeiro site de uma hierarquia cria um site primário autônomo. Os sites primários filho e sites primários autônomos oferecem suporte a sites secundários como sites filho do site primário.  

 Considere a utilização de um site primário por qualquer um dos seguintes motivos:  

-   Para gerenciar usuários e dispositivos.  

-   Para aumentar o número de dispositivos, você pode gerenciar com uma única hierarquia.  

-   Para fornecer um ponto adicional de conectividade para a administração da sua implantação.  

-   Para satisfazer requisitos de gestão organizacional. Por exemplo, você pode instalar um site primário em uma localização remota para gerenciar a transferência de conteúdo de implantação em uma rede de baixa largura de banda. No entanto, com o System Center Configuration Manager, você pode usar opções para restringir o uso de largura de banda de rede ao transferir dados para um ponto de distribuição. Essa capacidade de gerenciamento de conteúdo pode substituir a necessidade de instalar sites adicionais.  


**As informações a seguir podem ajudá-lo a decidir quando instalar um site primário:**  

-   Um site primário pode ser um site primário autônomo ou um site primário filho em uma hierarquia maior. Quando um site primário é um membro de uma hierarquia com um site de administração central, os sites utilizam a replicação de base de dados para replicar dados entre os sites. A menos que você precisa dar suporte a mais clientes e dispositivos que pode oferecer suporte a um único site primário, considere a instalação de um site primário autônomo.  Depois que um site primário autônomo é instalado, você pode expandi-lo para relatar para um novo site de administração central para escalar verticalmente sua implantação.  

-   Um site primário oferece suporte a apenas um site de administração central como um site pai.  

-   Um site primário oferece suporte somente a sites secundários como sites filho e também pode oferecer suporte a múltiplos sites secundários filho.  

-   Os sites primários são responsáveis pelo processamento de todos os dados de cliente de seus clientes atribuídos.  

-   Sites primários usam a replicação de banco de dados para se comunicar diretamente com seu site de administração central (que é configurado automaticamente quando um novo site é instalado).  

##  <a name="BKMK_ChooseSecondary"></a>Determinar quando usar um site secundário  
 Use sites secundários para gerenciar a transferência de dados de cliente e conteúdo de implantação em redes de baixa largura de banda.  

 Gerencie um site secundário de um site de administração central ou site primário do pai direto do site secundário. Sites secundários devem ser anexados a um site primário, e você não pode movê-los para um site pai diferente sem desinstalá-los e, em seguida, reinstalá-los como um site filho abaixo do novo site primário.

No entanto, você pode rotear o conteúdo entre dois sites secundários pares para ajudar a gerenciar a replicação baseada em arquivo de conteúdo de implantação. Para transferir dados do cliente para um site primário, o site secundário usa replicação baseada em arquivo. Um site secundário também utiliza a replicação de base de dados para comunicar com o respetivo site primário principal.  

 Considere a instalação de um site secundário se qualquer uma das seguintes condições se aplicar:  

-   Você precisa de um ponto local de conectividade para um usuário administrativo.  

-   Você deve gerenciar a transferência de conteúdo de implantação para sites inferiores na hierarquia.  

-   Você deve gerenciar as informações de cliente que são enviadas para sites mais altos na hierarquia.  

 Se não pretender instalar um site secundário e tiver clientes em localizações remotas, considere utilizar o Windows BranchCache ou instalar pontos de distribuição ativados para o controlo da largura de banda e agendamento. Você pode usar essas opções de gerenciamento de conteúdo com ou sem sites secundários, e eles podem ajudar a reduzir o número de sites e servidores que você deve instalar. Para obter informações sobre as opções de gerenciamento de conteúdo no Configuration Manager, consulte [determinar quando usar as opções de gerenciamento de conteúdo](#BKMK_ChooseSecondaryorDP).  


**As informações a seguir podem ajudá-lo a decidir quando instalar um site secundário:**  

-   Sites secundários instalam automaticamente SQL Server Express durante a instalação do site se uma instância local do SQL Server não está disponível.  

-   Instalação do site secundário é iniciada do console do Configuration Manager, em vez de executar a instalação diretamente em um computador.  

-   Sites secundários usam um subconjunto das informações do banco de dados do site, que reduz a quantidade de dados replicados pela replicação de banco de dados entre o site pai primário e secundário.  

-   Sites secundários oferecem suporte a roteamento de conteúdo baseado em arquivo para outros sites secundários que têm um site primário pai em comum.  

-   As instalações do site secundário implantam automaticamente um ponto de gerenciamento e ponto de distribuição que estão localizados no servidor do site secundário.  

##  <a name="BKMK_ChooseSecondaryorDP"></a>Determinar quando usar as opções de gerenciamento de conteúdo  
 Se tiver clientes em localizações de rede remotas, considere utilizar uma ou mais opções de gestão de conteúdo em vez de um site primário ou secundário. Geralmente, você pode remover a necessidade de instalar um site quando você usa o Windows BranchCache, configurar pontos de distribuição para controle de largura de banda ou copia manualmente conteúdo para pontos de distribuição (conteúdo de pré-teste).  


**Considere a implantação de um ponto de distribuição em vez de instalar outro site se alguma das seguintes condições se aplicar:**  

-   A largura de banda de rede é suficiente para computadores cliente no local remoto para se comunicar com um ponto de gerenciamento para baixar política do cliente e enviar inventário, status do relatório e informações de descoberta.  

-   Serviço de transferência inteligente em segundo plano (BITS) não fornece controle de largura de banda suficiente para suas necessidades de rede.  

 Para obter mais informações sobre as opções de gerenciamento de conteúdo no Configuration Manager, consulte [conceitos fundamentais para o gerenciamento de conteúdo no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

##  <a name="bkmk_beyond"></a>Além da topologia de hierarquia  
 Além de uma topologia de hierarquia inicial, considere quais serviços ou recursos estarão disponíveis em diferentes sites em que a hierarquia (funções de sistema de site) e as configurações e recursos de toda a hierarquia como serão gerenciados na sua infraestrutura. As seguintes considerações comuns são abordadas em tópicos separados. Estes são importantes, porque eles podem influenciar ou ser influenciados por seu design de hierarquia:  

-   Quando você estiver se preparando para [gerenciar computadores e dispositivos com o System Center Configuration Manager](/sccm/core/clients/manage/manage-clients), considere se os dispositivos que você gerencia estão no local, na nuvem ou incluem dispositivos pertencentes ao usuário (BYOD).  Além disso, considere como você gerenciará dispositivos que são suportados por várias opções de gerenciamento, como computadores Windows 10 que podem ser gerenciados diretamente pelo Configuration Manager ou que a integração com o Microsoft Intune.  

-   Entender como a infraestrutura de rede disponível pode afetar o fluxo de dados entre locais remotos (consulte [preparar seu ambiente de rede para o System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)). Considere também onde os usuários e dispositivos que você gerencia estão localizados geograficamente e se eles acessarem sua infraestrutura por meio de seu domínio corporativo ou pela Internet.  

-   Plano para uma infraestrutura de conteúdo distribuir com eficiência as informações que você implanta (arquivos e aplicativos) para dispositivos gerenciados (consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)).  

-   Determinar qual [recursos e funcionalidades do System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) você planeja usar a infraestrutura do Windows ou funções do sistema de site precisam e em quais sites em uma hierarquia de sites múltiplos você pode implantá-los para o uso mais eficiente dos recursos de rede e servidor.  

-   Considere a segurança dos dados e dispositivos, incluindo a utilização de um PKI. Consulte [requisitos de certificado PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  


**Revise os seguintes recursos para configurações específicas de site:**  

-   [Planejar o provedor de SMS para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [Planejar o banco de dados do site para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [Planejar para servidores de sistema de site e funções do sistema de site para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [Planejar a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md)  

-   [Gerir a largura de banda da rede](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) ao implementar conteúdos num site  


**Considere as configurações que estendem sites e hierarquias:**  

-   [Opções de elevada disponibilidade para o System Center Configuration Manager](/sccm/protect/understand/high-availability-options) para sites e hierarquias

-   [Estender o esquema do Active Directory para o System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) e configurar sites para [publicar dados do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)  

-   [Transferência de dados entre sites no System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Fundamentos da administração baseada em função para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md)

