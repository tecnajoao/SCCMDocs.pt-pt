---
title: Criar uma sequência de tarefas de atualização do SO
titleSuffix: Configuration Manager
description: Utilize uma sequência de tarefas para atualização do Windows 7 ou posterior para o Windows 10
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 48a5e7aa381924e3c0ad052833c9588e3dffa4f5
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Criar uma sequência de tarefas para atualizar um sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize sequências de tarefas no Configuration Manager para atualizar automaticamente um sistema operativo num computador de destino. Esta atualização pode ser do Windows 7 ou posterior para o Windows 10, ou do Windows Server 2012 ou posterior para o Windows Server 2016. Crie uma sequência de tarefas referencia o pacote de atualização do SO e qualquer outro conteúdo para instalar, tais como aplicações ou software atualizações. A sequência de tarefas para atualizar um sistema operativo faz parte o [atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md) cenário.  



##  <a name="BKMK_UpgradeOS"></a> Criar uma sequência de tarefas para atualizar um sistema operativo  
 Para atualizar o sistema operativo nos computadores, pode criar uma sequência de tarefas e selecione **atualizar um sistema operativo a partir do pacote de atualização** no Assistente de criação de sequência de tarefas. O assistente adiciona os passos de sequência de tarefas para atualizar o sistema operativo, aplicar atualizações de software e instalar aplicações. Antes de criar a sequência de tarefas, tem de ser os seguintes requisitos no local:    

-   **Necessário**  

     - O [pacote de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) devem estar disponíveis na consola do Configuration Manager.
     - Quando atualizar para o Windows Server 2016, selecione o **ignorar quaisquer mensagens de compatibilidade dismissable** no passo de sequência de tarefas atualizar sistema operativo. Caso contrário, a atualização falhar.

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

7.  No **incluir atualizações** página, especifique se instalar necessário, de atualizações de software todas ou nenhuma. Em seguida, clique em **Seguinte**. Se especificar a instalação de atualizações de software, o Configuration Manager instala apenas as atualizações de software direcionadas para coleções das quais o computador de destino é um membro.  

8.  Na página **Instalar Aplicações** , especifique as aplicações a instalar no computador de destino e clique em **Seguinte**. Se especificar várias aplicações, poderá também especificar que a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

9. Conclua o assistente.  


 > [!Important] 
 > Quando a sequência de tarefas estiver concluída, o cliente não remove os scripts de reversão e pós-processamento enquanto o computador é reiniciado. Estes ficheiros de script não contêm informações confidenciais.  


 > [!Note]
 > A partir de versão 1802, o modelo de sequência de tarefas predefinido para a atualização no local do Windows 10 inclui grupos adicionais com as ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que com êxito estiver a atualizar dispositivos para Windows 10. Para obter mais informações, consulte os passos de sequência de tarefas recomendadas [para preparar a atualização](#recommended-task-sequence-steps-to-prepare-for-upgrade) e [para pós-processamento](#recommended-task-sequence-steps-for-post-processing).



## <a name="configure-pre-cache-content"></a>Configurar pré-armazenar conteúdo em cache
<!--1021244-->
A funcionalidade de pré-cache para as implementações disponíveis de sequências de tarefas permite que os clientes transferir conteúdo do pacote de atualização de SO relevante antes de um utilizador instala a sequência de tarefas.  

> [!TIP]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1702 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1706, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  


> [!Note]  
> O Configuration Manager não ativar esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Por exemplo, que apenas pretende uma sequência de tarefas de atualização no local único para todos os utilizadores e tem muitas arquiteturas e idiomas. Em versões anteriores, o conteúdo é iniciado transferir quando o utilizador instala uma implementação de sequência de tarefas disponíveis a partir do Centro de Software. Este atraso demore mais tempo adicional antes da instalação estiver pronta para começar. Todos os conteúdos referenciados na sequência de tarefas é transferido. Este conteúdo inclui o pacote de atualização do sistema operativo para todos os idiomas e arquiteturas. Se cada pacote de atualização é de aproximadamente três GB de tamanho, o conteúdo total é muito grande.

Fornecem conteúdo de pré-cache de a opção para permitir que o cliente para transferência apenas o SO aplicável atualizar pacote, bem como todos os outros conteúdo referenciado, logo que recebe a implementação. Quando o utilizador clica **instalar** no Centro de Software, o conteúdo está pronto e a instalação inicia rapidamente porque o conteúdo no disco rígido local.

 > [!NOTE]
 > Este comportamento atualmente só se aplica ao pacote de atualização do SO. Esse pacote é o único conteúdo no qual especifique a arquitetura ou idioma correspondente. Por exemplo, se a sequência de tarefas referencia também vários pacotes de controladores, o cliente atualmente transfere todos eles. O motor de sequência de tarefas avalia as condições nos passos quando a sequência de tarefas é executado, não se encontra em Avançadas. O cliente utiliza as etiquetas em Propriedades do pacote para determinar que conteúdo em cache previamente.

### <a name="to-configure-the-pre-cache-feature"></a>Configurar a funcionalidade de pré-cache

1. Crie pacotes de atualização do SO para idiomas e arquiteturas específicas. Especifique a arquitetura e idioma de **origem de dados** separador do pacote. Para o idioma, utilize a conversão decimal. Por exemplo, 1033 é o valor decimal para inglês e 0x0409 é o equivalente hexadecimal.

    O cliente avalia os valores de arquitetura e de idioma para determinar que transfere durante previamente a colocação em cache do pacote de atualização do SO.

1. Crie uma sequência de tarefas com condicionais passos para os idiomas diferentes e arquiteturas. Por exemplo, o passo seguinte utiliza a versão inglesa:

    ![Editor de sequência de tarefas que mostra os vários passos de atualização de SO para Português, DEU e JPN](../media/precacheproperties2.png)

    ![Editor de sequência de tarefas, separador de opções, que apresenta a consulta WQL de WMI para a região e OSArchitecture](../media/precacheoptions2.png)  

3. Implemente a sequência de tarefas. Para a funcionalidade de pré-cache, configure as seguintes definições:
    - No **geral** separador, selecione **previamente transferir conteúdo para esta sequência de tarefas**.
    - No **definições de implementação** separador, configure a sequência de tarefas com o **disponível** para **objetivo**.
    - No **agendamento** separador, para o **agendar quando esta implementação ficará disponível** definição, escolha a hora atualmente selecionada. O cliente inicia previamente a colocação em cache conteúdo na hora de disponibilização da implementação. Quando um cliente de destino recebe esta política, o tempo disponível está no passado, deste modo, transferências de pré-cache inicia imediatamente. Se o cliente recebe esta política, mas o tempo disponível é no futuro, o cliente não é iniciado previamente a colocação em cache conteúdo até ocorre o tempo disponível. 
    - No **pontos de distribuição** separador, configure o **opções de implementação** definições. Se o conteúdo não é previamente em cache antes de um utilizador inicia a instalação, o cliente utiliza estas definições.
  

### <a name="user-experience"></a>Experiência de utilizador
- Quando o cliente recebe a política de implementação, começa a previamente os conteúdos em cache após a hora de disponibilização da implementação. Este conteúdo inclui pacotes de todos os referenciado, mas apenas o SO pacote de atualização que satisfaça os atributos de arquitetura e de idioma no pacote.
- Quando o cliente efetua a implementação disponíveis para os utilizadores, apresenta uma notificação a informar os utilizadores sobre a nova implementação. A sequência de tarefas está agora visível no Centro de Software. O utilizador pode aceder ao centro de Software e clicar em **instalar** para iniciar a instalação.
- Se o conteúdo não esteja totalmente previamente em cache quando o utilizador instala a sequência de tarefas, em seguida, o cliente utiliza as definições que especifica o **a opção de implementação** separador da implementação. 



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Passos de sequência de tarefas recomendadas para preparar a atualização

A partir de versão 1802, o modelo de sequência de tarefas predefinido para a atualização no local do Windows 10 inclui grupos adicionais com as ações recomendadas para adicionar antes do processo de atualização. Estas ações no **preparar a atualização** grupo são comuns entre muitos clientes que com êxito estiver a atualizar dispositivos para Windows 10. Para sites em versões anteriores à 1802, adicione manualmente estas ações à sequência de tarefas no **preparar a atualização** grupo.
- **Verifica a bateria**: Adicione passos neste grupo para verificar se o computador está a utilizar bateria ou com fios energia. Esta ação requer um script personalizado ou o utilitário para executar esta verificação.
- **Rede/com fios verificações de ligação**: Adicione passos neste grupo para verificar se o computador está ligado a uma rede e não está a utilizar uma ligação sem fios. Esta ação requer um script personalizado ou o utilitário para executar esta verificação.
- **Remover aplicações incompatíveis**: Adicione passos neste grupo para remover todas as aplicações que são incompatíveis com esta versão do Windows 10. Varia consoante o método para desinstalar uma aplicação. Se a aplicação utiliza o Windows Installer, copie o **programa de desinstalação** linha de comandos a partir de **programas** separador Propriedades do tipo de implementação do Windows Installer da aplicação. Em seguida, adicione um **executar linha de comandos** passo neste grupo com a linha de comandos do programa de desinstalação. Por exemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Remover controladores incompatíveis**: Adicione passos neste grupo para remover os controladores que sejam incompatíveis com esta versão do Windows 10.
- **Remover/suspender a segurança de terceiros**: Adicione passos neste grupo para remover ou suspender a programas de segurança de terceiros, como antivírus.
   - Se estiver a utilizar um programa de encriptação de disco de terceiros, fornecer o controlador de encriptação à configuração do Windows com o **/ReflectDrivers** [opção da linha de comandos](/windows-hardware/manufacture/desktop/windows-setup-command-line-options). Adicionar um [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo à sequência de tarefas neste grupo. Definir a variável de sequência de tarefas **OSDSetupAdditionalUpgradeOptions**. Defina o valor como **/ReflectDriver** com o caminho para o controlador. Isto [variável de ação de sequência de tarefas](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) acrescenta a configuração do Windows da linha de comandos utilizada pela sequência de tarefas. Contacte o fabricante de software para qualquer orientações adicionais sobre este processo.

### <a name="download-package-content-task-sequence-step"></a>Transferir o conteúdo do pacote passo de sequência de tarefas  
 O [transferir conteúdo do pacote](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) passo pode ser utilizado antes do **atualizar sistema operativo** passo nos seguintes cenários:  

-   Utilizar uma sequência de tarefas de atualização única para plataformas x86 e x64. Inclua dois **transferir conteúdo do pacote** os passos no **preparar a atualização** grupo. Definir condições de cada passo para detetar a arquitetura do cliente. Esta condição faz com que o passo transferir apenas o pacote de atualização do sistema operativo adequado. Configure cada passo **Transferir Conteúdo do Pacote** para utilizar a mesma variável e utilize a variável para o caminho do suporte de dados no passo **Atualizar Sistema Operativo** .  

-   Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada **transferir conteúdo do pacote** passo para utilizar a mesma variável. Em seguida, utilizar essa variável para o **conteúdo de teste** valor na secção controladores no **atualizar sistema operativo** passo.  

   > [!NOTE]
   > Quando existe mais do que um pacote, o Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se especificar uma variável de % omeuconteúdo % como uma variável personalizada, esta localização é onde o cliente armazena todo o conteúdo referenciado. Quando fizer referência à variável num passo subsequente, tais como **atualizar sistema operativo**, utilize a variável com um sufixo numérico. Neste exemplo, % osmeusconteúdos01% ou % osmeusconteúdos02%, onde o número corresponde à ordem na qual o **transferir conteúdo do pacote** passo lista este conteúdo específico.



## <a name="recommended-task-sequence-steps-for-post-processing"></a>Passos de sequência de tarefas recomendadas para pós-processamento   
 Depois de criar a sequência de tarefas, adicionar os passos adicionais no **pós-processamento** grupo da sequência de tarefas.  

> [!NOTE]  
>  Esta sequência de tarefas não é linear. Existem condições nos passos que podem afetar os resultados da sequência de tarefas. Este comportamento depende se de que atualiza o computador cliente com êxito ou se tem de reverter o computador cliente para o sistema operativo original.  

A partir de versão 1802, o modelo de sequência de tarefas predefinido para a atualização no local do Windows 10 inclui grupos adicionais com as ações recomendadas para adicionar depois do processo de atualização. Estas ações no **pós-processamento** grupo são comuns entre muitos clientes que com êxito estiver a atualizar dispositivos para Windows 10. Para sites em versões anteriores à 1802, adicione manualmente estas ações à sequência de tarefas no **pós-processamento** grupo.
- **Aplicar controladores baseados na configuração**: Adicione passos neste grupo para instalar controladores baseados no programa de configuração (.exe) a partir de pacotes.
- **Instalar/ativar segurança de terceiros**: Adicione passos neste grupo para instalar ou ative a programas de segurança de terceiros, como antivírus. 
- **Definir aplicações do Windows predefinido e as associações**: Adicione passos neste grupo para definir as aplicações do Windows predefinido e associações de ficheiros. Primeiro, prepare um computador de referência com associações a aplicação pretendida. Em seguida, execute a seguinte linha de comandos para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Adicione o ficheiro XML a um pacote. Em seguida, adicione um [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo deste grupo. Especifique o pacote que contém o ficheiro XML e, em seguida, especifique a linha de comandos: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para obter mais informações, consulte [exportar ou importar predefinido associações de aplicação](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Aplicar as personalizações e personalização**: Adicione passos neste grupo para aplicar as personalizações do menu Iniciar, tais como organizar grupos de programa. Para obter mais informações, consulte [personalizar o ecrã de início](/windows-hardware/manufacture/desktop/customize-the-start-screen).



## <a name="optional-task-sequence-steps-for-rollback"></a>Passos de sequência de tarefas opcionais para reversão  
 Se houver algum problema com o processo de atualização depois de reiniciar o computador, a configuração do Windows irá reverter a atualização para o sistema operativo anterior. Em seguida, continua a sequência de tarefas com os passos no **reversão** grupo. Depois de criar a sequência de tarefas, pode adicionar passos opcionais no grupo reversão. Por exemplo, reverter as alterações efetuadas no sistema o preparar para o grupo de atualização, tais como desinstalar o software incompatível.



## <a name="additional-recommendations"></a>Recomendações adicionais
- Reveja a documentação do Windows para [erros de atualização do Windows 10 resolver](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também inclui informações detalhadas sobre o processo de atualização.
- A predefinição **verificar disponibilidade** passo, ativar **assegurar espaço mínimo livre em disco (MB)**. Defina o valor para, pelo menos, **16384** (16 GB) para um SO de 32 bits atualizar o pacote, ou **20480** (20 GB) de 64 bits. 
- Utilize o **SMSTSDownloadRetryCount** [variável de sequência de tarefas incorporadas](/sccm/osd/understand/task-sequence-built-in-variables) para transferir política de repetição. Atualmente, por predefinição, o cliente duas vezes; repetir Esta variável é definida como dois (2). Se os clientes não estiverem numa ligação de rede empresarial com fios, tentativas adicionais ajudam o cliente obter a política. Utilizar esta variável faz com que nenhum efeito negativo, que não sejam falha atrasada se não é possível transferir a política.<!-- 501016 --> Aumentar também o **SMSTSDownloadRetryDelay** variável da predefinição 15 segundos.
- Efetue uma avaliação de compatibilidade inline. 
   - Adicionar uma segunda **atualizar sistema operativo** passo antecipadamente no **preparar a atualização** grupo. Nome *da avaliação da atualização*. Especifique o mesmo pacote de atualização e, em seguida, ative a opção de **análise de compatibilidade de executar a configuração do Windows sem iniciar a atualização**. Ativar **continuar com o erro** no separador de opções. 
   - Imediatamente a seguir esta *da avaliação da atualização* passo, adicione um **executar linha de comandos** passo. Especifique a linha de comandos:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>No **opções** separador, adicione a seguinte condição: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno é o equivalente decimal MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma análise de compatibilidade efetuada com êxito sem problemas. Se o *avaliação da atualização* passo for bem sucedida e devolve este código, este passo é ignorado. Caso contrário, se o passo de avaliação devolve qualquer código de retorno, este passo falhe a sequência de tarefas com o código de retorno da análise de compatibilidade de configuração do Windows.
   - Para obter mais informações, consulte [atualizar sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Se pretender alterar o dispositivo de BIOS para UEFI durante esta sequência de tarefas, consulte [converter da BIOS UEFI durante uma atualização no local](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).
