---
title: Planear a migração
titleSuffix: Configuration Manager
description: Saiba mais sobre os sites e hierarquias antes de migrar dados para uma hierarquia de destino do System Center Configuration Manager.
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d3a54b7fabbd36b3c622c75622002d509540581
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141913"
---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>Planear a migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de migrar dados para uma hierarquia de destino do System Center Configuration Manager, certifique-se de que está familiarizado com sites e hierarquias no Configuration Manager. Para mais informações sobre sites e hierarquias, consulte [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Tem de instalar uma hierarquia do System Center Configuration Manager para ser a hierarquia de destino antes de migrar dados de uma hierarquia de origem suportada.  

 Depois de instalar a hierarquia de destino, configure as funcionalidades de gestão e as funções que pretende utilizar na sua hierarquia de destino antes de começar a migrar os dados.  

 Além disso, poderá ter de plano para a sobreposição entre a hierarquia de origem e a hierarquia de destino. Por exemplo, pode configurar a hierarquia de origem para utilizar as mesmas localizações de rede ou limites de como a hierarquia de destino e, em seguida, instalar novos clientes na hierarquia de destino e utilizar a atribuição automática de site. Neste cenário, uma vez que um cliente do Configuration Manager recém-instalado pode selecionar um site para associação a partir de qualquer uma das hierarquias, o cliente podem ser atribuídos incorretamente à hierarquia de origem. Por conseguinte, planeie atribuir cada novo cliente na hierarquia de destino a um site específico dessa hierarquia em vez de utilizar a atribuição automática de site.  

 Para obter mais informações sobre atribuições de sites, consulte [considerações de atribuição de site do cliente](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) na [interoperabilidade entre diferentes versões do System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

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
