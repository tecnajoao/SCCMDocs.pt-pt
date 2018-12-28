---
title: 'Gerir o estado do utilizador '
titleSuffix: Configuration Manager
description: System Center Configuration Manager utiliza a ferramenta de migração de perfil do usuário para capturar e restaurar dados de perfil do usuário nos cenários de implementação do sistema operativo.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 676131965165acda9633e7fbceaee7f25d823efe
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420384"
---
# <a name="manage-user-state-in-system-center-configuration-manager"></a>Gerir o estado do utilizador no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar sequências de tarefas do System Center Configuration Manager para capturar e restaurar dados de perfil do usuário nos cenários de implementação do sistema operativo em que pretende manter o estado do utilizador do sistema operativo atual. Por exemplo:  

- Implementações em que pretenda capturar o estado do utilizador de um computador para o restaurar noutro.  

- Implementações de atualizações em que pretenda capturar e restaurar o estado do utilizador no mesmo computador.  

  Configuration Manager utiliza o utilizador State Migration Tool (USMT) 10.0 para gerir a migração de dados de estado de utilizador de um computador de origem para um computador de destino após a conclusão da instalação do sistema operativo. Para obter mais informações sobre cenários comuns de migração para a USMT 10.0, consulte  [Cenários Comuns de Migração](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

  Utilize as secções seguintes para ajudar a capturar e restaurar dados de utilizador.


##  <a name="BKMK_StoringUserData"></a> Armazenar dados de estado do utilizador  
 Quando capturar o estado do utilizador, pode armazenar os dados de estado do utilizador no computador de destino ou num ponto de migração de estado. Para armazenar o estado do utilizador num ponto de migração de estado do utilizador, tem de utilizar um servidor do sistema de sites do Configuration Manager que aloja a função de sistema de sites de ponto de migração de estado. Para armazenar o estado do utilizador no computador de destino, terá de configurar a sequência de tarefas para armazenar os dados localmente utilizando ligações.  

> [!NOTE]  
>  As ligações utilizadas para armazenar localmente o estado do utilizador são referidas como ligações fixas. As ligações fixas constituem uma funcionalidade da USMT 10.0 que verifica a existência de ficheiros e definições de utilizador no computador, criando um diretório de ligações fixas para esses ficheiros. As ligações fixas são então utilizadas para restaurar os dados do utilizador após a implementação do novo sistema operativo.  

> [!IMPORTANT]  
>  Não é possível utilizar em simultâneo um ponto de migração de estado e ligações fixas para armazenar os dados de estado do utilizador.  

 Quando as informações de estado de utilizador são capturadas, podem ser armazenadas de uma das seguintes formas:  

-   Pode armazenar os dados de estado de utilizador remotamente através da configuração de um ponto de migração de estado. A sequência de tarefas **Captura** envia os dados para o ponto de migração de estado. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas **Restauro** obtém os dados e restaura o estado de utilizador no computador de destino.  

-   Pode armazenar os dados de estado de utilizador localmente numa localização específica. Neste cenário, a sequência de tarefas **Captura** copia os dados de utilizador para uma localização específica no computador de destino. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas **Restauro** obtém os dados de utilizador a partir dessa localização.  

-   Pode especificar ligações fixas que podem ser utilizadas para restaurar os dados de utilizador na localização original. Neste cenário, os dados de estado de utilizador permanecem na unidade quando o sistema operativo anterior é removido. Em seguida, depois de o novo sistema operativo ser implementado, a sequência de tarefas **Restauro** utiliza as ligações fixas para restaurar os dados de estado do utilizador para a localização original.  

###  <a name="BKMK_UserDataSMP"></a> Armazenar dados de utilizador num ponto de migração de estado  
 Para armazenar os dados de estado do utilizador num ponto de migração de estado, terá de efetuar o seguinte:  

1.  [Configure a state migration point](#BKMK_StateMigrationPoint) para armazenar os dados de estado do utilizador.  

2.  [Create a computer association](#BKMK_ComputerAssociation) entre o computador de origem e o computador de destino. Terá de criar esta associação antes de capturar o estado do utilizador no computador de origem.  

3.  [Criar uma sequência de tarefas para capturar e restaurar estado do utilizador no System Center Configuration Manager](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Especificamente, tem de adicionar os seguintes passos de sequência de tarefas para capturar os dados de utilizador a partir de um computador, armazenar os dados de utilizador num ponto de migração de estado e restaurar os dados de utilizador para um computador:  

    -   [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore) para solicitar acesso a um ponto de migração de estado ao capturar o estado de um computador ou ao restaurar o estado para um computador.  

    -   [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) para capturar e armazenar os dados de estado do utilizador no ponto de migração de estado.  

    -   [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) para restaurar o estado do utilizador no computador de destino ao obter os dados a partir de um ponto de migração de estado do utilizador.  

    -   [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) para informar o ponto de migração de estado de que a ação de captura ou de restauro está concluída.  

###  <a name="BKMK_UserDataDestination"></a> Armazenar dados do utilizador localmente  
 Para armazenar os dados de estado do utilizador localmente, terá de efetuar o seguinte:  

-   [Criar uma sequência de tarefas para capturar e restaurar estado do utilizador](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Especificamente, tem de adicionar os seguintes passos de sequência de tarefas para capturar os dados de utilizador a partir de um computador e restaurar os dados de utilizador para um computador utilizando ligações fixas.  

    -   [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) para capturar e armazenar os dados de estado do utilizador para uma pasta local utilizando ligações fixas.  

    -   [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) para restaurar o estado do utilizador no computador de destino ao obter os dados utilizando ligações fixas.  

        > [!NOTE]  
        >  Os dados de estado do utilizador a que as ligações fixas fazem referência permanecem no computador depois de a sequência de tarefas remover o sistema operativo anterior. Estes dados serão utilizados para restaurar o estado do utilizador aquando da implementação do novo sistema operativo.  

##  <a name="BKMK_StateMigrationPoint"></a> Configure a state migration point  
 O ponto de migração de estado armazena os dados de estado do utilizador que são capturados num computador e, em seguida, restaurados noutro. No entanto, quando captura definições de utilizador para a implementação de um sistema operativo no mesmo computador, como uma implementação em que atualiza o sistema operativo no computador de destino, pode armazenar os dados no mesmo computador através de ligações fixas ou num ponto de migração de estado. Algumas implementações de computadores, quando cria o arquivo de estado, o Configuration Manager automaticamente cria uma associação entre o armazenamento de Estados e o computador de destino. Poderá utilizar os seguintes métodos para configurar um ponto de migração de estado para armazenar os dados de estado do utilizador:  

- Utilize o **Assistente para Criar Servidor do Sistema de Sites** para criar um novo servidor do sistema de sites para o ponto de migração de estado.  

- Utilize o **Assistente para Adicionar Funções ao Sistema de Sites** para adicionar um ponto de migração de estado a um servidor existente.  

  Ao utilizar estes assistentes, será solicitado que forneça as seguintes informações sobre o ponto de migração de estado:  

- As pastas em que os dados de estado do utilizador serão armazenados.  

- O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

- O mínimo de espaço livre para que o ponto de migração de estado armazene os dados de estado do utilizador.  

- A política de eliminação da função. Poderá especificar que os dados de estado do utilizador sejam eliminados imediatamente ou um número de dias especificado após serem restaurados num computador.  

- Se o ponto de migração de estado responde apenas a pedidos de restauro dos dados de estado do utilizador. Se ativar esta opção, não será possível utilizar o ponto de migração de estado para armazenar os dados de estado do utilizador.  

  Para obter mais informações sobre o ponto de migração de estado e os passos para configurá-lo, consulte [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_ComputerAssociation"></a> Create a computer association  
 Crie uma associação de computadores para definir uma relação entre um computador de origem e um computador de destino quando instala um sistema operativo em novo hardware e pretende capturar e restaurar as definições de dados do utilizador. O computador de origem é um computador existente pelo Configuration Manager. Ao implementar o novo sistema operativo no computador de destino, o computador de origem contém o estado de utilizador que é migrado para o computador de destino.  

> [!NOTE]  
>  Não é suportada para criar uma associação de computadores entre computadores localizados num site principal do Configuration Manager com computadores localizados num site subordinado. As associações de computadores são específicas a um site e não são replicados.  

#### <a name="to-create-a-computer-association"></a>Para criar uma associação de computadores  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Migração de Estado de Utilizador**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Associação de Computadores**.  

4.  No separador **Associação de Computadores** da caixa de diálogo **Propriedades da Associação de Computadores** , especifique o computador de origem que possui o estado de utilizador a capturar e o computador de destino em que pretende restaurar os dados de estado do utilizador.  

5.  No separador **Contas de Utilizador** , especifique as contas de utilizador a migrar para o computador de destino. Especifique uma das seguintes definições:  

    -   **Capturar e restaurar todas as contas de utilizador**: Esta definição captura e restaura todas as contas de utilizador. Utilize esta definição para criar várias associações ao mesmo computador de origem.  

    -   **Capturar todas as contas de utilizador e restaurar contas especificadas**: Esta definição captura todas as contas de utilizador no computador de origem e restaura apenas as contas que especificar no computador de destino. Além disso, poderá utilizar esta definição quando pretender criar várias associações ao mesmo computador de origem.  

    -   **Capturar e restaurar contas de utilizador especificado**: Esta definição captura e restaura apenas as contas que especificar. Se selecionar esta definição, não será possível criar várias associações ao mesmo computador de origem.  

##  <a name="BKMK_MigrationFails"></a> Restaurar os dados de estado do utilizador quando a implementação do sistema operativo falha  
 Se a implementação do sistema operativo falhar, utilize a funcionalidade LoadState da USMT 10.0 para obter os dados de estado do utilizador que foram capturados durante o processo de implementação. Isto inclui dados armazenados num ponto de migração de estado ou dados que são guardados localmente no computador de destino. Para obter mais informações sobre esta funcionalidade USMT, consulte [LoadState Syntax (Sintaxe LoadState)](https://technet.microsoft.com/library/mt299188\(v=vs.85\).aspx).  
