---
title: "Criar uma sequência de tarefas para atualizar um sistema operativo | Documentos do Microsoft"
description: "Sequências de tarefas no System Center Configuration Manager podem atualizar automaticamente um sistema operativo a partir do Windows 7 ou posterior para Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d7b13f3dea5a3ae413ca6b8150ec24e1632a4d4d
ms.openlocfilehash: e63b639836bc38a030a051e80db4b057ab75a0b0
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para atualizar um sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize sequências de tarefas no System Center Configuration Manager para atualizar automaticamente um sistema operativo a partir do Windows 7 ou posterior para Windows 10 num computador de destino. Criar uma sequência de tarefas que faça referência à imagem de sistema operativo que pretende instalar no computador de destino e a eventuais conteúdos adicionais, tais como aplicações ou atualizações de software que pretende instalar. A sequência de tarefas para atualizar um sistema operativo faz parte de [atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md) cenário.  

##  <a name="BKMK_UpgradeOS"></a>Criar uma sequência de tarefas para atualizar um sistema operativo  
 Para atualizar o sistema operativo em computadores Windows 10, pode criar uma sequência de tarefas e selecione **atualizar um sistema operativo a partir do pacote de atualização** no Assistente de criação de sequência de tarefas. O assistente irá adicionar os passos para atualizar o sistema operativo, aplicar atualizações de software e instalar aplicações. Antes de criar a sequência de tarefas, o seguinte tem de estar no local:  

-   **Necessário**  

     - O Windows 10 [pacote de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) devem estar disponíveis na consola do Configuration Manager.  

-   **Necessário (se utilizado)**  

    -   [As atualizações de software](../../sum/get-started/synchronize-software-updates.md) têm de ser sincronizados na consola do Configuration Manager.  

    -   [Aplicações](../../apps/deploy-use/create-applications.md) tem de ser adicionado à consola do Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Para criar uma sequência de tarefas que atualiza um sistema operativo  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente de Criação de Sequência de Tarefas.  

4.  No **criar uma nova sequência de tarefas** página, clique em **atualizar um sistema operativo a partir do pacote de atualização**e, em seguida, clique em **seguinte**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Nome da sequência de tarefas**: Especifique um nome que identifica a sequência de tarefas.  

    -   **Descrição**: Especifique uma descrição da tarefa que é executada pela sequência de tarefas.  

6.  No **atualizar o sistema operativo Windows** página, especifique as seguintes definições e, em seguida, clique em **seguinte**.  

    -   **Pacote de atualização**: Especifique o pacote de atualização que contém os ficheiros de origem de atualização do sistema operativo. Pode verificar que selecionou o pacote de atualização correto verificando as informações de **propriedades** painel. Para obter mais informações, consulte o artigo [gerir pacotes de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Índice da edição**: Se existirem vários índices de edição do sistema operativo disponíveis no pacote, selecione o índice da edição pretendido. Por predefinição, o primeiro item está selecionado.  

    -   **Chave de produto**: Especifique a chave de produto para o sistema operativo Windows a instalar. Pode especificar chaves de licenciamento em volume codificadas e chaves de produto padrão. Se utilizar uma chave de produto não codificada, terá de separar cada grupo de 5 carateres por um hífen (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quando a atualização for para uma edição de licença de volume, a chave de produto não é necessária. Só precisa de uma chave de produto quando a atualização for para uma edição de revenda do Windows.  

7.  Na página **Incluir Atualizações** , especifique se devem ser instaladas as atualizações de software necessárias, todas as atualizações de software ou nenhuma atualização de software e clique em **Seguinte**. Se especificar a instalação de atualizações de software, o Configuration Manager instala apenas as atualizações de software destinadas às coleções de que o computador de destino é um membro de.  

8.  Na página **Instalar Aplicações** , especifique as aplicações a instalar no computador de destino e clique em **Seguinte**. Se especificar várias aplicações, poderá também especificar que a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

9. Conclua o assistente.  



## <a name="configure-pre-cache-content"></a>Configurar o conteúdo da pré-cache de
Iniciar na versão 1702, para as implementações de sequências de tarefas disponíveis, pode optar por utilizar a funcionalidade de pré-cache ter clientes a transferir apenas lhe conteúdo relevante antes de um utilizador instala o conteúdo.
> [!TIP]  
> Introduzida com a versão 1702, a pré-cache de é uma funcionalidade de versão de pré-lançamento. Para ativá-lo, consulte o artigo [utilizar funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/pre-release-features).

Por exemplo, digamos que pretende implementar uma sequência de tarefas de atualização no local do Windows 10, só pretende uma sequência de tarefas único para todos os utilizadores e vários arquiteturas de e/ou idiomas. Antes da versão 1702, se criar uma implementação disponível e, em seguida, o utilizador clica **instalar** no Centro de Software, o conteúdo transfere nesse momento. Esta ação adiciona mais tempo antes da instalação estiver pronta para começar. Além disso, todo o conteúdo referenciado na sequência de tarefas é transferido. Isto inclui o pacote de atualização do sistema operativo para todos os idiomas e arquiteturas. Se cada seja aproximadamente 3 GB de tamanho, o pacote de transferência pode ser bastante grande.

O conteúdo da pré-cache de oferece a opção para permitir que o cliente transferir apenas o conteúdo aplicável assim que receber a implementação. Por conseguinte, quando o utilizador clica **instalar** no Centro de Software, o conteúdo estiver disponível e a instalação for iniciada rapidamente porque o conteúdo está no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Para configurar a funcionalidade de pré-cache

1. Crie pacotes de atualização de arquiteturas específicas e idiomas de sistema operativo. Especifique a arquitetura e o idioma no **origem de dados** separador do pacote. Para o idioma, utilize a conversão decimal (por exemplo, 1033 é decimal para inglês e 0x0409 é equivalente a hexadecimal). Para obter mais detalhes, consulte o artigo [criar uma sequência de tarefas para atualizar um sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Os valores de arquitetura e de idioma são utilizados para correspondam às condições de passo de sequência de tarefas será criada no passo seguinte para determinar se o pacote de atualização do sistema operativo deve ser anterior à colocado em cache.
2. Crie uma sequência de tarefas com condicional passos para os idiomas diferentes e arquiteturas. Por exemplo, para a versão em inglês foi possível criar um passo como a seguinte:

    ![Propriedades de pré-cache](../media/precacheproperties2.png)

    ![Opções de pré-cache de](../media/precacheoptions2.png)  

3. Implemente a sequência de tarefas. Para a funcionalidade de pré-cache de configurado o seguinte:
    - No **geral** separador, selecione **previamente transferir conteúdo para esta sequência de tarefas**.
    - No **definições de implementação** separador, configure a sequência de tarefas com o **disponível** para **objetivo**. Se criar um **necessário** implementação, a funcionalidade de pré-cache não funcionará.
    - No **agendamento** separador, para o **agendar quando esta implementação ficará disponível** definição, escolher uma hora no futuro que proporcione tempo suficiente para o conteúdo em cache previamente antes da implementação é disponibilizada para os utilizadores de clientes. Por exemplo, pode definir o tempo disponível para ser 3 horas no futuro para dar tempo suficiente para o conteúdo seja previamente em cache.  
    - No **pontos de distribuição** separador, configure o **opções de implementação** definições. Se o conteúdo não é previamente em cache num cliente antes de um utilizador inicia a instalação, estas definições são utilizadas.


### <a name="user-experience"></a>Experiência de utilizador
- Quando o cliente recebe a política de implementação, iniciará para colocar em cache previamente o conteúdo. Isto inclui todo o conteúdo referenciado (quaisquer outros tipos de pacote) e apenas o pacote atualização do sistema operativo que corresponde ao cliente com base nas condições que configura na sequência de tarefas.
- Quando a implementação é disponibilizada para os utilizadores (a definição de **agendamento** separador da implementação), será apresentado uma notificação para informar os utilizadores sobre a nova implementação e a implementação torna-se visível no Centro de Software. O utilizador pode aceder ao centro de Software e clicar em **instalar** para iniciar a instalação.
- Se o conteúdo não está totalmente previamente colocadas em cache, em seguida, irá utilizar as definições especificadas no **opção de implementação** separador da implementação. Recomendamos que não existe tempo suficiente entre quando a implementação é criada e a hora em que a implementação torna-se disponíveis aos utilizadores para permitir que os clientes tempo suficiente para a pré-colocam o conteúdo em cache.



## <a name="download-package-content-task-sequence-step"></a>Transferir o conteúdo de pacotes passo de sequência de tarefas  
 O [transferir conteúdo de pacotes](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) passo pode ser utilizado antes do **atualizar o sistema operativo** passo nos seguintes cenários:  

-   Utilizar uma sequência de tarefas de atualização única que pode trabalhar com plataformas x86 e x64. Para tal, inclua dois passos **Transferir Conteúdo do Pacote** no grupo **Preparar para Atualização** com condições para detetar a arquitetura do cliente e transferir apenas o pacote de atualização do sistema operativo adequado. Configure cada passo **Transferir Conteúdo do Pacote** para utilizar a mesma variável e utilize a variável para o caminho do suporte de dados no passo **Atualizar Sistema Operativo** .  

-   Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada passo **Transferir Conteúdo do Pacote** para utilizar a mesma variável e utilize a variável para o valor **Conteúdo de teste** na secção de controladores no passo **Atualizar Sistema Operativo**.  

   > [!NOTE]
   > Quando existe mais do que um pacote, o Configuration Manager adiciona um sufixo numérico para o nome da variável. Por exemplo, se especificar uma variável de % mycontent % como uma variável personalizada, esta é a raiz para armazenar todo o conteúdo referenciado (que pode ser vários pacotes). Quando fizer referência à variável num passo subsequente, como, por exemplo, em Atualizar Sistema Operativo, esta é utilizada com um sufixo numérico. Este exemplo, % mycontent01% ou % mycontent02% em que o número corresponde a ordem na qual o pacote está listado neste passo.

## <a name="optional-post-processing-task-sequence-steps"></a>Opcional passos de sequência de tarefas pós-processamento  
 Depois de criar a sequência de tarefas, pode adicionar passos adicionais para desinstalar aplicações com problemas de compatibilidade conhecido ou adicionar ações pós-processamento seja executada após o reinício do computador e a atualização para o Windows 10 for concluída com êxito. Adicione passos adicionais no grupo de pós-processamento da sequência de tarefas.  

> [!NOTE]  
>  Esta sequência de tarefas não é linear, existem condições passos que podem afetar os resultados da sequência de tarefas, dependendo se atualização com êxito o computador cliente ou se tiver que reverter o computador cliente para a versão do sistema operativo tiver sido iniciado com.  

## <a name="optional-rollback-task-sequence-steps"></a>Passos de sequência de tarefas de reversão opcional  
 Quando algo corra mal com o processo de atualização depois do computador seja reiniciado, a configuração irá reverter a atualização para o sistema operativo anterior e a sequência de tarefas continuará com quaisquer passos no grupo de reversão. Depois de criar a sequência de tarefas, pode adicionar passos opcionais para o grupo de reversão.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Pasta e os ficheiros foram removidos após o computador reiniciar  
 Quando a sequência de tarefas para atualizar um sistema operativo para o Windows 10 e todos os outros passos da sequência de tarefas estiverem concluídos, os scripts de pós-processamento e de reversão não são removidos até que o computador seja reiniciado.  Estes ficheiros de script não contêm informações confidenciais.  

