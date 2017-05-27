---
title: Escolher o que pretende migrar | Documentos do Microsoft
description: "Saiba quais são os dados pode migrar e quais são os dados não é possível migrar para o System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d37261c03fddc3d576fcef73fabd7189e4c46d38
ms.openlocfilehash: 9dc5f6c9f58e1fc33b2dc9dd76737ae23af81993
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="determine-whether-to-migrate-data-to-system-center-configuration-manager"></a>Determinar se deve migrar os dados para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No System Center Configuration Manager, a migração fornece um processo para transferir dados e configurações que tiver criado a partir de versões suportadas do Configuration Manager para a nova hierarquia.  Pode utilizar esta funcionalidade para:  

-   Combine várias hierarquias numa só.  

-   Mova dados e configurações de uma implementação de laboratório para a implementação de produção.

-   Deslocar-se dados e a configuração a partir de uma versão anterior do Configuration Manager, como do Configuration Manager 2007, que não possui nenhum caminho de atualização para o System Center Configuration Manager, ou a partir do System Center 2012 Configuration Manager (o que suporte um caminho de atualização para o System Center Configuration Manager).  

Com exceção da função do sistema de sites do ponto de distribuição e dos computadores que alojam pontos de distribuição, nenhuma infraestrutura (incluindo sites, funções do sistema de sites e computadores que alojam uma função do sistema de sites) migra, transfere ou pode ser partilhada entre hierarquias.  

 Embora seja possível migrar a infraestrutura de servidor, é possível migrar clientes do Configuration Manager entre hierarquias. A migração de clientes envolve a migração dos dados utilizados pelos clientes da hierarquia de origem para a hierarquia de destino e a instalação e reatribuição do software de cliente de modo a que o cliente comunique com a nova hierarquia.

Depois de instalar um cliente na nova hierarquia e o cliente envia os dados, o respetivo ID exclusivo do Configuration Manager ajuda a associar os dados que migrou anteriormente a cada computador cliente do Configuration Manager.  

 A funcionalidade que é fornecida pela migração ajuda a manter os investimentos efetuados nas configurações e implementações, permitindo que a tirar o máximo partido das principais alterações no produto primeiro (que foi introduzida pela primeira vez no System Center 2012 Configuration Manager e, em seguida, continuação no System Center Configuration Manager). Estas alterações incluem uma hierarquia simplificada do Configuration Manager que utiliza menos sites e recursos e o processamento melhorado que provêm de utilização do código nativo de 64 bits executado em hardware de 64 bits.  

 Para obter informações sobre as versões do Configuration Manager que suporta a migração, consulte o artigo [os pré-requisitos da migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 As secções seguintes ajudam a planear para dados que pode ou não migrar:  

-   [Dados que pode migrar para o System Center Configuration Manager](#Can_Migrate)  

-   [Dados que não é possível migrar para o System Center Configuration Manager](#Cannot_migrate)  

##  <a name="Can_Migrate"></a>Dados que pode migrar para o System Center Configuration Manager  
 Migração permite migrar a maioria dos objetos entre hierarquias suportadas do Configuration Manager. As instâncias migradas de alguns objetos de uma versão suportada do Configuration Manager 2007 têm de ser modificadas para conformidade com o formato de esquema e de objeto do System Center 2012 Configuration Manager.

Estas alterações não afetam os dados na base de dados de site de origem. Objetos migrados a partir de uma versão suportada do System Center 2012 Configuration Manager ou System Center Configuration Manager não necessitam de alteração.  

 Seguem-se os objetos que podem migrar com base na versão do Configuration Manager na hierarquia de origem. Alguns objetos, como consultas, não são migrados. Se quiser continuar a utilizar estes objetos que não são migrados, tem de os recriar na nova hierarquia. Outros objetos, incluindo alguns dados do cliente, são recriados automaticamente na nova hierarquia quando gerir clientes nessa hierarquia.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-system-center-configuration-manager-current-branch"></a>Objetos que podem migrar a partir do System Center 2012 Configuration Manager ou System Center Configuration Manager ramo atual

-   Anúncios  

-   Aplicações para o System Center 2012 Configuration Manager e versões posteriores  

-   Ambiente Virtual de App-V a partir do System Center 2012 Configuration Manager e versões posteriores  

-   Personalizações do Asset Intelligence  

-   Limites  

-   Coleções: Para migrar coleções a partir de uma versão suportada do System Center 2012 Configuration Manager ou System Center Configuration Manager, pode utilizar uma tarefa de migração de objetos.  

-   Definições de compatibilidade:  

    -   Linhas de base de configuração  

    -   Itens de configuração  

-   Implementação do sistema operativo:  

    -   Imagens de arranque  

    -   Pacotes de controladores  

    -   Controladores  

    -   Imagens  

    -   Pacotes  

    -   Sequências de tarefas  

-   Resultados da pesquisa: Guardar os critérios de pesquisa  

-   Atualizações de software:  

    -   Implementações  

    -   Pacotes de implementação  

    -   Modelos  

    -   Listas de atualização de software  

-   Pacotes de distribuição de software  

-   Regras de medição de software  

-   Pacotes de aplicações virtuais  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Objetos que podem migrar a partir do Configuration Manager 2007 SP2

-   Anúncios  

-   Aplicações para o System Center 2012 Configuration Manager e versões posteriores  

-   Ambiente Virtual de App-V a partir do System Center 2012 Configuration Manager e versões posteriores  

-   Personalizações do Asset Intelligence  

-   Limites  

-   Coleções: É possível migrar coleções a partir de uma versão suportada do Configuration Manager 2007 utilizando uma tarefa de migração de coleção.  

-   Definições de compatibilidade (designadas como gestão de configuração pretendida no Configuration Manager 2007):  

    -   Linhas de base de configuração  

    -   Itens de configuração  

-   Implementação do sistema operativo:  

    -   Imagens de arranque  

    -   Pacotes de controladores  

    -   Controladores  

    -   Imagens  

    -   Pacotes  

    -   Sequências de tarefas  

-   Resultados da pesquisa: Pastas de pesquisa  

-   Atualizações de software:  

    -   Implementações  

    -   Pacotes de implementação  

    -   Modelos  

    -   Listas de atualização de software  

-   Pacotes de distribuição de software  

-   Regras de medição de software  

-   Pacotes de aplicações virtuais  

##  <a name="Cannot_migrate"></a>Dados que não é possível migrar para o System Center Configuration Manager  
 Não é possível migrar os seguintes tipos de objetos:  

-   Informações de aprovisionamento de cliente AMT  

-   Ficheiros nos clientes, incluindo:  

    -   Dados de inventário e histórico de cliente  

    -   Ficheiros na cache do cliente  

-   Consultas  

-   Direitos de segurança do Configuration Manager 2007 e instâncias do site e objetos  

-   Relatórios do Configuration Manager 2007 a partir do SQL Server Reporting Services  

-   Relatórios de web do Configuration Manager 2007  

-   Relatórios do System Center 2012 Configuration Manager e System Center Configuration Manager  

-   System Center 2012 Configuration Manager e System Center Configuration Manager baseada em funções de administração:  

    -   Funções de segurança  

    -   Âmbitos de segurança  

