---
title: Operações de migração
titleSuffix: Configuration Manager
description: Criar e executar tarefas para migrar dados e clientes para o System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b59ff47ace87e4c7e8a345402616de44342ea9c1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121418"
---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>Operações de migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para a migração no System Center Configuration Manager, pode migrar dados e clientes depois de recolher com êxito dados de um site de origem na hierarquia de origem suportada. Utilize as informações nas secções seguintes para criar e executar tarefas de migração para migrar dados e clientes e, em seguida, concluir o processo de migração.  

-   [Criar e editar tarefas de migração](#Create_Edit_migration_Jobs)  

-   [Executar tarefas de migração](#Run_Migration_Jobs)  

-   [Atualizar ou reatribuir um ponto de distribuição partilhado](#BKMK_ProcUpgrdSS)  

-   [Monitorizar a atividade de migração na área de trabalho Migração](#Monitor_MIgration)  

-   [Migrar clientes](#BKMK_MigrateClients)  

-   [Concluir migração](#Complete_Migration)  

##  <a name="Create_Edit_migration_Jobs"></a> Criar e editar tarefas de migração  
 Utilize os procedimentos seguintes para criar tarefas de migração de dados, editar a lista de exclusão para tarefas de migração baseada em coleções, configurar pontos de distribuição partilhados e editar agendamentos de trabalhos de migração.  

> [!NOTE]  
>  O procedimento seguinte para criar uma tarefa de migração que efetua migrações por coleções aplica-se apenas a hierarquias de origem que executem uma versão suportada do Configuration Manager 2007. O tipo de tarefa de migração baseada em coleções não está disponível quando migra de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Criar uma tarefa de migração para migrar por coleções  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Sobre o **home page** separador a **criar** de grupo, escolha **criar tarefa de migração**.  

4.  Sobre o **gerais** página do Assistente Criar tarefa de migração, configure o seguinte e, em seguida, escolha **OK**:  

    -   Especifique um nome para a tarefa de migração.  

    -   Na lista pendente **Tipo de tarefa** , selecione **Migração de coleção**.  

5.  Sobre o **selecionar coleções** página, configure o seguinte e, em seguida, escolha **próxima**:  

    -   Selecione as coleções que pretende migrar.  

    -   Se pretender migrar apenas coleções e não os objetos que estão associados essas coleções, desmarque **migrar objetos que estão associados às coleções especificadas**. Se desmarcar esta opção, não existem objetos associados são migrados nesta tarefa, e pode ignorar os passos 6 e 7.  

6.  Sobre o **selecionar objetos** página, desmarcar quaisquer tipos de objetos ou objetos específicos disponíveis que não pretende migrar. Por predefinição, são selecionados todos os tipos de objetos associados e objetos disponíveis. Selecione **Next**.  

7.  Sobre o **propriedade do conteúdo** página, atribua a propriedade do conteúdo de cada site de origem listado a um site na hierarquia de destino e, em seguida, escolha **próxima**.  

8.  Sobre o **âmbito de segurança** , selecione um ou mais âmbitos de segurança de administração baseada em funções para atribuir os objetos a migrar nesta tarefa de migração e, em seguida, escolha **próxima**.  

9. Sobre o **limitação de coleção** página, configurar uma coleção da hierarquia de destino para limitar o âmbito de cada coleção listada e, em seguida, escolha **próxima**. Não se estiver listada nenhuma coleção, escolha **seguinte**.  

10. Sobre o **substituição do código do Site** página, atribua um código de site da hierarquia de destino para substituir o código do site do Configuration Manager 2007 para cada coleção listada e, em seguida, escolha **próxima**. Não se estiver listada nenhuma coleção, escolha **seguinte**.  

11. Sobre o **rever informações** página, selecione **guardar no ficheiro** para guardar as informações apresentadas para posterior visualização. Quando estiver pronto para continuar, escolha **seguinte**.  

12. Sobre o **definições** página, configure quando será executada a tarefa de migração, escolha as definições adicionais que sejam necessárias para esta tarefa de migração e, em seguida, escolha **seguinte**.  

13. Confirme as definições e conclua o assistente.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Criar uma tarefa de migração para migrar por objetos  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Sobre o **home page** separador a **criar** de grupo, escolha **criar tarefa de migração**.  

4.  Sobre o **gerais** página do Assistente Criar tarefa de migração, configure o seguinte e, em seguida, escolha **próxima**:  

    -   Especifique um nome para a tarefa de migração.  

    -   Na lista pendente **Tipo de tarefa** , selecione **Migração de objeto**.  

5.  Na página **Selecionar Objetos** , selecione os tipos de objeto que pretende migrar. Por predefinição, são selecionados todos os objetos disponíveis para cada tipo de objeto que selecionou.  

6.  Sobre o **propriedade do conteúdo** página, atribua a propriedade do conteúdo de cada site de origem listado a um site na hierarquia de destino e, em seguida, escolha **próxima**. Se estiver listado nenhum site de origem, escolha **seguinte**.  

7.  Sobre o **âmbito de segurança** , selecione um ou mais âmbitos de segurança de administração baseada em funções para atribuir aos objetos nesta tarefa de migração e, em seguida, escolha **próxima**.  

8.  Sobre o **rever informações** página, selecione **guardar no ficheiro** para guardar as informações apresentadas para posterior visualização. Quando estiver pronto para continuar, escolha **seguinte**.  

9. Sobre o **definições** página, definir quando a tarefa de migração será executado e escolha as definições adicionais que sejam necessárias para esta tarefa de migração. Em seguida, escolha **seguinte**.  

10. Confirme as definições e conclua o assistente.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Criar uma tarefa de migração para migrar objetos alterados  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Sobre o **home page** separador a **criar** de grupo, escolha **criar tarefa de migração**.  

4.  Sobre o **gerais** página do Assistente Criar tarefa de migração, configure o seguinte e, em seguida, escolha **próxima**:  

    -   Especifique um nome para a tarefa de migração.  

    -   Na **tipo de tarefa** na lista pendente, selecione **objetos modificados após migração**.  

5.  Na página **Selecionar Objetos** , selecione os tipos de objeto que pretende migrar. Por predefinição, são selecionados todos os objetos disponíveis para cada tipo de objeto que selecionou.  

6.  Sobre o **propriedade do conteúdo** página, atribua a propriedade do conteúdo de cada site de origem listado a um site na hierarquia de destino e, em seguida, escolha **próxima**. Se estiver listado nenhum site de origem, escolha **seguinte**.  

7.  Sobre o **âmbito de segurança** , selecione um ou mais âmbitos de segurança de administração baseada em funções para atribuir aos objetos nesta tarefa de migração e, em seguida, escolha **próxima**.  

8.  Sobre o **rever informações** página, selecione **guardar no ficheiro** para guardar as informações apresentadas para posterior visualização. Quando estiver pronto para continuar, escolha **seguinte**.  

9. Sobre o **definições** página, definir quando a tarefa de migração será executado e escolha as definições adicionais que sejam necessárias para esta tarefa de migração. Ao contrário de outros migração tarefa tipos, esta tarefa de migração tem de substituir os objetos anteriormente migrados na base de dados do System Center Configuration Manager. Selecione **Next**.  

10. Confirme as definições e, em seguida, conclua o assistente.  

###  <a name="BKMK_Modify_Exclusion_List"></a> Modificar a lista de exclusão para migração  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, escolha **migração** para obter acesso à lista de exclusão. Também pode aceder à lista de exclusão a partir dos nós **Hierarquia de Origem** ou **Tarefas de Migração** .  

3.  Sobre o **home page** separador a **migração** de grupo, escolha **Editar lista de exclusão**.  

4.  Na **Editar lista de exclusão** caixa de diálogo caixa, selecione o objeto excluído que pretende remover da lista de exclusão e, em seguida, escolha **remover**.  

5.  Escolher **OK** para guardar as alterações e concluir a edição. Para cancelar as alterações em curso e restaurar todos os objetos que removeu, escolha **Cancelar**e, em seguida, escolha **não**. Este procedimento irá cancelar a remoção dos objetos e fechar a caixa de diálogo **Editar Lista de Exclusão** .  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Partilhar pontos de distribuição da hierarquia de origem  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**, escolha **hierarquia de origem**e, em seguida, selecione o site de origem que pretende configurar.  

3.  Sobre o **home page** separador a **Site de origem** de grupo, escolha **configurar**.  

4.  Sobre o **credenciais do Site de origem** caixa de diálogo, selecione **ativar partilha para o servidor de site de origem do ponto de distribuição**e, em seguida, escolha **OK**.  

5.  Quando estiver concluída, a recolha de dados escolha **fechar**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Alterar o agendamento de uma tarefa de migração  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Escolha a tarefa de migração que pretende alterar. Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

4.  Nas propriedades da tarefa de migração, selecione o **configurações** separador, alterar o tempo de execução da tarefa de migração e, em seguida, escolha **OK**.  

##  <a name="Run_Migration_Jobs"></a> Executar tarefas de migração  
 Utilize o procedimento seguinte para executar uma tarefa de migração que ainda não foi iniciada.  


1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Escolha a tarefa de migração que pretende executar. Sobre o **home page** separador a **tarefa de migração** de grupo, selecione **iniciar**.  

4.  Escolher **Sim** para iniciar a tarefa de migração.  

##  <a name="BKMK_ProcUpgrdSS"></a> Atualizar ou reatribuir um ponto de distribuição partilhado  
 Pode atualizar um ponto de distribuição suportado partilhado a partir de um site de origem do Configuration Manager 2007 (ou reatribuir um ponto de distribuição suportado partilhado a partir de um site de origem do System Center Configuration Manager) para um ponto de distribuição no hierarquia de destino.  

> [!IMPORTANT]  
>  Antes de atualizar um ponto de distribuição de filial do Configuration Manager 2007, tem de desinstalar o software de cliente do Configuration Manager 2007 do computador de ponto de distribuição de filial. Se o software de cliente do Configuration Manager 2007 estiver instalado quando tentar atualizar o ponto de distribuição, a atualização falhar e conteúdo que foi anteriormente implementado para o ponto de distribuição secundário é removido do computador.  

> [!CAUTION]  
>  Quando atualiza ou reatribui um ponto de distribuição partilhado, distribuição ponto de função e o site de sistema computador do sistema são removidos do site de origem e adicionados como um ponto de distribuição para o site na hierarquia de destino que selecionou.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Atualizar ou reatribuir um ponto de distribuição partilhado  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**e, em seguida, escolha **hierarquia de origem**.  

3.  Selecione o site que é proprietário do ponto de distribuição que pretende atualizar, escolha o **pontos de distribuição partilhados** separador e selecione o ponto de distribuição elegível que pretende atualizar ou reatribuir.  

4.  Sobre o **ponto de distribuição** separador a **ponto de distribuição** de grupo, escolha **reatribuir**.  

5.  Especifique as definições no Assistente para reatribuir ponto de distribuição partilhado, como está a instalar um novo ponto de distribuição da hierarquia de destino, acrescentando o seguinte:  

    -   Sobre o **conversão de conteúdo** , reveja as orientações sobre o espaço necessário para converter o conteúdo existente. Em seguida, no **definições de unidade** página do assistente, certifique-se de que a unidade do computador do ponto de distribuição selecionado tem a quantidade necessária de espaço livre em disco.  

6.  Confirme as definições e, em seguida, conclua o assistente.  

##  <a name="Monitor_MIgration"></a> Monitorizar a atividade de migração na área de trabalho Migração  
 Utilize a consola do Configuration Manager para monitorizar a migração.  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Escolha a tarefa de migração que pretende monitorizar.  

4.  Visualize os detalhes e o estado da tarefa de migração selecionada nos separadores **Resumo** e **Objetos na Tarefa**.  

##  <a name="BKMK_MigrateClients"></a> Migrar clientes  
 Após a migração de dados dos clientes entre hierarquias, mas antes de concluir a migração, planeie a migração dos clientes para a hierarquia de destino. A migração de clientes entre hierarquias envolve a desinstalar o software de cliente do Configuration Manager de computadores que estão atribuídos à hierarquia de origem e, em seguida, instalar o software de cliente do Configuration Manager do destino hierarquia. Quando instala o cliente na hierarquia de destino, também atribui o cliente a um site primário nessa hierarquia. Para obter mais informações sobre como migrar clientes, consulte [planear uma estratégia de migração de clientes no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="Complete_Migration"></a> Concluir migração  
 Utilize este procedimento para concluir a migração da hierarquia de origem.  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **migração**e, em seguida, escolha **hierarquia de origem**.  

3.  Para uma hierarquia de origem do Configuration Manager 2007, selecione um site de origem que esteja no nível inferior da hierarquia de origem. Para uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, selecione o site de origem disponível.  

4.  Sobre o **home page** separador o **limpar** de grupo, escolha **parar a recolha de dados**.  

5.  Escolher **Sim** para confirmar a ação.  

6.  Para uma hierarquia de origem do Configuration Manager 2007, antes de continuar para o passo seguinte, repita os passos 3, 4 e 5. Passam por estes passos em cada site na hierarquia, da parte inferior da hierarquia até ao topo. Para uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, avance para o passo seguinte.  

7.  Sobre o **home page** separador o **limpar** de grupo, escolha **limpar dados de migração**.  

8.  Sobre o **limpar dados de migração** caixa de diálogo, da **hierarquia de origem** na lista pendente, selecione o código do site e o servidor de site do site de nível superior da hierarquia de origem e, em seguida, escolha **OK** .  

9. Escolher **Sim** para concluir o processo de migração para a hierarquia de origem.  
