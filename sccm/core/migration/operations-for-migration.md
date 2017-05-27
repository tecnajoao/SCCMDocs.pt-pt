---
title: "Operações de migração | Documentos do Microsoft"
description: Criar e executar tarefas para migrar dados e clientes para o System Center Configuration Manager.
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5df6478362499d87038fa4ed2cb444aa8d5b4b7c
ms.openlocfilehash: fb8a292c4fecbe5744e2cd09bc1442fab11046bc
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>Operações de migração para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para a migração no System Center Configuration Manager, é possível migrar dados e clientes depois de recolher com êxito dados de um site de origem numa hierarquia de origem suportada. Utilize as informações nas secções seguintes para criar e executar tarefas de migração para migrar dados e clientes e, em seguida, concluir o processo de migração.  

-   [Criar e editar tarefas de migração](#Create_Edit_migration_Jobs)  

-   [Executar tarefas de migração](#Run_Migration_Jobs)  

-   [Atualizar ou reatribuir um ponto de distribuição partilhado](#BKMK_ProcUpgrdSS)  

-   [Monitorizar a atividade de migração na área de trabalho Migração](#Monitor_MIgration)  

-   [Migrar clientes](#BKMK_MigrateClients)  

-   [Concluir migração](#Complete_Migration)  

##  <a name="Create_Edit_migration_Jobs"></a> Criar e editar tarefas de migração  
 Utilize os procedimentos seguintes para criar tarefas de migração de dados, editar a lista de exclusão para tarefas de migração baseada em coleções, configurar pontos de distribuição partilhados e editar agendamentos de tarefas de migração.  

> [!NOTE]  
>  O procedimento seguinte para criar uma tarefa de migração que efetua migrações por coleções aplica-se apenas a hierarquias de origem que executem uma versão suportada do Configuration Manager 2007. O tipo de tarefa de migração baseada em coleções não está disponível quando migra de uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Criar uma tarefa de migração para migrar por coleções  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  No **base** separador o **criar** grupo, selecione **criar tarefa de migração**.  

4.  No **geral** página do Assistente Criar tarefa de migração, configure o seguinte procedimento e, em seguida, escolha **OK**:  

    -   Especifique um nome para a tarefa de migração.  

    -   Na lista pendente **Tipo de tarefa** , selecione **Migração de coleção**.  

5.  No **selecionar coleções** página, configure o seguinte procedimento e, em seguida, escolha **seguinte**:  

    -   Selecione as coleções que pretende migrar.  

    -   Se pretender migrar apenas coleções e não os objetos que estão associados essas coleções, desmarque **migrar objetos que estão associados às coleções especificadas**. Se desmarcar esta opção, são migrados nenhuns objetos associados nesta tarefa e pode ignorar os passos 6 e 7.  

6.  No **seleccionar objectos** página, desmarque todos os tipos de objeto ou objetos específicos disponíveis que não pretende migrar. Por predefinição, são selecionados todos os tipos de objetos associados e objetos disponíveis. Escolher **seguinte**.  

7.  No **propriedade do conteúdo** página, atribua a propriedade do conteúdo de cada site de origem listado a um site na hierarquia de destino e, em seguida, selecione **seguinte**.  

8.  No **âmbito de segurança** página, selecione um ou mais âmbitos de segurança de administração baseada em funções para atribuir os objetos a migrar nesta tarefa de migração e, em seguida, selecione **seguinte**.  

9. No **limitação de coleções** página, configure uma coleção da hierarquia de destino para limitar o âmbito de cada coleção listada e, em seguida, selecione **seguinte**. Se não estiver listadas nenhum coleções, selecione **seguinte**.  

10. No **substituição do código do Site** página, atribua um código de site da hierarquia de destino para substituir o código do site do Configuration Manager 2007 para cada coleção listada e, em seguida, selecione **seguinte**. Se não estiver listadas nenhum coleções, selecione **seguinte**.  

11. No **rever informações** página, selecione **guardar no ficheiro** para guardar as informações apresentadas para posterior visualização. Quando estiver pronto para continuar, escolha **seguinte**.  

12. No **definições** página, configure quando será executada a tarefa de migração, selecione quaisquer definições adicionais que sejam necessárias para esta tarefa de migração, e, em seguida, escolha **seguinte**.  

13. Confirme as definições e conclua o assistente.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Criar uma tarefa de migração para migrar por objetos  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  No **base** separador o **criar** grupo, selecione **criar tarefa de migração**.  

4.  No **geral** página do Assistente Criar tarefa de migração, configure o seguinte procedimento e, em seguida, escolha **seguinte**:  

    -   Especifique um nome para a tarefa de migração.  

    -   Na lista pendente **Tipo de tarefa** , selecione **Migração de objeto**.  

5.  Na página **Selecionar Objetos** , selecione os tipos de objeto que pretende migrar. Por predefinição, são selecionados todos os objetos disponíveis para cada tipo de objeto que selecionou.  

6.  No **propriedade do conteúdo** página, atribua a propriedade do conteúdo de cada site de origem listado a um site na hierarquia de destino e, em seguida, selecione **seguinte**. Se não estiver listado nenhum site de origem, escolher **seguinte**.  

7.  No **âmbito de segurança** página, selecione um ou mais âmbitos de segurança de administração baseada em funções para atribuir aos objetos nesta tarefa de migração e, em seguida, selecione **seguinte**.  

8.  No **rever informações** página, selecione **guardar no ficheiro** para guardar as informações apresentadas para posterior visualização. Quando estiver pronto para continuar, escolha **seguinte**.  

9. No **definições** página, configure quando a tarefa de migração será executada e escolher outras definições que sejam necessárias para esta tarefa de migração. Em seguida, escolha **seguinte**.  

10. Confirme as definições e conclua o assistente.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Criar uma tarefa de migração para migrar objetos alterados  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  No **base** separador o **criar** grupo, selecione **criar tarefa de migração**.  

4.  No **geral** página do Assistente Criar tarefa de migração, configure o seguinte procedimento e, em seguida, escolha **seguinte**:  

    -   Especifique um nome para a tarefa de migração.  

    -   No **tipo de tarefa** na lista pendente, selecione **objetos modificados após migração**.  

5.  Na página **Selecionar Objetos** , selecione os tipos de objeto que pretende migrar. Por predefinição, são selecionados todos os objetos disponíveis para cada tipo de objeto que selecionou.  

6.  No **propriedade do conteúdo** página, atribua a propriedade do conteúdo de cada site de origem listado a um site na hierarquia de destino e, em seguida, selecione **seguinte**. Se não estiver listado nenhum site de origem, escolher **seguinte**.  

7.  No **âmbito de segurança** página, selecione um ou mais âmbitos de segurança de administração baseada em funções para atribuir aos objetos nesta tarefa de migração e, em seguida, selecione **seguinte**.  

8.  No **rever informações** página, selecione **guardar no ficheiro** para guardar as informações apresentadas para posterior visualização. Quando estiver pronto para continuar, escolha **seguinte**.  

9. No **definições** página, configure quando a tarefa de migração será executada e escolher outras definições que sejam necessárias para esta tarefa de migração. Ao contrário de outros tarefa tipos de migração, esta tarefa de migração tem de substituir os objetos migrados anteriormente na base de dados do System Center Configuration Manager. Escolher **seguinte**.  

10. Confirme as definições e, em seguida, conclua o assistente.  

###  <a name="BKMK_Modify_Exclusion_List"></a>Modificar a lista de exclusão para migração  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, selecione **migração** para obter acesso à lista de exclusão. Também pode aceder à lista de exclusão a partir dos nós **Hierarquia de Origem** ou **Tarefas de Migração** .  

3.  No **base** separador o **migração** grupo, selecione **Editar lista de exclusão**.  

4.  No **Editar lista de exclusão** diálogo caixa, selecione o objeto excluído que pretende remover da lista de exclusão e, em seguida, selecione **remover**.  

5.  Escolher **OK** para guardar as alterações e concluir a edição. Para cancelar as alterações em curso e restaurar todos os objetos que removeu, escolha **Cancelar**e, em seguida, escolha **não**. Este procedimento irá cancelar a remoção dos objetos e fechar a caixa de diálogo **Editar Lista de Exclusão** .  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Partilhar pontos de distribuição da hierarquia de origem  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**, escolha **hierarquia de origem**e, em seguida, selecione o site de origem que pretende configurar.  

3.  No **base** separador o **Site de origem** grupo, selecione **configurar**.  

4.  No **credenciais do Site de origem** caixa de diálogo, selecione **ativar a partilha para o servidor de site de origem do ponto de distribuição**e, em seguida, escolha **OK**.  

5.  Quando estiver concluído, a recolha de dados escolher **fechar**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Alterar o agendamento de uma tarefa de migração  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Selecione a tarefa de migração que pretende alterar. No **base** separador o **propriedades** grupo, selecione **propriedades**.  

4.  Nas propriedades da tarefa de migração, selecione o **definições** separador, alterar o tempo de execução da tarefa de migração e, em seguida, selecione **OK**.  

##  <a name="Run_Migration_Jobs"></a> Executar tarefas de migração  
 Utilize o procedimento seguinte para executar uma tarefa de migração que ainda não foi iniciada.  


1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Selecione a tarefa de migração que pretende executar. No **base** separador o **tarefa de migração** grupo, selecione **iniciar**.  

4.  Escolher **Sim** para iniciar a tarefa de migração.  

##  <a name="BKMK_ProcUpgrdSS"></a> Atualizar ou reatribuir um ponto de distribuição partilhado  
 Pode atualizar um ponto de distribuição suportado partilhado a partir de um site de origem do Configuration Manager 2007 (ou reatribuir um ponto de distribuição suportado partilhado a partir de um site de origem do System Center Configuration Manager) para ser um ponto de distribuição na hierarquia de destino.  

> [!IMPORTANT]  
>  Antes de atualizar um ponto de distribuição secundário do Configuration Manager 2007, tem de desinstalar o software de cliente do Configuration Manager 2007 a partir do computador do ponto de distribuição secundário. Se o software de cliente do Configuration Manager 2007 estiver instalado quando tentar atualizar o ponto de distribuição, a atualização falhará e o conteúdo que foi anteriormente implementado no ponto de distribuição secundário será removido do computador.  

> [!CAUTION]  
>  Quando atualiza ou reatribui um ponto de distribuição partilhado, o computador ponto de distribuição site system site e função de sistema são removidos do site de origem e adicionados como um ponto de distribuição para o site na hierarquia de destino que selecionar.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Atualizar ou reatribuir um ponto de distribuição partilhado  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**e, em seguida, escolha **hierarquia de origem**.  

3.  Selecione o site que é proprietário do ponto de distribuição que pretende atualizar, escolha o **pontos de distribuição partilhados** separador e selecione o ponto de distribuição elegível que pretende atualizar ou reatribuir.  

4.  No **ponto de distribuição** separador o **ponto de distribuição** grupo, selecione **reatribuir**.  

5.  Especifique as definições no Assistente de ponto de distribuição partilhado de reatribuir como está a instalar um novo ponto de distribuição da hierarquia de destino, acrescentando o seguinte:  

    -   No **conversão de conteúdo** página, reveja as orientações sobre o espaço necessário para converter o conteúdo existente. Em seguida, no **definições de unidade** página do assistente, certifique-se de que a unidade do computador do ponto de distribuição selecionado possui a quantidade necessária de espaço livre em disco.  

6.  Confirme as definições e, em seguida, conclua o assistente.  

##  <a name="Monitor_MIgration"></a> Monitorizar a atividade de migração na área de trabalho Migração  
 Utilize a consola do Configuration Manager para monitorizar a migração.  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**e, em seguida, escolha **tarefas de migração**.  

3.  Selecione a tarefa de migração que pretende monitorizar.  

4.  Visualize os detalhes e o estado da tarefa de migração selecionada nos separadores **Resumo** e **Objetos na Tarefa**.  

##  <a name="BKMK_MigrateClients"></a> Migrar clientes  
 Depois de migrar os dados dos clientes entre hierarquias, mas antes de concluir a migração, planeie a migração dos clientes para a hierarquia de destino. A migração de clientes entre hierarquias envolve a desinstalar o software de cliente do Configuration Manager a partir de computadores que estão atribuídos à hierarquia de origem e, em seguida, instalar o software de cliente do Configuration Manager da hierarquia de destino. Quando instala o cliente na hierarquia de destino, também atribui o cliente a um site primário nessa hierarquia. Para obter mais informações sobre como migrar clientes, consulte [planear uma estratégia de migração do cliente no System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="Complete_Migration"></a>Concluir migração  
 Utilize este procedimento para concluir a migração da hierarquia de origem.  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **migração**e, em seguida, escolha **hierarquia de origem**.  

3.  Para uma hierarquia de origem do Configuration Manager 2007, selecione um site de origem que esteja no nível inferior da hierarquia de origem. Para uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, selecione o site de origem disponível.  

4.  No **base** separador o **limpar** grupo, selecione **parar a recolha de dados**.  

5.  Escolher **Sim** para confirmar a ação.  

6.  Para uma hierarquia de origem do Configuration Manager 2007, antes de continuar para o passo seguinte, repita os passos 3, 4 e 5. Seguir estes passos em cada site na hierarquia, a partir da parte inferior da hierarquia até ao topo. Para uma hierarquia de origem do System Center 2012 Configuration Manager ou System Center Configuration Manager, avance para o passo seguinte.  

7.  No **base** separador o **limpar** grupo, selecione **limpar dados de migração**.  

8.  No **limpar dados de migração** caixa de diálogo, a partir de **hierarquia de origem** na lista pendente, selecione o código de site e o servidor do site do site de nível superior da hierarquia de origem e, em seguida, escolha **OK**.  

9. Escolher **Sim** para concluir o processo de migração da hierarquia de origem.  

