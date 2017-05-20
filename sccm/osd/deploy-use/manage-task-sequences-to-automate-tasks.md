---
title: "Gerir sequências de tarefas para automatizar tarefas | Documentos do Microsoft"
description: "Pode criar, editar, implementar, importar e exportar sequências de tarefas para geri-los no seu ambiente do System Center Configuration Manager."
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
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 113fa73bf0bd1b3b8a4754eb1e96549c520d7995
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>Gerir sequências de tarefas para automatizar tarefas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize sequências de tarefas para automatizar os passos no seu ambiente do System Center Configuration Manager. Estes passos podem implementar uma imagem de sistema operativo num computador de destino, criar e capturar uma imagem de sistema operativo a partir de um conjunto de ficheiros de instalação de sistema operativo, e capturar e restaurar informações de estado do utilizador. Sequências de tarefas na consola do Configuration Manager em **biblioteca de Software** > **sistemas operativos** > **sequência de tarefas**. O **sequência de tarefas** nó, incluindo subpastas que crie, é replicado em toda a hierarquia do Configuration Manager. Para obter informações sobre planeamento, consulte o artigo [considerações sobre planeamento para automatizar tarefas](../plan-design/planning-considerations-for-automating-tasks.md).  

 Utilize as secções seguintes para gerir sequências de tarefas.

##  <a name="BKMK_CreateTaskSequence"></a> Criar sequências de tarefas  
 Crie sequências de tarefas utilizando o Assistente de Criação de Sequência de Tarefas. Este assistente pode criar os seguintes tipos de sequências de tarefas:  

|Tipo de sequência de tarefas|Mais informações|  
|------------------------|----------------------|  
|[Sequência de tarefas para instalar um sistema operativo](create-a-task-sequence-to-install-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para instalar um sistema operativo, bem como a opção para migrar dados de utilizador, incluir atualizações de software e instalar aplicações.|  
|[Sequência de tarefas para atualizar um sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para atualizar um sistema operativo, bem como a opção para incluir atualizações de software e instalar aplicações.|  
|[Sequência de tarefas para capturar um sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para criar e capturar um sistema operativo a partir de um computador de referência. Pode incluir atualizações de software e instalar aplicações no computador de referência antes da captura da imagem.|  
|[Sequência de tarefas para capturar e restaurar o estado do utilizador](create-a-task-sequence-to-capture-and-restore-user-state.md)|Esta sequência de tarefas fornece os passos a adicionar a uma sequência de tarefas existente para capturar e restaurar dados de estado do utilizador.|  
|[Sequência de tarefas para gerir discos rígidos virtuais](use-a-task-sequence-to-manage-virtual-hard-disks.md)|Este tipo de sequência de tarefas contém os passos para criar um VHD, o que inclui a instalar um sistema operativo e aplicações, que pode publicar para o System Center Virtual Machine Manager (VMM) a partir da consola do Configuration Manager.|  
|[Sequência de tarefas personalizada](create-a-custom-task-sequence.md)|Este tipo de sequência de tarefas não adiciona quaisquer passos à sequência de tarefas. Tem de editar a sequência de tarefas e adicionar passos à mesma depois de ser criada.|  

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior, quando uma sequência de tarefas falhar
A partir do Configuration Manager versão 1702, pode sempre voltar à página anterior quando executa uma sequência de tarefas e existir uma falha. Esta versão, era necessário reiniciar a sequência de tarefas quando ocorreu uma falha. Por exemplo, pode utilizar o **anterior** botão nos seguintes cenários:

- Quando um computador arrancar no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas apresentada com uma mensagem que não existem não sequências de tarefas disponível. Agora, pode clicar em **anterior** para procurar novamente sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdos dependentes ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falhará. Pode agora distribuir o conteúdo em falta (se não foi distribuída ainda) ou aguardar que o conteúdo fique disponível nos pontos de distribuição e, em seguida, clique em **anterior** com a pesquisa de sequência de tarefas novamente para o conteúdo.

##  <a name="BKMK_ModifyTaskSequence"></a> Editar uma sequência de tarefas  
 Pode modificar uma sequência de tarefas adicionando ou removendo passos de sequência de tarefas, adicionando ou removendo grupos de sequências de tarefas ou alterando a ordem dos passos. Utilize o procedimento seguinte para modificar uma sequência de tarefas existente.  

> [!IMPORTANT]  
>  Quando edita uma sequência de tarefas criada com o Assistente de Criação de Sequência de Tarefas, o nome do passo pode ser a ação do passo ou o tipo do mesmo. Por exemplo, poderá ver um passo com o nome "Particionar disco 0", que é a ação de um passo do tipo [formatar e particionar disco](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Todos os passos de sequência de tarefas estão documentados pelo respetivo tipo, não necessariamente pelo nome do passo que é apresentado no Editor.  

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

 Para obter uma lista dos passos de sequência de tarefas disponível, consulte o artigo [passos de sequência de tarefas](../understand/task-sequence-steps.md).  

## <a name="configure-high-impact-task-sequence-settings"></a>Configurar definições da sequência de tarefas de impacto elevado
A partir do Configuration Manager versão 1702, pode definir uma sequência de tarefas como de impacto elevado e personalizar as mensagens que os utilizadores recebem quando executam a sequência de tarefas.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de impacto elevado
Utilize o procedimento seguinte para definir uma sequência de tarefas como de impacto elevado.
> [!NOTE]
> Qualquer sequência de tarefas que cumpre determinadas condições é automaticamente definida como impacto elevado. Para obter mais detalhes, consulte o artigo [gerir implementações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **notificação do utilizador** separador, selecione **esta é uma sequência de tarefas de impacto elevado**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implementações de alto risco
Utilize o procedimento seguinte para criar uma notificação personalizada para implementações de impacto elevado.
1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **notificação do utilizador** separador, selecione **utilizar texto personalizado**.
>  [!NOTE]
>  Só é possível definir o texto de notificação do utilizador quando o **esta é uma sequência de tarefas de impacto elevado** está selecionada.

4. Configure as seguintes definições (máximo de 255 carateres para cada caixa de texto):

  **Texto do título de notificação de utilizador**: Especifica o texto azul que apresenta a notificação de utilizador do Centro de Software. Por exemplo, a notificação do utilizador predefinição, esta secção contém algo como "A confirmar que pretende atualizar o sistema operativo neste computador".

  **Texto de mensagem de notificação do utilizador**: Existem três caixas de texto que fornece o corpo da notificação personalizada. Todas as caixas de texto necessitam que o adicione texto.
  - caixa de texto 1º: Especifica o corpo principal do texto, normalmente, que contém instruções para o utilizador. Por exemplo, na notificação de utilizador predefinidas, esta secção contém algo como "atualizar o sistema operativo demorará e o computador poderá reiniciar várias vezes."
  - caixa de texto 2º: Especifica o texto a negrito sob o corpo principal do texto. Por exemplo, na notificação de utilizador predefinidas, esta secção contém algo como "esta atualização no local instala o novo sistema operativo e automaticamente migrada suas definições, aplicações e dados."
  - caixa de texto do 3º: Especifica a última linha do texto sob o texto a negrito. Por exemplo, na notificação de utilizador predefinidas, esta secção contém algo como "clique em instalar para iniciar. Caso contrário, clique em Cancelar."   

  Imaginemos que configura a seguinte notificação personalizada nas propriedades.

    ![Notificação personalizada para uma sequência de tarefas](..\media\user-notification.png)

    Será apresentada a seguinte mensagem de notificação quando o utilizador final é aberta a instalação a partir do Centro de Software.

    ![Notificação personalizada para uma sequência de tarefas](..\media\user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurar propriedades de centro de Software
Utilize o procedimento seguinte para configurar os detalhes da sequência de tarefas apresentada no Centro de Software. Estes detalhes são apenas para informação.  
1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **geral** separador, as seguintes definições para o Centro de Software estão disponíveis:
  - **Reinício necessário**: Permite ao utilizador saber se é necessário um reinício durante a instalação.
  - **Transferir o tamanho (MB)**: Especifica quantos megabytes é apresentada no Centro de Software para a sequência de tarefas.  
  - **Estimado (minutos) o tempo de execução**: Especifica que o estimado tempo de execução em minutos que é apresentada no Centro de Software para a sequência de tarefas.

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

 Pode pré-configurar o conteúdo referenciado na sequência de tarefas. O Configuration Manager cria um ficheiro de conteúdo comprimido e pré-configurado que contém os ficheiros, dependências associadas e metadados associados para o conteúdo que selecionou. Em seguida, poderá importar manualmente os conteúdos para um servidor de sites, site secundário ou ponto de distribuição. Para obter mais informações sobre como pré-configurar ficheiros de conteúdo, consulte o artigo [pré-configurar conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).  

##  <a name="BKMK_DeployTS"></a> Implementar uma sequência de tarefas  
 Utilize o seguinte procedimento para implementar uma sequência de tarefas nos computadores de uma coleção.  

> [!WARNING]  
>  Pode gerir o comportamento de implementações de sequência de tarefas de alto risco. Uma implementação de alto risco é uma implementação que é automaticamente instalada e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tenha um objetivo **Obrigatório** que implemente um sistema operativo é considerada uma implementação de alto risco. Para obter mais informações, consulte o artigo [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

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

    -   **Sequência de tarefas**: Especifique a sequência de tarefas que pretende implementar. Por predefinição, esta caixa apresenta a sequência de tarefas que selecionou.  

    -   **Recolha**: Especifique a coleção que contém os computadores que executarão a sequência de tarefas.  

         Não implemente sequências de tarefas que instalem sistemas operativos em coleções inadequadas, por exemplo a coleção **Todos os Sistemas** . Certifique-se de que a coleção que selecionou apenas contém os computadores nos quais pretende executar a sequência de tarefas.  

        > [!NOTE]  
        >  Ao implementar uma implementação de alto risco, tal como um sistema operativo, o **selecionar coleção** janela apresenta apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site. As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não pode selecionar uma coleção incorporada, como **Todos os Sistemas**. Desmarque **ocultar coleções com um membro da contagem maiores do que a configuração do site tamanho mínimo** para ver todas as coleções personalizadas que contenham menos de clientes que o tamanho máximo configurado. Para obter mais informações, consulte o artigo [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >   
        >  As definições de verificação da implementação são baseadas na associação atual da coleção. Após implementar a sequência de tarefas, a associação da coleção não é reavaliada relativamente às definições de implementação de alto risco.  
        >   
        >  Por exemplo, imaginemos que definiu **predefinido tamanho** a 100 e a **tamanho máximo** a 1000. Quando cria uma implementação de alto risco, a janela **Selecionar Coleção** só apresenta as coleções com menos de cem clientes. Se desmarcar a **ocultar coleções com um membro contam maiores do que a configuração do site tamanho mínimo** definição, a janela será apresentada coleções que contenham menos de 1000 clientes.  
        >   
        >  Quando seleciona uma coleção que contém uma função do site, são aplicáveis as seguintes situações:  
        >   
        >  -   Se a coleção contiver um servidor do sistema de sites e nas definições de verificação de implementação configurar o bloqueio das coleções com servidores do sistema de sites, ocorrerá um erro e não conseguirá continuar.  
        > -   Se a coleção contiver um servidor do sistema de sites e nas definições de verificação da implementação configurar a apresentação de um aviso caso as coleções incluam servidores do sistema de sites, se a coleção ultrapassar o valor do tamanho predefinido ou se a coleção contiver um servidor, o Assistente de Implementação de Software apresentará um aviso de alto risco. Tem de aceitar criar uma implementação de alto risco e é criada uma mensagem de estado de auditoria.  

    -   **Comentários (opcional)**: Especifique informações adicionais que descrevam esta implementação da sequência de tarefas.  

6.  Na página **Definições de Implementação** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Objetivo**: Na lista pendente, escolha uma das seguintes opções:  

        -   **Disponível**: Se a sequência de tarefas for implementada para um utilizador, o utilizador verá a sequência de tarefas publicada no catálogo de aplicações e poderá solicitá-la a pedido. Se a sequência de tarefas for implementada num dispositivo, o utilizador irá vê-la no Centro de Software e pode instalá-la a pedido.  

        -   **Obrigatório**: A sequência de tarefas é implementada automaticamente, de acordo com a agenda configurada. No entanto, um utilizador poderá controlar o estado de implementação da sequência de tarefas (desde que não esteja oculta) e instalar a sequência de tarefas antes do prazo utilizando o Centro de Software.  

    -   **Implementar automaticamente de acordo com a agenda quer exista ou não um utilizador tiver sessão iniciado**: Esta opção não está disponível ao implementar uma sequência de tarefas.  

    -   **Enviar pacotes de reativação**: Se o objetivo da implementação estiver definido como **necessário** e esta opção estiver selecionada, um pacote de reativação será enviado aos computadores antes da instalação da implementação para reativar o computador da suspensão quando for atingido o prazo de instalação. Para poder utilizar esta opção, os computadores e redes terão de estar configurados para Reativação por LAN.  

    -   **Permitir que os clientes numa ligação de Internet limitada transfiram conteúdo após o prazo de instalação, o que pode implicar custos adicionais**: Quando tiver uma sequência de tarefas que instala uma aplicação, mas não implementa um sistema operativo, pode especificar se pretende permitir que os clientes transfiram conteúdos após um prazo de instalação quando estiverem a utilizar ligações à Internet limitadas. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que envia e recebe quando se encontra numa ligação à Internet com tráfego limitado.  

        > [!NOTE]  
        >  Embora uma ligação de Internet limitada possa funcionar para sequências de tarefas que não implementam um sistema operativo, tal não é suportado.  

    -   **Exigir a aprovação do administrador caso os utilizadores solicitem esta aplicação**: Esta opção não está disponível ao implementar uma sequência de tarefas.  

    -   **Disponibilizar à seguinte**: Especifique se a sequência de tarefas está disponível para clientes do Configuration Manager, suportes de dados ou PXE.  

        > [!IMPORTANT]  
        >  Utilize a definição **Apenas suportes de dados e PXE (oculto)** para implementações com sequências de tarefas automatizadas. Selecione **Permitir implementação de sistema operativo autónoma** e defina a variável SMSTSPreferredAdvertID como parte do suporte de dados para que o computador arranque automaticamente para a implementação, sem interação do utilizador. Para obter mais informações sobre as variáveis de sequência de tarefas, consulte o artigo [variáveis incorporadas de sequência de tarefas](../understand/task-sequence-built-in-variables.md)  

7.  Na página **Agendamento** , especifique as seguintes informações e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  Quando um cliente Windows PE é iniciado a partir de um suporte de dados de arranque ou PXE, o cliente não avalia agendas de implementação (iniciar, extinguir ou horas de prazos). Configure apenas agendamentos em implementações para clientes que sejam iniciados a partir do sistema operativo Windows completo. Considere a utilização de outros métodos, como janelas de manutenção, para controlar sequências de tarefas ativas implementadas em clientes iniciados a partir do Windows PE.  

    -   **Agendar quando esta implementação ficará disponível**: Especifique a data e hora em que a sequência de tarefas ficará disponível para ser executada no computador de destino. Se selecionar a caixa de verificação **UTC** , esta definição garantirá que a sequência de tarefas ficará disponível para vários computadores de destino ao mesmo tempo, em vez de em alturas diferentes, de acordo com a hora local dos computadores de destino.  

         Se a hora de início for anterior à hora necessária, o cliente transfere a sequência de tarefas à hora de início que especificou.  

    -   **Agendar quando esta implementação expirará**: Especifique a data e hora em que a sequência de tarefas expira no computador de destino. Se seleciona a caixa de verificação **UTC** , a definição correspondente fará com que a sequência de tarefas expire em vários computadores de destino no mesmo tempo, em vez de tal acontecer em diferentes momentos, de acordo com a hora local dos computadores de destino.  

    -   **Agenda de atribuição**: Especifique quando a sequência de tarefas necessária é executada no computador de destino. Pode adicionar múltiplas agendas.  

         Pode especificar a data e hora em que a agenda é iniciada, se a sequência de tarefas é executada semanalmente, mensalmente ou num intervalo personalizado e se a sequência de tarefas é executada após um registo de eventos como, por exemplo, o início ou o fim de sessão num computador.  

        > [!NOTE]  
        >  Se agendar uma hora de início para uma sequência de tarefas necessária que seja anterior à data e hora em que a sequência de tarefas ficará disponível, o cliente do Configuration Manager transfere a sequência de tarefas à hora de início agendada, mesmo que a sequência de tarefas esteja mais cedo.  

    -   **Comportamento da nova execução**: Especifique quando a sequência de tarefas será novamente executada. Pode especificar uma das seguintes opções.  

        -   **Nunca executar novamente o programa implementado**: A sequência de tarefas não volte a executar no cliente se a sequência de tarefas tiver sido executada anteriormente no cliente. A sequência de tarefas não será novamente executada, mesmo que a respetiva execução inicial tenha falhado ou que os ficheiros de sequência de tarefas tenham sido alterados.  

        -   **Executar sempre novamente o programa**: A sequência de tarefas será sempre novamente executada no cliente quando a implementação estiver agendada, mesmo que a sequência de tarefas foi executada com êxito anteriormente. Esta definição é particularmente útil se utilizar implementações periódicas cuja sequência de tarefas seja regularmente atualizada.  

            > [!IMPORTANT]  
            >  Embora esta opção esteja definida por predefinição, não terá qualquer efeito enquanto não lhe for atribuída uma implementação necessária. As implementações disponíveis podem ser sempre novamente executadas por um utilizador.  

        -   **Executar novamente se a tentativa anterior**: A sequência de tarefas será novamente executada quando a implementação estiver agendada apenas se a sequência de tarefas Falha ao executar anteriormente. Esta definição é particularmente útil para implementações necessárias e permite que a execução das mesmas seja automaticamente repetida, de acordo com a agenda de atribuição, caso a última tentativa de execução não tenha sido concluída com êxito.  

        -   Executar novamente se a tentativa anterior tiver êxito: A sequência de tarefas será novamente executada apenas se tiver sido anteriormente executada com êxito no cliente. Esta definição é útil se utilizar implementações periódicas cuja sequência de tarefas seja regularmente atualizada e cada atualização necessitar que a atualização anterior tenha sido instalada com êxito.  

        > [!NOTE]  
        >  Uma vez que um utilizador pode executar novamente uma sequência de tarefas de implementação, certifique-se de que, antes de implementar uma sequência de tarefas disponível num ambiente de produção, avalia e testa cuidadosamente o que acontece quando um utilizador volta a executar a sequência de tarefas múltiplas vezes.  

8.  Na página **Experiência de Utilizador** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Permitir ao utilizador a executar o programa independentemente das atribuições**: Especifique se o utilizador tem permissão para executar uma sequência de tarefas necessária, independentemente das atribuições de implementação.  

    -   **Mostrar Progresso da sequência de tarefas**: Especifique se o cliente do Configuration Manager apresenta o progresso da sequência de tarefas.  

    -   **Instalação de software**: Especifique se o utilizador tem permissão para instalar o software fora das janelas de manutenção configurada e depois da data agendada.  

    -   **Reinício do sistema (se for necessário para concluir a instalação)**: Especifique se o utilizador tem permissão para reiniciar o computador após uma instalação de software fora de uma janela de manutenção configurada e depois da hora da atribuição.  

    -   **Permitir que a sequência de tarefas executar do cliente na Internet**: Especifique se a sequência de tarefas tem permissão para ser executada num cliente baseado na Internet que o Configuration Manager Deteta na Internet. As operações que instalam software, por exemplo um sistema operativo, não são suportadas por esta definição. Só deve utilizar esta opção para sequências de tarefas genéricas, baseadas em scripts, que executem operações padrão do sistema operativo.  

9. Na página **Alertas** , especifique as definições de alerta pretendidas para esta implementação de sequências de tarefas e, em seguida, clique em **Seguinte**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e, em seguida, clique em **Seguinte**.  

    -   **Opções de implementação**: Especifique uma das seguintes opções:  

        > [!NOTE]  
        >  Se utilizar multicast para implementar um sistema operativo, os conteúdos deverão ser transferidos para os computadores de destino quer à medida que forem necessários ou antes de a sequência de tarefas ser executada.  

        -   Especifique que os clientes devem transferir os conteúdos do ponto de distribuição para o computador de destino, se tal for necessário para a sequência de tarefas.  

        -   Especifique se os clientes deverão transferir todos os conteúdos do ponto de distribuição para o computador de destino antes de a sequência de tarefas ser executada. Esta opção não será apresentada se tiver especificado que a sequência de tarefas estará disponível para implementações com arranque PXE ou com suportes de dados (consulte a página **Definições de Implementação** ).  

        -   Especifique se os clientes deverão executar os conteúdos a partir do ponto de distribuição. Esta opção só estará disponível se todos os pacotes associados à sequência de tarefas estiverem configurados para utilizar uma partilha de pacote no ponto de distribuição. Para permitir que os conteúdos utilizem uma partilha de pacote, consulte o separador **Acesso a Dados** nas **Propriedades** de cada pacote.  

    -   **Se estiver disponível nenhum ponto de distribuição local, utilizar um ponto de distribuição remoto**: Especifique se os clientes podem utilizar pontos de distribuição que se encontram em redes lentas e pouco fiáveis para transferir o conteúdo necessário pela sequência de tarefas.  

11. Conclua o assistente.  

##  <a name="BKMK_ExportImport"></a> Exportar e importar sequências de tarefas  
 Pode exportar e importar sequências de tarefas, com ou sem os objetos a elas associados, como por exemplo uma imagem de sistema operativo, uma imagem de arranque, um pacote de agente do cliente, um pacote de controladores e aplicações que tenham dependências.  

 Pondere os seguintes aspetos ao exportar e importar sequências de tarefas.  

-   As palavras-passe que se encontram armazenadas na sequência de tarefas não são exportadas. Se exportar e importar uma sequência de tarefas que contenha palavras-passe, deverá editar a sequência de tarefas importada e especificar novamente as palavras-passe. Certifique-se de que especifica palavras-passe para [associar domínio ou grupo de trabalho](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [ligar à pasta de rede](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder), e [executar linha de comandos](../understand/task-sequence-steps.md#BKMK_RunCommandLine) ações.  

- Ao exportar uma sequência de tarefas com o **definir variáveis de Dynanmic** passo, são exportados sem valores das variáveis que estão configuradas com a **valor secreto** definição. Tem de reintroduzir os valores para estas variáveis depois de importar a sequência de tarefas.

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

5.  Na página **Conteúdo do Ficheiro** , selecione a ação de que necessita para cada objeto que importar. Esta página mostra todos os objetos do Configuration Manager irá importar.  

    -   Se o objeto nunca tiver sido importado, selecione **Criar Novo**.  

    -   Se o objeto tiver sido importado anteriormente, selecione uma das seguintes ações:  

        -   **Ignorar duplicado** (predefinição): Esta ação não importa o objeto. Em vez disso, o assistente liga o objeto existente à sequência de tarefas.  

        -   **Substituir**: Esta ação substitui o objeto existente pelo objeto importado. Para aplicações, pode adicionar uma revisão para atualizar a aplicação existente ou criar uma nova aplicação.  

6.  Conclua o assistente.  

 Depois de importar a sequência de tarefas, edite-a para especificar as palavras-passe que estavam na sequência de tarefas original. Por razões de segurança, as palavras-passe não são exportadas.  

##  <a name="BKMK_CreateTSVariables"></a> Criar variáveis de sequência de tarefas para computadores e coleções  
 Pode definir variáveis de sequência de tarefas personalizadas para computadores e coleções. As variáveis definidas para um computador são designadas variáveis de sequência de tarefas por computador. As variáveis definidas para uma coleção são designadas variáveis de sequência de tarefas por coleção. Em caso de conflito, as variáveis por computador têm precedência sobre as variáveis por coleção. Isto significa que as variáveis de sequência de tarefas atribuídas a um computador específico possuem automaticamente prioridade sobre as variáveis atribuídas à coleção que contém o computador.  

 Por exemplo, se a coleção ABC tiver atribuída uma variável e o computador XYZ, que é um membro da coleção ABC, tiver atribuída uma variável com o mesmo nome, a variável atribuída ao computador XYZ terá prioridade sobre a variável atribuída à coleção ABC.  

 Pode ocultar as variáveis por computador e por coleção para que não fiquem visíveis na consola do Configuration Manager. Se pretender que deixem de ficar ocultas, tem de as eliminar e redefinir sem selecionar a opção para as ocultar. Quando utiliza a opção **Não apresentar este valor na consola do Configuration Manager**, o valor da variável não é apresentado, mas pode continuar a ser utilizado pela sequência de tarefas quando for executado.  

 Pode gerir variáveis por computador num site primário ou num site de administração central. O Configuration Manager não suporta mais de 1000 variáveis atribuídas para um computador.  

> [!WARNING]  
>  Quando utiliza variáveis por coleção para sequências de tarefas, considere o seguinte:  
>   
>  -   Como as alterações nas coleções são sempre replicadas em toda a hierarquia, quaisquer alterações efetuadas nas variáveis da coleção serão aplicadas não apenas aos membros do site atual, mas a todos os membros da coleção de toda a hierarquia.  
> -   Quando elimina uma coleção, esta ação também elimina as variáveis de sequência de tarefas configuradas para a coleção.  

 Utilize os procedimentos seguintes para criar variáveis de sequência de tarefas para um computador ou uma coleção.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>Para criar variáveis de sequência de tarefas para um computador  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda a coleção que contém o computador ao qual pretende adicionar a variável.  

3.  Selecione o computador e clique em **Propriedades**.  

4.  Na caixa de diálogo **Propriedades** , clique no separador **Variáveis** .  

5.  Para cada variável que pretende criar, clique a **novo** ícone no **< New\> variável** diálogo caixa e especifique o nome e o valor da variável de sequência de tarefas. Limpar o **não apresentar este valor na consola do Configuration Manager** caixa de verificação se pretender ocultar as variáveis, para que não fiquem visíveis na consola do Configuration Manager.  

6.  Depois de ter adicionado todas as variáveis ao computador, clique em **OK**.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>Para criar variáveis de sequência de tarefas para uma coleção  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , selecione a coleção à qual pretende adicionar a variável e clique em **Propriedades**.  

3.  Na caixa de diálogo **Propriedades** , clique no separador **Variáveis da Coleção** .  

4.  Para cada variável que pretende criar, clique a **novo** ícone no **< New\> variável** diálogo caixa e especifique o nome e o valor da variável de sequência de tarefas. Limpar o **não apresentar este valor na consola do Configuration Manager** caixa de verificação se pretender ocultar as variáveis, para que não fiquem visíveis na consola do Configuration Manager.  

5.  Opcionalmente, especifique a prioridade para o Configuration Manager para utilizar quando são avaliadas as variáveis de sequência de tarefas.  

6.  Depois de ter adicionado todas as variáveis à coleção, clique em **OK**.  

##  <a name="BKMK_AdditionalActionsTS"></a> Ações adicionais para gerir sequências de tarefas  
 Pode gerir sequências de tarefas com ações adicionais ao selecionar a sequência de tarefas utilizando o seguinte procedimento.  

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
|**Criar Ficheiro de Conteúdo Pré-configurado**|Inicia o Assistente para Criar Ficheiro de Conteúdo Pré-configurado para pré-configurar o conteúdo da sequência de tarefas. Para obter informações sobre como criar um ficheiro de conteúdo pré-configurado, consulte o artigo [pré-configurar conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content).|  
|**Moverr**|Move a sequência de tarefas selecionada para outra pasta.|  
|**Propriedades**|Abre a caixa de diálogo **Propriedades** da sequência de tarefas selecionada. Utilize esta caixa de diálogo para alterar o comportamento do objeto da sequência de tarefas. No entanto, não é possível alterar os passos da sequência de tarefas utilizando esta caixa de diálogo.|  

## <a name="next-steps"></a>Passos seguintes
[Cenários para implementar sistemas operativos enterprise](scenarios-to-deploy-enterprise-operating-systems.md)

