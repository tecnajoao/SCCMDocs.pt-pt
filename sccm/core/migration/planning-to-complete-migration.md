---
title: Concluir a migração
titleSuffix: Configuration Manager
description: Saiba como concluir a migração para uma hierarquia de destino do System Center Configuration Manager depois de uma hierarquia de origem já não tem dados.
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9bdffc9271b1e59bbe459dffc0e3c69578a4711
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332669"
---
# <a name="plan-to-complete-migration-in-system-center-configuration-manager"></a>Planear a conclusão da migração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o System Center Configuration Manager, pode concluir o processo de migração quando uma hierarquia de origem já não tem dados que pretende migrar para a hierarquia de destino. Concluir migração inclui os seguintes passos gerais:  

-   Certifique-se de que necessita de dados foi migrada. Antes de concluir a migração a partir de uma hierarquia de origem, certifique-se de que migrou com êxito todos os recursos da hierarquia de origem que precisa na hierarquia de destino. Isto pode incluir dados e clientes.  

-   Pare a recolha de dados de sites de origem. Para concluir a migração a partir de uma hierarquia de origem, tem primeiro de parar a recolha de dados de sites de origem.  

-   Limpe dados de migração. Depois de interromper a recolha de dados de todos os sites de origem numa hierarquia de origem, pode remover os dados sobre a hierarquia de origem e o processo de migração da base de dados da hierarquia de destino.  

-   Desative a hierarquia de origem. Depois de concluir a migração a partir de uma hierarquia de origem e de que a hierarquia já não tem recursos por si, pode desativar os sites na hierarquia de origem e remover a infraestrutura relacionada do seu ambiente. Para obter informações sobre como encerrar sites e hierarquias de origem, consulte a documentação dessa versão do Configuration Manager.  

Utilize as secções seguintes para ajudar a planear concluir a migração de uma hierarquia de origem, parando a recolha de dados e da limpeza dos dados de migração:  

-   [Planear a interrupção da recolha de dados](#Plan_to_Stop_Data_Gath)  

-   [Planear a limpeza dos dados de migração](#Plan_to_clean_up)  

##  <a name="Plan_to_Stop_Data_Gath"></a> Planear a interrupção da recolha de dados  
 Antes de concluir a migração e limpar os dados de migração, tem de parar a recolha de dados de cada site de origem na hierarquia de origem. Para parar a recolha de dados de cada site de origem, terá de executar o **parar a recolha de dados** comando em sites de origem da camada inferior, repetindo então o processo em cada site principal. O site de nível superior da hierarquia de origem terá de ser o último em que a recolha de dados é interrompida. Tem de parar recolha de dados em cada site subordinado antes de executar este comando num site principal. Normalmente, apenas interromperá a recolha de dados quando estiver pronto para concluir o processo de migração.  

 Depois de interromper a recolha de dados de um site de origem, os pontos de distribuição partilhados a partir desse site deixam de estar disponíveis como localizações de conteúdo para clientes na hierarquia de destino. Por conseguinte, certifique-se de que qualquer conteúdo migrado que os clientes na hierarquia de destino necessitem de aceder permanece disponível utilizando uma das seguintes opções:  

-   Na hierarquia de destino, distribua o conteúdo para, pelo menos, um ponto de distribuição.  

-   Antes de parar a recolha de dados de um site de origem, atualizar ou reatribuir pontos de distribuição partilhados que tenham o conteúdo necessário. Para obter mais sobre a atualização ou reatribuição de pontos de distribuição partilhados, consulte as secções aplicáveis [planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Depois de interromper a recolha de dados de cada site de origem na hierarquia de origem, pode limpar os dados de migração. Até limpar os dados de migração, cada tarefa de migração executadas ou que esteja agendada para execução permanece acessível na consola do Configuration Manager.  

Para obter mais informações sobre sites de origem e a recolha de dados, consulte [planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="Plan_to_clean_up"></a> Planear a limpeza dos dados de migração  
 O último passo necessário para concluir a migração é a limpeza dos dados de migração. Pode utilizar o **limpar dados de migração** comando depois de interromper a recolha de dados de cada site de origem na hierarquia de origem. Esta ação opcional remove dados sobre a hierarquia de origem atual da base de dados da hierarquia de destino.  

 Quando limpar os dados de migração, a maioria dos dados sobre a migração são removidos da base de dados da hierarquia de destino. No entanto, os detalhes sobre objetos migrados são mantidos. Com estes detalhes, pode utilizar o **migração** área de trabalho para reconfigurar a hierarquia de origem que tenha os dados que foram migrados, para retomar a migração a partir dessa hierarquia de origem ou para rever os objetos e a propriedade do site dos objetos migrados anteriormente.  
