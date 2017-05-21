---
title: "Planear a migração | Documentos do Microsoft"
description: Saiba mais sobre sites e hierarquias antes de migrar dados para uma hierarquia de destino do System Center Configuration Manager.
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: a2405bc04889bd6ae46069fe447228149bbaf468
ms.openlocfilehash: fffef1e95e1dfa03971f140a6e5a7fff9bfe5e27
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>Planear a migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de migrar dados para uma hierarquia de destino do System Center Configuration Manager, certifique-se de que está familiarizado com sites e hierarquias no Configuration Manager. Para mais informações sobre sites e hierarquias, consulte o artigo [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Tem de instalar uma hierarquia do System Center Configuration Manager para ser a hierarquia de destino antes de migrar dados a partir de uma hierarquia de origem suportada.  

 Depois de instalar a hierarquia de destino, configure as funcionalidades de gestão e funções que pretende utilizar na hierarquia de destino antes de começar a migrar dados.  

 Além disso, poderá ter de plano para a sobreposição entre a hierarquia de origem e a hierarquia de destino. Por exemplo, pode configurar a hierarquia de origem para utilizar as mesmas localizações de rede ou limites da hierarquia de destino e que instala novos clientes na hierarquia de destino e utiliza a atribuição automática de site. Neste cenário, uma vez que um cliente do Configuration Manager recentemente instalado, pode selecionar um site para associação em qualquer das hierarquias, o cliente pode ser atribuído incorretamente à hierarquia de origem. Por conseguinte, planeie atribuir cada novo cliente na hierarquia de destino a um site específico dessa hierarquia em vez de utilizar a atribuição automática de site.  

 Para mais informações sobre atribuições de sites, consulte o artigo [considerações de atribuição de site do cliente](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) no [interoperabilidade entre diferentes versões do System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="plan-topics"></a>Tópicos de plano  
 Utilize os tópicos seguintes para o ajudar a planear a migração de uma hierarquia de origem suportada para uma hierarquia de destino do System Center Configuration Manager:

-   [Pré-requisitos da migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Listas de verificação de administrador para a migração no System Center Configuration Manager de planeamento](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determinar se deve migrar dados para o System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Listas de verificação de administrador para a migração no System Center Configuration Manager de planeamento](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planear uma estratégia de migração de clientes no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planear a migração de objetos do Configuration Manager para System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Plano para monitorizar a atividade de migração no System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planear a conclusão da migração no System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  

