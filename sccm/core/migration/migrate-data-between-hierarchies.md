---
title: Migrar dados | Documentos do Microsoft
description: Saiba como transferir dados a partir de uma hierarquia de origem para uma hierarquia de destino do System Center Configuration Manager.
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: 11
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: a8959c72608a1531fb323176c33a848a4a669b1c
ms.openlocfilehash: dface33392c2a2a662522656eabf0936b52b28fc
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>Migrar dados entre hierarquias no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize a migração para transferir dados de uma hierarquia de origem suportada para a hierarquia de destino do System Center Configuration Manager.  Ao migrar dados a partir de uma hierarquia de origem:  

-   Pode aceder aos dados das bases de dados do site que identifica na infraestrutura de origem e transferir esses dados para o seu ambiente atual.  

-   Migração não altera os dados na hierarquia de origem, mas identifica os dados e armazena uma cópia na base de dados da hierarquia de destino.  

Considere os seguintes aspetos quando planear a estratégia de migração :  

-   É possível migrar uma infraestrutura existente do Configuration Manager 2007 SP2 para o System Center Configuration Manager.  

-   Pode migrar alguns ou todos os dados suportados de um site de origem.  

-   Pode migrar os dados de um único site de origem para vários sites diferentes da hierarquia de destino.  

-   Pode mover dados de vários sites de origem para um único site da hierarquia de destino.  

##  <a name="BKMK_MigrationConcepts"></a> Conceitos de Migração  
 Poderá encontrar os seguintes conceitos e termos ao utilizar a migração.  

|Conceito ou termo|Mais informações|  
|---------------------|----------------------|  
|Hierarquia de origem|Uma hierarquia que executa uma versão suportada do Configuration Manager e contém os dados que pretende migrar. Quando configurar a migração, identifique a hierarquia de origem quando especifica o site de nível superior da hierarquia de origem. Após ter especificado uma hierarquia de origem, o site de nível superior da hierarquia de destino recolhe dados da base de dados do site de origem designado para identificar os dados que pode migrar.<br /><br /> Para obter mais informações, consulte o artigo [hierarquias de origem](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies) no [planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Sites de origem|Os sites da hierarquia de origem que contêm dados que pode migrar para a hierarquia de destino.<br /><br /> Para obter mais informações, consulte o artigo [sites de origem](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites) no [planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Hierarquia de destino|Uma hierarquia do System Center Configuration Manager onde é executada a migração para importar dados a partir de uma hierarquia de origem.|  
|Recolha de dados|O processo contínuo de identificar informações numa hierarquia de origem que pode migrar para a sua hierarquia de destino. O Configuration Manager verifica a hierarquia de origem com base numa agenda para identificar quaisquer alterações às informações da hierarquia de origem que migrou anteriormente e que pode querer atualizar na hierarquia de destino.<br /><br /> Para obter mais informações, consulte o artigo [recolha de dados](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) no [planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Tarefas de migração|O processo de configuração de objetos específicos para migrar e, em seguida, a gestão da migração desses objetos para a hierarquia de destino.<br /><br /> Para obter mais informações, consulte o artigo [planear uma estratégia de tarefa de migração no System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)|  
|Migração de clientes|O processo de transferência de informações utilizadas pelos clientes da base de dados do site de origem para a base de dados da hierarquia de destino. Esta migração de dados é depois seguida por uma atualização do software de cliente dos dispositivos com a versão de software de cliente da hierarquia de destino.<br /><br /> Para obter mais informações, veja [Planear uma estratégia de migração de clientes no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).|  
|Pontos de distribuição partilhados|Os pontos de distribuição da hierarquia de origem que são partilhados com a hierarquia de destino durante o período de migração.<br /><br /> Durante o período de migração, os clientes atribuídos a sites da hierarquia de destino podem obter conteúdos a partir de pontos de distribuição partilhados.<br /><br /> Para obter mais informações, consulte o artigo [partilhar pontos de distribuição entre hierarquias de origem e destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) no [planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).|  
|Monitorização da migração|O processo de monitorização de atividades de migração. Pode monitorizar o progresso da migração e o sucesso do **migração** nó o **administração** área de trabalho.<br /><br /> Para obter mais informações, consulte o artigo [planear a monitorização da atividade de migração no System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md).|  
|Parar a recolha de dados|O processo de interrupção da recolha de dados a partir de sites de origem. Quando já não tiver dados para migrar de uma hierarquia de origem, ou se pretender interromper as atividades relacionadas com a migração, pode configurar a hierarquia de destino para interromper a recolha de dados da hierarquia de origem.<br /><br /> Para obter mais informações, consulte o artigo [recolha de dados](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) no [planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Limpar dados de migração|O processo de conclusão da migração de uma hierarquia de origem através da remoção das informações sobre a migração da base de dados de hierarquias de destino.<br /><br /> Para obter mais informações, veja [Planear para concluir a migração no System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).|  

## <a name="typical-workflow-for-migration"></a>Fluxo de trabalho normal para a migração  
Para configurar um fluxo de trabalho para a migração:

1.  Especifique uma hierarquia de origem suportada.  

2.  Configure a recolha de dados. Recolha de dados permite que o Configuration Manager para recolher informações sobre os dados que podem migrar a partir da hierarquia de origem.  

     O Configuration Manager repete automaticamente o processo de recolha de dados de uma agenda simples enquanto o interromper os processo de recolha de dados. Por predefinição, os processo de recolha de dados é repetido a cada quatro horas para que o Configuration Manager pode identificar as alterações aos dados da hierarquia de origem que pode querer migrar. A recolha de dados também é necessária para partilhar pontos de distribuição entre a hierarquia de origem e a hierarquia de destino.  

3.  Crie tarefas de migração para migrar dados entre a hierarquia de origem e a hierarquia de destino.  

4.  É possível parar o o processo de recolha de dados em qualquer altura utilizando o comando **Parar a Recolha de Dados** . Quando parar a recolha de dados, o Configuration Manager já não identifica as alterações aos dados da hierarquia de origem e já não pode partilhar pontos de distribuição entre hierarquias de origem e destino. Normalmente, utiliza esta ação quando já não pretende migrar dados nem partilhar pontos de distribuição da hierarquia de origem.  

5.  Opcionalmente, após a interrupção da recolha de dados em todos os sites da hierarquia de origem, é possível limpar os dados de migração utilizando o comando **Limpar Dados de Migração** . Este comando elimina os dados históricos sobre a migração de uma hierarquia de origem a partir da base de dados da hierarquia de destino.  

Depois de migrar dados a partir de uma hierarquia de origem do Configuration Manager que já não irá utilizar para gerir o ambiente, pode desativar essa hierarquia de origem e a infraestrutura.  

##  <a name="BKMK_MigrationScenarios"></a> Cenários de migração  
 O Configuration Manager suporta os seguintes cenários de migração.  

> [!NOTE]  
>  A expansão de uma hierarquia que tenha um site autónomo numa hierarquia que tenha um site de administração central não é classificada como uma migração. Para obter informações sobre expansão da hierarquia, consulte o artigo [expandir um site primário autónomo](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) no [utilizar o Assistente de configuração para instalar sites](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>Migração a partir de hierarquias do Configuration Manager 2007  
 Quando utilizar a migração para migrar dados do Configuration Manager 2007, pode manter o investimento na infraestrutura de sites existente e obter os seguintes benefícios:  

|Benefícios|Mais informações|  
|-------------|----------------------|  
|Melhorias da base de dados do site|A base de dados do System Center Configuration Manager suporta Unicode completo.|  
|Replicação da base de dados entre sites|No System Center Configuration Manager a replicação baseia-se no Microsoft SQL Server. Isto melhora o desempenho da transferência dos dados de site para site.|  
|Gestão centrada no utilizador|Os utilizadores são o foco das tarefas de gestão no System Center Configuration Manager. Por exemplo, pode distribuir software por um utilizador mesmo que não saiba o nome do dispositivo desse utilizador. Além disso, o System Center Configuration Manager proporciona aos utilizadores muito mais controlo sobre o software instalado nos respetivos dispositivos e quando esse software é instalado.|  
|Simplificação da hierarquia|No System Center Configuration Manager, o tipo de site de administração central e as alterações ao comportamento dos sites primários e secundários permitem-lhe construir uma hierarquia de sites muito mais simples que utiliza menos largura de banda de rede e necessita de menos servidores.|  
|Administração baseada em funções|Este modelo de segurança central do System Center Configuration Manager oferece uma segurança de toda a hierarquia e gestão de que corresponde às suas necessidades administrativas e empresariais.|  

> [!NOTE]  
>  Devido às alterações de estrutura que foram primeiro introduzidas no System Center 2012 Configuration Manager, não é possível atualizar a infraestrutura do Configuration Manager 2007 para o System Center Configuration Manager. Atualização no local é suportada a partir do System Center 2012 Configuration Manager para System Center Configuration Manager.  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>Migração a partir do Configuration Manager 2012 ou de outra hierarquia do System Center Configuration Manager  
 O processo de migração dos dados a partir de uma hierarquia do System Center 2012 Configuration Manager ou System Center Configuration Manager são o mesmo. Isto inclui a migrar dados de várias hierarquias de origem para uma única hierarquia de destino, como quando a sua empresa obtém recursos adicionais que já são geridos pelo Configuration Manager. Além disso, pode migrar dados de ambiente de teste ao seu ambiente de produção do Configuration Manager. Isto permite-lhe manter o investimento no ambiente de teste do Configuration Manager.  

## <a name="additional-topics-for-migration"></a>Tópicos adicionais para a migração:  

-   [Planear a migração para o System Center Configuration Manager](../../core/migration/planning-for-migration.md)  

-   [Configurar hierarquias de origem e sites de origem para migração para o System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operações de migração para o System Center Configuration Manager](../../core/migration/operations-for-migration.md)  

-   [Segurança e privacidade da migração para o System Center Configuration Manager](../../core/migration/security-and-privacy-for-migration.md)  

## <a name="see-also"></a>Consulte Também  
 [Começar a utilizar o System Center Configuration Manager](../../core/servers/deploy/start-using.md)
