---
title: "Plano para a migração"
titleSuffix: Configuration Manager
description: Saiba mais sobre sites e hierarquias antes de migrar dados para uma hierarquia de destino do System Center Configuration Manager.
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b5162cfb8154ec23593533900a91da42239e3516
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>Planear a migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de migrar dados para uma hierarquia de destino do System Center Configuration Manager, certifique-se de que está familiarizado com sites e hierarquias no Configuration Manager. Para obter mais informações sobre sites e hierarquias, consulte [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Tem de instalar uma hierarquia do System Center Configuration Manager para ser a hierarquia de destino antes de migrar dados de uma hierarquia de origem suportada.  

 Depois de instalar a hierarquia de destino, configure as funcionalidades de gestão e as funções que pretende utilizar na sua hierarquia de destino antes de começar a migrar dados.  

 Além disso, poderá ter de plano para a sobreposição entre a hierarquia de origem e a hierarquia de destino. Por exemplo, pode configurar a hierarquia de origem a utilizar as mesmas localizações de rede ou limites de como a hierarquia de destino e, em seguida, instalar novos clientes para a hierarquia de destino e utilize a atribuição automática de site. Neste cenário, porque um cliente do Configuration Manager recém-instalado pode selecionar um site para associação em qualquer das hierarquias, o cliente podem ser atribuídos incorretamente à hierarquia de origem. Por conseguinte, planeie atribuir cada novo cliente na hierarquia de destino a um site específico dessa hierarquia em vez de utilizar a atribuição automática de site.  

 Para obter mais informações sobre atribuições de sites, consulte [considerações de atribuição de site do cliente](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) no [interoperabilidade entre diferentes versões do System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="plan-topics"></a>Tópicos de plano  
 Utilize os tópicos seguintes para o ajudar a planear a migração de uma hierarquia de origem suportada para uma hierarquia de destino do System Center Configuration Manager:

-   [Pré-requisitos para migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Listas de verificação de administrador para migração no System Center Configuration Manager de planeamento](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determinar se deve migrar dados para o System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Listas de verificação de administrador para migração no System Center Configuration Manager de planeamento](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planear uma estratégia de migração de cliente no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planear a migração de objetos do Configuration Manager para o System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planear monitorizar a atividade de migração no System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planear a conclusão da migração no System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  
