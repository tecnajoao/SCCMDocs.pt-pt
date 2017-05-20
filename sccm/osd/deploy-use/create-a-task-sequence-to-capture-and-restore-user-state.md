---
title: "Criar uma sequência de tarefas para capturar e restaurar o estado do utilizador | Documentos do Microsoft"
description: "Utilização do System Center Configuration Manager as sequências de tarefas para capturar e restaurar os dados de estado do utilizador em cenários de implementação do sistema operativo."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: fdfbdd1acb1190ca7de9cff2b4b7f916d8dc1272
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para capturar e restaurar o estado do utilizador no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar sequências de tarefas do System Center Configuration Manager para capturar e restaurar dados de estado do utilizador em cenários de implementação do sistema operativo em que pretende manter o estado de utilizador do sistema operativo atual. Consoante o tipo de sequência de tarefa que criar, os passos de captura e restauro podem ser adicionados automaticamente como parte da sequência de tarefas. Noutros cenários, poderá ser necessário adicionar os passos de captura e restauro manualmente à sequência de tarefas. Este tópico fornece os passos que tem de adicionar a uma sequência de tarefas existente para capturar e restaurar dados de estado do utilizador.  

##  <a name="BKMK_CaptureRestoreUserState"></a> Como capturar e restaurar dados de estado do utilizador  
 Para capturar e restaurar o estado do utilizador, tem de adicionar os seguintes passos à sequência de tarefas:  

-   **Solicitar armazenamento de Estados**: Este passo só será necessário se armazenar o estado do utilizador no ponto de migração de estado.  

-   **Capturar estado do utilizador**: Este passo captura os dados de estado de utilizador e armazena-os no ponto de migração de estado ou localmente utilizando ligações.  

-   **Restaurar estado do utilizador**: Este passo restaura os dados de estado de utilizador no computador de destino. Permite obter os dados a partir de um ponto de migração de estado do utilizador ou a partir do computador de destino.  

-   **Disponibilizar armazenamento de Estados**: Este passo só será necessário se armazenar o estado do utilizador no ponto de migração de estado. Este passo remove estes dados do ponto de migração de estado.  

 Utilize os procedimentos seguintes para adicionar os passos de sequência de tarefas necessários para capturar e restaurar o estado do utilizador. Para obter mais informações sobre como criar sequências de uma tarefa, consulte o artigo [gerir sequências de tarefas para automatizar tarefas](manage-task-sequences-to-automate-tasks.md).  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>Para adicionar os passos de sequência de tarefas para capturar o estado do utilizador  

1.  Na lista **Sequência de Tarefas** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Se estiver a utilizar um ponto de migração de estado para armazenar o estado do utilizador, adicione o passo **Solicitar Armazenamento de Estados** à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Solicitar Armazenamento de Estados**. Especifique as seguintes propriedades e opções do passo **Solicitar Armazenamento de Estados** e clique em **Aplicar**.  

     No separador **Propriedades** , especifique as seguintes opções:  

    -   Introduza um nome e uma descrição para o passo.  

    -   Clique em **Capturar estado a partir do computador**.  

    -   Na caixa **Número de tentativas** , especifique quantas vezes a sequência de tarefas tentará capturar os dados de estado do utilizador, se ocorrer um erro.  

    -   Na caixa **Intervalo de repetição (em segundos)** , especifique quantos segundos a sequência de tarefas deverá aguardar antes de voltar a tentar capturar os dados.  

    -   Selecione o **se conta de computador não consegue ligar ao armazenamento de Estados, utilize a conta de acesso à rede** caixa de verificação para especificar se pretende utilizar o Configuration Manager [conta de acesso à rede](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account) para estabelecer ligação com o armazenamento de Estados.  

     No separador **Opções** , especifique as seguintes opções:  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

3.  Adicione o passo **Capturar Estado do Utilizador** à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Capturar Estado do Utilizador**. Especifique as seguintes propriedades e opções do passo **Capturar Estado do Utilizador** e clique em **OK**.  

    > [!IMPORTANT]  
    >  Ao adicionar este passo à sequência de tarefas, defina também a variável da sequência de tarefas **OSDStateStorePath** para especificar onde serão armazenados os dados de estado do utilizador. Se armazenar o estado do utilizador localmente, não especifique uma pasta raiz, pois isso poderá fazer a sequência de tarefas falhar. Ao armazenar os dados do utilizador localmente, utilize sempre uma pasta ou subpasta. Para obter informações sobre esta variável, consulte o artigo [capturar variáveis de ação de sequência do utilizador Estado tarefas](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState).  

     No separador **Propriedades** , especifique as seguintes opções:  

    -   Introduza um nome e uma descrição para o passo.  

    -   Especifique o pacote que contém o ficheiro de origem USMT utilizado para capturar os dados de estado do utilizador.  

    -   Especifique os perfis de utilizador a capturar:  

        -   Clique em **Capturar todos os perfis de utilizador com opções padrão** para capturar todos os perfis de utilizador.  

        -   Clique em **Personalizar captura de perfil do utilizador** para especificar os perfis de utilizador individuais a capturar.  

    -   Selecione **Ativar registo verboso** para especificar a quantidade de informações a escrever nos ficheiros de registo, se ocorrer um erro.  

    -   Selecione **Ignorar ficheiros que utilizam o Sistema de Encriptação de Ficheiros (EFS)**.  

    -   Selecione **Copiar utilizando o acesso do sistema de ficheiros** para especificar as seguintes definições:  

        -   **Continuar se não for possível capturar alguns ficheiros**: Esta definição permite que o passo de sequência de tarefas continuar o processo de migração mesmo se não for possível capturar alguns ficheiros. Se desativar esta opção e não for possível capturar um ficheiro, o passo da sequência de tarefas falhará. Por predefinição, esta opção encontra-se ativada.  

        -   **Capturar localmente ao utilizar ligações em vez de copiar ficheiros**: Esta definição permite-lhe utilizar a funcionalidade de migração de disco rígido de ligação que está disponível no USMT 4.0. Esta definição é ignorada se utilizar versões do USMT anteriores ao USMT 4.0.  

        -   **Capturar no modo offline (apenas no Windows PE)**: Esta definição permite-lhe capturar o estado do Windows PE, sem arrancar o sistema operativo existente. Esta definição é ignorada se utilizar versões do USMT anteriores ao USMT 4.0.  

    -   Selecione **Capturar utilizando o Serviço Sombra de Cópia de Volume (VSS)**. Esta definição é ignorada se utilizar versões do USMT anteriores ao USMT 4.0.  

     No separador **Opções** , especifique as seguintes opções:  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

4.  Se estiver a utilizar um ponto de migração de estado para armazenar o estado do utilizador, adicione o [disponibilizar armazenamento de Estados](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) passo à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Disponibilizar Armazenamento de Estados**. Especifique as seguintes propriedades e opções do passo **Disponibilizar Armazenamento de Estados** e clique em **OK**.  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas executada antes do passo **Disponibilizar Armazenamento de Estados** deve ser bem-sucedida para iniciar o passo **Disponibilizar Armazenamento de Estados** .  

     No separador **Propriedades** , introduza um nome e uma descrição para o passo.  

     No separador **Opções** , especifique as seguintes opções.  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

 Implemente esta sequência de tarefas para capturar o estado do utilizador num computador de destino. Para obter informações sobre como implementar sequências de tarefas, consulte o artigo [implementar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>Para adicionar os passos de sequência de tarefas para restaurar o estado do utilizador  

1.  Na lista **Sequência de Tarefas** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Adicionar o [restaurar estado do utilizador](../understand/task-sequence-steps.md#BKMK_RestoreUserState) passo à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Restaurar Estado do Utilizador**. Este passo estabelece uma ligação ao ponto de migração de estado. Especifique as seguintes propriedades e opções do passo **Restaurar Estado do Utilizador** e clique em **OK**.  

     No separador **Propriedades** , especifique as seguintes propriedades:  

    -   Introduza um nome e uma descrição para o passo.  

    -   Especifique o pacote que contém a USMT para restaurar os dados de estado do utilizador.  

    -   Especifique os perfis de utilizador a restaurar:  

        -   Clique em **Restaurar todos os perfis de utilizador capturados com opções padrão** para restaurar todos os perfis de utilizador.  

        -   Clique em **Personalizar captura de perfil do utilizador** para restaurar os perfis de utilizador individuais.  

    -   Selecione **Restaurar perfis de utilizador do computador local** para fornecer uma palavra-passe nova para aos perfis restaurados. Não é possível migrar palavras-passe para perfis locais.  

        > [!NOTE]  
        >  Quando tiver contas de utilizador local e utilizar o [capturar estado do utilizador](../understand/task-sequence-steps.md#BKMK_CaptureUserState) passo e selecione **capturar todos os perfis de utilizador com opções padrão**, tem de selecionar o **restaurar perfis de utilizador do computador local** definição o [restaurar estado do utilizador](../understand/task-sequence-steps.md#BKMK_RestoreUserState) passo ou a sequência de tarefas falhará.  

    -   Selecione **Continuar se não for possível restaurar alguns ficheiros** se pretender que o passo **Restaurar Estado do Utilizador** continue caso não seja possível restaurar um ficheiro.  

         Se armazenar o estado do utilizador utilizando ligações locais e a restauração não for bem-sucedida, o utilizador administrativo pode eliminar manualmente as ligações fixas criadas para armazenar os dados ou a sequência de tarefas pode executar a ferramenta USMTUtils. Se utilizar o USMTUtils para eliminar a ligação fixa, adicione um [reiniciar o computador](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) passo após a execução do USMTUtils.  

    -   Selecione **Ativar registo verboso** para especificar a quantidade de informações a escrever nos ficheiros de registo, se ocorrer um erro.  

     No separador **Opções** , especifique as seguintes opções:  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

3.  Se estiver a utilizar um ponto de migração de estado para armazenar o estado do utilizador, adicione o [disponibilizar armazenamento de Estados](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) passo à sequência de tarefas. Na caixa de diálogo **Editor de Sequência de Tarefas** , clique em **Adicionar**, aponte para **Estado de Utilizador**e clique em **Disponibilizar Armazenamento de Estados**. Especifique as seguintes propriedades e opções do passo **Disponibilizar Armazenamento de Estados** e clique em **OK**.  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas executada antes do passo **Disponibilizar Armazenamento de Estados** deve ser bem-sucedida para iniciar o passo **Disponibilizar Armazenamento de Estados** .  

     No separador **Propriedades** , introduza um nome e uma descrição para o passo.  

     No separador **Opções** , especifique as seguintes opções.  

    -   Selecione a caixa de verificação **Continuar com o erro** se pretender que a sequência de tarefas continue para o passo seguinte caso este passo falhe.  

    -   Especifique as condições que devem ser satisfeitas antes de continuar com a sequência de tarefas em caso de erro.  

 Implemente esta sequência de tarefas para restaurar o estado do utilizador num computador de destino. Para obter informações sobre como implementar sequências de tarefas, consulte o artigo [implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

## <a name="next-steps"></a>Passos seguintes
[Monitorizar a implementação de sequência de tarefas](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)

