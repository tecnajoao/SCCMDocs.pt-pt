---
title: Capturar e restaurar estado do utilizador
titleSuffix: Configuration Manager
description: Utilize o Gestor de configuração de sequências de tarefas para capturar e restaurar o utilizador de estado dados nos cenários de implementação do sistema operacional.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0077cd6a906da59a06f4cf619b74ddc0af947cea
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133923"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Criar uma sequência de tarefas para capturar e restaurar estado do utilizador no Configuration Manager

 *Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Utilize o Gestor de configuração de sequências de tarefas para capturar e restaurar o utilizador de estado dados nos cenários de implementação do sistema operacional. Nestes cenários, que pretenda manter o estado do utilizador do sistema operacional atual. Consoante o tipo de sequência de tarefa que criar, os passos de captura e restauro podem ser adicionados automaticamente como parte da sequência de tarefas. Noutros cenários, poderá ser necessário adicionar os passos de captura e restauro manualmente à sequência de tarefas. Este artigo fornece os passos que tem de adicionar um existente já sequência de tarefas para capturar e restaurar dados de estado do utilizador.  



## <a name="task-sequence-steps"></a>Passos de sequência de tarefas  

 Para capturar e restaurar o estado do utilizador, adicione os seguintes passos à sequência de tarefas:  

 - [Store de estado do pedido](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore): Se armazenar o estado do utilizador no ponto de migração de estado, terá este passo.  

- [Capturar estado do utilizador](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState): Este passo captura os dados de estado do utilizador. Em seguida, armazena os dados no ponto de migração de estado ou no disco local com links.  

- [Restaurar estado do utilizador](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState): Este passo restaura os dados de estado de utilizador no computador de destino. Ele pode recuperar os dados de um ponto de migração de estado ou se hardlinked no disco local.  

- [Versão Estado Store](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore): Se armazenar o estado do utilizador no ponto de migração de estado, terá este passo. Este passo remove os dados do ponto de migração de estado.  


 Utilize os procedimentos seguintes para adicionar os passos de sequência de tarefas necessários para capturar e restaurar o estado do utilizador. Para obter mais informações sobre como criar uma sequência de tarefas, consulte [gerir sequências de tarefas para automatizar tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks).  



## <a name="capture-the-user-state"></a>Capturar o estado do utilizador  

 Para adicionar passos de sequência de tarefas para capturar o estado do utilizador, utilize os seguintes passos:

1.  Na lista **Sequência de Tarefas** , selecione uma sequência de tarefas e clique em **Editar**.  

2.  Se estiver a utilizar um ponto de migração de estado para armazenar o estado do utilizador, adicione a **Store de estado do pedido** passo à sequência de tarefas. Na **Editor de sequência de tarefas**, clique em **Add**. Aponte para **estado do utilizador**e, em seguida, clique em **Store de estado do pedido**. Configurar as propriedades e opções para este passo e, em seguida, clique em **aplicar**. Para obter mais informações sobre as definições disponíveis, consulte [Store de estado do pedido](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore).  

3.  Adicione o passo **Capturar Estado do Utilizador** à sequência de tarefas. Na **Editor de sequência de tarefas**, clique em **Add**. Aponte para **estado do utilizador**e, em seguida, clique em **capturar estado do utilizador**. Configurar as propriedades e opções para este passo e, em seguida, clique em **aplicar**. Para obter mais informações sobre as definições disponíveis, consulte [capturar estado do utilizador](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Ao adicionar este passo à sequência de tarefas, defina também a **OSDStateStorePath** variável de sequência de tarefas para especificar onde pretende armazenar os dados de estado do utilizador. Se armazenar o estado do utilizador localmente, não especifique uma pasta de raiz, que pode fazer com que a sequência de tarefas falhe. Ao armazenar os dados do utilizador localmente, utilize sempre uma pasta ou subpasta. Para obter mais informações sobre esta variável, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath).  

4.  Se estiver a utilizar um ponto de migração de estado, adicione a **Store de estado da versão** passo à sequência de tarefas. Na **Editor de sequência de tarefas**, clique em **Add**. Aponte para **estado do utilizador**e, em seguida, clique em **Store de estado da versão**. Configurar as propriedades e opções para este passo e, em seguida, clique em **aplicar**. Para obter mais informações sobre as definições disponíveis, consulte [Store de estado da versão](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  A ação de sequência de tarefas executada antes do **Store de estado da versão** passo deve ser bem-sucedida a **Store de estado da versão** passo é iniciado.  


 Implemente esta sequência de tarefas para capturar o estado do utilizador num computador de destino. Para obter informações sobre como implementar sequências de tarefas, consulte [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  



## <a name="restore-the-user-state"></a>Restaurar o estado do utilizador  

 Para adicionar passos de sequência de tarefas para restaurar o estado do utilizador, utilize os seguintes passos:

1. Na lista **Sequência de Tarefas** , selecione uma sequência de tarefas e clique em **Editar**.  

2. Adicione o passo **Restore User State** à sequência de tarefas. Na **Editor de sequência de tarefas**, clique em **Add**. Aponte para **estado do utilizador**e, em seguida, clique em **restaurar estado do utilizador**. Este passo estabelece uma ligação ao ponto de migração de estado, se necessário. Configurar as propriedades e opções para este passo e, em seguida, clique em **aplicar**. Para obter mais informações sobre as definições disponíveis, consulte [restaurar estado do utilizador](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState).  

   > [!Important]  
   >  Quando utiliza a [capturar estado do utilizador](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState) passo com a opção de **capturar todos os perfis de utilizador com opções padrão**, tem de selecionar o **restaurar perfis de utilizador do computador local** definição do **restaurar estado do utilizador** passo. Caso contrário, a sequência de tarefas falhará.  

   > [!Note]  
   > Se armazenar o estado do utilizador através da utilização de links locais e o restauro não for bem-sucedida, pode eliminar manualmente os links que foram criadas para armazenar os dados. A sequência de tarefas pode executar a ferramenta USMTUtils para automatizar esta ação com um [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo. Se utilizar o USMTUtils para eliminar o link físico, adicione uma [reiniciar o computador](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) passo após a execução do USMTUtils.  

3. Se estiver a utilizar um ponto de migração de estado para armazenar o estado do utilizador, adicione a **Store de estado da versão** passo à sequência de tarefas. Na **Editor de sequência de tarefas**, clique em **Add**. Aponte para **estado do utilizador**e, em seguida, clique em **Store de estado da versão**. Configurar as propriedades e opções para este passo e, em seguida, clique em **aplicar**. Para obter mais informações sobre as definições disponíveis, consulte [Store de estado da versão](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  A ação de sequência de tarefas executada antes do **Store de estado da versão** passo deve ser bem-sucedida a **Store de estado da versão** passo é iniciado.  


 Implemente esta sequência de tarefas para restaurar o estado do utilizador num computador de destino. Para mais informações sobre a implementação de sequências de tarefas, consulte [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  



## <a name="next-steps"></a>Passos seguintes

[Monitorizar a implementação da sequência de tarefas](/sccm/osd/deploy-use/monitor-operating-system-deployments#BKMK_TSDeployStatus)
