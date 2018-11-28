---
title: Gerir sequências de tarefas
titleSuffix: Configuration Manager
description: Criar, editar, implementar, importar e exportar sequências de tarefas para geri-los e automatizar tarefas no seu ambiente.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44cfb06c8d92568a4468c1f46b90ceeb259c3c1f
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456639"
---
# <a name="manage-task-sequences-to-automate-tasks-in-configuration-manager"></a>Gerir sequências de tarefas para automatizar tarefas no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize sequências de tarefas para automatizar passos no seu ambiente do Configuration Manager. Estes passos podem implementar uma imagem de sistema operacional num computador de destino, criar e capturar uma imagem de SO de um conjunto de arquivos de instalação do sistema operacional e capturar e restaurar informações de estado do utilizador. Sequências de tarefas estão localizadas na consola do Configuration Manager. Na **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**. O **sequências de tarefas** nó, incluindo as subpastas que criar, é replicado em toda a hierarquia do Configuration Manager. Para obter informações de planeamento, consulte [considerações sobre planeamento para automatizar tarefas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks).  



##  <a name="BKMK_CreateTaskSequence"></a> Criar sequências de tarefas  

 Crie sequências de tarefas utilizando o Assistente de Criação de Sequência de Tarefas. Este assistente pode criar os seguintes tipos de sequências de tarefas:  

|Tipo de sequência de tarefas|Mais informações|  
|------------------------|----------------------|  
|[Sequência de tarefas para instalar um sistema operacional](create-a-task-sequence-to-install-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para instalar um sistema operacional. Ele também inclui opções para migrar dados de utilizador, incluir atualizações de software e instalar aplicações.|  
|[Sequência de tarefas para atualizar um sistema operacional](create-a-task-sequence-to-upgrade-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para atualizar um sistema operacional. Ele também inclui opções para incluir atualizações de software e instalar aplicações.|  
|[Sequência de tarefas para capturar um sistema operacional](create-a-task-sequence-to-capture-an-operating-system.md)|Este tipo de sequência de tarefas cria os passos para criar e capturar um sistema operacional de um computador de referência. Pode incluir atualizações de software e instalar aplicações no computador de referência antes de capturar a imagem.|  
|[Sequência de tarefas para capturar e restaurar o estado do utilizador](create-a-task-sequence-to-capture-and-restore-user-state.md)|Esta sequência de tarefas fornece os passos a adicionar a uma sequência de tarefas existente para capturar e restaurar dados de estado do utilizador.|  
|[Sequência de tarefas personalizada](create-a-custom-task-sequence.md)|Este tipo de sequência de tarefas não adiciona quaisquer passos à sequência de tarefas. Depois de criar esta sequência de tarefas, editá-lo e adicionar passos.|  



## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Regressar à página anterior quando ocorre uma falha de uma sequência de tarefas

Pode retornar a uma página anterior quando executa uma sequência de tarefas e de falha. Nas versões anteriores do Configuration Manager, tinha que reinicie a sequência de tarefas quando ocorreu uma falha. Utilize o **Previous** botão nos seguintes cenários:

- Quando um computador é iniciado no Windows PE, o diálogo de arranque de configuração de sequência de tarefas pode apresentar-se antes da sequência de tarefas está disponível. Quando clicar em seguinte neste cenário, a página final da sequência de tarefas é apresentada uma mensagem que não há nenhum sequências de tarefas disponíveis. Agora, pode clicar **Previous** para procurar novamente sequências de tarefas disponíveis. Pode repetir esse processo até que a sequência de tarefas esteja disponível.  

- Quando executa uma sequência de tarefas, mas pacotes de conteúdos dependentes não estão disponíveis, mas em pontos de distribuição, a sequência de tarefas não funciona. Se o conteúdo em falta não foi distribuído ainda, distribuí-la agora. Em alternativa, aguarde que o conteúdo fique disponível nos pontos de distribuição. Em seguida, clique em **Previous** para que a pesquisa de sequência de tarefas novamente para o conteúdo.



##  <a name="BKMK_ModifyTaskSequence"></a> Editar uma sequência de tarefas  

 Modificar uma sequência de tarefas adicionando ou removendo passos, adicionando ou removendo grupos, ou alterando a ordem dos passos. Utilize o procedimento seguinte para modificar uma sequência já existente:  

> [!IMPORTANT]  
>  Ao editar uma sequência de tarefas que foi criada utilizando o Assistente de criação de sequência de tarefas, o nome do passo pode ser o tipo de passo ou ação. Por exemplo, poderá ver um passo com o nome "Criar partições do disco 0", que é a ação de um passo do tipo [formatar e particionar disco](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk). Todos os passos de sequência de tarefas estão documentados pelo respetivo tipo, não necessariamente pelo nome do passo que é o editor é apresentado.  

#### <a name="to-edit-a-task-sequence"></a>Para editar uma sequência de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende editar.  

4.  No separador **Home Page** , no grupo **Sequência de Tarefas** , clique em **Editar**e efetue qualquer uma das seguintes operações:  

    -   Para adicionar um passo de sequência de tarefas, clique em **adicionar**, selecione o tipo de passo e, em seguida, clique no passo para adicionar. Por exemplo, para adicionar o passo Executar Linha de Comandos, clique em **Adicionar**, selecione **Geral**e, em seguida, clique em **Executar Linha de Comandos**.  

    -   Para adicionar um grupo à sequência de tarefas, clique em **Adicionar**e clique em **Novo Grupo**. Depois de adicionar um grupo, em seguida, pode adicionar passos ao grupo.  

    -   Para alterar a ordem dos passos e grupos na sequência de tarefas, selecione o passo ou grupo que pretende reordenar e, em seguida, utilize o **Mover Item para cima** ou **Mover Item para baixo** ícones. Apenas pode mover um passo ou um grupo de cada vez.  

    -   Para remover um passo ou um grupo, selecione o passo ou o grupo e clique em **Remover**.  

5.  Clique em **OK** para guardar as alterações.  


 Para obter uma lista dos passos de sequência de tarefas disponíveis, consulte [passos de sequência de tarefas](/sccm/osd/understand/task-sequence-steps).  



## <a name="bkmk_prop-general"></a> Configurar as propriedades do Centro de Software

 Utilize o procedimento seguinte para configurar os detalhes para a sequência de tarefas apresentadas no Centro de Software. Esses detalhes são apenas para informação.  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.  

2. Selecione a sequência de tarefas para editar e clique em **propriedades**.  

3. Sobre o **gerais** guia, as seguintes definições para o Centro de Software estão disponíveis:  

  - **Reinício necessário**: Permite ao utilizador saber se é necessário reiniciar durante a instalação.  

  - **Tamanho (MB) de download**: Especifica o número de megabytes são apresentadas no Centro de Software para a sequência de tarefas.  

  - **Estimado (minutos) de tempo de execução**: Especifica que o estimado tempo de execução em minutos, que é apresentado no Centro de Software para a sequência de tarefas.  



## <a name="bkmk_prop-advanced"></a> Configurar as definições de sequência de tarefas avançadas

 Utilize o procedimento seguinte para configurar o comportamento da sequência de tarefas no cliente do Configuration Manager.  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.  

2. Selecione a sequência de tarefas para editar e clique em **propriedades**.  

3. Sobre o **avançadas** separador, estão disponíveis as seguintes definições:  

    - **Executar outro programa primeiro**: Selecione esta opção para executar um programa em outro pacote antes da sequência de tarefas é executado. Por predefinição, esta caixa de verificação está desmarcada. Não precisa de implementar separadamente o programa que especificar para executar primeiro.  

        > [!IMPORTANT]     
        Esta definição aplica-se apenas a sequências de tarefas que são executados em todo o sistema operacional. Se iniciar a sequência de tarefas utilizando suportes de dados de arranque ou PXE, o Gestor de configuração ignora esta definição.  

        - **Pacote**: Navegue para o pacote que contém o programa seja executado antes desta sequência de tarefas.  

        - **Programa**: Selecione o programa seja executado antes desta sequência de tarefas.  

        > [!NOTE]    
        > Se o programa selecionado não for executado num cliente, a sequência de tarefas não é executado. Se o programa selecionado é executado com êxito, ele não é executado novamente, mesmo que a sequência de tarefas será novamente executada no mesmo cliente.  
 
    - **Desativar esta sequência de tarefas nos computadores em que é implementada**: Se selecionar esta opção, o Configuration Manager desativa temporariamente as implementações que contêm esta sequência de tarefas. Esta operação também remove a sequência de tarefas da lista de implementações disponíveis para ser executada. A sequência de tarefas não é executado até que o ative. Por predefinição, esta opção estiver desmarcada.  

    - **Tempo de execução máximo permitido**: Especifica o tempo máximo em minutos que espera que a sequência de tarefas para executar no computador de destino. Utilize um número inteiro igual ou maior que zero. Por predefinição, este valor é de 120 minutos.  

        > [!IMPORTANT]    
        > Se estiver a utilizar janelas de manutenção para a coleção em que pretende implementar esta sequência de tarefas, poderá ocorrer um conflito se o **máximo de tempo de execução permitido** é superior à janela de manutenção agendada. Se definir o tempo de execução máximo **0**, a sequência de tarefas é iniciada durante a janela de manutenção. Ele continua a ser executado até concluir ou falhar depois de fechar a janela de manutenção. Como resultado, as sequências de tarefas com um tempo máximo de execução definido como **0** possam ser executadas passou o final de suas janelas de manutenção. Se definir o máximo tempo de execução para um período específico (diferente de zero) que excede o comprimento de qualquer janela de manutenção disponível, em seguida, a sequência de tarefas não é executado. Para obter mais informações, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).  
 
       Se definir o valor como **0**, o tempo máximo de execução permitido como o Configuration Manager avalia **12** horas (720 minutos) para monitorizar o progresso. No entanto, a sequência de tarefas é iniciada, desde que a duração de contagem regressiva não excede o valor da janela de manutenção.  

       > [!NOTE]    
       > Quando atingir o tempo máximo de execução, se definir a opção para **executados com direitos administrativos**e não defina a opção como **permitir que os utilizadores interajam com este programa**, em seguida, o Configuration Manager interrompe o sequência de tarefas. Se a sequência de tarefas em si não está parada, o Configuration Manager para a monitorização da sequência de tarefas depois de atingir o máximo permitido tempo de execução.  

    - **Utilizar uma imagem de arranque**: Utilize a imagem de arranque selecionada quando a sequência de tarefas é executada. Clique em **procurar** para selecionar uma imagem de arranque diferentes. Desmarque esta opção para desativar a utilização da imagem de arranque selecionada quando a sequência de tarefas é executada.  

    - **Esta sequência de tarefas pode ser executado em qualquer plataforma**: Se selecionar esta opção, o Configuration Manager não verifica o tipo de plataforma de computador de destino quando a sequência de tarefas é executada. Esta opção está selecionada por predefinição.  

    - **Esta sequência de tarefas só pode ser executado nas plataformas de cliente especificado**: Esta opção especifica os processadores, versões de SO e pacotes de serviço no qual pode executar esta sequência de tarefas. Quando seleciona esta opção, selecione pelo menos uma plataforma na lista. Por predefinição, não existem plataformas são selecionadas. O Configuration Manager utiliza estas informações quando é avalia a quais computadores de destino numa coleção de recebem a sequência de tarefas implementada.  

        > [!NOTE]    
        > Quando executa uma sequência de tarefas a partir do suporte de dados ou PXE, o Gestor de configuração ignora esta opção. A sequência de tarefas é executado como se a opção **este programa pode ser executado em qualquer plataforma** está selecionada.  



## <a name="configure-high-impact-task-sequence-settings"></a>Configurar as definições de sequência de tarefas de impacto elevado

 Configurar uma sequência de tarefas como elevado impacto e personalizar as mensagens que os utilizadores recebem quando executam a sequência de tarefas.


### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de alto impacto

 Utilize o procedimento seguinte para definir uma sequência de tarefas como alto impacto.

> [!NOTE]    
> Qualquer sequência de tarefas que cumpre determinadas condições automaticamente é definida como alto impacto. Para obter mais informações, consulte [gerir implementações de alto risco](/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.  

2. Selecione a sequência de tarefas para editar e clique em **propriedades**.  

3. Sobre o **notificação do utilizador** separador, selecione **trata de uma sequência de tarefas de alto impacto**.  


### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação para implementações de alto risco

 Utilize o procedimento seguinte para criar uma notificação para implementações de alto impacto.

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.  

2. Selecione a sequência de tarefas para editar e clique em **propriedades**.  

3. Sobre o **notificação do utilizador** separador, selecione **utilizar texto personalizado**.  

    >  [!NOTE]    
    >  Apenas pode definir o texto de notificação do utilizador ao selecionar a opção **esta é uma sequência de tarefas de alto impacto**.  

4. Configure as seguintes definições:  

    > [!Note]  
    > Cada caixa de texto tem um limite máximo de 255 carateres.  

    **Texto do cabeçalho de notificação de utilizador**: Especifica o texto azul que apresenta a notificação de utilizador do Centro de Software. Por exemplo, na notificação de utilizador padrão, esta secção contém "Confirmar que pretende atualizar o sistema operativo neste computador."  

    **Texto de mensagem de notificação do utilizador**: Existem três caixas de texto que fornecem o corpo da notificação personalizado. Todas as caixas de texto requerem a adição de texto.  

    - Primeira caixa de texto: Especifica o corpo principal do texto, normalmente, que contém instruções para o utilizador. Por exemplo, na notificação de utilizador padrão, esta secção contém "atualização do sistema operativo demora algum tempo e o computador poderá reiniciar várias vezes."  

    - Segunda caixa de texto: Especifica o texto em negrito no corpo principal do texto. Por exemplo, na notificação de utilizador padrão, esta secção contém "esta atualização no local instala o novo sistema operativo e migra automaticamente as suas aplicações, dados e definições."  

    - Terceira caixa de texto: Especifica a última linha de texto sob o texto em negrito. Por exemplo, na notificação de utilizador padrão, esta secção contém "clique em instalar para iniciar. Caso contrário, clique em Cancelar."   

#### <a name="example"></a>Exemplo
Digamos que configura a seguinte notificação personalizada nas propriedades.

![Separador de notificação do utilizador personalizado de propriedades de sequência de tarefas](..\media\user-notification.png)

A seguinte mensagem de notificação apresentada quando o utilizador final abre a instalação do Centro de Software.

![Notificação de sequência de tarefas personalizada para o utilizador final no Centro de Software](..\media\user-notification-enduser.png)



##  <a name="BKMK_DistributeTS"></a> Distribuir conteúdo referenciado por uma sequência de tarefas  

 Antes dos clientes executam uma sequência de tarefas que referencie conteúdos, distribua esse conteúdo aos pontos de distribuição. Em qualquer altura, pode selecionar a sequência de tarefas e distribuir o respetivo conteúdo para criar uma nova lista de pacotes de referência para distribuição. Se efetuar alterações à sequência de tarefas com conteúdo atualizado, redistribuir o conteúdo antes de ser disponibilizada aos clientes. Utilize o seguinte procedimento para distribuir os conteúdos que são referenciados por uma sequência de tarefas.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Para distribuir conteúdo referenciado a pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende distribuir.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Distribuir Conteúdo** para iniciar o Assistente para Distribuir Conteúdo.  

5.  Sobre o **gerais** página, certifique-se de que a sequência de tarefas correta está selecionada para distribuição. Em seguida, clique em **Seguinte**.  

6.  Na página **Conteúdo** , confirme os conteúdos a distribuir, por exemplo a imagem de arranque referenciada pela sequência de tarefas e, em seguida, clique em **Seguinte**.  

7.  Sobre o **destino do conteúdo** , especifique as coleções, ponto de distribuição ou grupo de pontos de distribuição em que pretende distribuir os conteúdos da sequência de tarefas. Em seguida, clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  Se a sequência de tarefas que selecionadas referências de conteúdo que já tenham sido distribuído para um ponto de distribuição específico, o assistente não lista esse ponto de distribuição.  

8.  Conclua o assistente.  


 Também pode pré-configurar o conteúdo referenciado na sequência de tarefas. O Configuration Manager cria um ficheiro de conteúdo comprimido e pré-configurado que contém os ficheiros, dependências associadas e metadados associados para o conteúdo que selecionar. Em seguida, importar manualmente o conteúdo num servidor de site, site secundário, ou ponto de distribuição. Para obter mais informações sobre como pré-configurar ficheiros de conteúdo, consulte [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  



##  <a name="BKMK_DeployTS"></a> Implementar uma sequência de tarefas  

 Utilize o seguinte procedimento para implementar uma sequência de tarefas nos computadores de uma coleção.  

> [!WARNING]  
>  Pode gerir o comportamento de implementações de sequência de tarefas de alto risco. Uma implementação de alto risco é uma implementação que é automaticamente instalada e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tenha um objetivo **necessário** que implementa um sistema operacional é considerada uma implementação de alto risco. Para obter mais informações, consulte [definições para gerir implementações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

> [!NOTE]  
>  As mensagens de estado para a implementação de sequência de tarefas são apresentadas na janela da mensagem num site primário, mas eles não são apresentados no site de administração central.  

#### <a name="to-deploy-a-task-sequence"></a>Para implementar uma sequência de tarefas    

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende implementar.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

    > [!NOTE]  
    >  Se **Deploy** não estiver disponível, a sequência de tarefas tem uma referência que não é válida. Corrija a referência e tente implementar a sequência de tarefas novamente.  

5.  Na página **Geral** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Sequência de tarefas**: Especifique a sequência de tarefas para implementar. Por predefinição, esta caixa apresenta a sequência de tarefas selecionada.  

    -   **Coleção**: Selecione a coleção que contenha os computadores a executar a sequência de tarefas.  

         Não implemente uma sequência de tarefas que instala um sistema operacional em coleções inadequadas, por exemplo, uma coleção de todos os servidores do Centro de dados. Certifique-se de que a coleção selecionada contém apenas os computadores que pretende executar a sequência de tarefas.  

        > [!NOTE]  
        >  Ao implementar uma implementação de alto risco, como um sistema operacional, o **selecionar coleção** janela exibe apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site. As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não é possível selecionar uma coleção incorporada, como **todos os sistemas**. Desmarque **ocultar coleções com um membro contagem superiores à configuração de tamanho mínimo do site** para ver todas as coleções personalizadas que incluem menos clientes do que o tamanho máximo configurado. Para obter mais informações, consulte [definições para gerir implementações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  
        >   
        >  As definições de verificação da implementação são baseadas na associação atual da coleção. Depois de implementar a sequência de tarefas, o Configuration Manager não reavaliar a associação da coleção para que as definições de implementação de alto risco.  
        >   
        >  Por exemplo, digamos que definiu **tamanho predefinido** para 100 e o **tamanho máximo** a 1000. Quando cria uma implementação de alto risco, o **selecionar coleção** janela apresenta apenas as coleções com menos de 100 clientes. Se desmarcar a **ocultar coleções com um membro contagem superiores à configuração de tamanho mínimo do site** definição, a janela apresenta coleções que contenham menos de 1 000 clientes.  
        >   
        >  Quando seleciona uma coleção que contém uma função de site, o seguinte comportamento aplica-se:  
        >   
        >  -   Se a coleção contiver um servidor de sistema de sites e configurou as definições de verificação de implementação para o bloqueio das coleções com servidores de sistema de sites, em seguida, ocorrerá um erro. Não é possível continuar a criação da implementação.  
        > -   Se um dos seguintes critérios aplica-se, em seguida, o Assistente de implementação de Software apresenta um aviso de alto risco. Para continuar, terá de aceitar criar uma implementação de alto risco. O site gera uma mensagem de estado de auditoria.  
        >     - Se a coleção contiver um servidor de sistema de sites e configurou as definições de verificação de implementação para o avisar de coleções com servidores de sistema de sites
        >     - Se a coleção excede o valor do tamanho predefinido
        >     - Se a coleção contiver um servidor  

    - **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**: Store o conteúdo da sequência de tarefas no grupo de pontos de distribuição de predefinido da coleção. Se ainda não associado a coleção selecionada um grupo de pontos de distribuição, esta opção está a cinzento.  

    - **Distribuir automaticamente o conteúdo para dependências**: Se qualquer conteúdo referenciado tem dependências, o site também envia conteúdo dependente para pontos de distribuição.  

    - **Pré-transferir conteúdos para esta sequência de tarefas**: Para obter mais informações, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

    - **Selecione o modelo de implementação**: A partir do Configuration Manager versão 1802,<!--1357391--> pode guardar e especifique um modelo de implementação para uma sequência de tarefas.     

         > [!IMPORTANT]  
         > Na versão 1802 de versão do Configuration Manager, alguns itens não são guardadas no modelo.  <!--510610--> Certifique-se de que aplicar os seguintes itens quando executa o Assistente de implementação:  
         > - Instalação de software 
         > - Agendamento 
         > - Pré-transferir conteúdo
 
    -   **Comentários (opcional)**: Especifique informações adicionais que descrevam esta implementação da sequência de tarefas.  

6.  Na página **Definições de Implementação** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Objetivo**: Na lista pendente, escolha uma das seguintes opções:  

        -   **Disponível**: O utilizador verá a sequência de tarefas no Centro de Software e pode instalá-la a pedido.  

        -   **Necessário**: O Configuration Manager é executado automaticamente a sequência de tarefas, de acordo com a agenda configurada. Se a sequência de tarefas não está oculto, um utilizador ainda pode controlar o estado de implementação. Eles também podem utilizar o Centro de Software para instalar a sequência de tarefas antes do prazo.  

        >  [!NOTE]  
        >  Se vários utilizadores tem sessão iniciados no dispositivo, implementações de sequência de pacotes e tarefas não podem aparecer no Centro de Software.  

    -   **Tornar disponível para o seguinte**: Especifique se a sequência de tarefas está disponível para um dos seguintes tipos:  
        - Apenas os clientes do Configuration Manager  
        - Clientes do Configuration Manager, suportes de dados e PXE  
        - Apenas suportes de dados e PXE  
        - Apenas suportes de dados e PXE (oculto)  

        > [!IMPORTANT]  
        >  Utilize a definição **Apenas suportes de dados e PXE (oculto)** para implementações com sequências de tarefas automatizadas. Para que o computador arranque automaticamente para a implantação sem interação do utilizador, selecione **permitir a implementação do sistema operativo autónoma** e defina a **SMSTSPreferredAdvertID** variável como parte das suporte de dados. Para obter mais informações sobre as variáveis de sequência de tarefas, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables#SMSTSPreferredAdvertID).  

    -   **Enviar pacotes de reativação**: Se a implementação for **necessário** e selecionar esta opção, o site envia um pacote de reativação para computadores antes do cliente é executada a implementação. Este pacote reativa o computador da suspensão quando for atingido o prazo de instalação. Antes de utilizar esta opção, os computadores e redes devem ser configurados para reativação por LAN. Para obter mais informações, consulte [planear como reativar clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

    -   **Permitir que os clientes numa ligação de Internet limitada para transferir conteúdo após o prazo de instalação, o que pode implicar custos adicionais**: Esta opção só está disponível para **necessário** implementações. Quando tiver uma sequência de tarefas personalizado que instala uma aplicação, mas não implementa um sistema operacional, pode especificar se pretende permitir que os clientes transfiram conteúdos após um prazo de instalação quando estiverem a utilizar de ligações à internet limitadas. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que utilize quando estiver a utilizar uma ligação de internet com tráfego limitado.  

        > [!NOTE]  
        >  Apesar de utilizar uma ligação de internet limitada possa funcionar para sequências de tarefas que não implementar um sistema operacional, não é suportada.  

7.  Na página **Agendamento** , especifique as seguintes informações e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  Quando um cliente do Windows PE é iniciado a partir do suporte de dados de arranque ou PXE, o cliente não avalia agendas de implementação. Estas agendas incluem início, expirarem e horas de prazos. Configure apenas agendamentos em implementações em clientes iniciados do sistema operacional Windows completo. Considere a utilização de outros métodos, como janelas de manutenção, para controlar sequências de tarefas ativas implementadas em clientes iniciados a partir do Windows PE.  

    -   **Agendar quando esta implementação ficará disponível**: Especifique a data e hora em que a sequência de tarefas ficará disponível para ser executada no computador de destino. Quando seleciona a **UTC** caixa de verificação, a sequência de tarefas está disponível para vários computadores ao mesmo tempo. Caso contrário, a implementação está disponível em diferentes momentos, de acordo com a hora local em cada computador.  

         Se a hora de início é anterior à hora necessária, o cliente transfere o conteúdo da sequência de tarefas à hora de início.  

    -   **Agendar quando esta implementação expirará**: Especifique a data e hora em que a sequência de tarefas expira no computador de destino. Quando seleciona a **UTC** caixa de verificação, a sequência de tarefas expire em vários computadores de destino ao mesmo tempo. Caso contrário, a implementação expira em diferentes momentos, de acordo com a hora local em cada computador.  

    -   **Agenda da atribuição**: Para uma **necessário** implementação, especifique quando o cliente executa a sequência de tarefas. Pode adicionar múltiplas agendas. A agenda de atribuição pode ter uma das seguintes configurações:   
        - Uma data e hora específicas  
        - Padrão de periodicidade personalizadas, semanal ou mensal  
        - Assim que possível  
        - O logon ou logoff de eventos  

        > [!NOTE]  
        >  Se agendar uma hora de início para uma implementação necessária que seja anterior à data e hora em que a sequência de tarefas ficará disponível, o cliente do Configuration Manager transfere o conteúdo à hora de início atribuído. Este comportamento ocorre mesmo que agendado a sequência de tarefas para estar disponível num momento posterior.<!--SCCMDocs issue 777-->  

    -   **Comportamento da nova execução**: Especifique quando a sequência de tarefas volta a executar. Selecione uma das seguintes opções:  

        -   **Nunca executar novamente o programa implementado**: Se o cliente tiver sido anteriormente executada a sequência de tarefas, ele não volta a executar. A sequência de tarefas não volta a executar, mesmo que tenha falhado ou os ficheiros de sequência de tarefas foram alterados.  

        -   **Executar sempre novamente o programa**: A sequência de tarefas volta sempre executar no cliente quando a implementação estiver agendada. Volta executar, mesmo que a sequência de tarefas já foi executada com êxito. Esta definição é útil quando utilizar implementações periódicas no qual a sequência de tarefas seja regularmente atualizada.  

            > [!IMPORTANT]  
            >  Esta opção está selecionada por predefinição. No entanto, não tem efeito até que o atribua uma implementação necessária. Um utilizador pode sempre voltar a executar as implementações disponíveis.  

        -   **Executar novamente se a tentativa anterior falhar**: A sequência de tarefas volta executar quando a implementação estiver agendada, apenas se anteriormente não foi executado. Esta definição é útil para uma implementação necessária. Se a última tentativa de execução foi concluída com êxito, ele tenta automaticamente voltar a executar, de acordo com a agenda de atribuição.  

        -   **Executar novamente se tiver êxito tentativa anterior**: A sequência de tarefas volta executar apenas se tiver sido executado com êxito no cliente. Esta definição é útil se utilizar implementações periódicas cuja sequência de tarefas seja regularmente atualizada e cada atualização necessitar que a atualização anterior tenha sido instalada com êxito.  

        > [!NOTE]  
        >  Um utilizador pode voltar a executar uma implementação de sequência de tarefas disponíveis. Antes de implementar uma sequência de tarefas disponível num ambiente de produção, teste primeiro o que acontece se um utilizador volta executar a sequência de tarefas múltiplas vezes.  

8.  Na página **Experiência de Utilizador** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Permitir que o utilizador executar o programa independentemente das atribuições**: Especifica se um usuário pode executar uma implementação necessária fora do agendamento de atribuição. Esta opção está sempre habilitada para as implementações disponíveis.   

    -   **Mostrar Progresso da sequência de tarefas**: Especifique se o cliente do Configuration Manager apresenta o progresso da sequência de tarefas.  

    -   **Instalação de software**: Especifique se o utilizador tem permissão para instalar o software fora de uma janela de manutenção configuradas e depois da data agendada.  

    -   **Reinício do sistema (se for necessário para concluir a instalação)**: Especifique se o utilizador tem permissão para reiniciar o computador após uma instalação de software fora de uma janela de manutenção configuradas e depois da hora da atribuição.  

    - **Processamento para dispositivos Windows Embedded do filtro de escrita**: Esta definição controla o comportamento de instalação em dispositivos Windows Embedded que estão ativados com um filtro de escrita. Escolha a opção para consolidar as alterações no prazo de instalação ou durante uma janela de manutenção. Quando seleciona esta opção, é necessário um reinício e as alterações sejam mantidas no dispositivo. Caso contrário, o aplicativo é instalado para a sobreposição temporária e confirmado posteriormente. Quando implementa uma sequência de tarefas num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada.  

    -   **Permitir que a sequência de tarefas executar o cliente na Internet**: Especifique se a sequência de tarefas pode ser executada num cliente baseado na internet. As operações que instalam software, como um sistema operacional, não são suportadas com esta definição. Utilize esta opção apenas para sequências de tarefas genéricas, baseadas em scripts que executam operações no sistema operacional padrão.  

         - A partir da versão 1802, esta definição é suportada para implementações de uma sequência de tarefa de atualização in-loco do Windows 10 para clientes baseados na internet através do gateway de gestão na cloud. Para obter mais informações, consulte [atualização in-loco de implementar o Windows 10 através do CMG](#deploy-windows-10-in-place-upgrade-via-cmg).    

9. Na página **Alertas** , especifique as definições de alerta pretendidas para esta implementação de sequências de tarefas e, em seguida, clique em **Seguinte**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e, em seguida, clique em **Seguinte**.  

    -   **Opções de implementação**: Especifique uma das seguintes opções:  

        > [!NOTE]  
        >  Quando for utilizado multicast para implementar um sistema operacional, transferir o conteúdo para os computadores, conforme necessário ou antes da sequência de tarefas é executado.  

        - **Transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução**: Especifique que os clientes transferem conteúdo do ponto de distribuição, conforme necessário pela sequência de tarefas. O cliente inicia a sequência de tarefas. Quando um passo na sequência de tarefas necessita de conteúdo, é transferido antes do passo for executado.  

        - **Transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas**: Especifique que os clientes transferem todo o conteúdo do ponto de distribuição antes da sequência de tarefas é executado. Se fizer a sequência de tarefas disponível para implementações de suportes de dados de arranque PXE ou sobre o **definições de implementação** página, esta opção não é mostrada.  

        - **Aceder ao conteúdo diretamente a partir de um ponto de distribuição quando necessário pela sequência de tarefas em execução**: Especifique se os clientes deverão executar os conteúdos a partir do ponto de distribuição. Esta opção só está disponível quando ativa a todos os pacotes associados à sequência de tarefas a utilizar uma partilha de pacote no ponto de distribuição. Para permitir que os conteúdos utilizem uma partilha de pacote, consulte o separador **Acesso a Dados** nas **Propriedades** de cada pacote.  

    -   **Se estiver disponível nenhum ponto de distribuição local, utilizar um ponto de distribuição remoto**: Especifique se os clientes podem utilizar pontos de distribuição de um grupo de limite vizinho para transferir o conteúdo exigido pela sequência de tarefas.  

    - **Permitir aos clientes utilizar pontos de distribuição do grupo de limite de site predefinido**: Especifique se os clientes devem transferir conteúdo de um ponto de distribuição no grupo de limite predefinido de site, quando não está disponível a partir de um ponto de distribuição nos grupos de limites atual ou vizinhança.  

        > [!Note]  
        > A partir da versão 1810, quando um dispositivo é executada uma sequência de tarefas e tem de adquirir o conteúdo, ele usa comportamentos de grupo de limites semelhantes para o cliente do Configuration Manager. Para obter mais informações, consulte [grupos de limites suporte a sequência de tarefas](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).<!--1359025-->  

11. A partir do Configuration Manager 1802, no **resumo** separador, clique em **guardar como modelo** se pretender guardar as definições para utilizar novamente. Forneça um nome para o modelo, selecione as definições para guardar.  

12. Conclua o assistente.  


### <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Implementar atualização in-loco do Windows 10 através do CMG
<!-- 1357149 -->

A partir da versão 1802, a sequência de tarefas de atualização in-loco do Windows 10 suporta a implementação para clientes baseados na internet geridos através da [gateway de gestão da nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG). Esta capacidade permite aos usuários remotos mais facilmente atualizar para o Windows 10, sem terem de se ligar à intranet. 

Certifique-se de todo o conteúdo referenciado pela sequência de tarefas de atualização in-loco é distribuído para um [ponto de distribuição da nuvem](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Caso contrário, os dispositivos não é possível executar a sequência de tarefas.

Quando implementa uma sequência de tarefas de atualização, utilize as seguintes definições:

- **Permitir que a sequência de tarefas executar o cliente na Internet**, no separador experiência de utilizador da implementação.  

- **Transferir todo o conteúdo localmente antes de iniciar a sequência de tarefas**, no separador de pontos de distribuição da implantação. Outras opções, como **transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução** não funcionam neste cenário. O motor de sequência de tarefas é atualmente não é possível obter o conteúdo a partir de um ponto de distribuição de nuvem. O cliente do Configuration Manager tem de transferir o conteúdo do ponto de distribuição de cloud antes de iniciar a sequência de tarefas.  

- (*Opcional*) **pré-transferir conteúdos para esta sequência de tarefas**, na guia Geral da implantação. Para obter mais informações, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  



##  <a name="BKMK_ExportImport"></a> Exportar e importar sequências de tarefas  

 Pode exportar e importar sequências de tarefas, com ou sem seus objetos relacionados. Este conteúdo referenciado inclui os seguintes objetos:  
 - Imagens do sistema operacional  
 - Imagens de arranque  
 - Pacotes de como o cliente instalam pacote  
 - Pacotes de controladores  
 - Aplicações com dependências  


 Considere os seguintes pontos ao exportar e importar sequências de tarefas:  

 - O Configuration Manager não exportar as palavras-passe na sequência de tarefas. Se exportar e importar uma sequência de tarefas que contém as palavras-passe, edite a sequência de tarefas importada Reintroduza as palavras-passe. Reveja os seguintes passos que podem incluir uma palavra-passe:  
    - [Associar domínio ou grupo de trabalho](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup)  
    - [Ligar à pasta de rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  
    - [Executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

 - Ao exportar uma sequência de tarefas com o **definir variáveis dinâmicas** passo, o Configuration Manager não exportar a valores de variáveis que configurar com o **valor secreto** definição. Reintroduza os valores para estas variáveis, depois de importar a sequência de tarefas.  

 - Quando tiver vários sites primários, importe sequências de tarefas no site de administração central.  


### <a name="to-export-task-sequences"></a>Para exportar sequências de tarefas  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione as sequências de tarefas que pretende exportar. Se selecionar mais do que uma sequência de tarefas, eles são todos armazenados num arquivo de exportação.  

4.  No separador **Início** , no grupo **Sequência de Tarefas** , clique em **Exportar** para iniciar o Assistente de Criação de Sequência de Tarefas.  

5.  Na página **Geral** , especifique as seguintes definições e clique em **Seguinte**.  

    -   Na caixa **Ficheiro** , especifique a localização e o nome do ficheiro de exportação. Se introduzir diretamente o nome do ficheiro, certifique-se de que inclui a extensão .zip no nome do ficheiro. Se navegar para o ficheiro de exportação, o assistente adicionará automaticamente esta extensão de nome de ficheiro.  

    -   Se não pretender exportar as dependências de sequência de tarefas, desmarque a opção para **exportar todas as dependências de sequência de tarefas**. Por predefinição, o assistente verifica se existem todos os objetos relacionados e exporta-os juntamente com a sequência de tarefas. Estas dependências incluem qualquer para aplicações.  

    -   Se não quiser copiar o conteúdo da origem do pacote para a localização de exportação, desmarque a opção para **exportar todo o conteúdo para as dependências e sequências de tarefas selecionadas**. Se selecionar esta opção, o Assistente para importar sequência de tarefas utiliza o caminho de importação como a nova localização de origem do pacote.  

    -   Na caixa **Comentários do administrador** , adicione uma descrição das sequências de tarefas a exportar.  

6.  Conclua o assistente.  


 O assistente cria os seguintes ficheiros de saída:  

-   Se não exportar conteúdos: um ficheiro. zip.  

-   Se não exportar conteúdos: um ficheiro .zip e uma pasta designada *exportar*_files, em que *exportar* corresponde ao nome do ficheiro .zip que contém os conteúdos exportados.  


 Se incluir conteúdos ao exportar uma sequência de tarefas, certifique-se de que copia o ficheiro. zip e o *exportar*pasta Files, ou a importação falhará.  


### <a name="to-import-task-sequences"></a>Para importar sequências de tarefas  

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


 Depois de importar a sequência de tarefas, edite-a para especificar as palavras-passe que estavam na sequência de tarefas original. Por motivos de segurança, as palavras-passe não são exportadas.  



##  <a name="BKMK_CreateTSVariables"></a> Criar variáveis de sequência de tarefas para computadores e coleções  

 Pode definir variáveis de sequência de tarefas personalizadas para computadores e coleções. As variáveis definidas para um computador são designadas variáveis de sequência de tarefas por computador. As variáveis definidas para uma coleção são designadas variáveis de sequência de tarefas por coleção. Se houver um conflito, as variáveis por computador têm precedência sobre as variáveis por coleção. Este comportamento significa que as variáveis de sequência de tarefas que são atribuídas automaticamente a um computador específico tem prioridade sobre as variáveis que estão atribuídos à coleção que contenha o computador.  

 Por exemplo, o computador XYZ é um membro da coleção ABC. Atribuir MyVariable à coleção ABC com um valor de 1. Também atribuir MyVariable ao computador XYZ com um valor de 2. A variável que é atribuída ao computador XYZ terá prioridade a variável que está atribuída à coleção ABC. Quando uma sequência de tarefas com esta variável é executado no computador XYZ, MyVariable tem um valor de 2. 

 Pode ocultar as variáveis por computador e por coleção para que não estão visíveis na consola do Configuration Manager. Quando utiliza a opção **não apresentar este valor na consola do Configuration Manager**, o valor da variável não for apresentado na consola do. A variável ainda pode ser utilizada pela sequência de tarefas quando for executado. Se já não pretender que essas variáveis como ocultas, eliminá-los primeiro. Em seguida, redefina as variáveis sem selecionar a opção para ocultá-los.  

 > [!WARNING]    
 > O **não apresentar este valor na consola do Configuration Manager** definição aplica-se apenas a consola do Configuration Manager. Os valores para as variáveis ainda são apresentados no ficheiro de registo de sequência de tarefas (SMSTS. REGISTO). 

 Pode gerir variáveis por computador num site primário ou num site de administração central. O Configuration Manager não suporta mais de 1000 variáveis atribuídas para um computador.  

> [!IMPORTANT]  
>  Quando utiliza variáveis por coleção para sequências de tarefas, considere os seguintes comportamentos:  
>   
> - As alterações nas coleções são sempre replicadas em toda a hierarquia. Aplicam-se todas as alterações que fizer às variáveis de coleção não apenas aos membros do site atual, mas a todos os membros da coleção em toda a hierarquia.  
>  
> - Quando elimina uma coleção, esta ação também elimina as variáveis de sequência de tarefas que configurou para a coleção.  


### <a name="to-create-task-sequence-variables-for-a-computer"></a>Para criar variáveis de sequência de tarefas para um computador  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na **ativos e compatibilidade** área de trabalho, selecione a **dispositivos** nó.  

3.  Selecione o computador de destino e clique em **propriedades**.  

4.  Na caixa de diálogo **Propriedades** , clique no separador **Variáveis** .  

5.  Para cada variável que pretende criar, clique a **New** ícone. Especifique a **Name** e **valor** de variável de sequência de tarefas. Se pretender ocultar a variável para que esta não estiver visível na consola do Configuration Manager, selecione a opção **não apresentar este valor na consola do Configuration Manager**.  

6.  Depois de adicionar todas as variáveis para as propriedades do computador, clique em **OK**.  


### <a name="to-create-task-sequence-variables-for-a-collection"></a>Para criar variáveis de sequência de tarefas para uma coleção  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na **ativos e compatibilidade** área de trabalho, selecione a **coleções de dispositivos** nó. Selecione a coleção de destino e clique em **propriedades**.  

3.  Na caixa de diálogo **Propriedades** , clique no separador **Variáveis da Coleção** .  

4.  Para cada variável que pretende criar, clique a **New** ícone. Especifique a **Name** e **valor** de variável de sequência de tarefas. Se pretender ocultar a variável para que esta não estiver visível na consola do Configuration Manager, selecione a opção **não apresentar este valor na consola do Configuration Manager**.  

5.  Opcionalmente, especifique a prioridade para o Configuration Manager para utilizar quando são avaliadas as variáveis de sequência de tarefas.  

6.  Depois de adicionar todas as variáveis para as propriedades de coleção, clique em **OK**.  



##  <a name="BKMK_AdditionalActionsTS"></a> Ações adicionais para gerir sequências de tarefas  

 Pode gerir sequências de tarefas com ações adicionais ao selecionar uma sequência de tarefas.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Para selecionar uma sequência de tarefas para gerir  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos** e clique em **Sequências de Tarefas**.  

3.  Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende gerir e selecione uma das opções disponíveis.  


### <a name="available-options"></a>Opções disponíveis

#### <a name="edit"></a>Editar
 Para obter mais informações, consulte [editar uma sequência de tarefas](#BKMK_ModifyTaskSequence).

#### <a name="enable"></a>Ativar
 Permite que a sequência de tarefas para que os clientes podem executá-lo. Não precisa de voltar a implementar uma sequência de tarefas depois de ser ativada.  

#### <a name="disable"></a>Desativar
 Desativa a sequência de tarefas para que ele não pode ser executado em computadores. Pode implementar uma sequência de tarefas desativada, mas os computadores não executam a sequência de tarefas até que o ative.  

#### <a name="export"></a>Exportar
 Para obter mais informações, consulte [exportar e importar sequências de tarefas](#BKMK_ExportImport).

#### <a name="copy"></a>cópia
 Efetua uma cópia da sequência tarefas selecionada. Esta ação é útil para criar uma nova sequência de tarefas que se baseia numa sequência de tarefas existente. 

 Quando efetuar uma cópia de uma sequência de tarefas numa pasta, esta é listada nessa pasta até a atualizar o nó da sequência de tarefas. Após a atualização, cópia aparece na pasta raiz.  

#### <a name="refresh"></a>Atualizar
 Atualiza os detalhes para a sequência de tarefas selecionada.

#### <a name="delete"></a>Eliminar
 Elimina a sequência de tarefas selecionada.

#### <a name="create-phased-deployment"></a>Criar implementação faseada
 Para obter mais informações, consulte [criar implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

#### <a name="deploy"></a>Implementar
 Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](#BKMK_DeployTS).

#### <a name="distribute-content"></a>Distribuir Conteúdo
 Inicia o Assistente para distribuir conteúdo para enviar o conteúdo referenciado a pontos de distribuição. 

#### <a name="create-prestaged-content-file"></a>Criar ficheiro de conteúdo pré-configurado
 Inicia o Assistente para Criar Ficheiro de Conteúdo Pré-configurado para pré-configurar o conteúdo da sequência de tarefas. Para obter mais informações sobre como criar um ficheiro de conteúdo pré-configurado, consulte [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).

#### <a name="move"></a>Mover
 Move a sequência de tarefas selecionada para outra pasta no **sequências de tarefas** nó. 

#### <a name="set-security-scopes"></a>Definir âmbitos de segurança
 Selecione os âmbitos de segurança para a sequência de tarefas selecionada. Para obter mais informações, veja [Âmbitos de segurança](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope). 

#### <a name="properties"></a>Propriedades
 Para obter mais informações, consulte [propriedades de configurar o Centro de Software](#bkmk_prop-general) e [configurar definições de sequência de tarefas avançadas](#bkmk_prop-advanced).



## <a name="see-also"></a>Consulte também

[Cenários para implementar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md)
