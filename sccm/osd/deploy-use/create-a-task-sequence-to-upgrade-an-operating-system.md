---
title: Criar uma sequência de tarefas de atualização de SO
titleSuffix: Configuration Manager
description: Utilizar uma sequência de tarefas para automaticamente atualizar do Windows 7 ou posterior para o Windows 10
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 483b5f8b285fb256005e31e01a0786cef6c8e11d
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383090"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Criar uma sequência de tarefas para atualizar um sistema operacional no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize sequências de tarefas no Configuration Manager para atualizar automaticamente um sistema operacional no computador de destino. Esta atualização pode ser do Windows 7 ou posterior para o Windows 10, ou do Windows Server 2012 ou posterior para o Windows Server 2016. Crie uma sequência de tarefas que referencia o pacote de atualização de SO e qualquer outro conteúdo para instalar, tais como aplicações ou software de atualizações. A sequência de tarefas para atualizar um sistema operacional faz parte do [atualizar o Windows para a versão mais recente](upgrade-windows-to-the-latest-version.md) cenário.  



## <a name="prerequisites"></a>Pré-requisitos

Antes de criar a sequência de tarefas, devem ser cumpridos os seguintes requisitos:    

#### <a name="required"></a>Necessário  

- O [pacote de atualização de SO](/sccm/osd/get-started/manage-operating-system-upgrade-packages) tem de estar disponível na consola do Configuration Manager.  

- Quando atualizar para o Windows Server 2016, selecione o **ignorar todas as mensagens de compatibilidade que pode ser dispensado** definir no passo de sequência de tarefas atualizar sistema operativo. Caso contrário, a atualização falha.  

#### <a name="required-if-used"></a>Necessário (se utilizado)  

-   [Atualizações de software](/sccm/sum/get-started/synchronize-software-updates) têm de ser sincronizadas na consola do Configuration Manager.  

-   [Aplicativos](/sccm/apps/deploy-use/create-applications) deve ser adicionado à consola do Configuration Manager.  



##  <a name="BKMK_UpgradeOS"></a> Criar uma sequência de tarefas para atualizar um sistema operacional  

Para atualizar o sistema operacional nos clientes, criar uma sequência de tarefas e selecionar **atualizar um sistema operativo a partir do pacote de atualização** no Assistente de criação de sequência de tarefas. O assistente adiciona os passos de sequência de tarefas para atualizar o sistema operacional, aplicar atualizações de software e instalar aplicações. 

#### <a name="to-create-a-task-sequence-that-upgrades-an-os"></a>Para criar uma sequência de tarefas que Atualize um sistema operacional  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e, em seguida, clique em **sequências de tarefas**.  

2.  Sobre o **home page** separador do Friso, no **criar** , clique em **criar sequência de tarefas**.  

3.  Sobre o **criar uma nova sequência de tarefas** página do Assistente de criação tarefas sequência, selecione **atualizar um sistema operativo a partir de um pacote de atualização**e, em seguida, clique em **seguinte**.  

4.  Sobre o **informações da sequência de tarefas** página, especifique as seguintes definições e, em seguida, clique em **próxima**:  

    -   **Nome da sequência de tarefas**: Especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: Opcionalmente, especifique uma descrição.  

5.  Sobre o **atualizar o sistema operativo do Windows** página, especifique as seguintes definições e, em seguida, clique em **próxima**:  

    -   **Pacote de atualização**: Especifique o pacote de atualização que contém os arquivos de origem da atualização do sistema operacional. Certifique-se de que selecionou o pacote de atualização correto ao observar as informações a **propriedades** painel. Para obter mais informações, consulte [pacotes de atualização de SO gerir](/sccm/osd/get-started/manage-operating-system-upgrade-packages).  

    -   **Índice da edição**: Se existirem vários índices de edição do SO disponível no pacote, selecione o índice de edição pretendido. Por predefinição, o assistente seleciona o primeiro índice.  

    -   **Chave de produto**: Especifique a chave de produto do Windows para o sistema operativo instalar. Especifica chaves de licença de volume codificadas ou chaves de produto padrão. Se utilizar uma chave de produto padrão, separe cada grupo de cinco caracteres por um travessão (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quando a atualização for para uma edição de licença de volume, a chave de produto pode não ser necessária.  

        > [!Note]  
        > Esta chave de produto pode ser uma chave de ativação múltipla (MAK) ou um volume genérico (GVLK) de chave de licenciamento. Uma GVLK é também referida como uma chave de configuração de cliente do gerenciamento de chaves (KMS serviço). Para obter mais informações, consulte [plano para ativação de volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obter uma lista de chaves de configuração de cliente KMS, consulte [apêndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server. 

    -   **Ignorar todas as mensagens de compatibilidade que pode ser dispensado**: Selecione esta definição se estiver a atualizar para o Windows Server 2016. Se não selecionar esta definição, a sequência de tarefas não consegue concluir porque a configuração do Windows está à espera que o usuário clique **confirmar** numa caixa de diálogo de compatibilidade de aplicações Windows.   

7.  Sobre o **incluir atualizações** , especifique se para instalar necessários, de atualizações de software de todos ou nenhum. Em seguida, clique em **Seguinte**. Se especificar a instalação de atualizações de software, o Configuration Manager instala apenas essas atualizações direcionadas para as coleções do qual o computador de destino é um membro.  

8.  Na página **Instalar Aplicações** , especifique as aplicações a instalar no computador de destino e clique em **Seguinte**. Se selecionar mais de um aplicativo, também especifica se a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

9. Conclua o assistente.  


> [!Important]  
> Quando a sequência de tarefas é executada num dispositivo, o cliente do Configuration Manager cria vários scripts para controlar o comportamento de sequência de tarefas em vários cenários. Quando a sequência de tarefas é concluída, o cliente não remove estes scripts até que o computador for reiniciado. Esses arquivos de script não contêm informações confidenciais.  


A partir da versão 1802, o modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui grupos adicionais com as ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que estão com êxito a atualizar dispositivos Windows 10. Para obter mais informações, consulte os passos de sequência de tarefa recomendada [para se preparar para atualização](#recommended-task-sequence-steps-to-prepare-for-upgrade) e [para o pós-processamento](#recommended-task-sequence-steps-for-post-processing).

A partir da versão 1806, este modelo de sequência de tarefas inclui também um grupo com as ações recomendadas para adicionar no caso do processo de atualização falha. Estas ações facilitam a resolução de problemas. Para obter mais informações, consulte [recomendado passos de sequência de tarefas em caso de falha](#recommended-task-sequence-steps-on-failure).<!--1358500-->  



## <a name="configure-pre-cache-content"></a>Configurar pré-armazenar conteúdo em cache
<!--1021244--> A funcionalidade de pré-cache para implementações disponíveis de sequências de tarefas permite que os clientes a transferir conteúdo do pacote de atualização de SO relevante antes de um utilizador instala a sequência de tarefas.  

> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Por exemplo, só pretende uma sequência de tarefas de atualização no local único para todos os utilizadores e tem inúmeras arquiteturas e linguagens. Nas versões anteriores, o conteúdo é iniciado transferir quando o utilizador instala uma implementação de sequência de tarefas disponível no Centro de Software. Este atraso adiciona mais tempo antes da instalação estiver pronta para começar. Todo o conteúdo referenciado na sequência de tarefas é transferido. Este conteúdo inclui o pacote de atualização de SO para todos os idiomas e arquiteturas. Se cada pacote de atualização é aproximadamente 3 GB de tamanho, o conteúdo total é muito grande.

Pré-armazenar conteúdo em cache dá-lhe a opção para o cliente transferir apenas o pacote de atualização do SO aplicável e todos os outros conteúdos referenciados assim que receber a implementação. Quando o usuário clica **instalar** no Centro de Software, os conteúdos estiverem prontos. A instalação inicia-se rapidamente porque o conteúdo está no disco rígido local.

> [!NOTE]  
> Este comportamento atualmente só se aplica ao pacote de atualização do sistema operacional. Esse pacote é o único conteúdo no qual especifica a arquitetura ou idioma correspondente. Por exemplo, se a sequência de tarefas também faz referência a vários pacotes de controladores, o cliente atualmente transfere todos eles. O motor de sequência de tarefas avalia as condições nos passos quando a sequência de tarefas é executado, não está em progresso. O cliente utiliza as marcas nas propriedades de pacote para determinar o conteúdo que deve colocar previamente no cache.


### <a name="to-configure-the-pre-cache-feature"></a>Configurar a funcionalidade de pré-cache

1. Crie pacotes de atualização de SO específicas arquiteturas e linguagens. Especificar a arquitetura e o idioma no **origem de dados** Guia do pacote. Para o idioma, utilize a conversão em decimal. Por exemplo, **1033** é o valor decimal para inglês, e **0x0409** é o equivalente hexadecimal.  

    O cliente avalia os valores de arquitetura e o idioma para determinar qual transfere durante a colocação em pré-cache do pacote de atualização do sistema operacional.  

2. Crie uma sequência de tarefas com passos condicionais a diferentes idiomas e arquiteturas. Por exemplo, o passo seguinte utiliza a versão em inglês:  

    ![Editor de sequência de tarefas que mostra vários passos de atualização de SO para ENU, DEU e JPN](../media/precacheproperties2.png)

    ![Editor de sequência de tarefas, separador de opções, exibindo a consulta WQL de WMI para a Localidade e OSArchitecture](../media/precacheoptions2.png)  

3. Implemente a sequência de tarefas. Para a funcionalidade de pré-cache, configure as seguintes definições:  

    - Sobre o **gerais** separador, selecione **pré-transferir conteúdos para esta sequência de tarefas**.  

    - Sobre o **definições de implementação** separador, configure a sequência de tarefas como **disponível**.  

    - Sobre o **agendamento** separador, escolha o tempo atualmente selecionado para a definição **agendar quando esta implementação ficará disponível**. O cliente inicia a colocação em pré-cache conteúdo na hora de disponibilização da implementação. Quando um cliente de destino recebe esta política, o tempo disponível é no passado, assim, transferências de pré-cache começa imediatamente. Se o cliente recebe esta política, mas o tempo disponível é no futuro, o cliente não começa a colocação em pré-cache conteúdo até que ocorra o tempo disponível.  

    - Sobre o **pontos de distribuição** separador, configure a **opções de implementação** definições. Se o conteúdo não está em pré-cache antes de um utilizador inicia a instalação, o cliente utiliza estas definições.  
  

### <a name="user-experience"></a>Experiência de utilizador

- Quando o cliente recebe a política de implementação, começa a pré-colocar em cache o conteúdo após a hora de disponibilização da implementação. Este conteúdo inclui pacotes tudo referenciados, mas apenas o pacote atualização do SO que corresponda aos atributos de arquitetura e o idioma no pacote.  

- Quando o cliente efetua a implementação disponível para os utilizadores, é apresentada uma notificação a informar os utilizadores sobre a nova implementação. Agora a sequência de tarefas é visível no Centro de Software. O utilizador pode aceder ao centro de Software e clique em **instalar** para iniciar a instalação.  

- Se o cliente ainda não totalmente previamente em cache o conteúdo quando o utilizador instala a sequência de tarefas, em seguida, o cliente utiliza as definições que especifique a **opção de implementação** separador da implementação.  



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Passos de sequência de tarefa recomendada para se preparar para atualização

A partir da versão 1802, o modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui grupos adicionais com as ações recomendadas para adicionar antes do processo de atualização. Estas ações no **preparar para a atualização** grupo são comuns entre muitos clientes que estão com êxito a atualizar dispositivos Windows 10. Para sites em versões anteriores à 1802, adicione manualmente estas ações à sequência de tarefas no **preparar para a atualização** grupo.  

- **Verificações da bateria**: Adicione passos neste grupo para verificar se o computador está utilizar bateria ou alimentação. Esta ação requer um script personalizado ou o utilitário para executar esta verificação.  

- **Verificações de ligação de rede/wired**: Adicione passos neste grupo para verificar se o computador está ligado a uma rede e não está usando uma conexão sem fio. Esta ação requer um script personalizado ou o utilitário para executar esta verificação.  

- **Remover aplicações incompatíveis**: Adicione passos neste grupo para remover todas as aplicações que são incompatíveis com esta versão do Windows 10. O método para desinstalar uma aplicação varia.  

    - Se o aplicativo usa o Windows Installer, copie os **programa de desinstalação** linha de comandos da **programas** separador Propriedades do tipo de implementação do Windows Installer do aplicativo. Em seguida, adicione uma **executar linha de comandos** passo neste grupo com a linha de comando do programa de desinstalação. Por exemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br>  

- **Remover controladores incompatíveis**: Adicione passos neste grupo para remover todos os controladores que são incompatíveis com esta versão do Windows 10.  

- **Remover/suspender a segurança de terceiros**: Adicione passos neste grupo para remover ou suspender programas de segurança de terceiros, como um antivírus.  

   - Se estiver a utilizar um programa de encriptação de disco de terceiros, forneça o respectivo driver de encriptação à configuração do Windows com o `/ReflectDrivers` [opção da linha de comandos](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#23). Adicionar uma [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo à sequência de tarefas neste grupo. Defina a variável de sequência de tarefas **OSDSetupAdditionalUpgradeOptions**. Defina o valor como `/ReflectDrivers` com o caminho para o controlador. Isso [variável de ação de sequência de tarefas](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) acrescenta a configuração do Windows da linha de comandos utilizado pela sequência de tarefas. Contacte o fabricante de software para obter orientações adicionais sobre este processo.  


### <a name="download-package-content-task-sequence-step"></a>Transferir o conteúdo do pacote passo de sequência de tarefas  

Utilize o [transferir conteúdo do pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) passo antes do **atualizar sistema operativo** passo nos seguintes cenários:  

-   Utilizar uma sequência de tarefas de atualização única para plataformas x86 e x64. Inclua dois **transferir conteúdo do pacote** etapas na **preparar para a atualização** grupo. Definir as condições em cada etapa para detetar a arquitetura do cliente. Esta condição faz com que o passo para transferir apenas o sistema operacional atualização pacote adequado. Configure cada passo **Transferir Conteúdo do Pacote** para utilizar a mesma variável e utilize a variável para o caminho do suporte de dados no passo **Atualizar Sistema Operativo** .  

-   Para transferir dinamicamente um pacote de controlador aplicável, utilize dois passos **Transferir Conteúdo do Pacote** com condições para detetar o tipo de hardware adequado a cada pacote de controlador. Configure cada **transferir conteúdo do pacote** passo para utilizar a mesma variável. Em seguida, utilizar essa variável para o **conteúdo de teste** valor na secção de controladores no **atualizar sistema operativo** passo.  

    > [!NOTE]  
    > Quando existe mais do que um pacote, o Configuration Manager adiciona um sufixo numérico ao nome da variável. Por exemplo, se especificar `%mycontent%` como uma variável personalizada, o cliente armazena conteúdo de todos os referenciado nesta localização. Quando consultar a variável num passo subsequente, como **atualizar sistema operativo**, utilize a variável com um sufixo numérico. Neste exemplo, `%mycontent01%` ou `%mycontent02%`, onde o número corresponde à ordem na qual o **transferir conteúdo do pacote** passo apresenta uma lista deste conteúdo específico.  



## <a name="recommended-task-sequence-steps-for-post-processing"></a>Passos de sequência de tarefa recomendada para pós-processamento   

Depois de criar a sequência de tarefas, adicionar passos adicionais a **pós-processamento** grupo da sequência de tarefas.  

> [!NOTE]  
>  Esta sequência de tarefas não é linear. Existem condições nos passos que podem afetar os resultados da sequência de tarefas. Este comportamento depende se ele atualiza o computador cliente com êxito ou se tem de reverter o computador cliente para o sistema operacional original.  

A partir da versão 1802, o modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui grupos adicionais com as ações recomendadas para adicionar após o processo de atualização. Estas ações no **pós-processamento** grupo são comuns entre muitos clientes que estão com êxito a atualizar dispositivos Windows 10. Para sites em versões anteriores à 1802, adicione manualmente estas ações à sequência de tarefas no **pós-processamento** grupo.  

- **Aplicar controladores baseados na configuração**: Adicione passos neste grupo para instalar controladores baseados na configuração (.exe) dos pacotes.  

- **Instalar/ativar segurança de terceiros**: Adicione passos neste grupo para instalar ou ativar programas de segurança de terceiros, como um antivírus.  

- **Definir aplicações predefinidas do Windows e associações**: Adicione passos neste grupo para definir aplicações predefinidas do Windows e associações de arquivo. Em primeiro lugar, prepare um computador de referência com suas associações de aplicação pretendida. Em seguida, execute a seguinte linha de comando para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Adicione o ficheiro XML a um pacote. Em seguida, adicione uma [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo neste grupo. Especifique o pacote que contém o arquivo XML e, em seguida, especifique a linha de comandos: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para obter mais informações, consulte [exportação ou importação predefinido associações de aplicativos](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).  

- **Aplicar personalizações e personalização**: Adicione passos neste grupo para aplicar personalizações do menu Iniciar, por exemplo, organizar grupos de programas. Para obter mais informações, consulte [personalizar o ecrã de início](/windows-hardware/manufacture/desktop/customize-the-start-screen).  



## <a name="optional-task-sequence-steps-for-rollback"></a>Passos de sequência de tarefas opcionais para reversão  

Quando houver algum problema com o processo de atualização depois do computador é reiniciado, a configuração do Windows reverte o sistema para o sistema operacional anterior. A sequência de tarefas, em seguida, continua com os passos existentes no **reversão** grupo. Depois de criar a sequência de tarefas, adicione passos opcionais neste grupo, conforme necessário. Por exemplo, reverter quaisquer alterações efetuadas no sistema em preparação para o grupo de atualização, como desinstalar o software incompatível.



## <a name="recommended-task-sequence-steps-on-failure"></a>Passos de sequência de tarefa recomendada em caso de falha
<!--1358500-->

A partir da versão 1806, o modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui um grupo para **executar ações em caso de falha**. Esse grupo inclui ações recomendadas para adicionar no caso do processo de atualização falha. Estas ações facilitam a resolução de problemas.

- **Recolher registos**: Para recolher os registos do cliente, adicione passos neste grupo.  

    - Uma prática comum é copiar os ficheiros de registo para uma partilha de rede. Para estabelecer esta ligação, utilize o [ligar à pasta de rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder) passo.  

    - Para efetuar a operação de cópia, usar um utilitário ou um script personalizado com o [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) ou [executar Script do PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript) passo.  

    - Ficheiros a recolher podem incluir os seguintes registos:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

    - Para obter mais informações no log e outros registos de configuração do Windows, consulte [ficheiros de registo de configuração do Windows](https://docs.microsoft.com/windows/deployment/upgrade/log-files).  

    - Para obter mais informações sobre registos de cliente do Configuration Manager, consulte [registos de cliente do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).  

    - Para obter mais informações sobre smstslogpath e outras variáveis útil, consulte [variáveis incorporadas de sequência de tarefas](/sccm/osd/understand/task-sequence-built-in-variables).  

- **Executar as ferramentas de diagnóstico**: Para executar as ferramentas de diagnóstico adicionais, adicione passos neste grupo. Automatize essas ferramentas para recolher informações adicionais do sistema logo após a falha.  

    - Uma dessas ferramentas é o Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). É uma ferramenta de diagnóstico de autónomo para obter detalhes sobre o motivo pelo qual uma atualização do Windows 10 foi concluída com êxito.  

        - No Configuration Manager, [criar um pacote](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) para a ferramenta.  

        - Adicionar uma [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo para este grupo da sequência de tarefas. Utilize o **pacote** opção para fazer referência a ferramenta. A seguinte cadeia de caracteres é um exemplo **linha de comandos**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  



## <a name="additional-recommendations"></a>Recomendações adicionais

- Consulte a documentação de Windows para [erros de atualização do Windows 10 resolver](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também contém informações detalhadas sobre o processo de atualização.  

- A predefinição **verificar disponibilidade** passo, ative **assegurar espaço mínimo livre em disco (MB)**. Defina, pelo menos, o valor como **16384** (16 GB) para um sistema operacional de 32 bits Atualize o pacote, ou **20480** (20 GB) de 64 bits.  

- Utilize o **SMSTSDownloadRetryCount** [variável de sequência de tarefas incorporadas](/sccm/osd/understand/task-sequence-built-in-variables) para transferir política de repetição. Atualmente por predefinição, o cliente tenta novamente duas vezes; Esta variável é definida como duas (2). Se seus clientes não estão numa conexão de rede com fio intranet, tentativas adicionais ajudam o cliente obter a política. Utilizar esta variável faz com que nenhum efeito negativo, que não seja atrasada falha se ele não é possível transferir a política.<!--501016--> Também aumentar o **SMSTSDownloadRetryDelay** variável da predefinição de 15 segundos.  

- Efetue uma avaliação de compatibilidade de inline:  

   - Adicione um segundo **atualizar sistema operativo** entrar no início do **preparar para a atualização** grupo. Atribua o nome *avaliação da atualização*. Especifique o pacote de atualização do mesmo e, em seguida, ativar a opção para **análise de compatibilidade de executar a configuração do Windows sem iniciar a atualização**. Ativar **continuar com o erro** no separador de opções.  

   - Imediatamente após isso *avaliação da atualização* passo, adicione um **executar linha de comandos** passo. Especifica a seguinte linha de comando:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Sobre o **opções** separador, adicione a seguinte condição: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de retorno é o equivalente decimal MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma análise de compatibilidade bem-sucedida sem problemas. Se o *avaliação da atualização* passo for concluída com êxito e devolve esse código, a sequência de tarefas ignore este passo. Caso contrário, se o passo de avaliação retornar qualquer outro código de retorno, este passo falha a sequência de tarefas com o código de retorno da análise de compatibilidade de configuração do Windows.  

   - Para obter mais informações, consulte [atualizar sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).  

- Se pretender alterar o dispositivo de BIOS para UEFI durante esta sequência de tarefas, consulte [converter BIOS para UEFI durante uma atualização in-loco](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).  

- Se estiver a utilizar encriptação de disco BitLocker, em seguida, por predefinição a configuração do Windows automaticamente suspende-lo durante a atualização. A partir do Windows 10 versão 1803, a configuração do Windows inclui o `/BitLocker` parâmetro da linha de comandos para controlar esse comportamento. Se os requisitos de segurança necessitar de manter a encriptação de disco ativa durante todo o tempo, em seguida, utilize o **OSDSetupAdditionalUpgradeOptions** variável de sequência de tarefas no **preparar para a atualização** grupo para incluir `/BitLocker TryKeepActive`. Para obter mais informações, consulte [opções de linha de comandos de configuração do Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#33).<!--SCCMDocs issue #494-->  

- Alguns clientes remover aplicações predefinidas aprovisionada no Windows 10. Por exemplo, a aplicação Bing meteorologia ou a coleção de paciência da Microsoft. Em algumas situações, estas aplicações devolvem depois de atualizar o Windows 10. Para obter mais informações, consulte [como manter as aplicações removidas do Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update). Adicionar uma **executar linha de comandos** passo à sequência de tarefas no **preparar para a atualização** grupo. Especifique uma linha de comando semelhante ao seguinte exemplo:</br> `cmd /c reg delete "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f` <!--SCCMDocs issue #526-->  
