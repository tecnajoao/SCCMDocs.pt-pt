---
title: Configurar sites e hierarquias
titleSuffix: Configuration Manager
description: Consulte esta lista de verificação para garantir que considera as configurações mais comuns que afetam sites e hierarquias.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9b56f408dc76b3b9bf48fbdab64a50eed14f0f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133617"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Configurar sites e hierarquias do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de instalar o primeiro site do Configuration Manager ou adicionar sites adicionais para a hierarquia, utilize esta lista de verificação para se certificar de que considere as configurações mais comuns que afetam sites e hierarquias.  

As notas de configuração seguintes aplicam-se para a maioria das implementações:  

- Algumas opções interdependentes, como grupos de limites, limites e deteção de floresta do Active Directory.  

- Várias configurações possuem valores predefinidos para utilizar sem alterar a configuração, pelo menos para iniciar.  

- Outras configurações, como grupos de limites e pontos de distribuição grupos, tem de configurá-los antes de utilizar.  

| Action | Detalhes |  
|------------|-------------|  
| Configurar a administração baseada em funções | Segregar as atribuições administrativas para controlar quais os utilizadores administrativos podem ver e gerir diferentes objetos e os dados no seu ambiente do Configuration Manager.<br /><br /> As configurações para a administração baseada em funções são partilhadas com todos os sites numa hierarquia.   <br/><br/>Para obter mais informações, consulte [configurar a administração baseada em funções](/sccm/core/servers/deploy/configure/configure-role-based-administration). |  
| Publicar dados do site para serviços de domínio do Active Directory | Torna mais fácil para os clientes encontrar serviços e utilizem eficazmente os recursos de site.<br /><br /> Primeira [expandir o esquema do Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema). Em seguida, configurar individualmente cada site para [publicar dados do site](/sccm/core/servers/deploy/configure/publish-site-data) |  
| Configurar um ponto de ligação de serviço | Plano instalar e configurar o ponto de ligação no site de nível superior da sua hierarquia. Para obter mais informações, consulte [sobre o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point). |  
| Adicionar funções do sistema de sites | Instale um ou mais funções de sistema de sites adicionais para sites individuais. Para obter mais informações, consulte [adicionar funções do sistema de sites](/sccm/core/servers/deploy/configure/add-site-system-roles). |  
| Configurar limites e grupos de limites de sites | Especifique os limites que definem as localizações de rede na sua intranet que pode conter dispositivos que pretende gerir. Em seguida, configure grupos de limites para que os clientes nessas localizações de rede podem encontrar os recursos do Configuration Manager. Para obter mais informações, consulte [definir limites de site e grupos de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups). |  
| Configurar grupos de pontos de distribuição | Configure grupos lógicos de pontos de distribuição para facilitar a gestão de implementações. Para obter mais informações, consulte [gerir grupos de pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage). |  
| Executar a deteção | Execute a deteção para localizar recursos na sua rede, incluindo a infraestrutura de rede, dispositivos e utilizadores.<br /><br /> Para obter mais informações, consulte [executar a deteção](/sccm/core/servers/deploy/configure/run-discovery). |  
| Adicionar redundância e capacidade para administradores | Instale consolas adicionais de fornecedores de SMS e o Configuration Manager para expandir a capacidade dos administradores gerir a infraestrutura:<br /><br /> **Instalar fornecedores de SMS adicionais** para fornecer redundância para a consola e ligações de API para o site. Para obter mais informações, consulte [gerir o fornecedor de SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).<br /><br /> **Instalar consolas adicionais do Configuration Manager** para fornecer acesso a utilizadores administrativos adicionais. Para obter mais informações, consulte [consolas do Configuration Manager instalar](/sccm/core/servers/deploy/install/install-consoles). |  
| Configurar componentes de site | Configure componentes do site em cada site para modificar o comportamento das funções do sistema de sites e relatórios de estado de site. Para obter mais informações, consulte [componentes do Site](/sccm/core/servers/deploy/configure/site-components). |  
| Criar coleções personalizadas | Com informações que o site Deteta sobre dispositivos e utilizadores, crie coleções personalizadas de objetos para simplificar as tarefas de gerenciamento no futuro. Para obter mais informações, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections). |  
| Configurar definições para gerir implementações de alto risco | Configure as definições de um site de alertar os administradores quando criarem uma implementação de alto risco. Para obter mais informações, consulte [definições para gerir implementações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments). |  
| Configurar réplicas de bases de dados para pontos de gestão | Configure uma réplica de base de dados para reduzir a carga do processador que é colocada no servidor de base de dados do site por pontos de gestão à medida que atendem pedidos de clientes. Para obter mais informações, consulte [réplicas para pontos de gestão de base de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points). |  
| Configurar um grupo de disponibilidade Always On do SQL Server | Configure grupos de disponibilidade como soluções de elevada disponibilidade e recuperação de desastres para alojar a base de dados do site em sites primários e o site de administração central. Para obter mais informações, consulte [SQL Server AlwaysOn para uma base de dados do site de elevada disponibilidade](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database). |  
| Modificar a replicação entre sites | Ver [transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites) para saber mais sobre os seguintes assuntos:<br /><br /> Configurar [replicação de ficheiros](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_fileroute) entre sites secundários<br /><br /> Configurar [ligações de replicação de base de dados](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_Dblinks)<br /><br /> Configurar [vistas distribuídas](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews) |  
| Configurar servidores de site em modo passivo | A partir da versão 1806, configure um servidor de site em modo passivo para cada site primário e o site de administração central. Esta funcionalidade fornece um servidor de site de elevada disponibilidade. Para obter mais informações, consulte [elevada disponibilidade do servidor do Site](/sccm/core/servers/deploy/configure/site-server-high-availability). |  
