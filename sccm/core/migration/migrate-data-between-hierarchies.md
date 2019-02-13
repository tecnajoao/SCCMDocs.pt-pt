---
title: Migrar dados
titleSuffix: Configuration Manager
description: Saiba como transferir dados de uma hierarquia de origem para uma hierarquia de destino do Configuration Manager.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6f0b7f67c1b25fc28f82956a43f9a503ad3d190
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123506"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Migrar dados entre hierarquias no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize a migração para transferir dados de uma hierarquia de origem suportada para a hierarquia de destino do Configuration Manager (ramo atual). Ao migrar dados de uma hierarquia de origem:  

- Aceder a dados das bases de dados do site na infraestrutura de origem e, em seguida, transferir esses dados para seu ambiente atual.  

- Migração não altera os dados na hierarquia de origem. Em vez disso, ele identifica os dados e armazena uma cópia na base de dados da hierarquia de destino.  

Considere os seguintes pontos ao planejar sua estratégia de migração:  

- Pode migrar uma infraestrutura existente do Configuration Manager 2007 SP2 para o Configuration Manager (ramo atual).  

- Pode migrar alguns ou todos os dados suportados de um site de origem.  

- Pode migrar os dados de um único site de origem para vários sites diferentes da hierarquia de destino.  

- Pode mover dados de vários sites de origem para um único site da hierarquia de destino.  


O vídeo seguinte descreve e demonstra dois comum [cenários de migração](#BKMK_MigrationScenarios). Ele também inclui opções para Microsoft Azure, incluindo em planos de migração.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="BKMK_MigrationConcepts"></a> Conceitos  

 O Configuration Manager utiliza os seguintes conceitos e termos durante a migração.  

#### <a name="source-hierarchy"></a>Hierarquia de origem
Uma hierarquia que executa uma versão suportada do Configuration Manager e tem dados que pretende migrar. Quando configurar a migração, que identifica a hierarquia de origem ao especificar o site de nível superior de uma hierarquia de origem. Após ter especificado uma hierarquia de origem, o site de nível superior da hierarquia de destino recolhe dados da base de dados do site de origem designado para identificar os dados que pode migrar. 

Para obter mais informações, consulte [hierarquias de origem](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Sites de origem
Os sites da hierarquia de origem que contêm dados que pode migrar para a hierarquia de destino. 

Para obter mais informações, consulte [sites de origem](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Hierarquia de destino
Uma hierarquia do Configuration Manager (ramo atual) em que é executada a migração para importar dados de uma hierarquia de origem.

#### <a name="data-gathering"></a>Recolha de dados
O processo contínuo de identificar informações numa hierarquia de origem que pode migrar para a sua hierarquia de destino. O Configuration Manager verifica a hierarquia de origem com base numa agenda. Esse processo identifica quaisquer alterações às informações da hierarquia de origem que migrou anteriormente e que pode querer atualizar na hierarquia de destino.

Para obter mais informações, consulte [recolha de dados](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Tarefas de migração
O processo de configuração de objetos específicos para migrar e, em seguida, a gestão da migração desses objetos para a hierarquia de destino.

Para obter mais informações, consulte [planear uma estratégia de tarefa de migração](/sccm/core/migration/planning-a-migration-job-strategy).

#### <a name="client-migration"></a>Migração de clientes
O processo de transferência de informações utilizadas pelos clientes da base de dados do site de origem para a base de dados da hierarquia de destino. Esta migração de dados é depois seguida por uma atualização de software de cliente em dispositivos para a versão do software de cliente da hierarquia de destino.

Para obter mais informações, consulte [planear uma estratégia de migração de clientes](/sccm/core/migration/planning-a-client-migration-strategy).

#### <a name="shared-distribution-points"></a>Pontos de distribuição partilhados
Os pontos de distribuição da hierarquia de origem que o Configuration Manager partilha com a hierarquia de destino durante o período de migração.

Durante o período de migração, os clientes atribuídos a sites da hierarquia de destino podem obter o conteúdo de pontos de distribuição partilhados.

Para obter mais informações, consulte [partilhar pontos de distribuição entre hierarquias de origem e destino](/sccm/core/migration/planning-a-content-deployment-migration-strategy#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Monitorização da migração
O processo de monitorização de atividades de migração. Monitorizar o progresso da migração e o sucesso dos **migração** nó a **administração** área de trabalho.

Para obter mais informações, consulte [planear a monitorização da atividade de migração](/sccm/core/migration/planning-to-monitor-migration-activity).

#### <a name="stop-gathering-data"></a>Parar a recolha de dados
O processo de interrupção da recolha de dados a partir de sites de origem. Quando já não tem dados para migrar de uma hierarquia de origem, ou se pretende colocar em pausa atividades relacionadas com a migração, pode configurar a hierarquia de destino para interromper a recolha de dados da hierarquia de origem.

Para obter mais informações, consulte [recolha de dados](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Limpar dados de migração
O processo de conclusão da migração de uma hierarquia de origem através da remoção das informações sobre a migração da base de dados de hierarquias de destino.

Para obter mais informações, consulte [planear a conclusão da migração](/sccm/core/migration/planning-to-complete-migration).



## <a name="typical-workflow"></a>Fluxo de trabalho típico  

Para configurar um fluxo de trabalho para a migração:

1.  Especifique uma hierarquia de origem suportada.  

2.  Configure a recolha de dados. Recolha de dados permite que o Configuration Manager para recolher informações sobre os dados que podem migrar a partir da hierarquia de origem.  

     O Configuration Manager repete automaticamente o processo de recolha de dados com base numa agenda simple enquanto não o interromper os processo de recolha de dados. Por predefinição, os processo de recolha de dados repete-se a cada quatro horas para que o Configuration Manager possa identificar as alterações aos dados da hierarquia de origem. Recolha de dados também são necessários para partilhar pontos de distribuição.  

3.  Crie tarefas de migração para migrar dados entre a hierarquia de origem e a hierarquia de destino.  

4.  Pode parar o processo de recolha dados em qualquer altura utilizando o **parar de recolher dados** ação. Quando parar a recolha de dados, o Configuration Manager já não identifica as alterações aos dados da hierarquia de origem e já não pode partilhar pontos de distribuição. Normalmente, utiliza esta ação quando já não pretende migrar dados nem partilhar pontos de distribuição da hierarquia de origem.  

5.  Opcionalmente, após a recolha de dados interrupção em todos os sites da hierarquia de origem, pode limpar os dados de migração utilizando o **limpar dados de migração** ação. Esta ação elimina os dados históricos sobre a migração de uma hierarquia de origem da base de dados da hierarquia de destino.  

Depois de migrar dados e já não necessita de hierarquia de origem para gerir dispositivos no seu ambiente, pode desativar essa hierarquia de origem e a infraestrutura.  



##  <a name="BKMK_MigrationScenarios"></a> Cenários  

 O Configuration Manager suporta os seguintes cenários de migração:
- [Migração de hierarquias do Configuration Manager 2007](#bkmk_2007)  
- [Migração do Configuration Manager 2012 ou de outra hierarquia do Configuration Manager](#bkmk_2012)

> [!NOTE]  
>  A expansão de uma hierarquia que tenha um site autónomo para uma hierarquia que tenha um site de administração central não está categorizada como uma migração. Para obter informações sobre expansão da hierarquia, consulte [expandir um site primário autónomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand).  


### <a name="bkmk_2007"></a> Migração de hierarquias do Configuration Manager 2007  

 Quando utiliza a migração para migrar dados do Configuration Manager 2007, pode manter o seu investimento na infraestrutura de sites existente e obter os seguintes benefícios:  

#### <a name="site-database-improvements"></a>Melhorias da base de dados do site
A base de dados do Configuration Manager (ramo atual) suporta Unicode completo.

#### <a name="database-replication-between-sites"></a>Replicação da base de dados entre sites
Replicação no Configuration Manager (ramo atual) baseia-se no Microsoft SQL Server. Este comportamento melhora o desempenho de transferência de dados de site a site.

#### <a name="user-centric-management"></a>Gestão centrada no utilizador
Os utilizadores são o foco das tarefas de gestão no Configuration Manager (ramo atual). Por exemplo, pode distribuir software por um utilizador, mesmo se não souber o nome do dispositivo para esse utilizador. Além disso, o Configuration Manager fornece aos usuários muito mais controlo sobre que software está instalado nos respetivos dispositivos e quando esse software é instalado.

#### <a name="hierarchy-simplification"></a>Simplificação da hierarquia
Configuration Manager (ramo atual) permite-lhe construir uma hierarquia de sites mais simples. Este aprimoramento é devido à introdução do tipo de site de administração central e alterações ao comportamento dos sites primários e secundários. Configuration Manager (ramo atual) usa menos largura de banda de rede e necessita de menos servidores que as versões anteriores.

#### <a name="role-based-administration"></a>Administração baseada em funções
Este modelo de segurança central no Configuration Manager (ramo atual) oferece segurança ao nível da hierarquia e o gerenciamento que corresponde às suas necessidades administrativas e empresariais.

> [!NOTE]  
>  Devido às alterações estruturais introduzidas inicialmente no System Center 2012 Configuration Manager, não é possível atualizar do Configuration Manager 2007 para o Configuration Manager (ramo atual). Atualização no local é suportada a partir do System Center 2012 Configuration Manager para o Configuration Manager (ramo atual).  


### <a name="bkmk_2012"></a> Migração do Configuration Manager 2012 ou de outra hierarquia do Configuration Manager  
 O processo de migração dos dados a partir de uma hierarquia do System Center 2012 Configuration Manager ou Configuration Manager são o mesmo. Este processo inclui a migrar dados a partir de várias hierarquias de origem para uma hierarquia de destino único. Pode utilizar este processo, quando a sua empresa obtém os recursos adicionais que já são geridos pelo Configuration Manager. Além disso, pode migrar dados a partir de um ambiente de teste para seu ambiente de produção do Configuration Manager. Este processo permite-lhe manter o seu investimento no ambiente de teste do Configuration Manager.  



## <a name="see-also"></a>Consulte também  

-   [Planear a migração para o Configuration Manager](/sccm/core/migration/planning-for-migration)  

-   [Configurar hierarquias de origem e sites de origem para migração](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration)  

-   [Operações de migração](/sccm/core/migration/operations-for-migration)  

-   [Segurança e privacidade da migração](/sccm/core/migration/security-and-privacy-for-migration)  

-   [Começar a utilizar o Configuration Manager](/sccm/core/servers/deploy/start-using)
