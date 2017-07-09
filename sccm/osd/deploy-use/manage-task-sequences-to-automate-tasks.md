---
title: "Gerenciar sequências de tarefas para automatizar tarefas | Microsoft Docs"
description: "Você pode criar, editar, implantar, importar e exportar as sequências de tarefas para gerenciá-los em seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: 10
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 2f3d66362c49d28a52d7f9c535eb0b3b4cc4eaf7
ms.contentlocale: pt-pt
ms.lasthandoff: 06/08/2017


---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>Gerir sequências de tarefas para automatizar tarefas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Use sequências de tarefas para automatizar as etapas em seu ambiente do System Center Configuration Manager. Estes passos podem implementar uma imagem de sistema operativo num computador de destino, criar e capturar uma imagem de sistema operativo a partir de um conjunto de ficheiros de instalação de sistema operativo, e capturar e restaurar informações de estado do utilizador. Sequências de tarefas estão localizadas no console do Configuration Manager no **biblioteca de Software** > **sistemas operacionais** > **sequência de tarefas**. O **sequência de tarefas** nó, incluindo as subpastas que você cria, é replicado em toda a hierarquia do Configuration Manager. Para obter informações sobre planejamento, consulte [considerações de planejamento para automatizar tarefas](../plan-design/planning-considerations-for-automating-tasks.md).  

 Use as seções a seguir para gerenciar sequências de tarefas.

##  <a name="BKMK_CreateTaskSequence"></a> Criar sequências de tarefas  
 Crie sequências de tarefas utilizando o Assistente de Criação de Sequência de Tarefas. Este assistente pode criar os seguintes tipos de sequências de tarefas:  

|Tipo de sequência de tarefas|Mais informações|  
|------------------------|----------------------|  
|[Sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para instalar um sistema operativo, bem como a opção para migrar dados de utilizador, incluir atualizações de software e instalar aplicações.|  
|[Sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para atualizar um sistema operativo, bem como a opção para incluir atualizações de software e instalar aplicações.|  
|[Sequência de tarefas para capturar um sistema operacional](create-a-task-sequence-to-capture-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para criar e capturar um sistema operativo a partir de um computador de referência. Pode incluir atualizações de software e instalar aplicações no computador de referência antes da captura da imagem.|  
|[Sequência de tarefas para capturar e restaurar o estado do usuário](create-a-task-sequence-to-capture-and-restore-user-state.md)|Esta sequência de tarefas fornece os passos a adicionar a uma sequência de tarefas existente para capturar e restaurar dados de estado do utilizador.|  
|[Sequência de tarefas para gerenciar discos rígidos virtuais](use-a-task-sequence-to-manage-virtual-hard-disks.md)|Esse tipo de sequência de tarefas contém as etapas para criar um VHD, o que inclui para instalar um sistema operacional e aplicativos, que você pode publicar para o System Center Virtual Machine Manager (VMM) no console do Configuration Manager.|  
|[Sequência de tarefas personalizada](create-a-custom-task-sequence.md)|Este tipo de sequência de tarefas não adiciona quaisquer passos à sequência de tarefas. Tem de editar a sequência de tarefas e adicionar passos à mesma depois de ser criada.|  

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Retornar à página anterior, quando não é uma sequência de tarefas
A partir do Configuration Manager versão 1702, você pode retornar à página anterior quando você executa uma sequência de tarefas e houver uma falha. Antes desta versão, era necessário reiniciar a sequência de tarefas quando houve uma falha. Por exemplo, você pode usar o **anterior** botão nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, o diálogo de inicialização de sequência de tarefas pode ser exibido antes da sequência de tarefas está disponível. Quando você clicar em Avançar neste cenário, a página final da sequência de tarefas exibe uma mensagem que não há sequências de tarefas estão disponíveis. Agora, você pode clicar em **anterior** pesquisar novamente para sequências de tarefas disponíveis. Você pode repetir este processo até que a sequência de tarefas está disponível.
- Quando você executar uma sequência de tarefas, mas os pacotes de conteúdo dependentes ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Distribuir o conteúdo ausente (se ela ainda não foi distribuída) ou aguarde até que o conteúdo esteja disponível nos pontos de distribuição e, em seguida, clique em **anterior** para que a pesquisa de sequência de tarefas novamente para o conteúdo.

##  <a name="BKMK_ModifyTaskSequence"></a> Editar uma sequência de tarefas  
 Pode modificar uma sequência de tarefas adicionando ou removendo passos de sequência de tarefas, adicionando ou removendo grupos de sequências de tarefas ou alterando a ordem dos passos. Utilize o procedimento seguinte para modificar uma sequência de tarefas existente.  

> [!IMPORTANT]  
>  Quando edita uma sequência de tarefas criada com o Assistente de Criação de Sequência de Tarefas, o nome do passo pode ser a ação do passo ou o tipo do mesmo. Por exemplo, você talvez veja uma etapa que tem o nome "Particionar disco 0", que é a ação de uma etapa do tipo [Formatar e particionar disco](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Todos os passos de sequência de tarefas estão documentados pelo respetivo tipo, não necessariamente pelo nome do passo que é apresentado no Editor.  

#### <a name="to-edit-a-task-sequence"></a>Para editar uma sequência de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende editar.  

4.  No separador **Home Page** , no grupo **Sequência de Tarefas** , clique em **Editar**e efetue qualquer uma das seguintes operações:  

    -   Para adicionar um passo de sequência de tarefas, clique em **Adicionar**, selecione o tipo de passo e, em seguida, clique no passo de sequência de tarefas que pretende adicionar. Por exemplo, para adicionar o passo Executar Linha de Comandos, clique em **Adicionar**, selecione **Geral**e, em seguida, clique em **Executar Linha de Comandos**.  

         Para obter uma lista de todos os passos de sequência de tarefas e o respetivo tipo, consulte a tabela que se segue a este procedimento.  

    -   Para adicionar um grupo à sequência de tarefas, clique em **Adicionar**e clique em **Novo Grupo**. Depois de adicionar um grupo, pode adicionar passos ao grupo.  

    -   Para alterar a ordem dos passos e grupos na sequência de tarefas, selecione o passo ou o grupo que pretende reordenar e utilize os ícones **Mover Item Para Cima** ou **Mover Item Para Baixo** . Apenas pode mover um passo ou um grupo de cada vez.  

    -   Para remover um passo ou um grupo, selecione o passo ou o grupo e clique em **Remover**.  

5.  Clique em **OK** para guardar as alterações.  

 Para obter uma lista das etapas de sequência de tarefas disponíveis, consulte [etapas da sequência de tarefas](../understand/task-sequence-steps.md).  

## <a name="configure-software-center-properties"></a>Configurar propriedades do Centro de Software
Use o procedimento a seguir para configurar os detalhes da sequência de tarefas exibido no Centro de Software. Esses detalhes são apenas para fins informativos.  
1. No console do Configuration Manager, vá para **biblioteca de Software** > **sistemas operacionais** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. Sobre o **geral** guia, as seguintes configurações para o Centro de Software estão disponíveis:
  - **Reinicialização necessária**: Permite que o usuário saiba se uma reinicialização é necessária durante a instalação.
  - **Tamanho (MB) do download**: Especifica a quantidade de megabytes é exibido no Centro de Software para a sequência de tarefas.  
  - **Tempo estimado para execução (minutos)**: Especifica que o estimado tempo de execução em minutos em que é exibido no Centro de Software para a sequência de tarefas.

## <a name="configure-advanced-task-sequence-settings"></a>Definir configurações de sequência de tarefas avançadas
Use o procedimento a seguir para configurar os detalhes da sequência de tarefas exibido no Centro de Software. Esses detalhes são apenas para fins informativos.  
1. No console do Configuration Manager, vá para **biblioteca de Software** > **sistemas operacionais** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. Sobre o **avançado** guia, as seguintes configurações estão disponíveis:

    - **Executar outro programa primeiro**    
    Marque esta caixa de seleção para executar outro programa (em outro pacote) antes da sequência de tarefas é executada. Por predefinição, esta caixa de verificação está desmarcada. O programa que você especificar para executar o primeiro não precisa ser publicado separadamente.

        > [!IMPORTANT]     
        Essa configuração se aplica apenas às sequências de tarefas que são executados no sistema operacional completo. Gerenciador de configuração ignora esta configuração se a sequência de tarefas é iniciada usando mídia de inicialização ou PXE.

    - **Pacote**     
        Quando você seleciona **executar outro programa primeiro**, digite ou navegue para o pacote que contém o programa que deve ser executado antes dessa sequência de tarefas.

    - **Programa**     
    Quando você seleciona **executar outro programa primeiro**, selecione o programa que deve ser executado antes dessa sequência de tarefas do **programa** lista suspensa.

        > [!NOTE]    
        > Se o programa selecionado não é executado em um cliente, a sequência de tarefas não será executada. Se o programa selecionado for executado com êxito, ele será não ser executado novamente, mesmo se a sequência de tarefas é executada novamente no mesmo cliente.
 
    - **Desabilitar esta sequência de tarefas em computadores onde está implantada**    
    Se você selecionar essa opção, todas as implantações que contêm essa sequência de tarefas estão temporariamente desabilitadas. A sequência de tarefas é removida da lista de anúncios disponíveis para execução e não será executado até que ele tenha sido habilitado novamente. Por padrão, essa opção é desmarcada.

    - **Tempo de execução máximo permitido**    
    Especifica o tempo máximo (em minutos) que é esperado para executar a sequência de tarefas no computador de destino. Você deve usar um número inteiro igual ou maior que zero. Por predefinição, este valor é definido para 120 minutos.

        > [!IMPORTANT]    
        > Se você estiver usando janelas de manutenção para a coleção na qual esta sequência de tarefas é executada, um conflito poderá ocorrer se o **tempo de execução máximo permitido** é maior que a janela de manutenção agendada. Se o tempo de execução máximo for definido como **0**, a sequência de tarefas será iniciado durante a janela de manutenção e continuar a executar até que ela é concluída ou falha depois que a janela de manutenção é fechada. Como resultado, as sequências de tarefas com um tempo máximo de execução definido como **0** pode ser executado após o término de suas janelas de manutenção. Se você definir o tempo máximo de execução para um período específico (ou seja, não definido como **0**) que excede o comprimento de qualquer janela de manutenção disponível e, em seguida, sequência de tarefas não será executada. Para obter mais informações, consulte [como usar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).
 
        Se o valor é definido como **0**, o Configuration Manager avalia o tempo máximo de execução permitido como **12** horas (720 minutos) para monitorar o progresso. No entanto, a sequência de tarefas será iniciado, desde que a duração da contagem regressiva não exceder o valor de janela de manutenção.

    > [!NOTE]    
    > Se o tempo de execução máximo for atingido, o Configuration Manager interromperá a sequência de tarefas se ele estiver definido para executar com direitos administrativos e os permitir que os usuários interajam com a configuração do programa não estiver selecionada. Se a sequência de tarefas não for interrompida, o Configuration Manager parará de monitoramento a sequência de tarefas após o máximo permitido em tempo de execução for atingido. 

    - **Usar uma imagem de inicialização**   
        Habilite esta opção para usar a imagem de inicialização selecionada quando a sequência de tarefas é executada. 

        Clique em **procurar** para selecionar uma imagem de inicialização diferente. Desmarque essa opção para desabilitar o uso da imagem de inicialização selecionada quando a sequência de tarefas é executada.

    - **Essa sequência de tarefas pode ser executado em qualquer plataforma**     
        Se você selecionar essa opção, o Configuration Manager não verifica o tipo de plataforma do computador de destino quando a sequência de tarefas é implantada. Esta opção está selecionada por predefinição.

    - **Essa sequência de tarefas pode ser executado somente nas plataformas cliente especificadas**    
        Esta opção especifica os processadores, sistemas operacionais e service packs em que pode executar essa sequência de tarefas. Quando você seleciona essa opção, pelo menos uma plataforma também deve ser selecionada na lista. Por padrão, nenhuma plataforma é selecionada. O Configuration Manager usa essas informações quando é avalia os computadores de destino em uma coleção recebem a sequência de tarefas implantada.

        > [!NOTE]    
        > Quando uma sequência de tarefas é executada da mídia de inicialização ou pela inicialização PXE, essa opção será ignorada e a sequência de tarefas é executado como se a opção **este programa pode ser executado em qualquer plataforma** está selecionado.

## <a name="configure-high-impact-task-sequence-settings"></a>Definir configurações de sequência de tarefas de alto impacto
A partir do Configuration Manager versão 1702, você pode definir uma sequência de tarefas como alto impacto e personalizar as mensagens recebidas pelos usuários quando eles executam a sequência de tarefas.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de alto impacto
Use o procedimento a seguir para definir uma sequência de tarefas como alto impacto.
> [!NOTE]    
> Qualquer sequência de tarefas que atende a certas condições é automaticamente definida como alto impacto. Para obter detalhes, consulte [gerenciar implantações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. No console do Configuration Manager, vá para **biblioteca de Software** > **sistemas operacionais** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. Sobre o **notificação do usuário** guia, selecione **isso é uma sequência de tarefas de alto impacto**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implantações de alto risco
Use o procedimento a seguir para criar uma notificação personalizada para implantações de alto impacto.
1. No console do Configuration Manager, vá para **biblioteca de Software** > **sistemas operacionais** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. Sobre o **notificação do usuário** guia, selecione **usar texto personalizado**.
>  [!NOTE]    
>  Você só pode definir o texto de notificação do usuário quando o **isso é uma sequência de tarefas de alto impacto** está selecionado.

4. Defina as seguintes configurações (máximo de 255 caracteres para cada caixa de texto):

  **Texto do título de notificação de usuário**: Especifica o texto azul que exibe a notificação de usuário do Centro de Software. Por exemplo, a notificação do usuário padrão, esta seção contém algo como "Confirmar que você deseja atualizar o sistema operacional neste computador".

  **Texto de mensagem de notificação do usuário**: Há três caixas de texto que fornecem o corpo da notificação personalizada. Todas as caixas de texto exigem que você adicionar texto.
  - 1º de caixa de texto: Especifica o corpo principal do texto, que normalmente contém instruções para o usuário. Por exemplo, a notificação do usuário padrão, esta seção contém algo como "atualização do sistema operacional levará tempo e o computador pode ser reiniciado várias vezes."
  - 2º caixa de texto: Especifica o texto em negrito no corpo principal do texto. Por exemplo, a notificação do usuário padrão, esta seção contém algo como "Esta atualização instala o novo sistema operacional e migra automaticamente os aplicativos, dados e configurações."
  - 3 de caixa de texto: Especifica a última linha de texto sob o texto em negrito. Por exemplo, a notificação do usuário padrão, esta seção contém algo como "clique em instalar para começar. Caso contrário, clique em Cancelar."   
    
Digamos que você configurar a notificação personalizada a seguir nas propriedades.

![Notificação personalizada para uma sequência de tarefas](..\media\user-notification.png)

Aparecerá a seguinte mensagem de notificação quando o usuário final abre a instalação do Centro de Software.

![Notificação personalizada para uma sequência de tarefas](..\media\user-notification-enduser.png)


##  <a name="BKMK_DistributeTS"></a> Distribuir conteúdo referenciado por uma sequência de tarefas  
 Para que os clientes possam executar uma sequência de tarefas que referencie conteúdos, é necessário distribuir esses conteúdos aos pontos de distribuição. Em qualquer altura, pode selecionar a sequência de tarefas e distribuir o respetivo conteúdo para criar uma nova lista de pacotes de referência para distribuição. Se efetuar alterações à sequência de tarefas com conteúdo atualizado, tem de redistribuir o conteúdo antes de ser disponibilizado aos clientes. Utilize o seguinte procedimento para distribuir os conteúdos que são referenciados por uma sequência de tarefas.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Para distribuir conteúdo referenciado a pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende distribuir.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Distribuir Conteúdo** para iniciar o Assistente para Distribuir Conteúdo.  

5.  Na página **Geral** , verifique se a sequência de tarefas correta está selecionada para distribuição e, em seguida, clique em **Seguinte**.  

6.  Na página **Conteúdo** , confirme os conteúdos a distribuir, por exemplo a imagem de arranque referenciada pela sequência de tarefas e, em seguida, clique em **Seguinte**.  

7.  Na página **Destino do Conteúdo** , especifique as coleções, o ponto de distribuição ou grupo de pontos de destino aos quais pretende distribuir os conteúdos da sequência de tarefas e, em seguida, clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  Se a sequência de tarefas que selecionou referenciar conteúdos que já tenham sido distribuídos a um ponto de distribuição específico, esse ponto de distribuição não será incluído na lista do assistente.  

8.  Conclua o assistente.  

 Pode pré-configurar o conteúdo referenciado na sequência de tarefas. Configuration Manager cria um arquivo de conteúdo compactado e pré-configurado que contém os arquivos, as dependências associadas e os metadados associados para o conteúdo que você selecionar. Em seguida, poderá importar manualmente os conteúdos para um servidor de sites, site secundário ou ponto de distribuição. Para obter mais informações sobre como pré-configurar arquivos de conteúdo, consulte [pré-configurar conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).  

##  <a name="BKMK_DeployTS"></a> Implementar uma sequência de tarefas  
 Utilize o seguinte procedimento para implementar uma sequência de tarefas nos computadores de uma coleção.  

> [!WARNING]  
>  Pode gerir o comportamento de implementações de sequência de tarefas de alto risco. Uma implementação de alto risco é uma implementação que é automaticamente instalada e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tenha um objetivo **Obrigatório** que implemente um sistema operativo é considerada uma implementação de alto risco. Para obter mais informações, consulte [configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

> [!NOTE]  
>  As mensagens de estado para a implementação da sequência de tarefas são apresentadas na janela Mensagem de um site primário, mas não são apresentadas num site de administração central.  

#### <a name="to-deploy-a-task-sequence"></a>Para implementar uma sequência de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende implementar.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

    > [!NOTE]  
    >  Se a opção **Implementar** não estiver disponível, a sequência de tarefas tem uma referência que não é válida.  Corrija a referência e tente implementar a sequência de tarefas novamente.  

5.  Na página **Geral** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Sequência de tarefas**: Especifique a sequência de tarefas que você deseja implantar. Por predefinição, esta caixa apresenta a sequência de tarefas que selecionou.  

    -   **Coleção**: Especifique a coleção que contém os computadores que executarão a sequência de tarefas.  

         Não implemente sequências de tarefas que instalem sistemas operativos em coleções inadequadas, por exemplo a coleção **Todos os Sistemas** . Certifique-se de que a coleção que selecionou apenas contém os computadores nos quais pretende executar a sequência de tarefas.  

        > [!NOTE]  
        >  Quando você implanta uma implantação de alto risco, como um sistema operacional, o **selecionar coleção** janela exibe somente as coleções personalizadas que atendem às configurações de verificação de implantação que são configuradas nas propriedades do site. As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não pode selecionar uma coleção incorporada, como **Todos os Sistemas**. Desmarque **ocultar coleções com um membro contagem maiores que a configuração de tamanho mínimo do site** para ver todas as coleções personalizadas que contêm menos clientes do que o tamanho máximo configurado. Para obter mais informações, consulte [configurações para gerenciar implantações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >   
        >  As definições de verificação da implementação são baseadas na associação atual da coleção. Após implementar a sequência de tarefas, a associação da coleção não é reavaliada relativamente às definições de implementação de alto risco.  
        >   
        >  Por exemplo, suponhamos que você defina **tamanho padrão** a 100 e o **tamanho máximo** a 1000. Quando cria uma implementação de alto risco, a janela **Selecionar Coleção** só apresenta as coleções com menos de cem clientes. Se você desmarcar a **ocultar coleções com um membro contagem maiores que a configuração de tamanho mínimo do site** configuração, a janela exibirá coleções que contêm menos de 1.000 clientes.  
        >   
        >  Quando seleciona uma coleção que contém uma função do site, são aplicáveis as seguintes situações:  
        >   
        >  -   Se a coleção contiver um servidor do sistema de sites e nas definições de verificação de implementação configurar o bloqueio das coleções com servidores do sistema de sites, ocorrerá um erro e não conseguirá continuar.  
        > -   Se a coleção contiver um servidor do sistema de sites e nas definições de verificação da implementação configurar a apresentação de um aviso caso as coleções incluam servidores do sistema de sites, se a coleção ultrapassar o valor do tamanho predefinido ou se a coleção contiver um servidor, o Assistente de Implementação de Software apresentará um aviso de alto risco. Tem de aceitar criar uma implementação de alto risco e é criada uma mensagem de estado de auditoria.  

    -   **Comentários (opcional)**: Especifique informações adicionais que descrevem essa implantação da sequência de tarefas.  

6.  Na página **Definições de Implementação** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Finalidade**: Na lista suspensa, escolha uma das seguintes opções:  

        -   **Disponível**: Se a sequência de tarefas é implantada para um usuário, o usuário verá a sequência de tarefas publicada no catálogo de aplicativos e pode solicitá-la sob demanda. Se a sequência de tarefas for implementada num dispositivo, o utilizador irá vê-la no Centro de Software e pode instalá-la a pedido.  

        -   **Necessário**: A sequência de tarefas é implantada automaticamente de acordo com o agendamento configurado. No entanto, um utilizador poderá controlar o estado de implementação da sequência de tarefas (desde que não esteja oculta) e instalar a sequência de tarefas antes do prazo utilizando o Centro de Software.  

    -   **Implantar automaticamente de acordo com a agenda se um usuário estiver conectado ou não**: Essa opção não está disponível quando você implanta uma sequência de tarefas.  

    -   **Enviar pacotes de ativação**: Se a finalidade da implantação for definida como **necessário** e essa opção for selecionada, um pacote de ativação será enviado aos computadores antes da implantação ser instalada para ativar o computador da suspensão no prazo da instalação. Para poder utilizar esta opção, os computadores e redes terão de estar configurados para Reativação por LAN.  

    -   **Permitir que os clientes em uma conexão de Internet limitada baixem conteúdo após o prazo de instalação, o que pode incorrer em custos adicionais**: Quando você tiver uma sequência de tarefas que instala um aplicativo, mas não implantar um sistema operacional, você pode especificar se deseja permitir que os clientes baixem conteúdo após o prazo de instalação quando usarem de Internet limitados. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

        > [!NOTE]  
        >  Embora uma ligação de Internet limitada possa funcionar para sequências de tarefas que não implementam um sistema operativo, tal não é suportado.  

    -   **Exigir aprovação do administrador se os usuários solicitarem este aplicativo**: Essa opção não está disponível quando você implanta uma sequência de tarefas.  

    -   **Tornar disponível para o seguinte**: Especifique se a sequência de tarefas está disponível para clientes do Configuration Manager, mídia ou PXE.  

        > [!IMPORTANT]  
        >  Utilize a definição **Apenas suportes de dados e PXE (oculto)** para implementações com sequências de tarefas automatizadas. Selecione **Permitir implementação de sistema operativo autónoma** e defina a variável SMSTSPreferredAdvertID como parte do suporte de dados para que o computador arranque automaticamente para a implementação, sem interação do utilizador. Para obter mais informações sobre variáveis de sequência de tarefas, consulte [variáveis internas de sequência de tarefas](../understand/task-sequence-built-in-variables.md)  

7.  Na página **Agendamento** , especifique as seguintes informações e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  Quando um cliente Windows PE é iniciado a partir de um suporte de dados de arranque ou PXE, o cliente não avalia agendas de implementação (iniciar, extinguir ou horas de prazos). Configure apenas agendamentos em implementações para clientes que sejam iniciados a partir do sistema operativo Windows completo. Considere a utilização de outros métodos, como janelas de manutenção, para controlar sequências de tarefas ativas implementadas em clientes iniciados a partir do Windows PE.  

    -   **Agendar quando essa implantação estará disponível**: Especifique a data e a hora em que a sequência de tarefas está disponível para ser executado no computador de destino. Se selecionar a caixa de verificação **UTC** , esta definição garantirá que a sequência de tarefas ficará disponível para vários computadores de destino ao mesmo tempo, em vez de em alturas diferentes, de acordo com a hora local dos computadores de destino.  

         Se a hora de início for anterior à hora necessária, o cliente transfere a sequência de tarefas à hora de início que especificou.  

    -   **Agendar quando esta implantação expirará**: Especifique a data e a hora em que a sequência de tarefas expirará no computador de destino. Se seleciona a caixa de verificação **UTC** , a definição correspondente fará com que a sequência de tarefas expire em vários computadores de destino no mesmo tempo, em vez de tal acontecer em diferentes momentos, de acordo com a hora local dos computadores de destino.  

    -   **Agendamento de atribuição**: Especifique quando a sequência de tarefas necessária é executada no computador de destino. Pode adicionar múltiplas agendas.  

         Pode especificar a data e hora em que a agenda é iniciada, se a sequência de tarefas é executada semanalmente, mensalmente ou num intervalo personalizado e se a sequência de tarefas é executada após um registo de eventos como, por exemplo, o início ou o fim de sessão num computador.  

        > [!NOTE]  
        >  Se você agendar uma hora de início para uma sequência de tarefas necessária que seja anterior à data e hora em que a sequência de tarefas disponível, o cliente do Configuration Manager baixa a sequência de tarefas na hora de início agendada, mesmo que a sequência de tarefas está disponível em um momento anterior.  

    -   **Reexecutar comportamento**: Especifique quando a sequência de tarefas é executada novamente. Pode especificar uma das seguintes opções.  

        -   **Nunca executar novamente o programa implantado**: A sequência de tarefas não será executada novamente no cliente se a sequência de tarefas tiver sido executada anteriormente no cliente. A sequência de tarefas não será novamente executada, mesmo que a respetiva execução inicial tenha falhado ou que os ficheiros de sequência de tarefas tenham sido alterados.  

        -   **Sempre executar novamente o programa**: A sequência de tarefas sempre é executada novamente no cliente quando a implantação está agendada, mesmo se a sequência de tarefas foi executado com êxito anteriormente. Esta definição é particularmente útil se utilizar implementações periódicas cuja sequência de tarefas seja regularmente atualizada.  

            > [!IMPORTANT]  
            >  Embora esta opção esteja definida por predefinição, não terá qualquer efeito enquanto não lhe for atribuída uma implementação necessária. As implementações disponíveis podem ser sempre novamente executadas por um utilizador.  

        -   **Executar novamente se a tentativa anterior**: A sequência de tarefas é executada novamente quando a implantação é agendada somente se a sequência de tarefas não for executado anteriormente. Esta definição é particularmente útil para implementações necessárias e permite que a execução das mesmas seja automaticamente repetida, de acordo com a agenda de atribuição, caso a última tentativa de execução não tenha sido concluída com êxito.  

        -   Executar novamente se a tentativa anterior tiver êxito: A sequência de tarefas é executada novamente somente se tiver sido executada com êxito no cliente. Esta definição é útil se utilizar implementações periódicas cuja sequência de tarefas seja regularmente atualizada e cada atualização necessitar que a atualização anterior tenha sido instalada com êxito.  

        > [!NOTE]  
        >  Uma vez que um utilizador pode executar novamente uma sequência de tarefas de implementação, certifique-se de que, antes de implementar uma sequência de tarefas disponível num ambiente de produção, avalia e testa cuidadosamente o que acontece quando um utilizador volta a executar a sequência de tarefas múltiplas vezes.  

8.  Na página **Experiência de Utilizador** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Permitir que o usuário executar o programa de forma independente das atribuições**: Especifique se o usuário tem permissão para executar uma sequência de tarefas necessária independentemente das atribuições de implantação.  

    -   **Mostrar andamento da sequência de tarefas**: Especifique se o cliente do Configuration Manager exibe o progresso da sequência de tarefas.  

    -   **Instalação do software**: Especifique se o usuário tem permissão para instalar software fora de uma janela de manutenção configurada após a hora agendada.  

    -   **Reinicialização do sistema (se necessário para concluir a instalação)**: Especifique se o usuário tem permissão para reiniciar o computador após uma instalação de software fora de uma janela de manutenção configurada após a hora de atribuição.  

    -   **Permitir que a sequência de tarefas seja executada para cliente na Internet**: Especifique se a sequência de tarefas pode ser executado em um cliente baseado na Internet que o Configuration Manager detecta na Internet. As operações que instalam software, por exemplo um sistema operativo, não são suportadas por esta definição. Só deve utilizar esta opção para sequências de tarefas genéricas, baseadas em scripts, que executem operações padrão do sistema operativo.  

9. Na página **Alertas** , especifique as definições de alerta pretendidas para esta implementação de sequências de tarefas e, em seguida, clique em **Seguinte**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e, em seguida, clique em **Seguinte**.  

    -   **Opções de implantação**: Especifique uma das seguintes opções:  

        > [!NOTE]  
        >  Se utilizar multicast para implementar um sistema operativo, os conteúdos deverão ser transferidos para os computadores de destino quer à medida que forem necessários ou antes de a sequência de tarefas ser executada.  

        -   Especifique que os clientes devem transferir os conteúdos do ponto de distribuição para o computador de destino, se tal for necessário para a sequência de tarefas.  

        -   Especifique se os clientes deverão transferir todos os conteúdos do ponto de distribuição para o computador de destino antes de a sequência de tarefas ser executada. Esta opção não será apresentada se tiver especificado que a sequência de tarefas estará disponível para implementações com arranque PXE ou com suportes de dados (consulte a página **Definições de Implementação** ).  

        -   Especifique se os clientes deverão executar os conteúdos a partir do ponto de distribuição. Esta opção só estará disponível se todos os pacotes associados à sequência de tarefas estiverem configurados para utilizar uma partilha de pacote no ponto de distribuição. Para permitir que os conteúdos utilizem uma partilha de pacote, consulte o separador **Acesso a Dados** nas **Propriedades** de cada pacote.  

    -   **Quando nenhum ponto de distribuição local estiver disponível, use um ponto de distribuição remoto**: Especifique se os clientes podem usar pontos de distribuição que estão em redes lentas e não confiáveis para baixar o conteúdo exigido pela sequência de tarefas.  

11. Conclua o assistente.  

##  <a name="BKMK_ExportImport"></a> Exportar e importar sequências de tarefas  
 Pode exportar e importar sequências de tarefas, com ou sem os objetos a elas associados, como por exemplo uma imagem de sistema operativo, uma imagem de arranque, um pacote de agente do cliente, um pacote de controladores e aplicações que tenham dependências.  

 Pondere os seguintes aspetos ao exportar e importar sequências de tarefas.  

-   As palavras-passe que se encontram armazenadas na sequência de tarefas não são exportadas. Se exportar e importar uma sequência de tarefas que contenha palavras-passe, deverá editar a sequência de tarefas importada e especificar novamente as palavras-passe. Certifique-se de que você especifica senhas para [ingressar no domínio ou grupo de trabalho](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [Connect To Network Folder](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder), e [executar linha de comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) ações.  

- Quando você exporta uma sequência de tarefas com o **definir variáveis de Dynanmic** etapa, valores não é exportado para variáveis que são configurados com o **valor secreto** configuração. Você deve reinserir os valores para essas variáveis, depois de importar a sequência de tarefas.

-   Como procedimento recomendado, sempre que existam vários sites primários, as sequências de tarefas deverão ser importadas no site de administração central.  

 Utilize os seguintes procedimentos para exportar e importar uma sequência de tarefas.  

#### <a name="to-export-task-sequences"></a>Para exportar sequências de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione as sequências de tarefas que pretende exportar. Se selecionar mais do que uma sequência de tarefas, estas serão armazenadas num ficheiro de exportação.  

4.  No separador **Início** , no grupo **Sequência de Tarefas** , clique em **Exportar** para iniciar o Assistente de Criação de Sequência de Tarefas.  

5.  Na página **Geral** , especifique as seguintes definições e clique em **Seguinte**.  

    -   Na caixa **Ficheiro** , especifique a localização e o nome do ficheiro de exportação. Se introduzir diretamente o nome do ficheiro, certifique-se de que inclui a extensão .zip no nome do ficheiro. Se navegar para o ficheiro de exportação, o assistente adicionará automaticamente esta extensão de nome de ficheiro.  

    -   Desative a caixa de verificação **Exportar todas as dependências de sequência de tarefas** se não pretender exportar as dependências das sequências de tarefas. Por predefinição, o assistente verifica se existem todos os objetos relacionados e exporta-os juntamente com a sequência de tarefas. Esta operação abrange eventuais dependências de aplicações.  

    -   Desative a caixa de verificação **Exportar todo o conteúdo para as dependências e sequências de tarefas selecionadas** se não pretender que os conteúdos da origem do pacote sejam copiados para a localização de exportação. Se esta caixa de verificação estiver selecionada, o Assistente para Importar Sequência de Tarefas utilizará o caminho de importação como a nova localização de origem do pacote.  

    -   Na caixa **Comentários do administrador** , adicione uma descrição das sequências de tarefas a exportar.  

6.  Conclua o assistente.  

 O assistente cria os seguintes ficheiros de saída:  

-   Se não exportar conteúdos: um ficheiro .zip.  

-   Se não exportar conteúdos: um ficheiro .zip e uma pasta designada *exportar*_files, em que *exportar* corresponde ao nome do ficheiro .zip que contém os conteúdos exportados.  

 Se incluir conteúdos ao exportar uma sequência de tarefas, certifique-se de que o ficheiro .zip e a pasta *exportar*_files são copiados, caso contrário a importação não será concluída com êxito.  

#### <a name="to-import-task-sequences"></a>Para importar sequências de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Importar Sequência de Tarefas** para iniciar o Assistente Importar Sequência de Tarefas.  

4.  Na página **Geral** , especifique o ficheiro .zip exportado e clique em **Seguinte**.  

5.  Na página **Conteúdo do Ficheiro** , selecione a ação de que necessita para cada objeto que importar. Esta página mostra todos os objetos do Configuration Manager serão importados.  

    -   Se o objeto nunca tiver sido importado, selecione **Criar Novo**.  

    -   Se o objeto tiver sido importado anteriormente, selecione uma das seguintes ações:  

        -   **Ignorar duplicado** (padrão): Esta ação não importa o objeto. Em vez disso, o assistente liga o objeto existente à sequência de tarefas.  

        -   **Substituir**: Essa ação substitui o objeto existente pelo objeto importado. Para aplicações, pode adicionar uma revisão para atualizar a aplicação existente ou criar uma nova aplicação.  

6.  Conclua o assistente.  

 Depois de importar a sequência de tarefas, edite-a para especificar as palavras-passe que estavam na sequência de tarefas original. Por razões de segurança, as palavras-passe não são exportadas.  

##  <a name="BKMK_CreateTSVariables"></a> Criar variáveis de sequência de tarefas para computadores e coleções  
Pode definir variáveis de sequência de tarefas personalizadas para computadores e coleções. As variáveis definidas para um computador são designadas variáveis de sequência de tarefas por computador. As variáveis definidas para uma coleção são designadas variáveis de sequência de tarefas por coleção. Em caso de conflito, as variáveis por computador têm precedência sobre as variáveis por coleção. Isto significa que as variáveis de sequência de tarefas atribuídas a um computador específico possuem automaticamente prioridade sobre as variáveis atribuídas à coleção que contém o computador.  

Por exemplo, se a coleção ABC tiver atribuída uma variável e o computador XYZ, que é um membro da coleção ABC, tiver atribuída uma variável com o mesmo nome, a variável atribuída ao computador XYZ terá prioridade sobre a variável atribuída à coleção ABC.  

Você pode ocultar as variáveis por computador e por coleção para que elas não fiquem visíveis no console do Configuration Manager. Se pretender que deixem de ficar ocultas, tem de as eliminar e redefinir sem selecionar a opção para as ocultar. Quando você usa a opção **não exibir esse valor no console do Configuration Manager**, o valor da variável não é exibido no console do, mas pode ainda ser usado pela sequência de tarefas quando ele é executado.  

> [!WARNING]    
> O **não exibir esse valor no console do Configuration Manager** configuração aplica-se ao console do Configuration Manager, mas os valores das variáveis de ainda são exibidos no arquivo de log de sequência de tarefas (SMSTS. LOG). 

Pode gerir variáveis por computador num site primário ou num site de administração central. Gerenciador de configuração não oferece suporte a mais de 1.000 variáveis atribuídas para um computador.  

> [!IMPORTANT]  
>  Quando utiliza variáveis por coleção para sequências de tarefas, considere o seguinte:  
>   
> - Como as alterações nas coleções são sempre replicadas em toda a hierarquia, quaisquer alterações efetuadas nas variáveis da coleção serão aplicadas não apenas aos membros do site atual, mas a todos os membros da coleção de toda a hierarquia.  
> - Quando elimina uma coleção, esta ação também elimina as variáveis de sequência de tarefas configuradas para a coleção.  

 Utilize os procedimentos seguintes para criar variáveis de sequência de tarefas para um computador ou uma coleção.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>Para criar variáveis de sequência de tarefas para um computador  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda a coleção que contém o computador ao qual pretende adicionar a variável.  

3.  Selecione o computador e clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** , clique no separador **Variáveis** .  

5.  Para cada variável que você deseja criar, clique o **novo** ícone no **< New\> variável** caixa de diálogo caixa e especifique o nome e o valor da variável de sequência de tarefas. Limpar o **não exibir esse valor no console do Configuration Manager** caixa de seleção se você deseja ocultar as variáveis de forma que elas não fiquem visíveis no console do Configuration Manager.  

6.  Depois de ter adicionado todas as variáveis ao computador, clique em **OK**.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>Para criar variáveis de sequência de tarefas para uma coleção  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , selecione a coleção à qual pretende adicionar a variável e clique em **Propriedades**.  

3.  Na caixa de diálogo **Propriedades** , clique no separador **Variáveis da Coleção** .  

4.  Para cada variável que você deseja criar, clique o **novo** ícone no **< New\> variável** caixa de diálogo caixa e especifique o nome e o valor da variável de sequência de tarefas. Limpar o **não exibir esse valor no console do Configuration Manager** caixa de seleção se você deseja ocultar as variáveis de forma que elas não fiquem visíveis no console do Configuration Manager.  

5.  Opcionalmente, especifique a prioridade para o Configuration Manager para usar quando as variáveis de sequência de tarefas são avaliadas.  

6.  Depois de ter adicionado todas as variáveis à coleção, clique em **OK**.  

##  <a name="BKMK_AdditionalActionsTS"></a> Ações adicionais para gerir sequências de tarefas  
 Você pode gerenciar sequências de tarefas usando ações adicionais ao selecionar uma sequência de tarefas.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Para selecionar uma sequência de tarefas para gerir  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos** e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende gerir e selecione uma das opções disponíveis.  

 Utilize a seguinte tabela para obter mais informações sobre algumas das ações adicionais para gerir as sequências de tarefas.  

|Ação|Descrição|  
|------------|-----------------|  
|**Copiar**|Efetua uma cópia da sequência tarefas selecionada. Esta ação pode ser útil quando pretender criar uma nova sequência de tarefas baseada numa sequência de tarefas existente.<br /><br /> Quando efetuar uma cópia de uma sequência de tarefas numa pasta, esta é listada nessa pasta até a atualizar o nó da sequência de tarefas.  Após a atualização, cópia aparece na pasta raiz.|  
|**Desativar**|Desativa a sequência de tarefas para não ser executada nos computadores. As sequências de tarefas desativadas podem ser implementadas nos computadores, mas os computadores não executam a sequência de tarefas enquanto não for ativada.|  
|**Ativar**|Ativa a sequência de tarefas para poder ser executada. Não necessita de voltar a implementar uma sequência de tarefas implementada depois de ser ativada.|  
|**Criar Ficheiro de Conteúdo Pré-configurado**|Inicia o Assistente para Criar Ficheiro de Conteúdo Pré-configurado para pré-configurar o conteúdo da sequência de tarefas. Para obter informações sobre como criar um arquivo de conteúdo pré-configurado, consulte [pré-configurar conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).|  
|**Moverr**|Move a sequência de tarefas selecionada para outra pasta.|  

## <a name="next-steps"></a>Passos seguintes
[Cenários para implementar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md)

