---
title: Selecione o que pretende migrar
titleSuffix: Configuration Manager
description: Saiba o que pode migrar os dados e os dados que não é possível migrar para o System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b260a9e3deeb8668d736c3ed5ec2c2519e3ed50
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138981"
---
# <a name="determine-whether-to-migrate-data-to-system-center-configuration-manager"></a>Determinar se deve migrar os dados para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No System Center Configuration Manager, a migração fornece um processo para a transferência de dados e configurações que criou a partir de versões suportadas do Configuration Manager para a nova hierarquia.  Pode utilizar esta funcionalidade para:  

-   Combine várias hierarquias numa só.  

-   Mova dados e configurações de uma implantação de laboratório para a implementação de produção.

-   Mover dados e a configuração de uma versão anterior do Configuration Manager, como o Configuration Manager 2007, que não tem nenhum caminho de atualização para o System Center Configuration Manager, ou do System Center 2012 Configuration Manager (o que oferece suporte a um caminho de atualização System Center Configuration Manager).  

Com exceção da função do sistema de sites do ponto de distribuição e dos computadores que alojam pontos de distribuição, nenhuma infraestrutura (incluindo sites, funções do sistema de sites e computadores que alojam uma função do sistema de sites) migra, transfere ou pode ser partilhada entre hierarquias.  

 Embora não é possível migrar a infra-estrutura de servidor, é possível migrar clientes do Configuration Manager entre hierarquias. A migração de clientes envolve a migração dos dados utilizados pelos clientes da hierarquia de origem para a hierarquia de destino e a instalação e reatribuição do software de cliente de modo a que o cliente comunique com a nova hierarquia.

Depois de instalar um cliente para a nova hierarquia e o cliente envia os dados, o respetivo ID exclusivo do Configuration Manager ajuda a associar os dados que migrou anteriormente a cada computador cliente do Configuration Manager.  

 A funcionalidade que é fornecida pela migração ajuda a manter os investimentos efetuados nas configurações e implementações, permitindo que tire total partido das principais alterações no produto primeiro (o que foi introduzida inicialmente no System Center 2012 O Configuration Manager e, em seguida, continuou no System Center Configuration Manager). Estas alterações incluem uma hierarquia simplificada do Configuration Manager que utiliza menos sites e recursos e o processamento melhorado proveniente usando código nativo de 64 bits que é executado no hardware de 64 bits.  

 Para obter informações sobre as versões do Configuration Manager que suporta a migração, consulte [pré-requisitos para migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 As secções seguintes ajudar a planear para os dados que pode ou não migrar:  

-   [Dados que podem ser migrados para o System Center Configuration Manager](#Can_Migrate)  

-   [Dados que não é possível migrar para o System Center Configuration Manager](#Cannot_migrate)  

##  <a name="Can_Migrate"></a> Dados que podem ser migrados para o System Center Configuration Manager  
 Migração permite migrar a maioria dos objetos entre hierarquias suportadas do Configuration Manager. As instâncias migradas de alguns objetos de uma versão suportada do Configuration Manager 2007 têm de ser modificadas para estar em conformidade com o formato de esquema e de objeto do System Center 2012 Configuration Manager.

Estas alterações não afetam os dados na base de dados do site de origem. Objetos que são migrados a partir de uma versão suportada do System Center 2012 Configuration Manager ou System Center Configuration Manager não necessitam de alteração.  

 Seguem-se objetos que podem migrar com base na versão do Configuration Manager na hierarquia de origem. Alguns objetos, como consultas, não são migrados. Se quiser continuar a utilizar estes objetos que não são migrados, tem de os recriar na nova hierarquia. Outros objetos, incluindo alguns dados de cliente, são recriados automaticamente na nova hierarquia quando gerir clientes dessa hierarquia.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-system-center-configuration-manager-current-branch"></a>Objetos que podem ser migrados a partir do ramo atual do System Center 2012 Configuration Manager ou System Center Configuration Manager

-   Aplicativos para o System Center 2012 Configuration Manager e versões posteriores  

-   Ambiente Virtual App-V do System Center 2012 Configuration Manager e versões posteriores  

-   Personalizações do Asset Intelligence  

-   Limites  

-   Coleções: Para migrar coleções a partir de uma versão suportada do System Center 2012 Configuration Manager ou System Center Configuration Manager, utilize uma tarefa de migração de objetos.  

-   Definições de compatibilidade:  

    -   Linhas de base de configuração  

    -   Itens de configuração  

-   Implementações  

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

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Objetos que pode migrar a partir do Configuration Manager 2007 SP2

-   Anúncios  

-   Aplicativos para o System Center 2012 Configuration Manager e versões posteriores  

-   Ambiente Virtual App-V do System Center 2012 Configuration Manager e versões posteriores  

-   Personalizações do Asset Intelligence  

-   Limites  

-   Coleções: É possível migrar coleções de uma versão suportada do Configuration Manager 2007 utilizando uma tarefa de migração de coleção.  

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

##  <a name="Cannot_migrate"></a> Dados que não é possível migrar para o System Center Configuration Manager  
 Não é possível migrar os seguintes tipos de objetos:  

-   Informações de aprovisionamento de cliente AMT  

-   Ficheiros em clientes, incluindo:  

    -   Dados de inventário e histórico de cliente  

    -   Ficheiros na cache do cliente  

-   Consultas  

-   Direitos de segurança do Configuration Manager 2007 e as instâncias para o site e os objetos  

-   Relatórios do Configuration Manager 2007 a partir do SQL Server Reporting Services  

-   Relatórios de web do Configuration Manager 2007  

-   Relatórios do System Center 2012 Configuration Manager e o System Center Configuration Manager  

-   System Center 2012 Configuration Manager e System Center Configuration Manager baseada em funções de administração:  

    -   Funções de segurança  

    -   Âmbitos de segurança  
