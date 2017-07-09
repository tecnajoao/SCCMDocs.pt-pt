---
title: "Criar uma sequência de tarefas para capturar e restaurar o estado do usuário | Microsoft Docs"
description: "Sequências de tarefas Use o System Center Configuration Manager para capturar e restaurar os dados de estado do usuário em cenários de implantação de sistema operacional."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: 7
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 4b3668094d576b1b8710f08b384aa2f7c5eb0cca
ms.contentlocale: pt-pt
ms.lasthandoff: 06/08/2017


---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para capturar e restaurar o estado do usuário no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Você pode usar sequências de tarefas do System Center Configuration Manager para capturar e restaurar os dados de estado do usuário em cenários de implantação do sistema operacional onde você deseja manter o estado do usuário do sistema operacional atual. Consoante o tipo de sequência de tarefa que criar, os passos de captura e restauro podem ser adicionados automaticamente como parte da sequência de tarefas. Noutros cenários, poderá ser necessário adicionar os passos de captura e restauro manualmente à sequência de tarefas. Este tópico fornece os passos que tem de adicionar a uma sequência de tarefas existente para capturar e restaurar dados de estado do utilizador.  

##  <a name="BKMK_CaptureRestoreUserState"></a> Como capturar e restaurar dados de estado do utilizador  
 Para capturar e restaurar o estado do utilizador, tem de adicionar os seguintes passos à sequência de tarefas:  

-   **Solicitar armazenamento de estado**: Essa etapa é necessária somente se você armazenar o estado do usuário no ponto de migração de estado.  

-   **Capturar estado do usuário**: Essa etapa captura os dados de estado do usuário e os armazena no ponto de migração de estado ou localmente usando links.  

-   **Restaurar estado do usuário**: Essa etapa restaura os dados de estado do usuário no computador de destino. Permite obter os dados a partir de um ponto de migração de estado do utilizador ou a partir do computador de destino.  

-   **Liberar armazenamento de estado**: Essa etapa é necessária somente se você armazenar o estado do usuário no ponto de migração de estado. Este passo remove estes dados do ponto de migração de estado.  

 Utilize os procedimentos seguintes para adicionar os passos de sequência de tarefas necessários para capturar e restaurar o estado do utilizador. Para obter mais informações sobre como criar sequências de tarefas, consulte [gerenciar sequências de tarefas para automatizar tarefas](manage-task-sequences-to-automate-tasks.md).  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>Para adicionar os passos de sequência de tarefas para capturar o estado do utilizador  

1.  Na lista **Sequência de Tarefas** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Se estiver a utilizar um ponto de migração de estado para armazenar o estado do utilizador, adicione o passo **Solicitar Armazenamento de Estados** à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Solicitar Armazenamento de Estados**. Especifique as seguintes propriedades e opções do passo **Solicitar Armazenamento de Estados** e clique em **Aplicar**.  

     No separador **Propriedades** , especifique as seguintes opções:  

    -   Introduza um nome e uma descrição para o passo.  

    -   Clique em **Capturar estado a partir do computador**.  

    -   Na caixa **Número de tentativas** , especifique quantas vezes a sequência de tarefas tentará capturar os dados de estado do utilizador, se ocorrer um erro.  

    -   Na caixa **Intervalo de repetição (em segundos)** , especifique quantos segundos a sequência de tarefas deverá aguardar antes de voltar a tentar capturar os dados.  

    -   Selecione o **se a conta de computador não conseguir se conectar ao armazenamento de estado, use a conta de acesso à rede** caixa de seleção para especificar se deseja usar o Configuration Manager [Network Access Account](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account) para se conectar ao armazenamento de estado.  

     No separador **Opções** , especifique as seguintes opções:  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

3.  Adicione o passo **Capturar Estado do Utilizador** à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Capturar Estado do Utilizador**. Especifique as seguintes propriedades e opções do passo **Capturar Estado do Utilizador** e clique em **OK**.  

    > [!IMPORTANT]  
    >  Ao adicionar este passo à sequência de tarefas, defina também a variável da sequência de tarefas **OSDStateStorePath** para especificar onde serão armazenados os dados de estado do utilizador. Se armazenar o estado do utilizador localmente, não especifique uma pasta raiz, pois isso poderá fazer a sequência de tarefas falhar. Ao armazenar os dados do utilizador localmente, utilize sempre uma pasta ou subpasta. Para obter informações sobre essa variável, consulte [capturar usuário estado Task Sequence Action Variables](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState).  

     No separador **Propriedades** , especifique as seguintes opções:  

    -   Introduza um nome e uma descrição para o passo.  

    -   Especifique o pacote que contém o ficheiro de origem USMT utilizado para capturar os dados de estado do utilizador.  

    -   Especifique os perfis de utilizador a capturar:  

        -   Clique em **Capturar todos os perfis de utilizador com opções padrão** para capturar todos os perfis de utilizador.  

        -   Clique em **Personalizar captura de perfil do utilizador** para especificar os perfis de utilizador individuais a capturar. Selecione o arquivo de configuração (MigUser, Migsys ou Migapp. xml) que contém as informações de perfil de usuário. Você não pode usar o arquivo de configuração de config.xml aqui, mas você pode adicioná-lo manualmente para a linha de comando da USMT usando as variáveis OSDMigrageAdditionalCaptureOptions e OSDMigrateAdditionalRestoreOptions.

    -   Selecione **Ativar registo verboso** para especificar a quantidade de informações a escrever nos ficheiros de registo, se ocorrer um erro.  

    -   Selecione **Ignorar ficheiros que utilizam o Sistema de Encriptação de Ficheiros (EFS)**.  

    -   Selecione **Copiar utilizando o acesso do sistema de ficheiros** para especificar as seguintes definições:  

        -   **Continuar se alguns arquivos não podem ser capturados**: Essa configuração permite que a etapa de sequência de tarefas continuar o processo de migração mesmo que alguns arquivos não puderem ser capturados. Se desativar esta opção e não for possível capturar um ficheiro, o passo da sequência de tarefas falhará. Por predefinição, esta opção encontra-se ativada.  

        -   **Capturar localmente usando links em vez de copiando os arquivos**: Essa configuração permite que você use o recurso de migração de link físico que está disponível no USMT 4.0. Esta definição é ignorada se utilizar versões do USMT anteriores ao USMT 4.0.  

        -   **Capturar em modo offline (somente Windows PE)**: Essa configuração permite que você capture o estado de uso do Windows PE sem inicializar o sistema operacional existente. Esta definição é ignorada se utilizar versões do USMT anteriores ao USMT 4.0.  

    -   Selecione **Capturar utilizando o Serviço Sombra de Cópia de Volume (VSS)**. Esta definição é ignorada se utilizar versões do USMT anteriores ao USMT 4.0.  

     No separador **Opções** , especifique as seguintes opções:  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

4.  Se você estiver usando um ponto de migração de estado para armazenar o estado do usuário, adicione o [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) etapa à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Disponibilizar Armazenamento de Estados**. Especifique as seguintes propriedades e opções do passo **Disponibilizar Armazenamento de Estados** e clique em **OK**.  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas executada antes do passo **Disponibilizar Armazenamento de Estados** deve ser bem-sucedida para iniciar o passo **Disponibilizar Armazenamento de Estados** .  

     No separador **Propriedades** , introduza um nome e uma descrição para o passo.  

     No separador **Opções** , especifique as seguintes opções.  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

 Implemente esta sequência de tarefas para capturar o estado do utilizador num computador de destino. Para obter informações sobre como implantar sequências de tarefas, consulte [implantar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>Para adicionar os passos de sequência de tarefas para restaurar o estado do utilizador  

1.  Na lista **Sequência de Tarefas** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Adicionar o [restaurar estado do usuário](../understand/task-sequence-steps.md#BKMK_RestoreUserState) etapa à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Restaurar Estado do Utilizador**. Este passo estabelece uma ligação ao ponto de migração de estado. Especifique as seguintes propriedades e opções do passo **Restaurar Estado do Utilizador** e clique em **OK**.  

     No separador **Propriedades** , especifique as seguintes propriedades:  

    -   Introduza um nome e uma descrição para o passo.  

    -   Especifique o pacote que contém a USMT para restaurar os dados de estado do utilizador.  

    -   Especifique os perfis de utilizador a restaurar:  

        -   Clique em **Restaurar todos os perfis de utilizador capturados com opções padrão** para restaurar todos os perfis de utilizador.  

        -   Clique em **personalizar restauração do perfil do usuário** para restaurar perfis de usuário individuais. Selecione o arquivo de configuração (MigUser, Migsys ou Migapp. xml) que contém as informações de perfil de usuário. Você não pode usar o arquivo de configuração de config.xml aqui, mas você pode adicioná-lo manualmente para a linha de comando da USMT usando as variáveis OSDMigrageAdditionalCaptureOptions e OSDMigrateAdditionalRestoreOptions.

    -   Selecione **Restaurar perfis de utilizador do computador local** para fornecer uma palavra-passe nova para aos perfis restaurados. Não é possível migrar palavras-passe para perfis locais.  

        > [!NOTE]  
        >  Quando você tiver contas de usuário local, e você usar o [capturar estado do usuário](../understand/task-sequence-steps.md#BKMK_CaptureUserState) etapa e selecione **capturar todos os perfis de usuário com opções padrão**, você deve selecionar o **restaurar perfis de usuário do computador local** definindo no [restaurar estado do usuário](../understand/task-sequence-steps.md#BKMK_RestoreUserState) etapa ou a sequência de tarefas irá falhar.  

    -   Selecione **Continuar se não for possível restaurar alguns ficheiros** se pretender que o passo **Restaurar Estado do Utilizador** continue caso não seja possível restaurar um ficheiro.  

         Se armazenar o estado do utilizador utilizando ligações locais e a restauração não for bem-sucedida, o utilizador administrativo pode eliminar manualmente as ligações fixas criadas para armazenar os dados ou a sequência de tarefas pode executar a ferramenta USMTUtils. Se você usar o USMTUtils para excluir o link físico, adicione um [Reiniciar computador](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) etapa depois de executar USMTUtils.  

    -   Selecione **Ativar registo verboso** para especificar a quantidade de informações a escrever nos ficheiros de registo, se ocorrer um erro.  

     No separador **Opções** , especifique as seguintes opções:  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

3.  Se você estiver usando um ponto de migração de estado para armazenar o estado do usuário, adicione o [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) etapa à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Disponibilizar Armazenamento de Estados**. Especifique as seguintes propriedades e opções do passo **Disponibilizar Armazenamento de Estados** e clique em **OK**.  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas executada antes do passo **Disponibilizar Armazenamento de Estados** deve ser bem-sucedida para iniciar o passo **Disponibilizar Armazenamento de Estados** .  

     No separador **Propriedades** , introduza um nome e uma descrição para o passo.  

     No separador **Opções** , especifique as seguintes opções.  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

 Implemente esta sequência de tarefas para restaurar o estado do utilizador num computador de destino. Para obter informações sobre como implantar sequências de tarefas, consulte [implantar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

## <a name="next-steps"></a>Passos seguintes
[Monitorar a implantação de sequência de tarefas](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)

