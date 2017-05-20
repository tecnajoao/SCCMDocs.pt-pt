---
title: Configurar sites | Documentos do Microsoft
description: "Consulte esta lista de verificação para se certificar de que considerar as configurações mais comuns que afetam o sites e hierarquias."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5f1efaa776079b21d52b9936273380e9bb8963e9
ms.openlocfilehash: 862f420c063cb44c419d4904fbb4696efb739758
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Configurar sites e hierarquias do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de instalar o primeiro site do System Center Configuration Manager ou adicionar sites adicionais para a hierarquia, utilize a lista de verificação seguinte para garantir que considerar as configurações mais comuns que afetam o sites e hierarquias.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Lista de verificação de configurações comuns para sites novos e adicionais  
Tenha em atenção as seguintes notas sobre a configuração, que se aplicam a maioria das implementações de:

-   Algumas opções são interdependentes, tais como grupos de limites, limites e deteção de floresta do Active Directory.  

-   Várias configurações possuem valores predefinidos que pode utilizar sem alterar a configuração, pelo menos temporariamente.  

-   Outras configurações, como os grupos de limites e os grupos de pontos de distribuição, necessitam de configuração para poder utilizá-las.  

|Ação|Detalhes|  
|------------|-------------|  
|Configurar a administração baseada em funções|Segregar as atribuições administrativas para controlar quais os utilizadores administrativos podem ver e gerir objetos diferentes e os dados no seu ambiente do Configuration Manager.<br /><br /> As configurações para a administração baseada em funções são partilhadas com todos os sites numa hierarquia.   <br/><br/>Para obter mais informações, consulte o artigo [configurar a administração baseada em funções para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Publicar dados do site nos Serviços de Domínio do Active Directory (AD DS)|É mais fácil para os clientes localizar serviços e eficiente utilizar recursos do site.<br /><br /> Tem primeiro [expandir o esquema do Active Directory para o System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md), e, em seguida, cada site deve ser configurada individualmente a [publicar dados do site para o System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md)|  
|Configurar um ponto de ligação de serviço|Planear a instalar e configurar o ponto de ligação de serviço no site de nível superior da hierarquia. Para obter mais informações, veja [Sobre o ponto de ligação de serviço no System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Adicionar funções do sistema de sites|Instale uma ou mais funções de sistema de sites adicionais para sites individuais.  Para obter mais informações, consulte o artigo [adicionar funções do sistema de sites para o System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Configurar limites e grupos de limites de sites|Especifique os limites que definem localizações de rede na sua intranet que pode conter os dispositivos que pretende gerir. Em seguida, configure grupos de limites para que os clientes nessas localizações de rede possam localizar recursos do Configuration Manager. Para obter mais informações, consulte o artigo [definir limites de site e os grupos de limites para o System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Configurar grupos de pontos de distribuição|Configure grupos lógicos de pontos de distribuição para simplificar a gestão de implementações. Para obter mais informações, consulte o artigo [gerir grupos de pontos de distribuição](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) no [instalar e configurar pontos de distribuição para o System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).|  
|Executar Deteção|Execute a deteção para localizar recursos na sua rede, incluindo a infraestrutura de rede, dispositivos e utilizadores.<br /><br /> Para obter mais informações, veja [Executar a deteção no System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Adicionar e a capacidade para administradores que gerir a infraestrutura de redundância|Instale consolas do Configuration Manager e os fornecedores SMS adicionais para expandir a capacidade para os administradores a gerir a sua infraestrutura:<br /><br /> **Instalar fornecedores de SMS adicionais** para fornecer redundância de pontos de contacto ao administrar o site e a hierarquia. Para obter mais informações, consulte o artigo [gerir o fornecedor de SMS](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) no [modificar a infraestrutura do System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).<br /><br /> **Instalar consolas adicionais do Configuration Manager** para fornecer acesso a utilizadores administrativos adicionais. Para obter mais informações, consulte o artigo [consolas do Configuration Manager instalar](../../../../core/servers/deploy/install/install-consoles.md).|  
|Configurar componentes de site|Configure componentes do site em cada site para modificar o comportamento das funções do sistema de sites e relatórios de estado de site. Para obter mais informações, veja [Componentes do site para o System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Criar coleções personalizadas|Utilizando as informações que foi detetadas sobre utilizadores e dispositivos, crie coleções personalizadas de objetos para simplificar tarefas de gestão futura. Para obter mais informações, consulte o artigo [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Configurar definições para gerir implementações de alto risco|Configure definições de um site que avisa os utilizadores administrativos quando criam uma implementação de sequência de tarefas de alto risco.  Para obter mais informações, consulte o artigo [definições para gerir implementações de alto risco para o System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Configurar réplicas de bases de dados para pontos de gestão|Configure uma réplica de base de dados para reduzir a carga de CPU é colocada no servidor de base de dados do site pelos pontos de gestão à medida que pedidos a partir de clientes de serviço. Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Configurar um grupo de disponibilidade de AlwaysOn do SQL Server para alojar a base de dados do site|A partir da versão 1602, configure grupos de disponibilidade como soluções de elevada disponibilidade e recuperação de desastres para alojar a base de dados do site em sites primários e o site de administração central. Para obter mais informações, consulte o artigo [SQL Server AlwaysOn numa base de dados do site elevada para o System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).|  
|Modificar a replicação entre sites|Consulte [Transferência de dados entre sites no System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) para saber mais sobre os seguintes assuntos:<br /><br /> Configurar [replicação baseada em ficheiros](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) entre os sites secundários<br /><br /> Configurar [ligações de replicação de base de dados](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configurar [vistas distribuídas](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  
