---
title: "Criar uma sequência de tarefas para atualizar um sistema operativo"
titleSuffix: Configuration Manager
description: "Sequências de tarefas no System Center Configuration Manager podem atualizar automaticamente um sistema operativo do Windows 7 ou posterior para Windows 10."
ms.custom: na
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 058b0710484a0452ddf19655bf2cabbb43f624ad
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/02/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para atualizar um sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize sequências de tarefas no Configuration Manager para atualizar automaticamente um sistema operativo num computador de destino. Esta atualização pode ser do Windows 7 ou posterior para o Windows 10, ou do Windows Server 2012 ou posterior para o Windows Server 2016. Criar uma sequência de tarefas referencia o pacote de atualização do sistema operativo e qualquer outro conteúdo para instalar, tais como aplicações ou software atualizações. A sequência de tarefas para atualizar um sistema operativo faz parte o [atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md) cenário.  

##  <a name="BKMK_UpgradeOS"></a>Criar uma sequência de tarefas para atualizar um sistema operativo  
 Para atualizar o sistema operativo nos computadores, pode criar uma sequência de tarefas e selecione **atualizar um sistema operativo a partir do pacote de atualização** no Assistente de criação de sequência de tarefas. O assistente adiciona os passos para atualizar o sistema operativo, aplicar atualizações de software e instalar aplicações. Antes de criar a sequência de tarefas, tem de ser os seguintes requisitos no local:    

-   **Necessário**  

     - O [pacote de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) devem estar disponíveis na consola do Configuration Manager.
     - Quando atualizar para o Windows Server 2016, selecione o **ignorar quaisquer mensagens de compatibilidade dismissable** no passo de sequência de tarefas atualizar sistema operativo. Caso contrário, a atualização falhará.

-   **Necessário (se utilizado)**  

    -   [As atualizações de software](../../sum/get-started/synchronize-software-updates.md) têm de ser sincronizados na consola do Configuration Manager.  

    -   [Aplicações](../../apps/deploy-use/create-applications.md) tem de ser adicionado à consola do Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Para criar uma sequência de tarefas que Atualize um sistema operativo  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente de Criação de Sequência de Tarefas.  

4.  No **criar uma nova sequência de tarefas** página, clique em **atualizar um sistema operativo a partir do pacote de atualização**e, em seguida, clique em **seguinte**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Nome da sequência de tarefas**: Especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: Especifique uma descrição da tarefa que é executada pela sequência de tarefas.  

6.  No **atualizar o sistema operativo Windows** página, especifique as seguintes definições e, em seguida, clique em **seguinte**.  

    -   **Pacote de atualização**: Especifique o pacote de atualização que contém os ficheiros de origem da atualização do sistema operativo. Pode verificar que selecionou o pacote de atualização correto ao observar as informações de **propriedades** painel. Para obter mais informações, consulte [gerir pacotes de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Índice da edição**: Se existirem vários índices de edição do sistema operativo disponíveis no pacote, selecione o índice de edição pretendido. Por predefinição, o primeiro item está selecionado.  

    -   **Chave de produto**: Especifique a chave de produto para o sistema operativo do Windows instalar. Pode especificar chaves de licenciamento em volume codificadas e chaves de produto padrão. Se utilizar uma chave de produto não codificada, cada grupo de cinco carateres têm de ser separado por um traço (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quando a atualização para uma edição de licença de volume, a chave de produto não é necessária. Só precisa de uma chave de produto quando a atualização for para uma edição de revenda do Windows.  

    -   **Ignorar quaisquer mensagens de compatibilidade dismissable**: Selecione esta definição se estiver a atualizar para o Windows Server 2016. Se não selecionar esta definição, a sequência de tarefas não consegue concluir porque a configuração do Windows está a aguardar que o utilizador clica em **confirmar** uma caixa de diálogo de compatibilidade de aplicações Windows.   

7.  Na página **Incluir Atualizações** , especifique se devem ser instaladas as atualizações de software necessárias, todas as atualizações de software ou nenhuma atualização de software e clique em **Seguinte**. Se especificar a instalação de atualizações de software, o Configuration Manager instala apenas as atualizações de software direcionadas para coleções das quais o computador de destino é um membro.  

8.  Na página **Instalar Aplicações** , especifique as aplicações a instalar no computador de destino e clique em **Seguinte**. Se especificar várias aplicações, poderá também especificar que a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

9. Conclua o assistente.  



## <a name="configure-pre-cache-content"></a>Configurar pré-armazenar conteúdo em cache
A partir da versão 1702, a funcionalidade de pré-cache para as implementações disponíveis de sequências de tarefas permite que os clientes transferir apenas o conteúdo relevante antes de um utilizador instala a sequência de tarefas.
> [!TIP]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1702 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1706, esta funcionalidade já não é uma funcionalidade de pré-lançamento.

Por exemplo, digamos que pretende implementar uma sequência de tarefas de atualização no local do Windows 10, apenas pretende uma única sequência de tarefas para todos os utilizadores e ter várias arquiteturas de e/ou idiomas. Em versões anteriores, o conteúdo é iniciado transferir quando o utilizador instala uma implementação de sequência de tarefas disponíveis a partir do Centro de Software. Este atraso demore mais tempo adicional antes da instalação estiver pronta para começar. Além disso, todo o conteúdo referenciado na sequência de tarefas é transferido. Este conteúdo inclui o pacote de atualização do sistema operativo para todos os idiomas e arquiteturas. Se cada pacote de atualização é de aproximadamente três GB de tamanho, o conteúdo total é muito grande.

Pré-armazenar conteúdo em cache dá-lhe a opção para permitir que o cliente transferir apenas o conteúdo aplicável logo que recebe a implementação. Por conseguinte, quando o utilizador clica em **instalar** no Centro de Software, o conteúdo está pronto e a instalação inicia rapidamente porque o conteúdo no disco rígido local.

### <a name="to-configure-the-pre-cache-feature"></a>Configurar a funcionalidade de pré-cache

1. Criação de pacotes de atualização para idiomas e arquiteturas específicas de sistema operativo. Especifique a arquitetura e idioma de **origem de dados** separador do pacote. Para o idioma, utilize a conversão decimal (por exemplo, 1033 é o valor decimal para inglês e 0x0409 é o equivalente hexadecimal). Para obter mais informações, consulte [criar uma sequência de tarefas para atualizar um sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Os valores de arquitetura e de idioma que corresponde ao condições, os passos da sequência de tarefas para determinar se o pacote de atualização do sistema operativo é previamente em cache.
1. Crie uma sequência de tarefas com condicionais passos para os idiomas diferentes e arquiteturas. Por exemplo, o passo seguinte utiliza a versão inglesa:

    ![Propriedades da pré-cache de](../media/precacheproperties2.png)

    ![Opções de pré-cache](../media/precacheoptions2.png)  

3. Implemente a sequência de tarefas. Para a funcionalidade de pré-cache, configure as seguintes definições:
    - No **geral** separador, selecione **previamente transferir conteúdo para esta sequência de tarefas**.
    - No **definições de implementação** separador, configure a sequência de tarefas com o **disponível** para **objetivo**.
    - No **agendamento** separador, para o **agendar quando esta implementação ficará disponível** definição, escolha a hora atualmente selecionada. O cliente inicia previamente a colocação em cache conteúdo na hora de disponibilização da implementação. Quando um cliente de destino recebe esta política, o tempo disponível está no passado, deste modo, transferências de pré-cache inicia imediatamente. Se o cliente recebe esta política, mas o tempo disponível é no futuro, o cliente não é iniciado previamente a colocação em cache conteúdo até ocorre o tempo disponível. 
    - No **pontos de distribuição** separador, configure o **opções de implementação** definições. Se o conteúdo não é previamente em cache no cliente antes de um utilizador inicia a instalação, estas definições são utilizadas.


### <a name="user-experience"></a>Experiência de utilizador
- Quando o cliente recebe a política de implementação, será iniciada a previamente os conteúdos em cache após a hora de disponibilização da implementação. Este conteúdo inclui todos os pacotes referenciados e apenas o pacote atualização do sistema operativo que corresponda ao cliente com base nas condições definido na sequência de tarefas.
- Quando a implementação é disponibilizada para os utilizadores, apresenta uma notificação a informar os utilizadores sobre a nova implementação e a sequência de tarefas está visível no Centro de Software. O utilizador pode aceder ao centro de Software e clicar em **instalar** para iniciar a instalação.
- Se o conteúdo não esteja totalmente previamente em cache quando o utilizador instala a sequência de tarefas, em seguida, o cliente utiliza as definições que especifica o **a opção de implementação** separador da implementação. 



## <a name="download-package-content-task-sequence-step"></a>Transferir o conteúdo do pacote passo de sequência de tarefas  
 O [transferir conteúdo do pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) passo pode ser utilizado antes do **atualizar sistema operativo** passo nos seguintes cenários:  

-   Utilizar uma sequência de tarefas de atualização única para plataformas x86 e x64. Inclua dois **transferir conteúdo do pacote** os passos no **preparar a atualização** grupo. Definir condições de cada passo para detetar a arquitetura do cliente. Esta condição faz com que o passo transferir apenas o pacote de atualização do sistema operativo adequado. Configure cada passo **Transferir Conteúdo do Pacote** para utilizar a mesma variável e utilize a variável para o caminho do suporte de dados no passo **Atualizar Sistema Operativo** .  

-   Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada **transferir conteúdo do pacote** passo para utilizar a mesma variável. Em seguida, utilizar essa variável para o **conteúdo de teste** valor na secção controladores no **atualizar sistema operativo** passo.  

   > [!NOTE]
   > Quando existe mais do que um pacote, o Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se especificar uma variável de % omeuconteúdo % como uma variável personalizada, esta localização é onde o cliente armazena todo o conteúdo referenciado. Quando fizer referência à variável num passo subsequente, tais como **atualizar sistema operativo**, utilize a variável com um sufixo numérico. Neste exemplo, % osmeusconteúdos01% ou % osmeusconteúdos02%, onde o número corresponde à ordem na qual o **transferir conteúdo do pacote** passo lista este conteúdo específico.

## <a name="optional-post-processing-task-sequence-steps"></a>Passos de sequência de tarefas pós-processamento opcionais  
 Depois de criar a sequência de tarefas, adicione passos adicionais conforme necessário. Por exemplo, para desinstalar aplicações com problemas de compatibilidade conhecidos ou adicionar ações de pós-processamento para que execute após o computador é reiniciado e a atualização para o Windows 10 é efetuada com êxito. Adicione estes passos adicionais no grupo de pós-processamento da sequência de tarefas.  

> [!NOTE]  
>  Como esta sequência de tarefas não é linear, existem condições nos passos que podem afetar os resultados da sequência de tarefas, dependendo se atualiza com êxito o computador cliente ou se tem de reverter o computador cliente para a versão do sistema operativo começar a utilizar.  

## <a name="optional-rollback-task-sequence-steps"></a>Passos de sequência de tarefas de reversão opcionais  
 Se houver algum problema com o processo de atualização depois de reiniciar o computador, a configuração do Windows irá reverter a atualização para o sistema operativo anterior. A sequência de tarefas, em seguida, irá continuar com os passos existentes no grupo reversão. Depois de criar a sequência de tarefas, pode adicionar passos opcionais ao grupo reversão.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Pasta e os ficheiros foram removidos após o computador reiniciar  
 Quando a sequência de tarefas estiver concluída, o cliente não remove os scripts de reversão e pós-processamento enquanto o computador é reiniciado. Estes ficheiros de script não contêm informações confidenciais.  
