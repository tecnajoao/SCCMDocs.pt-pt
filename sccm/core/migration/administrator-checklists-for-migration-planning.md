---
title: Listas de verificação da migração
titleSuffix: Configuration Manager
description: Utilize listas de verificação de administrador para ajudar a planear uma estratégia de migração para o System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3136c8add4256a646409c4a540da783a04a5b71d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128294"
---
# <a name="administrator-checklists-for-migration-planning-in-system-center-configuration-manager"></a>Listas de verificação de administrador para planeamento da migração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as seguintes listas de verificação de administrador para ajudar a planear a estratégia de migração para o System Center Configuration Manager.

##  <a name="Checklist_Migraiton_Planning"></a> Lista de verificação de administrador para planeamento da migração  
 Utilize a lista de verificação seguinte para obter os passos de planeamento de pré-migração.  

-   **Avalie o ambiente atual:**  

     Identifique as necessidades empresariais existentes que são satisfeitas pela hierarquia de origem e desenvolva planos para continuar a satisfazer essas necessidades na hierarquia de destino.  

-   **Reveja as funcionalidades e alterações que estão disponíveis com a versão do Configuration Manager que utiliza e utilize estas informações para o ajudar a criar a sua hierarquia de destino:**  

    Para obter mais informações, veja [Noções básicas do System Center Configuration Manager](../../core/understand/fundamentals.md) e [Novidades do System Center Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Determine o modelo de segurança administrativa a utilizar para a administração baseada em funções:**  

    Para obter mais informações, consulte [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Avalie sua rede e topologia do Active Directory:** Reveja a topologia da estrutura de domínio existente e da rede e considere a forma como esta influencia a estrutura da hierarquia e as tarefas de migração.  

-   **Finalize a estrutura de hierarquia de destino:**  

    Decida o posicionamento de um site de administração central, sites primários, sites secundários e opções de distribuição de conteúdo.  

-   **Mapeie a hierarquia para os computadores que irá utilizar para sites e servidores de site na hierarquia de destino:**  

    Identifique os computadores que sites e servidores do sistema de sites irão utilizar na hierarquia de destino e, em seguida, certifique-se de que possuem capacidade suficiente para atender a requisitos operacionais existentes e futuros.  

-   **Planeie a estratégia de migração de objetos:**  

    Recomendamos que utilize as tarefas de migração disponíveis para migrar objetos diferentes, incluindo limites de sites, coleções, anúncios e implementações. Para obter mais informações, consulte [tipos de tarefas de migração](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) no [planear uma estratégia de tarefa de migração no System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)  

    O Configuration Manager migra apenas os objetos que selecionar. Os objetos que não forem migrados e que sejam necessários na hierarquia de destino tem de ser recriados na hierarquia de destino.  

    Os objetos que podem migrar são apresentados quando configurar as tarefas de migração.  

-   **Planeie a estratégia de migração de clientes:**  

    Planeie a migração dos clientes utilizando uma abordagem controlada que limita a largura de banda da rede e os requisitos de processamento do servidor quando migra os clientes para a hierarquia de destino. Para obter mais informações sobre como planear uma estratégia de migração de cliente, consulte [planear uma estratégia de migração de clientes no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Planear os dados de inventário e de compatibilidade de:**  

    Do Configuration Manager não suporta migração inventário de hardware, inventário de software ou dados de compatibilidade de gestão de configuração pretendida para as atualizações de software ou clientes.  

    Em vez disso, após a migração do cliente para o novo site na hierarquia de destino e após ter recebido a política dessas configurações, o cliente envia as informações para o site atribuído. Esta ação preenche a base de dados do site de destino com os dados atuais de inventário e de compatibilidade.  

-   **Planeie a conclusão da migração da hierarquia de origem:**  

    Decida quando deverão ser migrados os clientes e os objetos. Depois de concluída a migração, pode optar por desativar os servidores do site na hierarquia de origem.  

##  <a name="Checklist_Hierarchy_for_migration"></a> Lista de verificação de administrador para migração da hierarquia  
Utilize a lista de verificação seguinte para planear uma hierarquia de destino antes de iniciar a migração.  

-   **Identificar os computadores a utilizar na hierarquia de destino:**  

    O Configuration Manager não suporta uma atualização no local da infraestrutura do Configuration Manager 2007. Em vez disso, utiliza a migração para mover dados do Configuration Manager 2007 para o System Center Configuration Manager. Isto requer a utilizar uma implementação lado a lado e instalar o System Center Configuration Manager em novos computadores.  

    Da mesma forma, quando migrar de outra hierarquia do System Center Configuration Manager, tem de instalar uma nova hierarquia de destino que seja uma implementação lado a lado para a hierarquia de origem.  

-   **Crie a hierarquia de destino:**  

    Para preparar a migração, instale e configure uma hierarquia de destino do System Center Configuration Manager que inclua um site primário. Por exemplo:  

    -   Instalar um site de administração central e, em seguida, instale, pelo menos, um subordinado principal.  

    -   Instale um site primário autónomo se não pretender utilizar um site de administração central.  

-   **Se pretender migrar informações relacionadas com atualizações de software, configure um ponto de atualização de software na hierarquia de destino e sincronizar atualizações de software:**  

    Tem de configurar e sincronizar atualizações de software na hierarquia de destino para poder migrar informações de atualizações de software a partir da hierarquia de origem.  


-   **Instalar e configurar funções de sistema de sites adicionais na hierarquia de destino:**  

    Configure funções de sistema de sites adicionais e sistemas de sites que necessita.  

-   **Verifique a funcionalidade operacional da hierarquia de destino:**  

    Verifique o seguinte:  

    -   Se a hierarquia de destino incluir vários sites, certifique-se de que a replicação da base de dados está a funcionar entre sites. Replicação de base de dados não se aplica aos sites primários autónomos.  

    -   Verifique se todas as funções de sistema de sites instaladas estão operacionais.  

    -   Verificação de que os clientes do Configuration Manager instale à hierarquia de destino pode comunicar com êxito com o site atribuído.  


##  <a name="Checklisit_Migration"></a> Lista de verificação de administrador para migração  
Utilize a lista de verificação seguinte para migrar dados da hierarquia de origem para a hierarquia de destino.  

-   **Ative a migração na hierarquia de destino:**  

    Configure uma hierarquia de origem especificando o site de nível superior da hierarquia de origem. Para obter mais informações sobre como especificar o site de origem, consulte [planear uma estratégia de hierarquia de origem no System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Quando a hierarquia de origem executar o Configuration Manager 2007 SP2, selecione e configure sites adicionais na hierarquia de origem:**  

    Para cada site adicional da hierarquia de origem do Configuration Manager 2007 SP2 que pretende recolher dados a partir de, tem de configurar credenciais para a recolha de dados. Ao configurar cada site de origem, o processo de coleta de dados começa de imediato e continua durante o período de migração até parar a recolha de dados para esse site. Recolha de dados garante que pode migrar objetos da hierarquia de origem que são atualizados ou adicionados após um processo de coleta de dados anterior.

    > [!NOTE]  
    >  Quando a hierarquia de origem executar o System Center 2012 Configuration Manager ou posterior, não precisa de configurar sites de origem adicionais.  

-   **Configure a partilha do ponto de distribuição:**  

    Pode partilhar pontos de distribuição entre as duas hierarquias para disponibilizar o conteúdo dos objetos migrados para os clientes da hierarquia de destino. Isso garante que o mesmo conteúdo permanece disponível para clientes de ambas as hierarquias e pode manter este conteúdo até que interrompa a recolha de dados e concluir a migração.  

    Para obter informações sobre pontos de distribuição partilhados, consulte [partilhar pontos de distribuição entre hierarquias de origem e de destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) no [planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Criar e executar tarefas de migração para migrar objetos associados a clientes na hierarquia de origem:**  

    Crie tarefas de migração para migrar objetos entre hierarquias. As configurações necessárias a cada tarefa de migração podem variar consoante os dados migrados pela tarefa.  

    Por exemplo, quando efetua a migração do conteúdo, independentemente da tarefa de migração utilizada, tem de atribuir a gestão desse conteúdo a um site da hierarquia de destino. O site atribuído terá acesso à localização original do ficheiro de origem para obter o conteúdo, sendo responsável pela distribuição desse conteúdo pelos pontos de distribuição da hierarquia de destino.  

    Para obter mais informações, consulte [criar e editar tarefas de migração do system center configuration manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) na [operações de migração para o System Center Configuration Manager](../../core/migration/operations-for-migration.md).  

-   **Migração dos clientes para a hierarquia de destino:**  

    O processo de migração dos clientes depende do cenário de migração:  

    -   Quando migrar clientes que possuem uma versão de cliente que não é o mesmo que a hierarquia de destino, terá de atualizar o software de cliente. A atualização requer a remoção do cliente do Configuration Manager atual, seguida da instalação da nova versão de cliente que corresponde ao site de destino.  

    -   Quando migrar clientes que possuem uma versão do cliente que corresponde à versão da hierarquia de destino, o cliente não é atualizado nem reinstalado. Em vez disso, é reatribuído a um site primário da hierarquia de destino.  

    Quando migrar um cliente para a hierarquia de destino, este é associado aos respetivos dados migrados anteriormente para esta hierarquia de destino.  

    Para mais informações, consulte [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Atualizar ou reatribuir pontos de distribuição partilhados:**  

    Quando já não necessitar de suportar clientes na sua hierarquia de origem, pode atualizar pontos de distribuição partilhados a partir de um site de origem do Configuration Manager 2007 ou reatribuir pontos de distribuição partilhados a partir de um System Center 2012 Configuration Manager ou System Center Site de origem do Configuration Manager. Se atualizar ou reatribuir um ponto de distribuição, a função do sistema de sites é transferida para um site primário da hierarquia de destino e o ponto de distribuição é removido do site de origem da hierarquia de origem. Quando atualiza ou reatribui um ponto de distribuição partilhado, o conteúdo permanece no computador do ponto de distribuição e não é necessário voltar a implementar o conteúdo para novos pontos de distribuição na hierarquia de destino.  

    Também pode atualizar um ponto de distribuição que está colocalizado num servidor do site secundário do Configuration Manager 2007. Esta operação remove o site secundário e conserva apenas um ponto de distribuição na hierarquia de destino.  

    Para obter informações sobre pontos de distribuição partilhados, consulte [partilhar pontos de distribuição entre hierarquias de origem e de destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) no [planear uma estratégia de migração de implementação de conteúdos no System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Concluir a migração:**  

    Depois de ter migrado os dados e clientes de todos os sites na hierarquia de origem e atualizar pontos de distribuição aplicável, pode concluir a migração. Para concluir a migração interromper a recolha de dados de cada site de origem na hierarquia de origem. Em seguida, pode remover as informações de migração de que não necessita e encerrar a infraestrutura da hierarquia de origem. Para mais informações, consulte [Planning to complete migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).  
