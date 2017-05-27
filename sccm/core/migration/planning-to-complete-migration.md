---
title: "Concluir a migração | Documentos do Microsoft"
description: "Saiba como concluir a migração para uma hierarquia de destino do System Center Configuration Manager depois de uma hierarquia de origem já não tem dados."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0f4a10ba7bbe397f05d724141b562b6cd8b78ea8
ms.openlocfilehash: eb1d2e320df02b26423ed4341d5bd1568b9444ad
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-to-complete-migration-in-system-center-configuration-manager"></a>Planear a conclusão da migração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o System Center Configuration Manager, pode concluir o processo de migração quando uma hierarquia de origem já não tem dados que pretende migrar para a hierarquia de destino. A conclusão da migração inclui os seguintes passos gerais:  

-   Certifique-se de que os dados que necessita foram migrados. Antes de concluir a migração a partir de uma hierarquia de origem, certifique-se de que migrou com êxito todos os recursos da hierarquia de origem que necessita na hierarquia de destino. Isto pode incluir os dados e clientes.  

-   Pare a recolha de dados de sites de origem. Para concluir a migração a partir de uma hierarquia de origem, tem primeiro de parar a recolha de dados de sites de origem.  

-   Limpe dados de migração. Depois de interromper a recolha de dados de todos os sites de origem numa hierarquia de origem, pode remover os dados sobre a hierarquia de processo e a origem de migração da base de dados da hierarquia de destino.  

-   Encerre a hierarquia de origem. Depois de concluir a migração a partir de uma hierarquia de origem e de hierarquia já não tem recursos que gere, pode encerrar os sites na hierarquia de origem e remover a infraestrutura relacionada do ambiente. Para obter informações sobre como encerrar sites e hierarquias de origem, consulte a documentação dessa versão do Configuration Manager.  

Utilize as secções seguintes para o ajudar a planear a conclusão da migração a partir de uma hierarquia de origem por parar a recolha de dados e da limpeza dos dados de migração:  

-   [Planear a interrupção da recolha de dados](#Plan_to_Stop_Data_Gath)  

-   [Planear a limpeza dos dados de migração](#Plan_to_clean_up)  

##  <a name="Plan_to_Stop_Data_Gath"></a>Planear a interrupção da recolha de dados  
 Antes de concluir a migração e limpar os dados de migração, tem de parar a recolha de dados de cada site de origem na hierarquia de origem. Para parar a recolha de dados de cada site de origem, terá de executar o **parar a recolha de dados** comando nos sites de origem da camada inferior, repetindo então o processo em cada site principal. O site de nível superior da hierarquia de origem terá de ser o último em que a recolha de dados é interrompida. Deve parar a recolha de dados em cada site subordinado antes de executar este comando num site principal. Normalmente, apenas interromperá a recolha de dados quando estiver pronto para concluir o processo de migração.  

 Depois de interromper a recolha de dados de um site de origem, os pontos de distribuição partilhados a partir desse site já não estão disponíveis como localizações de conteúdo para clientes na hierarquia de destino. Por conseguinte, certifique-se de que qualquer conteúdo migrado a que os clientes na hierarquia de destino necessitem de aceder permanece disponível utilizando uma das seguintes opções:  

-   Na hierarquia de destino, distribua o conteúdo para, pelo menos, um ponto de distribuição.  

-   Antes de interromper a recolha de dados de um site de origem, atualize ou reatribua pontos de distribuição partilhados que tenham o conteúdo necessário. Para obter mais informações sobre como atualizar ou reatribuir pontos de distribuição partilhados, consulte as secções aplicáveis [planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Depois de interromper a recolha de dados de cada site de origem na hierarquia de origem, pode limpar os dados de migração. Até limpar os dados de migração, cada tarefa de migração que tenha sido executada ou que está agendada para execução permanece acessível na consola do Configuration Manager.  

Para mais informações sobre sites de origem e a recolha de dados, consulte o artigo [planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="Plan_to_clean_up"></a>Planear a limpeza dos dados de migração  
 A limpeza dos dados de migração, é o último passo necessário para concluir a migração. Pode utilizar o **limpar dados de migração** comando depois de interromper a recolha de dados de cada site de origem na hierarquia de origem. Esta ação opcional remove dados sobre a hierarquia de origem atual da base de dados da hierarquia de destino.  

 Quando limpar os dados de migração, a maioria dos dados sobre a migração serão removidos da base de dados da hierarquia de destino. No entanto, os detalhes sobre objetos migrados são mantidos. Com estes detalhes, pode utilizar o **migração** área de trabalho para reconfigurar a hierarquia de origem que contém os dados que foram migrados, para retomar a migração a partir dessa hierarquia de origem ou para rever os objetos e a propriedade do site dos objetos migrados anteriormente.  

