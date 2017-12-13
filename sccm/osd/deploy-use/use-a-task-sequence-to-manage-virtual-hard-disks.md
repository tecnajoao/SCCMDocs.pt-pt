---
title: "Utilizar uma sequência de tarefas para gerir discos rígidos virtuais"
titleSuffix: Configuration Manager
description: "Criar e modificar um VHD, adicionar aplicações e atualizações de software e publicá-lo para o System Center Virtual Machine Manager (VMM) do Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
caps.latest.revision: "5"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 89e30f81648aff16de2f7db55cbdda06cf69551d
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/12/2017
---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>Utilizar uma sequência de tarefas para gerir discos rígidos virtuais no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No System Center Configuration Manager, pode gerir discos rígidos virtuais (VHDs) e integrar os VHDs que criar no seu centro de dados a partir da consola do Configuration Manager. Especificamente, pode criar e modificar um VHD, adicionar aplicações e atualizações de software ao VHD e publicá-lo para o System Center Virtual Machine Manager (VMM) da consola do Configuration Manager.  

 Utilize as secções seguintes para gerir VHDs no Configuration Manager.

## <a name="prerequisites"></a>Pré-requisitos  
 Antes de começar, verifique os seguintes pré-requisitos:  

-   O computador a partir do qual gere os VHDs tem de ter um dos seguintes sistemas operativos:  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   Virtualização tem de estar ativada no BIOS e Hyper-V tem de estar instalado no computador em que executa a consola do Configuration Manager para gerir os VHDs. Como procedimento recomendado, instale ainda as ferramentas de gestão de Hyper-V para o ajudar a testar e resolver problemas com os discos rígidos virtuais. Por exemplo, para monitorizar o ficheiro smsts.log para controlar o progresso da sequência de tarefas no Hyper-V, terá de ter as ferramentas de gestão de Hyper-V instaladas. Para mais informações sobre os requisitos do Hyper-V, consulte [Pré-requisitos de Instalação do Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!IMPORTANT]  
    >  O processo de criação de um VHD consome tempo do processador e memória. Por conseguinte, é recomendado que gere os VHDs a partir de uma consola do Configuration Manager que não está instalada no servidor do site.  

-   O servidor de site terá de ter permissão de acesso de **Escrita** à pasta que conterá o ficheiro VHD ao gerir VHDs a partir de um computador que seja remoto relativamente ao servidor de site.  

-   Verifique se tem espaço livre suficiente no disco do computador a partir do qual gere os VHDs. Os requisitos de espaço no disco rígido do VHD variam consoante o sistema operativo e as aplicações que instalar.  

-   Verifique se tem memória suficiente no computador a partir do qual gere os VHDs. Durante o processo de criação do VHD, a máquina virtual encontra-se configurada para consumir 2 GB de memória.  

-   Instale a consola do System Center Virtual Machine Manager (VMM) no computador a partir do qual carrega o VHD para o VMM. Poderá instalar a consola do VMM num computador separado daquele em que gere os VHDs, o que significa que não precisa de ter o Hyper-V instalado para importar o VHD para o VMM.  

    > [!NOTE]  
    >  Se instalar a consola do VMM enquanto a consola do Configuration Manager está aberta, tem de reiniciar a consola do Configuration Manager após a conclusão da instalação da consola do VMM. Caso contrário, o Configuration Manager não irá ligar com êxito ao servidor de gestão do VMM para carregar um VHD.  

##  <a name="BKMK_CreateVHDSteps"></a> Passos para Criar um VHD  
 Para criar um VHD, terá de criar uma sequência de tarefas que contenha os passos para criar o VHD, utilizando em seguida a sequência de tarefas do Assistente para Criar Discos Rígidos Virtuais para criar o VHD. As secções seguintes fornecem os passos para criar o VHD.  

###  <a name="BKMK_CreateTS"></a> Criar uma Sequência de Tarefas para o VHD  
 Terá de criar uma sequência de tarefas que contenha os passos para criar o VHD. No Assistente de Criação de Sequência de Tarefas encontra a opção **Instalar um pacote de imagem existente num disco rígido virtual** , que cria os passos a utilizar para criar o VHD. Por exemplo, o assistente adiciona os seguintes passos necessários: Reiniciar no Windows PE, formatar e particionar disco, aplicar sistema operativo e encerrar o computador. Não é possível criar o VHD a partir do sistema operativo completo. Além disso, o Configuration Manager tem de aguardar até que a máquina virtual seja encerrada para poder concluir o pacote. Por predefinição, o assistente aguarda 5 minutos até encerrar a máquina virtual. Depois de criar a sequência de tarefas poderá, se necessário, acrescentar passos adicionais.  

> [!IMPORTANT]  
>  O procedimento seguinte cria a sequência de tarefas utilizando a opção **Instalar um pacote de imagem existente num disco rígido virtual** , que inclui automaticamente os passos necessários para criar o VHD com êxito. Se optar por utilizar uma sequência de tarefas existente ou por criar manualmente uma sequência de tarefas, não se esqueça de adicionar o passo Encerrar o Computador no final da sequência de tarefas. Sem este passo, a máquina virtual temporária não será eliminada e o processo de criação do VHD não será concluído. No entanto, o assistente será concluído e informará que foi bem sucedido.  

 Utilize o procedimento seguinte para criar a sequência de tarefas de criação do VHD:  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>Para criar a sequência de tarefas de criação do VHD  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente de Criação de Sequência de Tarefas.  

4.  Na página **Criar uma Nova Sequência de Tarefas** , selecione **Instalar um pacote de imagem existente num disco rígido virtual**e clique em **Seguinte**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Nome da sequência de tarefas**: Especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: Especifique uma descrição da sequência de tarefas.  

    -   **Imagem de arranque**: Especifique a imagem de arranque que instala o sistema operativo no computador de destino. Para obter mais informações, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

6.  Na página **Instalar o Windows** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Pacote de imagem**: Especifique o pacote que contém a imagem do sistema operativo a instalar.  

    -   **Imagem**: Se o pacote de imagem do sistema operativo tiver várias imagens, especifique o índice da imagem do sistema operativo a instalar.  

    -   **Chave de produto**: Especifique a chave de produto para o sistema operativo do Windows instalar. Pode especificar chaves de licenciamento em volume codificadas e chaves de produto padrão. Se utilizar uma chave de produto não codificada, terá de separar cada grupo de 5 carateres por um hífen (-). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modo de licenciamento de servidor**: Especifique se a licença do servidor é **por posto**, **por servidor**, ou se for especificada qualquer licença. Se a licença do servidor for **Por servidor**, especifique também o número máximo de ligações de servidor.  

    -   Especifique como lidar com a conta de administrador utilizada quando a imagem de sistema operativo é implementada.  

        -   **Aleatoriamente gerar a palavra-passe de administrador local e desativar a conta nas plataformas suportadas (recomendado)**: Utilize esta definição para que o assistente aleatoriamente criar uma palavra-passe da conta de administrador local e desative a conta quando a imagem do sistema operativo é implementada.  

        -   **Ativar a conta e especificar a palavra-passe de administrador local**: Utilize esta definição para utilizar uma palavra-passe específica para a conta de administrador local em todos os computadores onde a imagem de sistema operativo é implementada.  

7.  Na página **Configurar Rede** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Aderir a um grupo de trabalho**: Especifique se pretende adicionar o computador de destino a um grupo de trabalho.  

    -   **Aderir a um domínio**: Especifique se pretende adicionar o computador de destino a um domínio. Em **Domínio**, especifique o nome do domínio.  

        > [!IMPORTANT]  
        >  Pode navegar para localizar domínios na floresta local, mas tem de especificar o nome de domínio de uma floresta remota.  

         Também pode especificar uma unidade organizacional (UO). Trata-se de uma definição opcional que especifica o nome único LDAP X.500 da UO em que deverá ser criada a conta de computador, caso ainda não exista.  

    -   **Conta**: Especifique o nome de utilizador e palavra-passe para a conta que possui permissões para aderir ao domínio especificado. Por exemplo: *domínio\utilizador* ou *%variable%*.  

8.  No **instalar Configuration Manager** página, especifique o pacote de cliente do Configuration Manager para instalar no computador de destino e, em seguida, clique em **seguinte**.  

9. Na página **Instalar Aplicações** , especifique as aplicações a instalar no computador de destino e clique em **Seguinte**. Se especificar várias aplicações, poderá também especificar que a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

10. Conclua o assistente.  

###  <a name="BKMK_CreateVHD"></a> Criar um VHD  
 Após criar uma sequência de tarefas para o VHD, utilize o Assistente para Criar Discos Rígidos Virtuais para criar o VHD.  

> [!IMPORTANT]  
>  Antes de executar este procedimento, certifique-se de que cumpre os pré-requisitos listados no início deste tópico.  

 Utilize o procedimento seguinte para criar um VHD.  

#### <a name="to-create-a-vhd"></a>Para criar um VHD  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Discos Rígidos Virtuais**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Disco Rígido Virtual** para iniciar o Assistente para Criar Discos Rígidos Virtuais.  

    > [!NOTE]  
    >  Hyper-V tem de estar instalado no computador que executa a consola do Configuration Manager a partir do qual gere os VHDs ou a **criar disco rígido Virtual** opção não está ativada. Para mais informações sobre os requisitos do Hyper-V, consulte [Pré-requisitos de Instalação do Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!TIP]  
    >  Para organizar os seus VHDs, crie uma nova pasta ou selecione uma pasta existente sob o nó **Discos Rígidos Virtuais** e clique em **Criar Disco Rígido Virtual** a partir da pasta.  

4.  Na página **Geral** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Nome**: Especifique um nome exclusivo para o VHD.  

    -   **Versão**: Especifique um número de versão para o VHD. Esta definição é opcional.  

    -   **Comentário**: Especifique uma descrição para o VHD.  

    -   **Caminho**: Especifique o nome de ficheiro e caminho para onde o assistente irá criar o ficheiro VHD.  

         Terá de introduzir um caminho de rede válido no formato UNC. Por exemplo:  **\\\servername\\< sharename\>\\< filename\>. vhd**.  

        > [!WARNING]  
        >  O Configuration Manager tem de ter **escrever** permissão para o caminho especificado para criar o VHD de acesso. Quando o Configuration Manager não conseguir aceder ao caminho, registará o erro associado no ficheiro distmgr.log, no servidor do site.  

5.  Na página **Sequência de Tarefas** , especifique a sequência de tarefas que especificou na secção anterior e clique em **Seguinte**.  

6.  Na página **Pontos de Distribuição** , selecione um ou vários pontos de distribuição que contenham o conteúdo exigido pela sequência de tarefas e clique em **Seguinte**.  

7.  Na página **Personalização** , clique em **Seguinte**. O processo de criação do VHD ignorará quaisquer definições que especifique nesta página.  

8.  Verifique as definições e clique em **Seguinte**. O assistente criará o VHD.  

    > [!TIP]  
    >  O tempo de execução do processo de criação do VHD poderá variar. Enquanto o assistente executa este processo, poderá monitorizar os seguintes ficheiros de registo para acompanhar o progresso. Por predefinição, os registos estão localizados no computador que executa a consola do Configuration Manager em %*ProgramFiles (x86)*%\Microsoft Configuration manager\adminconsole\adminuilog.  
    >   
    >  -   **CreateTSMedia.log**: O assistente escreve informações neste registo enquanto cria o suporte de dados de sequência de tarefas. Consulte este ficheiro de registo para acompanhar o progresso do assistente enquanto cria o suporte de dados autónomo.  
    > -   **DeployToVHD.log**: O assistente escreve informações neste registo enquanto executa o processo de criação do VHD. Consulte este ficheiro de registo para acompanhar o progresso do assistente enquanto cria o suporte de dados autónomo.  
    >   
    >  Além disso, quando a instalação do sistema operativo for iniciada, poderá abrir o Gestor de Hyper-V (se tiver instalado as ferramentas de gestão de Hyper-V no computador) e ligar à máquina virtual temporária criada pelo assistente para ver a sequência de tarefas em execução. Na máquina virtual poderá monitorizar o ficheiro smsts.log para acompanhar o progresso da sequência de tarefas. Se ocorrerem problemas ao executar um passo da sequência de tarefas, poderá utilizar este ficheiro de registo para o ajudar a resolver o problema. O ficheiro smsts.log encontra x: \windows\temp\smstslog\smsts.log antes do disco rígido formatado e c:\\_SMSTaskSequence\Logs\Smstslog\ após a formatação. Após a conclusão dos passos da sequência de tarefas, a máquina virtual será encerrada ao fim de 5 minutos (por predefinição) e eliminada.  

 Depois do Configuration Manager cria o VHD, este ficará localizado no **discos rígidos virtuais** nó na consola do Configuration Manager no **implementação do sistema operativo** no nó de **biblioteca de Software** área de trabalho.  

> [!NOTE]  
>  Configuration Manager obtém o tamanho do VHD estabelecendo ligação à localização de origem do VHD. Se o Configuration Manager não é possível aceder ao ficheiro VHD, **0** é apresentado no **tamanho (KB)** coluna para o VHD.  

##  <a name="BKMK_ModifyVHDSteps"></a> Passos para Modificar um VHD Existente  
 Para modificar um VHD, terá de criar uma sequência de tarefas com os passos necessários para modificar o VHD. Em seguida, selecione a sequência de tarefas no Assistente para Modificar Discos Rígidos Virtuais. O assistente anexa o VHD à máquina virtual, executa a sequência de tarefas no VHD e atualiza o ficheiro VHD. As secções seguintes fornecem os passos para modificar o VHD.  

###  <a name="BKMK_ModifyTS"></a> Criar uma Sequência de tarefas para Modificar o VHD  
 Para modificar um VHD existente, terá primeiro de criar uma sequência de tarefas. Escolha apenas os passos necessários para modificar a sequência de tarefas. Por exemplo, se pretender adicionar uma aplicação ao VHD, crie uma sequência de tarefas personalizada e adicione apenas o passo Instalar Aplicação.  

 Utilize o procedimento seguinte para criar a sequência de tarefas de modificação do VHD.  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>Para criar uma sequência de tarefas personalizada para modificar o VHD  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente de Criação de Sequência de Tarefas.  

4.  Na página **Criar uma Nova Sequência de Tarefas** , selecione **Criar uma nova sequência de tarefas personalizada**e clique em **Seguinte**.  

5.  Na página **Informações da Sequência de Tarefas** , especifique as seguintes definições e clique em **Seguinte**.  

    -   **Nome da sequência de tarefas**: Especifique um nome que identifique a sequência de tarefas.  

    -   **Descrição**: Especifique uma descrição da sequência de tarefas.  

    -   **Imagem de arranque**: Especifique a imagem de arranque que instala o sistema operativo no computador de destino. Para obter mais informações, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

6.  Conclua o assistente.  

 Utilize o procedimento seguinte para adicionar passos à sequência de tarefas personalizada.  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>Para adicionar passos à sequência de tarefas personalizada  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** expanda **Sistemas Operativos**, clique em **Sequências de Tarefas**e selecione a sequência de tarefas personalizada que criou no procedimento anterior.  

3.  No separador **Home Page** , no grupo **Sequência de Tarefas** , clique em **Editar** para iniciar o editor de sequência de tarefas.  

4.  Adicione os passos da sequência de tarefas a utilizar para modificar o VHD.  

5.  Clique em **OK** para sair do editor de sequência de tarefas.  

###  <a name="BKMK_ModifyVHD"></a> Modificar um VHD  
 Após criar uma sequência de tarefas para o VHD, utilize o Assistente para Modificar Discos Rígidos Virtuais para modificar o VHD.  

 Utilize o procedimento seguinte para modificar um VHD.  

#### <a name="to-modify-a-vhd"></a>Para modificar um VHD  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**, clique em **Discos Rígidos Virtuais**e selecione o VHD a modificar.  

3.  No separador **Home Page** , no grupo **Disco Rígido Virtual** , clique em **Modificar Disco Rígido Virtual** para iniciar o Assistente para Modificar Discos Rígidos Virtuais.  

    > [!NOTE]  
    >  Hyper-V tem de estar instalado no computador que executa a consola do Configuration Manager a partir do qual gere os VHDs ou a **modificar disco rígido Virtual** opção não está ativada. Para mais informações sobre os requisitos do Hyper-V, consulte [Pré-requisitos de Instalação do Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

4.  Na página **Geral** , confirme as seguintes definições e clique em **Seguinte**.  

    -   **Nome**: Especifica o nome exclusivo para o VHD.  

    -   **Versão**: Especifica o número de versão para o VHD. Esta definição é opcional.  

    -   **Comentário**: Especifica a descrição para o VHD.  

    -   **Caminho**: Especifica o nome de ficheiro e caminho para onde está localizado o ficheiro VHD. Não é possível modificar esta definição.  

        > [!WARNING]  
        >  O Configuration Manager tem de ter **escrever** permissão para o caminho especificado para criar o VHD de acesso. Quando o Configuration Manager não conseguir aceder ao caminho, registará o erro associado no ficheiro distmgr.log, no servidor do site.  

5.  Na página **Sequência de Tarefas** , especifique a sequência de tarefas personalizada que criou na secção anterior e clique em **Seguinte**.  

6.  Na página **Pontos de Distribuição** , selecione um ou vários pontos de distribuição que contenham o conteúdo exigido pela sequência de tarefas e clique em **Seguinte**.  

7.  Na página **Personalização** , clique em **Seguinte**. O processo de modificação do VHD ignorará quaisquer definições que especifique nesta página.  

8.  Verifique as definições e clique em **Seguinte**. O assistente criará o VHD modificado.  

    > [!TIP]  
    >  O tempo de execução do processo de modificação do VHD poderá variar. Enquanto o assistente executa este processo, poderá monitorizar os seguintes ficheiros de registo para acompanhar o progresso. Por predefinição, os registos estão localizados no computador que executa a consola do Configuration Manager em %*ProgramFiles (x86)*%\Microsoft Configuration manager\adminconsole\adminuilog.  
    >   
    >  -   **CreateTSMedia.log**: O assistente escreve informações neste registo enquanto cria o suporte de dados de sequência de tarefas. Consulte este ficheiro de registo para acompanhar o progresso do assistente enquanto cria o suporte de dados autónomo.  
    > -   **DeployToVHD.log**: O assistente escreve informações neste registo enquanto executa o processo de modificação do VHD. Consulte este ficheiro de registo para acompanhar o progresso do assistente enquanto cria o suporte de dados autónomo.  
    >   
    >  Além disso, pode abrir o Gestor de Hyper-V (se tiver instalado as ferramentas de gestão de Hyper-V no computador) e ligar à máquina virtual temporária criada pelo assistente para ver a sequência de tarefas em execução. Na máquina virtual poderá monitorizar o ficheiro smsts.log para acompanhar o progresso da sequência de tarefas. Se ocorrerem problemas ao executar um passo da sequência de tarefas, poderá utilizar este ficheiro de registo para o ajudar a resolver o problema. O ficheiro smsts.log encontra x: \windows\temp\smstslog\smsts.log antes do disco rígido formatado e c:\\_SMSTaskSequence\Logs\Smstslog\ após a formatação. Após a conclusão dos passos da sequência de tarefas, a máquina virtual será encerrada ao fim de 5 minutos (por predefinição) e eliminada.  

##  <a name="BKMK_ApplyUpdates"></a> Aplicar atualizações de software a um VHD  
 Periodicamente, são lançadas novas atualizações de software que são aplicáveis ao sistema operativo do VHD. Pode aplicar atualizações de software aplicáveis a um VHD numa agenda especificada. Na agenda que especificar, Gestor de configuração aplica-se as atualizações de software que selecionar para o VHD.  

 As informações sobre sobre o VHD são armazenadas na base de dados do site, incluindo as atualizações de software que foram aplicadas no momento em que criou o VHD. As atualizações de software aplicadas ao VHD desde que este foi inicialmente criado também são armazenadas na base de dados do site. Ao iniciar o assistente para aplicar as atualizações de software ao VHD, o assistente obtém uma lista de atualizações de software aplicáveis que ainda não foram aplicadas ao VHD para que possa selecioná-las.  

 Pode selecionar o **continuar com o erro** definição para o Configuration Manager para continuar a aplicar o software de atualizações, mesmo se ocorrer um erro ao aplicar uma ou mais o software de atualizações que selecionou.  

> [!NOTE]  
>  As atualizações de software são copiadas a partir da biblioteca de conteúdos no servidor do site.  

 Utilize o procedimento seguinte para aplicar atualizações de software ao VHD.  

#### <a name="to-apply-software-updates-to-a-vhd"></a>Para aplicar atualizações de software a um VHD  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Discos Rígidos Virtuais**.  

3.  Selecione o VHD para aplicar as atualizações de software.  

4.  No separador **Home Page** , no grupo **Disco Rígido Virtual** , clique em **Agendar Atualizações** para iniciar o assistente.  

5.  Na página **Escolher as Atualizações** , selecione as atualizações de software para aplicar no VHD e clique em **Seguinte**.  

6.  Na página **Definir Agendamento** , especifique as seguintes definições e clique em **Seguinte**.  

    1.  **Agenda**: Especifique o agendamento para quando as atualizações de software são aplicadas ao VHD.  

    2.  **Continuar com o erro**: Selecione esta opção para continuar a aplicar atualizações de software à imagem, mesmo se ocorrer um erro.  

7.  Na página **Resumo** , verifique as informações e clique em **Seguinte**.  

8.  Na página **Conclusão** , certifique-se de que as atualizações de software foram aplicadas com êxito na imagem do sistema operativo.  

##  <a name="BKMK_ImportToVMM"></a> Importar o VHD para o System Center Virtual Machine Manager  
 O System Center VMM é uma solução de gestão para o centro de dados virtualizado, que permite configurar e gerir o anfitrião de virtualização, o funcionamento em rede e os recursos de armazenamento para criar e implementar máquinas virtuais e serviços em nuvens privadas que criou. Depois de criar um VHD no Configuration Manager, pode importar e gerir o VHD utilizando o VMM.  

> [!TIP]  
>  Antes de carregar um VHD para o VMM, certifique-se de que a consola do VMM estabelece corretamente ligação com o servidor de gestão do VMM.  

 Utilize o procedimento seguinte para importar um VHD para o VMM.  

#### <a name="to-import-a-vhd-to-vmm"></a>Para importar um VHD para o VMM  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Discos Rígidos Virtuais**.  

3.  No separador **Home Page** , no grupo **Disco Rígido Virtual** , clique em **Carregar no Virtual Machine Manager** para iniciar o Assistente de Carregamento no Virtual Machine Manager.  

4.  Na página **Geral** , configure as seguintes definições e clique em **Seguinte**.  

    -   **Nome do servidor VMM**: Especifique o FQDN do computador no qual o servidor de gestão do VMM está instalado. O assistente liga ao servidor de gestão do VMM para transferir as partilhas de biblioteca para o servidor.  

    -   **Partilha de biblioteca VMM**: Especifique a partilha de biblioteca do VMM na lista pendente.  

    -   **Utilizar transferência não encriptada**: Selecione esta definição para transferir o ficheiro VHD para o servidor de gestão do VMM sem a utilização da encriptação.  

5.  Na página Resumo, verifique as definições e, em seguida, conclua o assistente. O tempo que demora a carregar o VHD varia consoante o tamanho do ficheiro VHD e a largura de banda de rede para o servidor de gestão do VMM.  
