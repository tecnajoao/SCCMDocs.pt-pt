---
title: Gerir sequências de tarefas
titleSuffix: Configuration Manager
description: Criar, editar, implementar, importar e exportar sequências de tarefas para geri-los e automatizar tarefas no seu ambiente.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: nac
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: ''
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 262bfa3991bbd95fad779da9520358d527a42b07
ms.sourcegitcommit: a19e12d5c3198764901d44f4df7c60eb542e765f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/28/2018
---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>Gerir sequências de tarefas para automatizar tarefas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize sequências de tarefas para automatizar passos no seu ambiente do Configuration Manager. Estes passos podem implementar uma imagem de SO para um computador de destino, criar e capturar uma imagem de SO de um conjunto de ficheiros de instalação do SO e capturar e restaurar informações de estado do utilizador. Sequências de tarefas na consola do Configuration Manager. No **biblioteca de Software** área de trabalho, expanda **sistemas operativos** e selecione **sequências de tarefas**. O **sequências de tarefas** nó, incluindo as subpastas que crie, é replicado em toda a hierarquia do Configuration Manager. Para obter informações de planeamento, consulte [considerações sobre planeamento para automatizar tarefas](../plan-design/planning-considerations-for-automating-tasks.md).  

 Utilize as secções seguintes para gerir sequências de tarefas.

##  <a name="BKMK_CreateTaskSequence"></a> Criar sequências de tarefas  
 Crie sequências de tarefas utilizando o Assistente de Criação de Sequência de Tarefas. Este assistente pode criar os seguintes tipos de sequências de tarefas:  

|Tipo de sequência de tarefas|Mais informações|  
|------------------------|----------------------|  
|[Sequência de tarefas para instalar um sistema operativo](create-a-task-sequence-to-install-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para instalar o sistema operativo, bem como a opção para migrar dados de utilizador, incluir atualizações de software e instalar aplicações.|  
|[Sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para atualizar o sistema operativo, bem como a opção para incluir atualizações de software e instalar aplicações.|  
|[Sequência de tarefas para capturar um sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para criar e capturar o sistema operativo de um computador de referência. Pode incluir atualizações de software e instalar aplicações no computador de referência antes da captura da imagem.|  
|[Sequência de tarefas para capturar e restaurar o estado do utilizador](create-a-task-sequence-to-capture-and-restore-user-state.md)|Esta sequência de tarefas fornece os passos a adicionar a uma sequência de tarefas existente para capturar e restaurar dados de estado do utilizador.|  
|[Sequência de tarefas personalizada](create-a-custom-task-sequence.md)|Este tipo de sequência de tarefas não adiciona quaisquer passos à sequência de tarefas. Edite a sequência de tarefas e adicionar passos à sequência de tarefas depois de criado.|  



## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior, quando ocorre uma falha de uma sequência de tarefas
Poderá regressar à página anterior quando executa uma sequência de tarefas e não existe uma falha. Nas versões anteriores do Configuration Manager, era necessário reiniciar a sequência de tarefas quando ocorreu uma falha. Utilize o **anterior** botão nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas é apresentada uma mensagem que existem não existem sequências de tarefas disponíveis. Agora, pode clicar em **anterior** para novamente procurar sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdos dependentes ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Se o conteúdo em falta ainda não foi distribuído, distribui-lo agora. Ou aguarde que o conteúdo fique disponível nos pontos de distribuição. Em seguida, clique em **anterior** ter a pesquisa de sequência de tarefas novamente para o conteúdo.

##  <a name="BKMK_ModifyTaskSequence"></a> Editar uma sequência de tarefas  
 Pode modificar uma sequência de tarefas adicionando ou removendo passos, adicionando ou removendo grupos, ou alterando a ordem dos passos. Utilize o procedimento seguinte para modificar uma sequência de tarefas existente:  

> [!IMPORTANT]  
>  Ao editar uma sequência de tarefas que foi criada utilizando o Assistente de criação de sequência de tarefas, o nome do passo pode ser o tipo de passo ou ação. Por exemplo, poderá ver um passo com o nome "Criar partições do disco 0", que é a ação de um passo do tipo [formatar e particionar disco](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Todos os passos de sequência de tarefas estão documentados pelo respetivo tipo, não necessariamente pelo nome do passo que é apresentado no editor.  

#### <a name="to-edit-a-task-sequence"></a>Para editar uma sequência de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende editar.  

4.  No separador **Home Page** , no grupo **Sequência de Tarefas** , clique em **Editar**e efetue qualquer uma das seguintes operações:  

    -   Para adicionar um passo de sequência de tarefas, clique em **adicionar**, selecione o tipo de passo e, em seguida, clique no passo para adicionar. Por exemplo, para adicionar o passo Executar Linha de Comandos, clique em **Adicionar**, selecione **Geral**e, em seguida, clique em **Executar Linha de Comandos**.  

         Para obter uma lista de todos os passos de sequência de tarefas e o respetivo tipo, consulte a tabela que se segue a este procedimento.  

    -   Para adicionar um grupo à sequência de tarefas, clique em **Adicionar**e clique em **Novo Grupo**. Depois de adicionar um grupo, em seguida, pode adicionar passos ao grupo.  

    -   Para alterar a ordem dos passos e grupos na sequência de tarefas, selecione o passo ou grupo que pretende reordenar e, em seguida, utilize o **Mover Item para cima** ou **Mover Item para baixo** ícones. Apenas pode mover um passo ou um grupo de cada vez.  

    -   Para remover um passo ou um grupo, selecione o passo ou o grupo e clique em **Remover**.  

5.  Clique em **OK** para guardar as alterações.  

 Para obter uma lista dos passos de sequência de tarefas disponíveis, consulte [passos de sequência de tarefas](../understand/task-sequence-steps.md).  

## <a name="configure-software-center-properties"></a>Configurar propriedades de centro de Software
Utilize o procedimento seguinte para configurar os detalhes para a sequência de tarefas apresentadas no Centro de Software. Estes detalhes estão apenas para informação.  
1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **geral** separador, estão disponíveis as seguintes definições no Centro de Software:
  - **Reinício necessário**: Permite que o utilizador saber se é necessário reiniciar durante a instalação.
  - **Transferir o tamanho (MB)**: Especifica a quantidade de megabytes são apresentados no Centro de Software para a sequência de tarefas.  
  - **Estimado (minutos) o tempo de execução**: Especifica que o estimado tempo de execução em minutos, que é apresentado no Centro de Software para a sequência de tarefas.

## <a name="configure-advanced-task-sequence-settings"></a>Configurar as definições de sequência de tarefas avançadas
Utilize o procedimento seguinte para configurar os detalhes para a sequência de tarefas apresentadas no Centro de Software. Estes detalhes estão apenas para informação.  
1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **avançadas** separador, estão disponíveis as seguintes definições:

    - **Executar outro programa primeiro**    
    Selecione esta caixa de verificação para executar outro programa (por outro pacote) antes de executar a sequência de tarefas. Por predefinição, esta caixa de verificação está desmarcada. O programa que especificar para ser executado primeiro não tem de ser anunciado separadamente.

        > [!IMPORTANT]     
        Esta definição só se aplica a sequências de tarefas que executam no SO completo. Gestor de configuração ignora esta definição se a sequência de tarefas é iniciada através de suportes de dados de arranque ou PXE.

    - **Pacote**     
        Quando seleciona **executar outro programa primeiro**, procure o pacote que contém o programa que tem de executar antes desta sequência de tarefas.

    - **Programa**     
    Quando seleciona **executar outro programa primeiro**, seleccione o programa que tem de executar antes desta sequência de tarefas a partir de **programa** na lista pendente.

        > [!NOTE]    
        > Se o programa selecionado não for executado num cliente, a sequência de tarefas não é executado. Se o programa selecionado é executada com êxito, este não é executado novamente, mesmo se a sequência de tarefas será novamente executada no mesmo cliente.
 
    - **Desativar esta sequência de tarefas nos computadores onde está implementada**    
    Se selecionar esta opção, todas as implementações que contêm esta sequência de tarefas estão temporariamente desativadas. A sequência de tarefas é removida da lista de implementações disponíveis para ser executada. -Não é executado até que volte a reativá-la. Por predefinição, esta opção estiver desmarcada.

    - **Tempo de execução máximo permitido**    
    Especifica o tempo máximo (em minutos) que é esperado para executar a sequência de tarefas no computador de destino. Utilize um número inteiro igual ou maior que zero. Por predefinição, este valor é definido para 120 minutos.

        > [!IMPORTANT]    
        > Se estiver a utilizar janelas de manutenção para a coleção em que esta sequência de tarefas é executada, poderá ocorrer um conflito se o **máximo tempo de execução permitido** é superior à janela de manutenção agendada. Se o tempo de execução máximo for definido como **0**, a sequência de tarefas for iniciada durante a janela de manutenção. Continua a ser executado até concluir ou falhar depois de fechar a janela de manutenção. Como resultado, as sequências de tarefas com um tempo máximo de execução definido como **0** poderá ser executado depois do fim do respetivos janelas de manutenção. Se definir o tempo máximo de execução para um período específico (não **0**) que excede o comprimento de qualquer janela de manutenção disponível, em seguida, a sequência de tarefas não é executado. Para obter mais informações, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
 
        Se o valor é definido como **0**, Configuration Manager avalia o tempo máximo de execução permitido como **12** horas (720 minutos) para monitorizar o progresso. No entanto, a sequência de tarefas é iniciada, desde a duração da contagem decrescente não excede o valor de janela de manutenção.

    > [!NOTE]    
    > Se for atingido o tempo de execução máximo, o Configuration Manager interrompe a sequência de tarefas se está definido para executar com direitos de administrador e os permitir que os utilizadores interajam com esta definição de programa não está selecionada. Se a sequência de tarefas propriamente dito não está parada, o Configuration Manager para a monitorização da sequência de tarefas após o máximo permitido tempo de execução foi atingido. 

    - **Utilizar uma imagem de arranque**   
        Ative esta opção para utilizar a imagem de arranque selecionada quando a sequência de tarefas é executada. 

        Clique em **procurar** para selecionar uma imagem de arranque diferentes. Desmarque esta opção para desativar a utilização da imagem de arranque selecionada quando a sequência de tarefas é executada.

    - **Esta sequência de tarefas pode executar em qualquer plataforma**     
        Se selecionar esta opção, o Configuration Manager não verifica se o tipo de plataforma do computador de destino quando a sequência de tarefas é implementada. Esta opção está selecionada por predefinição.

    - **Esta sequência de tarefas só pode ser executada em plataformas cliente especificadas**    
        Esta opção especifica os processadores, as versões do SO e os service packs no qual pode executar esta sequência de tarefas. Quando seleciona esta opção, também é necessário selecionar pelo menos uma plataforma da lista. Por predefinição, são selecionadas não plataformas. O Configuration Manager utiliza estas informações quando é avalia os computadores de destino numa coleção recebem a sequência de tarefas implementada.

        > [!NOTE]    
        > Quando uma sequência de tarefas é executada a partir do suporte de dados ou pelo arranque PXE, esta opção é ignorada e a sequência de tarefas é executada, embora a opção **este programa pode ser executado em qualquer plataforma** está selecionada.



## <a name="configure-high-impact-task-sequence-settings"></a>Configurar as definições de sequência de tarefas de elevado impacto
Pode definir uma sequência de tarefas como de elevado impacto e personalizar as mensagens que os utilizadores recebem quando executam a sequência de tarefas.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de elevado impacto
Utilize o procedimento seguinte para definir uma sequência de tarefas como de elevado impacto.
> [!NOTE]    
> Qualquer sequência de tarefas que cumpra determinadas condições é automaticamente definida como impacto elevado. Para obter mais informações, consulte [gerir implementações de alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **notificação do utilizador** separador, selecione **esta é uma sequência de tarefas de elevado impacto**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação para implementações de alto risco
Utilize o procedimento seguinte para criar uma notificação para implementações de impacto elevado.
1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **notificação do utilizador** separador, selecione **utilizar texto personalizado**.
>  [!NOTE]    
>  Só é possível definir texto de notificação do utilizador quando o **esta é uma sequência de tarefas de elevado impacto** está selecionada.

4. Configure as seguintes definições (máximo de 255 carateres para cada caixa de texto):

  **Texto do título de notificação de utilizador**: Especifica o texto azul que apresenta na notificação de utilizador do Centro de Software. Por exemplo, a predefinição de notificação de utilizador, esta secção contém "Confirmar que pretende atualizar o sistema operativo neste computador."

  **Texto de mensagem de notificação do utilizador**: Existem três caixas de texto que fornecem o corpo da notificação personalizada. Todas as caixas de texto requerem que adicione o texto.
  - Caixa de texto primeiro: Especifica o corpo do principal de texto, normalmente, que contém instruções para o utilizador. Por exemplo, a predefinição de notificação de utilizador, esta secção contém "a atualização do sistema operativo demora tempo e o computador poderá reiniciar várias vezes."
  - Segunda caixa de texto: Especifica o texto a negrito no corpo do principal do texto. Por exemplo, a predefinição de notificação de utilizador, esta secção contém "esta atualização no local instala o novo sistema operativo e migra automaticamente as suas definições, aplicações e dados."
  - Terceira caixa de texto: Especifica a última linha de texto com o texto a negrito. Por exemplo, a predefinição de notificação de utilizador, esta secção contém "clique em instalar para iniciar. Caso contrário, clique em Cancelar."   
    
Vamos supor que configura a seguinte notificação personalizada nas propriedades.

![Separador de notificação do utilizador personalizada das propriedades de sequência de tarefas](..\media\user-notification.png)

Apresenta a seguinte mensagem de notificação quando o utilizador final abre a instalação do Centro de Software.

![Notificação de sequência de tarefas personalizadas para o utilizador final do Centro de Software](..\media\user-notification-enduser.png)


##  <a name="BKMK_DistributeTS"></a> Distribuir conteúdo referenciado por uma sequência de tarefas  
 Para que os clientes possam executar uma sequência de tarefas que referencie conteúdos, é necessário distribuir esses conteúdos aos pontos de distribuição. Em qualquer altura, pode selecionar a sequência de tarefas e distribuir o respetivo conteúdo para criar uma nova lista de pacotes de referência para distribuição. Se efetuar alterações à sequência de tarefas com conteúdo atualizado, tem de redistribuir o conteúdo antes de ser disponibilizado aos clientes. Utilize o seguinte procedimento para distribuir os conteúdos que são referenciados por uma sequência de tarefas.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Para distribuir conteúdo referenciado a pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende distribuir.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Distribuir Conteúdo** para iniciar o Assistente para Distribuir Conteúdo.  

5.  No **geral** página, certifique-se de que a sequência de tarefas correta está selecionada para distribuição. Em seguida, clique em **Seguinte**.  

6.  Na página **Conteúdo** , confirme os conteúdos a distribuir, por exemplo a imagem de arranque referenciada pela sequência de tarefas e, em seguida, clique em **Seguinte**.  

7.  No **destino do conteúdo** página, especifique as coleções, ponto de distribuição ou grupo de pontos de distribuição em que pretende distribuir os conteúdos da sequência de tarefas. Em seguida, clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  Se a sequência de tarefas que selecionou referenciar conteúdos que já tenham sido distribuídos a um ponto de distribuição específico, esse ponto de distribuição não será incluído na lista do assistente.  

8.  Conclua o assistente.  

 Pode pré-configurar o conteúdo referenciado na sequência de tarefas. O Configuration Manager cria um ficheiro de conteúdo comprimido e pré-configurado que contém os ficheiros, dependências associadas e metadados associados para o conteúdo que selecionar. Em seguida, poderá importar manualmente os conteúdos para um servidor de sites, site secundário ou ponto de distribuição. Para obter mais informações sobre como pré-configurar ficheiros de conteúdo, consulte [pré-configurar conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  



##  <a name="BKMK_DeployTS"></a> Implementar uma sequência de tarefas  
 Utilize o seguinte procedimento para implementar uma sequência de tarefas nos computadores de uma coleção.  

> [!WARNING]  
>  Pode gerir o comportamento de implementações de sequência de tarefas de alto risco. Uma implementação de alto risco é uma implementação que é automaticamente instalada e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tenha um objetivo **necessário** que implementa o sistema operativo é considerada uma implementação de alto risco. Para obter mais informações, consulte [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

> [!NOTE]  
>  As mensagens de estado para a implementação da sequência de tarefas são apresentadas na janela Mensagem de um site primário, mas não são apresentadas num site de administração central.  

#### <a name="to-deploy-a-task-sequence"></a>Para implementar uma sequência de tarefas    

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende implementar.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

    > [!NOTE]  
    >  Se a opção **Implementar** não estiver disponível, a sequência de tarefas tem uma referência que não é válida. Corrija a referência e tente implementar a sequência de tarefas novamente.  

5.  Na página **Geral** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Sequência de tarefas**: Especifique a sequência de tarefas que pretende implementar. Por predefinição, esta caixa apresenta a sequência de tarefas que selecionou.  

    -   **Coleção**: Especifique a coleção que contenha os computadores a executar a sequência de tarefas.  

         Não implemente uma sequência de tarefas que instala um SO em coleções inadequadas, tais como o **todos os sistemas** coleção. Certifique-se de que a coleção que selecionou apenas contém os computadores nos quais pretende executar a sequência de tarefas.  

        > [!NOTE]  
        >  Ao implementar uma implementação de alto risco, como sistema operativo, o **selecionar coleção** janela apresenta apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site. As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não pode selecionar uma coleção incorporada, como **Todos os Sistemas**. Desmarque **ocultar coleções com um membro contagem superiores à configuração de tamanho mínimo do site** para ver todas as coleções personalizadas que incluem menos clientes do que o tamanho máximo configurado. Para obter mais informações, consulte [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >   
        >  As definições de verificação da implementação são baseadas na associação atual da coleção. Após implementar a sequência de tarefas, a associação da coleção não é reavaliada relativamente às definições de implementação de alto risco.  
        >   
        >  Por exemplo, digamos que definiu **tamanho predefinido** a 100 e o **tamanho máximo** a 1000. Quando cria uma implementação de alto risco, a **selecionar coleção** janela apresenta apenas as coleções com menos de 100 clientes. Se desmarcar a **ocultar coleções com um membro contagem superiores à configuração de tamanho mínimo do site** definição, a janela apresenta as coleções com menos de 1 000 clientes.  
        >   
        >  Quando seleciona uma coleção que contém uma função de site, aplica-se o comportamento seguinte:  
        >   
        >  -   Se a coleção contiver um servidor de sistema de sites e configurou as definições de verificação de implementação para o bloqueio das coleções com servidores de sistema de sites, em seguida, ocorre um erro. Não é possível continuar a criação da implementação.  
        > -   Se um dos seguintes critérios aplica-se, em seguida, o Assistente de implementação de Software apresenta um aviso de alto risco. Para continuar, terá de aceitar criar uma implementação de alto risco. O site gera uma mensagem de estado de auditoria.
        >     - Se a coleção contiver um servidor de sistema de sites e configurou as definições de verificação de implementação para o avisar de coleções com servidores de sistema de sites
        >     - Se a coleção ultrapassar o valor do tamanho predefinido
        >     - Se a coleção contiver um servidor  

    -   **Comentários (opcional)**: Especifique informações adicionais que descrevam esta implementação da sequência de tarefas.  
    - **Selecione o modelo de implementação**: A partir do Configuration Manager versão 1802,<!--1357391--> pode guardar e especifique um modelo de implementação de uma sequência de tarefas.     

         > [!IMPORTANT]
         > No Configuration Manager versão 1802, alguns itens não estão guardadas no modelo.  <!--510610--> Certifique-se de que se aplicam os itens seguintes quando executar o Assistente de implementação:
         > - Instalação de software 
         > - Agendamento 
         > - Pré-transferir conteúdo
 
6.  Na página **Definições de Implementação** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Objetivo**: Na lista pendente, escolha uma das seguintes opções:  

        -   **Disponível**: Se a sequência de tarefas for implementada para um utilizador, o utilizador verá a sequência de tarefas publicada no catálogo de aplicações e poderá solicitá-la a pedido. Se a sequência de tarefas for implementada num dispositivo, o utilizador vê-lo no Centro de Software e pode instalá-la a pedido.  

        -   **Necessário**: A sequência de tarefas é implementada automaticamente, de acordo com a agenda configurada. Se a sequência de tarefas não se encontre oculto, um utilizador pode ainda monitorizar o estado de implementação. Também podem instalar a sequência de tarefas antes do prazo utilizando o Centro de Software.  

    -   **Implementar automaticamente de acordo com a agenda quer exista ou não um utilizador tiver sessão iniciado**: Esta opção não está disponível ao implementar uma sequência de tarefas.  

    -   **Enviar pacotes de reativação**: Se o objetivo da implementação estiver definido como **necessário** e esta opção estiver selecionada, o site envia um pacote de reativação para computadores antes de executar a implementação. Este pacote sair o computador da suspensão quando for atingido o prazo instalação. Para poder utilizar esta opção, os computadores e redes terão de estar configurados para Reativação por LAN.  

    -   **Permitir que os clientes numa ligação à Internet limitada para transferir conteúdo após o prazo de instalação, o que pode implicar custos adicionais**: Quando tiver uma sequência de tarefas que instala uma aplicação, mas não implementa o sistema operativo, pode especificar se pretende permitir que os clientes transfiram conteúdos após um prazo de instalação quando estiverem a utilizar ligações à Internet limitadas. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

        > [!NOTE]  
        >  Ao utilizar uma ligação à Internet com tráfego limitado poderá funcionar para sequências de tarefas não implementará um sistema, não é suportada.  

    -   **Exigir aprovação do administrador caso os utilizadores solicitem esta aplicação**: Esta opção não está disponível ao implementar uma sequência de tarefas.  

    -   **Tornar disponível para o seguinte**: Especifique se a sequência de tarefas está disponível para clientes do Configuration Manager, suportes de dados ou PXE.  

        > [!IMPORTANT]  
        >  Utilize a definição **Apenas suportes de dados e PXE (oculto)** para implementações com sequências de tarefas automatizadas. Para que o computador arranque automaticamente para a implementação sem interação do utilizador, selecione **permitir a implementação do sistema operativo autónoma** e defina a variável SMSTSPreferredAdvertID como parte do suporte de dados. Para obter mais informações sobre as variáveis de sequência de tarefas, consulte [variáveis incorporadas de sequência de tarefas](../understand/task-sequence-built-in-variables.md)  

7.  Na página **Agendamento** , especifique as seguintes informações e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  Quando um cliente Windows PE é iniciado a partir de um suporte de dados de arranque ou PXE, o cliente não avalia agendas de implementação (iniciar, extinguir ou horas de prazos). Configure apenas agendamentos em implementações em clientes iniciados a partir do sistema operativo Windows completo. Considere a utilização de outros métodos, como janelas de manutenção, para controlar sequências de tarefas ativas implementadas em clientes iniciados a partir do Windows PE.  

    -   **Agendar quando esta implementação ficará disponível**: Especifique a data e hora em que a sequência de tarefas ficará disponível para ser executada no computador de destino. Se selecionar a caixa de verificação **UTC** , esta definição garantirá que a sequência de tarefas ficará disponível para vários computadores de destino ao mesmo tempo, em vez de em alturas diferentes, de acordo com a hora local dos computadores de destino.  

         Se a hora de início for anterior à hora necessária, o cliente transfere a sequência de tarefas à hora de início que especificou.  

    -   **Agendar quando esta implementação expirará**: Especifique a data e hora em que a sequência de tarefas expira no computador de destino. Se seleciona a caixa de verificação **UTC** , a definição correspondente fará com que a sequência de tarefas expire em vários computadores de destino no mesmo tempo, em vez de tal acontecer em diferentes momentos, de acordo com a hora local dos computadores de destino.  

    -   **Agenda de atribuição**: Especifique quando a sequência de tarefas necessária é executada no computador de destino. Pode adicionar múltiplas agendas.  

         Pode especificar a data e hora em que a agenda é iniciada, se a sequência de tarefas é executada semanalmente, mensalmente ou num intervalo personalizado e se a sequência de tarefas é executada após um registo de eventos como, por exemplo, o início ou o fim de sessão num computador.  

        > [!NOTE]  
        >  Se agendar uma hora de início para uma sequência de tarefas necessária que seja anterior à data e hora em que a sequência de tarefas ficará disponível, o cliente do Configuration Manager transfere a sequência de tarefas à hora de início agendada, mesmo que a sequência de tarefas esteja mais cedo.  

    -   **Comportamento da nova execução**: Especifique quando a sequência de tarefas será novamente executada. Pode especificar uma das seguintes opções:  

        -   **Nunca executar novamente o programa implementado**: Se o cliente tiver sido anteriormente executada a sequência de tarefas, não novamente. A sequência de tarefas não novamente executada mesmo tenha falhado inicialmente ou os ficheiros de sequência de tarefas foram alterados.  

        -   **Executar sempre novamente o programa**: A sequência de tarefas será sempre novamente executada no cliente quando a implementação estiver agendada, mesmo se a sequência de tarefas foi executada com êxito anteriormente. Esta definição é útil quando utilizar implementações periódicas no qual a sequência de tarefas seja regularmente atualizada.  

            > [!IMPORTANT]  
            >  Embora esta opção é definida por predefinição, não tem efeito até que o atribua uma implementação necessária. As implementações disponíveis podem ser sempre novamente executadas por um utilizador.  

        -   **Executar novamente se a tentativa anterior**: A sequência de tarefas será novamente executada se a implementação é agendada apenas se a sequência de tarefas não executou anteriormente. Esta definição é útil para as implementações necessárias. Se a última tentativa de execução não foi bem-sucedida, eles automaticamente tentar novamente, de acordo com a agenda de atribuição.  

        -   Executar novamente se tiver êxito tentativa anterior: A sequência de tarefas é executado novamente apenas se tiver sido anteriormente executada com êxito no cliente. Esta definição é útil se utilizar implementações periódicas cuja sequência de tarefas seja regularmente atualizada e cada atualização necessitar que a atualização anterior tenha sido instalada com êxito.  

        > [!NOTE]  
        >  Porque um utilizador pode voltar a executar uma implementação de sequência de tarefas disponível, certifique-se de que antes de implementar uma sequência de tarefas disponível num ambiente de produção, cuidadosamente avaliar e testar o que acontece se um utilizador volta executar a sequência de tarefas múltiplas vezes.  

8.  Na página **Experiência de Utilizador** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Permitir que o utilizador executar o programa independentemente das atribuições**: Especifique se o utilizador tem permissão para executar uma sequência de tarefas necessária, independentemente das atribuições da implementação da.  

    -   **Mostrar Progresso da sequência de tarefas**: Especifique se o cliente do Configuration Manager apresenta o progresso da sequência de tarefas.  

    -   **Instalação de software**: Especifique se o utilizador tem permissão para instalar o software fora de uma janela de manutenção configuradas e depois da data agendada.  

    -   **Reinício do sistema (se for necessário para concluir a instalação)**: Especifique se o utilizador tem permissão para reiniciar o computador após uma instalação de software fora de uma janela de manutenção configuradas e depois da hora da atribuição.  

    -   **Permitir que a sequência de tarefas executar o cliente na Internet**: Especifique se a sequência de tarefas pode ser executada num cliente baseado na internet. As operações que instalam software, tal como o sistema operativo, não são suportadas com esta definição. Utilize esta opção apenas para as sequências de tarefas genéricas, baseadas em scripts que executam operações no sistema operativo padrão.  

         - A partir de versão 1802, esta definição é suportada para implementações de uma sequência de tarefas de atualização no local do Windows 10 para clientes baseados na internet através do gateway de gestão de nuvem. Para obter mais informações, consulte [atualização no local de implementar o Windows 10 através de CMG](#deploy-windows-10-in-place-upgrade-via-cmg).    

9. Na página **Alertas** , especifique as definições de alerta pretendidas para esta implementação de sequências de tarefas e, em seguida, clique em **Seguinte**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e, em seguida, clique em **Seguinte**.  

    -   **Opções de implementação**: Especifique uma das seguintes opções:  

        > [!NOTE]  
        >  Quando utilizar multicast para implementar o sistema operativo, o conteúdo deverão ser transferido para os computadores de destino, conforme é necessário ou antes de executar a sequência de tarefas.  

        -   Especifique que os clientes devem transferir os conteúdos do ponto de distribuição para o computador de destino, se tal for necessário para a sequência de tarefas.  

        -   Especifique se os clientes deverão transferir todos os conteúdos do ponto de distribuição para o computador de destino antes de a sequência de tarefas ser executada. Esta opção não será apresentada se tiver especificado que a sequência de tarefas está disponível para implementações de suportes de dados de arranque PXE e no **definições de implementação** página.  

        -   Especifique se os clientes deverão executar os conteúdos a partir do ponto de distribuição. Esta opção só está disponível quando todos os pacotes associados à sequência de tarefas estão ativados para utilizar uma partilha de pacote no ponto de distribuição. Para permitir que os conteúdos utilizem uma partilha de pacote, consulte o separador **Acesso a Dados** nas **Propriedades** de cada pacote.  

    -   **Se estiver disponível nenhum ponto de distribuição local, utilizar um ponto de distribuição remoto**: Especifique se os clientes podem utilizar pontos de distribuição localizados em redes lentas e pouco fiáveis para transferir o conteúdo necessário pela sequência de tarefas.  
11. A partir do Configuration Manager 1802, no **resumo** separador, clique em **guardar como modelo** se pretender guardar as definições para utilizar novamente. Forneça um nome para o modelo e selecione as definições para guardar. 

 
12. Conclua o assistente.  


### <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Implementar a atualização no local do Windows 10 através de CMG
<!-- 1357149 -->

A partir de versão 1802, a sequência de tarefas de atualização no local do Windows 10 suporta a implementação de clientes baseados na internet geridos através de [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG). Esta capacidade permite aos utilizadores remotos mais facilmente atualizar para o Windows 10, sem necessitar de ligar à intranet. 

Certifique-se de que todo o conteúdo referenciado pela sequência de tarefas de atualização no local é distribuído para um [ponto de distribuição de nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Caso contrário, os dispositivos não é possível executar a sequência de tarefas.

Quando implementa uma sequência de tarefas de atualização, utilize as seguintes definições:
- **Permitir que a sequência de tarefas executar o cliente na Internet**, no separador de experiência de utilizador da implementação.
- **Transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas**, no separador de pontos de distribuição da implementação. Outras opções como **transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução** não funcionam neste cenário. O motor de sequência de tarefas é atualmente não é possível obter conteúdo de um ponto de distribuição na nuvem. O cliente do Configuration Manager tem de transferir o conteúdo do ponto de distribuição de nuvem antes de iniciar a sequência de tarefas.
- (*Opcional*) **previamente transferir conteúdo para esta sequência de tarefas**, no separador Geral da implementação. Para obter mais informações, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).



##  <a name="BKMK_ExportImport"></a> Exportar e importar sequências de tarefas  
 Pode exportar e importar sequências de tarefas com ou sem os respetivos objetos relacionados. Este conteúdo referenciado inclui uma imagem do SO, uma imagem de arranque, um pacote de agente do cliente, um pacote de controladores e aplicações com dependências.  

 Pondere os seguintes aspetos ao exportar e importar sequências de tarefas.  

-   As palavras-passe que se encontram armazenadas na sequência de tarefas não são exportadas. Se exportar e importar uma sequência de tarefas que contenha palavras-passe, tem de editar a sequência de tarefas importada e reintroduza as palavras-passe. Certifique-se de que especifica palavras-passe para [associar domínio ou grupo de trabalho](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [ligar à pasta de rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder), e [executar linha de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) ações.  

- Quando exporta uma sequência de tarefas com o **definir variáveis dinâmicas** passo, são exportados sem valores das variáveis que estão configuradas com o **valor secreto** definição. Reintroduza os valores para estas variáveis, depois de importar a sequência de tarefas.

-   Como procedimento recomendado, sempre que existam vários sites primários, as sequências de tarefas deverão ser importadas no site de administração central.  

 Utilize os seguintes procedimentos para exportar e importar uma sequência de tarefas.  

#### <a name="to-export-task-sequences"></a>Para exportar sequências de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione as sequências de tarefas que pretende exportar. Se selecionar mais do que uma sequência de tarefas, estas serão armazenadas num ficheiro de exportação.  

4.  No separador **Início** , no grupo **Sequência de Tarefas** , clique em **Exportar** para iniciar o Assistente de Criação de Sequência de Tarefas.  

5.  Na página **Geral** , especifique as seguintes definições e clique em **Seguinte**.  

    -   Na caixa **Ficheiro** , especifique a localização e o nome do ficheiro de exportação. Se introduzir diretamente o nome do ficheiro, certifique-se de que inclui a extensão .zip no nome do ficheiro. Se navegar para o ficheiro de exportação, o assistente adicionará automaticamente esta extensão de nome de ficheiro.  

    -   Desative a caixa de verificação **Exportar todas as dependências de sequência de tarefas** se não pretender exportar as dependências das sequências de tarefas. Por predefinição, o assistente verifica se existem todos os objetos relacionados e exporta-os juntamente com a sequência de tarefas. Estas dependências incluem qualquer para aplicações.  

    -   Desative a caixa de verificação **Exportar todo o conteúdo para as dependências e sequências de tarefas selecionadas** se não pretender que os conteúdos da origem do pacote sejam copiados para a localização de exportação. Se esta caixa de verificação estiver selecionada, o Assistente para Importar Sequência de Tarefas utilizará o caminho de importação como a nova localização de origem do pacote.  

    -   Na caixa **Comentários do administrador** , adicione uma descrição das sequências de tarefas a exportar.  

6.  Conclua o assistente.  

 O assistente cria os seguintes ficheiros de saída:  

-   Se não exportar conteúdos: um ficheiro .zip.  

-   Se não exportar conteúdos: um ficheiro .zip e uma pasta designada *exportar*_files, em que *exportar* corresponde ao nome do ficheiro .zip que contém os conteúdos exportados.  

 Se incluir conteúdos ao exportar uma sequência de tarefas, certifique-se de que copie o ficheiro. zip e a *exportar*Files pasta ou a importação falhará.  

#### <a name="to-import-task-sequences"></a>Para importar sequências de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Importar Sequência de Tarefas** para iniciar o Assistente Importar Sequência de Tarefas.  

4.  Na página **Geral** , especifique o ficheiro .zip exportado e clique em **Seguinte**.  

5.  Na página **Conteúdo do Ficheiro** , selecione a ação de que necessita para cada objeto que importar. Esta página mostra todos os objetos que o Configuration Manager encontrou para importar.  

    -   Se o objeto nunca tiver sido importado, selecione **Criar Novo**.  

    -   Se o objeto tiver sido importado anteriormente, selecione uma das seguintes ações:  

        -   **Ignorar duplicado** (predefinição): Esta ação não importa o objeto. Em vez disso, o assistente liga o objeto existente à sequência de tarefas.  

        -   **Substituir**: Esta ação substitui o objeto existente pelo objeto importado. Para aplicações, pode adicionar uma revisão para atualizar a aplicação existente ou criar uma nova aplicação.  

6.  Conclua o assistente.  

 Depois de importar a sequência de tarefas, edite-a para especificar as palavras-passe que estavam na sequência de tarefas original. Por razões de segurança, as palavras-passe não são exportadas.  

##  <a name="BKMK_CreateTSVariables"></a> Criar variáveis de sequência de tarefas para computadores e coleções  
Pode definir variáveis de sequência de tarefas personalizadas para computadores e coleções. As variáveis definidas para um computador são designadas variáveis de sequência de tarefas por computador. As variáveis definidas para uma coleção são designadas variáveis de sequência de tarefas por coleção. Em caso de conflito, as variáveis por computador têm precedência sobre as variáveis por coleção. Este comportamento significa que as variáveis de sequência de tarefas que são automaticamente atribuídas a um computador específico tem uma prioridade superior à variáveis que estão atribuídas à coleção que contenha o computador.  

Por exemplo, se a coleção ABC tiver atribuída uma variável e o computador XYZ, que é um membro da coleção ABC, tiver atribuída uma variável com o mesmo nome, a variável atribuída ao computador XYZ terá prioridade sobre a variável atribuída à coleção ABC.  

Pode ocultar as variáveis por computador e por coleção para que não fiquem visíveis na consola do Configuration Manager. Se pretender que deixem de ficar ocultas, tem de as eliminar e redefinir sem selecionar a opção para as ocultar. Quando utiliza a opção **não apresentar este valor na consola do Configuration Manager**, o valor da variável não for apresentado na consola do. A variável ainda pode ser utilizada pela sequência de tarefas quando for executada.  

> [!WARNING]    
> O **não apresentar este valor na consola do Configuration Manager** definição aplica-se apenas a consola do Configuration Manager. Os valores para as variáveis ainda são apresentados no ficheiro de registo de sequência de tarefas (SMSTS. REGISTO). 

Pode gerir variáveis por computador num site primário ou num site de administração central. O Configuration Manager não suporta mais de 1000 variáveis atribuídas para um computador.  

> [!IMPORTANT]  
>  Quando utiliza variáveis por coleção para sequências de tarefas, considere os comportamentos seguintes:  
>   
> - As alterações nas coleções são sempre replicadas em toda a hierarquia. Aplicam as alterações efetuadas nas variáveis da coleção não apenas a membros do site atual, mas para todos os membros da coleção de toda a hierarquia.  
> - Quando elimina uma coleção, esta ação também elimina as variáveis de sequência de tarefas configuradas para a coleção.  

 Utilize os procedimentos seguintes para criar variáveis de sequência de tarefas para um computador ou uma coleção.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>Para criar variáveis de sequência de tarefas para um computador  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda a coleção que contém o computador ao qual pretende adicionar a variável.  

3.  Selecione o computador e clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** , clique no separador **Variáveis** .  

5.  Para cada variável que pretende criar, clique o **novo** ícone no **< novo\> variável** caixa de diálogo. Especifique o nome e o valor da variável de sequência de tarefas. Limpar o **não apresentar este valor na consola do Configuration Manager** caixa de verificação se pretender ocultar as variáveis, para que não fiquem visíveis na consola do Configuration Manager.  

6.  Depois de ter adicionado todas as variáveis ao computador, clique em **OK**.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>Para criar variáveis de sequência de tarefas para uma coleção  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , selecione a coleção à qual pretende adicionar a variável e clique em **Propriedades**.  

3.  Na caixa de diálogo **Propriedades** , clique no separador **Variáveis da Coleção** .  

4.  Para cada variável que pretende criar, clique o **novo** ícone no **< novo\> variável** caixa de diálogo. Especifique o nome e o valor da variável de sequência de tarefas. Limpar o **não apresentar este valor na consola do Configuration Manager** caixa de verificação se pretender ocultar as variáveis, para que não fiquem visíveis na consola do Configuration Manager.  

5.  Opcionalmente, especifique a prioridade para o Configuration Manager para utilizar quando são avaliadas as variáveis de sequência de tarefas.  

6.  Depois de ter adicionado todas as variáveis à coleção, clique em **OK**.  

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicionar sequências de tarefas de subordinados a uma sequência de tarefas

A partir do Configuration Manager versão 1710, pode adicionar um novo passo de sequência de tarefas executa outra sequência de tarefas. Este passo cria uma relação principal-subordinado entre as sequências de tarefas. Utilizar este passo permite-lhe criar mais sequências de tarefas modulares que pode reutilizar.

Quando adicionar uma sequência de tarefas subordinados a uma sequência de tarefas, considere o seguinte:

 - As sequências de tarefas principais e subordinados eficazmente são combinadas uma única política que executa o cliente.
 - O ambiente é global. Por exemplo, se uma variável é definida pela sequência de tarefas principal e, em seguida, alterada pela sequência de tarefas subordinadas, continua a ser alterada. Da mesma forma, se a sequência de tarefas subordinado cria uma nova variável, está disponível para os passos restantes da sequência de tarefas principal.
 - Mensagens de estado são enviadas por normal para uma operação de sequência de tarefas único.
 - As sequências de tarefas escreverem entradas no ficheiro smsts.log, com o novo registo de entradas que desmarque quando uma sequência de tarefas subordinado é iniciado.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Para adicionar uma sequência de tarefas subordinados a uma sequência de tarefas

1. No editor de sequência de tarefas, clique em **adicionar**, selecione **geral**e clique em **executar a sequência de tarefas**.
2. Clique em **procurar** para selecionar a sequência de tarefas subordinado.  

##  <a name="BKMK_AdditionalActionsTS"></a> Ações adicionais para gerir sequências de tarefas  
 Pode gerir sequências de tarefas com ações adicionais ao selecionar uma sequência de tarefas.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Para selecionar uma sequência de tarefas para gerir  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos** e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende gerir e selecione uma das opções disponíveis.  

 Utilize a seguinte tabela para obter mais informações sobre algumas das ações adicionais para gerir as sequências de tarefas.  

|Action|Descrição|  
|------------|-----------------|  
|**Copiar**|Efetua uma cópia da sequência tarefas selecionada. Esta ação é útil para criar uma nova sequência de tarefas com base na sequência de tarefas existente.<br /><br /> Quando efetuar uma cópia de uma sequência de tarefas numa pasta, esta é listada nessa pasta até a atualizar o nó da sequência de tarefas. Após a atualização, cópia aparece na pasta raiz.|  
|**Desativar**|Desativa a sequência de tarefas para não ser executada nos computadores. Pode implementar uma sequência de tarefas desativada, mas os computadores executam a sequência de tarefas até que o ative.|  
|**Ativar**|Ativa a sequência de tarefas para poder ser executada. Não necessita de voltar a implementar uma sequência de tarefas implementada depois de ser ativada.|  
|**Criar Ficheiro de Conteúdo Pré-configurado**|Inicia o Assistente para Criar Ficheiro de Conteúdo Pré-configurado para pré-configurar o conteúdo da sequência de tarefas. Para obter informações sobre como criar um ficheiro de conteúdo pré-configurado, consulte [pré-configurar conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).|  
|**Moverr**|Move a sequência de tarefas selecionada para outra pasta.|  

## <a name="next-steps"></a>Passos seguintes
[Cenários para implementar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md)
