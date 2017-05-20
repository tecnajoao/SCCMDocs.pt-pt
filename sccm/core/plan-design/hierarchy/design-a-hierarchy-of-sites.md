---
title: Estruturar uma hierarquia do site - Configuration Manager | Documentos do Microsoft
description: "Compreenda as topologias disponíveis e as opções de gestão do System Center Configuration Manager pelo que pode planear a hierarquia de sites."
ms.custom: na
ms.date: 1/3/2017
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
ms.sourcegitcommit: 35e48666f4d1a2363304650f960531fd0630a291
ms.openlocfilehash: e346e83b0ae0dc7a612cef7a7b9fb1fdb42236bc
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>Estruturar uma hierarquia de sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de instalar o primeiro site numa nova hierarquia do System Center Configuration Manager, é uma boa ideia a compreender as topologias de disponíveis para o Configuration Manager, os tipos de sites disponíveis e respetivas relações entre si e o âmbito de gestão que fornece a cada tipo de site.
Em seguida, após considerar as opções de gestão de conteúdo que podem reduzir o número de sites que tem de instalar, pode planeia numa topologia de forma eficiente serva necessidades da sua empresa atual e pode expandir posteriormente para gerir futuro crescimento.  

> [!NOTE]
> Quando planear uma nova instalação do Configuration Manager, tenha em consideração o [notas de versão]( /sccm/core/servers/deploy/install/release-notes), que detalhe atuais problemas nas versões Active Directory. As notas de versão aplicam-se a todos os ramos do Configuration Manager.  No entanto, quando utiliza o [ramo de pré-visualização técnica]( /sccm/core/get-started/technical-preview), irá encontrar problemas específicos apenas nessa sucursal na documentação para cada versão do Technical Preview.  

##  <a name="bkmk_topology"></a>Topologia de hierarquia  
 Hierarquia topologias variar desde um único site primário autónomo a um grupo de sites primários e secundários ligadas com um site de administração central no site de nível superior (superior) da hierarquia.   O controlador do tipo de chave e contagem de sites que utilizam uma hierarquia são normalmente o número e tipo de dispositivos que têm de suportar, da seguinte forma:   

 **Site primário autónomo:** Utilizar um site primário autónomo, quando um único site primário pode suportar a gestão de todos os seus dispositivos e utilizadores (consulte [números dimensionamento e a escala](/sccm/core/plan-design/configs/size-and-scale-numbers)). Esta topologia também é efetuada com êxito quando diferentes localizações geográficas da sua empresa podem ser efetuadas com êxito por um único site primário.  Para ajudar a gerir o tráfego de rede, pode utilizar pontos de gestão preferenciais e de uma infraestrutura de conteúdo cuidadosamente planeada (consulte [os conceitos fundamentais para gestão de conteúdo no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  

 As vantagens desta topologia incluem:  

-   Overhead administrativo simplificado.  

-   A atribuição de site simplificado e a deteção de serviços e recursos disponíveis.  

-   Eliminação de atraso possíveis que é introduzida através da replicação de base de dados entre sites.

-   Opção de expandir uma hierarquia primária autónoma para uma hierarquia de grandes dimensões com um site de administração central. o que lhe permite, depois, instalar novos sites primários para expandir a escala da implementação.  


**Site de administração central com um ou mais sites primários subordinados:** Utilize esta topologia quando necessitar de mais do que um site primário para suportar a gestão de todos os seus dispositivos e utilizadores.  É obrigatório quando precisar de utilizar mais do que um único site primário. As vantagens desta topologia incluem:  


-   Suporta até 25 sites primários que permitem-lhe expandir a escala da hierarquia.  

-   Irá utilizar sempre o site de administração central (exceto se reinstalar os sites). Esta é uma opção permanente. Não é possível anular a exposição de um site primário subordinado para torná-la um site primário autónomo.

 As secções seguintes podem ajudá-lo a compreender quando deve utilizar um site específico ou a opção de gestão de conteúdos em vez de um site adicional.  

##  <a name="BKMK_ChooseCAS"></a>Determinar quando deve utilizar um site de administração central  
 Utilize um site de administração central para configurar definições ao nível da hierarquia e para monitorizar todos os sites e objetos da hierarquia. Este tipo de site não gere diretamente os clientes mas coordenar a replicação de dados entre sites, que inclui a configuração de sites e clientes em toda a hierarquia.  

**As seguintes informações podem ajudar a decidir quando pretende instalar um site de administração central:**  

-   O site de administração central é o site de nível superior numa hierarquia.  

-   Quando configura uma hierarquia que tem mais do que um site primário, tem de instalar um site de administração central e tem de ser o primeiro site que instalar.  

-   O site de administração central suporta apenas sites primários como sites subordinados.  

-   O site de administração central não pode ter clientes atribuídos a ele.  

-   O site de administração central não suporta funções de sistema de sites que suportam diretamente clientes, tais como pontos de gestão e pontos de distribuição.  

-   Pode gerir todos os clientes da hierarquia e executar tarefas de gestão do site para o site subordinado quando utiliza uma consola do Configuration Manager que está ligada ao site de administração central. Isto pode incluir a instalação de pontos de gestão ou de outras funções de sistema de sites em sites primários ou secundários subordinados.  

-   Quando utiliza um site de administração central, este é o único local onde pode ver os dados de todos os sites na hierarquia. Estes dados incluem informações como mensagens de estado e dados de inventário.  

-   Pode configurar operações de Deteção em toda a hierarquia do site de administração central através da atribuição de métodos de deteção a executar em sites individuais.  

-   Pode gerir a segurança em toda a hierarquia atribuindo diferentes funções de segurança, âmbitos de segurança e coleções a diferentes utilizadores administrativos. Estas configurações aplicam-se em cada site na hierarquia.  

-   Pode configurar a replicação de ficheiros e a replicação de base de dados para controlar a comunicação entre sites na hierarquia. Isto inclui agendar a replicação de base de dados para dados do site e gerir a largura de banda para a transferência de dados baseados em ficheiros entre sites.  

##  <a name="BKMK_ChoosePriimary"></a>Determinar quando deve utilizar um site primário  
 Utilize sites primários para gerir clientes. Pode instalar um site primário como site primário subordinado abaixo de um site de administração central ou como o primeiro site numa nova hierarquia. Um site primário que é instalado como o primeiro site de uma hierarquia cria um site primário autónomo. Sites primários subordinados e sites primários autónomos suportam sites secundários como sites subordinados do site primário.  

 Considere a utilização de um site primário por qualquer um dos seguintes motivos:  

-   Para gerir dispositivos e utilizadores.  

-   Para aumentar o número de dispositivos que pode gerir com uma única hierarquia.  

-   Para fornecer um ponto de conectividade adicional para a administração da implementação.  

-   Para satisfazer requisitos de gestão organizacional. Por exemplo, poderá instalar um site primário numa localização remota para gerir a transferência de conteúdo de implementação através de uma rede de largura de banda reduzida. No entanto, com o System Center Configuration Manager, pode utilizar as opções para otimizar a utilização de largura de banda de rede ao transferir dados para um ponto de distribuição. Esta capacidade de gestão de conteúdo pode substituir a necessidade de instalar sites adicionais.  


**As seguintes informações podem ajudar a decidir quando pretende instalar um site primário:**  

-   Um site primário pode ser um site primário autónomo ou um site primário subordinado numa hierarquia de grandes dimensões. Quando um site primário é um membro de uma hierarquia com um site de administração central, os sites utilizam a replicação de base de dados para replicar dados entre os sites. A menos que são necessários para suportar mais clientes e dispositivos que um único site primário pode suportar, considere a instalação de um site primário autónomo.  Depois de um site primário autónomo estiver instalado, pode expandi-lo para reportar a um novo site de administração central para dimensionar a sua implementação.  

-   Um site primário suporta apenas um site de administração central como site principal.  

-   Um site primário suporta apenas sites secundários como sites subordinados e pode também suporta vários sites subordinados secundários.  

-   Os sites primários são responsáveis por processar todos os dados de cliente dos respetivos clientes atribuídos.  

-   Sites primários utilizam a replicação de base de dados para comunicar diretamente com o respetivo site de administração central (que é configurado automaticamente quando instala um novo site).  

##  <a name="BKMK_ChooseSecondary"></a>Determinar quando deve utilizar um site secundário  
 Utilize sites secundários para gerir a transferência de dados de conteúdo e o cliente de implementação através de redes com pouca largura de banda.  

 Gerir um site secundário a partir de um site de administração central ou site primário principal direta do site secundário. Sites secundários tem de estar associados a um site primário e não é possível movê-los para outro site principal sem primeiro desinstalá-los e, em seguida, reinstalar como site subordinado abaixo do novo site primário.

No entanto, pode encaminhar conteúdos entre dois sites secundário membros para ajudar a gerir a replicação baseada em ficheiros de conteúdo de implementação. Para transferir dados de cliente a um site primário, o site secundário utiliza a replicação baseada em ficheiros. Um site secundário também utiliza a replicação de base de dados para comunicar com o respetivo site primário principal.  

 Considere a instalação de um site secundário se qualquer uma das seguintes condições se aplicar:  

-   Não necessita de um ponto local de conectividade para um utilizador administrativo.  

-   Tem de gerir a transferência de conteúdo de implementação para sites num nível inferior da hierarquia.  

-   Tem de gerir informações de cliente que são enviadas para sites num nível superior na hierarquia.  

 Se não pretender instalar um site secundário e tiver clientes em localizações remotas, considere utilizar o Windows BranchCache ou instalar pontos de distribuição ativados para o controlo da largura de banda e agendamento. Pode utilizar estas opções de gestão de conteúdo com ou sem sites secundários e estes podem ajudar a reduzir o número de sites e servidores que tem de instalar. Para obter informações sobre as opções de gestão de conteúdo no Configuration Manager, consulte o artigo [determinar quando deve utilizar as opções de gestão de conteúdo](#BKMK_ChooseSecondaryorDP).  


**As seguintes informações podem ajudar a decidir quando pretende instalar um site secundário:**  

-   Os sites secundários automaticamente instalam o SQL Server Express durante a instalação de site se não estiver disponível uma instância local do SQL Server.  

-   Instalação do site secundário é iniciada a partir da consola do Configuration Manager, em vez de executar o programa de configuração diretamente num computador.  

-   Os sites secundários utilizam um subconjunto de informações na base de dados do site, o que reduz a quantidade de dados que replicam através da replicação de base de dados entre o site primário principal e secundário.  

-   Os sites secundários suportam o encaminhamento de conteúdo baseado em ficheiros para outros sites secundários que tenham um site primário principal comum.  

-   As instalações de site secundário implementam automaticamente um ponto de gestão e o ponto de distribuição que estão localizados no servidor do site secundário.  

##  <a name="BKMK_ChooseSecondaryorDP"></a>Determinar quando deve utilizar as opções de gestão de conteúdo  
 Se tiver clientes em localizações de rede remotas, considere utilizar uma ou mais opções de gestão de conteúdo em vez de um site primário ou secundário. Muitas vezes, pode remover a necessidade de instalar um site quando utiliza o Windows BranchCache, configura pontos de distribuição para controlo de largura de banda ou copia manualmente conteúdo para pontos de distribuição (conteúdo pré-configurado).  


**Considere a implementação de um ponto de distribuição em vez de instalar outro site, se qualquer uma das seguintes condições se aplicar:**  

-   A largura de banda de rede é suficiente para computadores cliente na localização remota comuniquem com um ponto de gestão para transferir a política de cliente e enviar o inventário, comunicar o estado e informações de deteção.  

-   Serviço de transferência inteligente em segundo plano em segundo plano (BITS) não fornece controlo de largura de banda suficiente para os requisitos da rede.  

 Para obter mais informações sobre as opções de gestão de conteúdo no Configuration Manager, consulte o artigo [os conceitos fundamentais para gestão de conteúdo no System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

##  <a name="bkmk_beyond"></a>Para além da topologia de hierarquia  
 Além da topologia de uma hierarquia inicial, considere os serviços ou capacidades estará disponíveis a partir de diversos sites da hierarquia (funções de sistema de sites) e como em toda a hierarquia configurações e as funcionalidades serão geridas na sua infraestrutura. As seguintes considerações comuns são abordadas em tópicos separados. Estas são importantes porque pode influenciar ou influenciados pela estrutura da hierarquia:  

-   Quando estiver a preparar para [gerir computadores e dispositivos com o System Center Configuration Manager](/sccm/core/clients/manage/manage-clients), considere se os dispositivos que gere estão no local, na nuvem, incluem ou dispositivos detidos pelos utilizadores (BYOD).  Além disso, considere como gerir os dispositivos que são suportados pelo várias opções de gestão, tais como computadores Windows 10 que podem ser geridos diretamente pelo Configuration Manager ou embora integração com o Microsoft Intune.  

-   Compreender como a sua infraestrutura de rede disponível pode afetar o fluxo de dados entre localizações remotas (consulte [preparar o ambiente de rede para o System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)). Pondere também onde os utilizadores e dispositivos que gere se encontram geograficamente e que aceder à sua infraestrutura através do seu domínio da empresa ou na Internet.  

-   Plano para uma infraestrutura de conteúdo para distribuir eficazmente as informações que implementa (ficheiros e aplicações) aos dispositivos que gere (consulte [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)).  

-   Determinar que [funcionalidades e capacidades do System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) que pretende utilizar, as funções do sistema de sites ou de infraestrutura do Windows necessitam e em quais os sites numa hierarquia vários sites pode implementá-las para a utilização mais eficaz dos seus recursos de rede e dos servidores.  

-   Considere a segurança dos dados e dispositivos, incluindo a utilização de um PKI. Consulte o artigo [requisitos de certificados PKI para o System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  


**Reveja os seguintes recursos para configurações especificas de sites:**  

-   [Planear o fornecedor SMS para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [Planear a base de dados do site para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [Planear servidores de sistema de sites e funções de sistema de sites para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [Planear a segurança no System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md)  

-   [Gerir a largura de banda da rede](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) ao implementar conteúdos num site  


**Considere as configurações que abrangem sites e hierarquias:**  

-   [Opções de elevada disponibilidade para o System Center Configuration Manager](/sccm/protect/understand/high-availability-options) para sites e hierarquias

-   [Expandir o esquema do Active Directory para o System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) e configurar sites para [publicar dados do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)  

-   [Transferências de dados entre sites no System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md)

