---
title: 'Gerir imagens de arranque '
titleSuffix: Configuration Manager
description: "No Configuration Manager, saiba como gerir as imagens de arranque do Windows PE que utilizar durante a implementação do sistema operativo."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: "23"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 1f169dbf645096777f3fd244d24ca5be92efa180
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Gerir imagens de arranque com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma imagem de arranque no Configuration Manager é uma [Windows PE (WinPE)](https://msdn.microsoft.com/library/windows/hardware/dn938389%28v=vs.85%29.aspx) imagem que é utilizada durante a implementação do sistema operativo. As imagens de arranque são utilizadas para iniciar um computador no WinPE, que é um sistema operativo minimalista com componentes e serviços limitados que preparam o computador de destino para a instalação do Windows.  Utilize as secções seguintes para gerir imagens de arranque.

## <a name="BKMK_BootImageDefault"></a>Imagens de arranque predefinidas
Configuration Manager fornece duas imagens de arranque predefinidas: Uma para suportar plataformas x86 e outra para suportar x64 plataformas. Estas imagens estão armazenadas em: \\ \\ *servername*> \SMS_ <*sitecode*> \osd\boot\\<*x64*> ou <*i386*>. Imagens de arranque predefinidas são atualizadas ou regeneradas consoante a ação que efetuar.

Considere o seguinte para qualquer uma das ações descritas nas secções seguintes:
- Os objetos do controlador de origem tem de ser válidos, incluindo os ficheiros de origem do controlador ou os controladores não será adicionado às imagens de arranque no site.
- Imagens de arranque que não são baseadas nas imagens de arranque predefinidas, mesmo que utilizem a mesma versão do Windows PE, não serão modificadas.
- Necessitará de redistribuir as imagens de arranque modificado para pontos de distribuição.
- Tem de recriar qualquer suporte de dados que utiliza as imagens de arranque modificadas.
- Se não pretender que as imagens de arranque personalizadas/predefinidas atualizadas automaticamente, não armazene-os na localização predefinida.

> [!NOTE]
> A ferramenta de registo de rastreio do Configuration Manager é adicionada a todas as imagens de arranque que adiciona à **biblioteca de Software**. Quando estiver no Windows PE, pode iniciar a ferramenta de registo de rastreio do Configuration Manager escrevendo **CMTrace** numa linha de comandos.  

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Utilização de atualizações e manutenção para instalar a versão mais recente do Configuration Manager
A partir da versão 1702, quando atualizar a versão do Windows ADK e, em seguida, utilizar as atualizações e manutenção para instalar a versão mais recente do Configuration Manager, Configuration Manager gera de novo as imagens de arranque predefinidas. Isto inclui a nova versão do PE de janela do Windows ADK atualizado, a nova versão do cliente do Configuration Manager, controladores, personalizações, etc. Imagens de arranque personalizadas não são modificadas.

Antes de versão 1702, Configuration Manager atualiza a imagem de arranque (boot.wim) existente com os componentes de cliente, controladores, personalizações, etc., mas não irá utilizar a versão mais recente do Windows PE do Windows ADK. Tem de modificar manualmente a imagem de arranque para utilizar a nova versão do Windows ADK.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Atualização do Configuration Manager 2012 para o Configuration Manager atual Branch (CB)
Quando a atualização do Configuration Manager 2012 para CB do Configuration Manager, utilizando o processo de configuração, do Configuration Manager irá regenerar as imagens de arranque predefinidas. Isto inclui a nova versão do PE de janela do Windows ADK atualizado, a nova versão do cliente do Configuration Manager, e todas as personalizações permanecem inalteradas. Imagens de arranque personalizadas não são modificadas.

### <a name="update-distribution-points-with-the-boot-image"></a>Atualizar pontos de distribuição com a imagem de arranque
Quando utiliza o **atualizar pontos de distribuição** ação o **imagens de arranque** nó na consola do Configuration Manager, Configuration Manager atualiza a imagem de arranque de destino com os componentes de cliente controladores, personalizações, etc.    

A partir do Configuration Manager versão 1706, pode optar por recarregar a versão mais recente do Windows PE (a partir do diretório de instalação do Windows ADK) na imagem de arranque. O **geral** página do assistente atualizar pontos de distribuição fornece informações sobre a versão do Windows ADK instalada no servidor do site, a versão do Windows ADK partir do qual o Windows PE foi utilizado na imagem de arranque e a versão do cliente do Configuration Manager. Pode utilizar estas informações para ajudar a decidir se pretende recarregar a imagem de arranque. Além disso, uma nova coluna (**versão de cliente**) foi adicionado ao ver as imagens de arranque no **imagens de arranque** nó para saber qual a versão do cliente do Configuration Manager utiliza de cada imagem de arranque.    


##  <a name="BKMK_BootImageCustom"></a>Personalizar uma imagem de arranque  
 Pode personalizar uma imagem de arranque, ou [modificar uma imagem de arranque](#BKMK_ModifyBootImages), da consola do Configuration Manager quando se basear numa versão do Windows PE da versão suportada do Windows ADK. Quando um site é atualizado com uma nova versão e uma nova versão do Windows ADK estiver instalada, as imagens de arranque personalizadas (que não estejam na localização das imagens de arranque predefinidas) não são atualizadas com a nova versão do Windows ADK. Quando isso acontece, já não será possível personalizar as imagens de arranque na consola do Configuration Manager. No entanto, estas continuarão a funcionar como antes da atualização.  

 Quando uma imagem de arranque é baseada numa versão diferente do Windows ADK instalado num site, deve personalizar as imagens de arranque através de outro método, como a ferramenta de linha de comandos Gestão e Atualização de Imagens de Implementação (DISM) que faz parte do Windows AIK e do Windows ADK. Para obter mais informações, consulte [personalizar imagens de arranque](customize-boot-images.md).  

##  <a name="BKMK_AddBootImages"></a>Adicionar uma imagem de arranque  

 Durante a instalação de site do Configuration Manager adiciona automaticamente imagens de arranque baseadas numa versão do WinPE da versão suportada do Windows ADK. Dependendo da versão do Configuration Manager, poderá conseguir adicionar imagens de arranque baseadas numa versão do WinPE diferente da versão suportada do Windows ADK.  Ocorre um erro quando tenta adicionar uma imagem de arranque que contém uma versão não suportada do WinPE.  

 O seguinte fornece a versão suportada do Windows ADK, a versão do Windows PE nas quais se baseia a imagem de arranque que pode ser personalizada a partir da consola do Configuration Manager e as versões do Windows PE na qual se baseia a imagem de arranque que pode personalizar com o DISM e depois adicione a imagem para o Configuration Manager.  

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10  

-   **Versões do Windows PE para imagens de arranque personalizáveis a partir da consola do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE para imagens de arranque não podem ser personalizadas na consola do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> só é possível adicionar uma imagem de arranque para o Configuration Manager quando se baseia no Windows PE 3.1. Instale o Suplemento do Windows AIK para o Windows 7 SP1 para atualizar o Windows AIK para o Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Poderá transferir o Suplemento do Windows AIK para Windows 7 SP1 a partir do [Centro de Transferências da Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, quando tiver do Configuration Manager, pode personalizar imagens de arranque do Windows ADK para Windows 10 (baseado no Windows PE 10) na consola do Configuration Manager. No entanto, embora as imagens de arranque baseadas no Windows PE 5 sejam suportadas, tem de personalizá-las a partir de um computador diferente e utilizar a versão do DISM que é instalada com o Windows ADK para Windows 8. Em seguida, pode adicionar a imagem de arranque à consola do Configuration Manager. Para obter mais informações sobre os passos para personalizar uma imagem de arranque (adicionar componentes e controladores opcionais), ativar suporte de comando para a imagem de arranque, adicionar a imagem de arranque à consola do Configuration Manager e atualizar pontos de distribuição com a imagem de arranque, consulte [personalizar imagens de arranque](customize-boot-images.md).

 Utilize o procedimento seguinte para adicionar manualmente uma imagem de arranque.  

#### <a name="to-add-a-boot-image"></a>Para adicionar uma imagem de arranque  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

3.  No separador **Home Page**, no grupo **Criar**, clique em **Adicionar Imagem de Arranque** para iniciar o Assistente Adicionar Imagem de Arranque.  

4.  Na página **Origem de Dados**, especifique as seguintes opções e clique em **Seguinte**.  

    -   Na caixa **Caminho**, especifique o caminho do ficheiro WIM da imagem de arranque.  

         O caminho especificado tem de ser um caminho de rede válido no formato UNC. For example: \\\\<*servername*\\<*sharename*>\\<*bootimagename*>.wim.  

    -   Selecione a imagem de arranque na lista pendente **Imagem de Arranque**. Se o ficheiro WIM contiver várias imagens de arranque, selecione a imagem adequada.  

5.  Na página **Geral**, especifique as seguintes opções e clique em **Seguinte**.  

    -   Na caixa **Nome**, especifique um nome exclusivo para a imagem de arranque.  

    -   Na caixa **Versão**, especifique um número de versão para a imagem de arranque.  

    -   Na caixa **Comentário**, insira uma breve descrição do modo como a imagem de arranque é utilizada.  

6.  Conclua o assistente.  

 A imagem de arranque é agora listada no **imagem de arranque** nós da consola do Configuration Manager. No entanto, para poder utilizar a imagem de arranque para implementar um sistema operativo, tem de distribuir a imagem de arranque aos pontos de distribuição, grupos de pontos de distribuição ou coleções associadas a grupos de pontos de distribuição.  

> [!NOTE]  
>  Quando seleciona o **imagem de arranque** nó na consola do Configuration Manager, o **tamanho (KB)** coluna apresenta o tamanho descomprimido de cada imagem de arranque. No entanto, quando o Configuration Manager envia uma imagem de arranque através da rede, envia uma cópia comprimida da imagem, que é normalmente muito menor do que o tamanho listado no **tamanho (KB)** coluna.  

##  <a name="BKMK_DistributeBootImages"></a>Distribuir imagens de arranque para um ponto de distribuição  
 As imagens de arranque são distribuídas para pontos de distribuição da mesma forma que são distribuídos outros conteúdos. Na maioria dos casos, terá de distribuir a imagem de arranque para, pelo menos, um ponto de distribuição antes de implementar um sistema operativo e antes de criar suportes de dados.  

> [!NOTE]  
>  Para utilizar o PXE para implementar um sistema operativo, considere o seguinte antes de distribuir a imagem de arranque:  
>   
>  -   O ponto de distribuição tem de ser configurado para aceitar pedidos PXE.  
> -   Tem de distribuir uma imagem de arranque preparada para PXE x86 e x64 para, pelo menos, um ponto de distribuição preparado para PXE.  
> -   As imagens de arranque para o Configuration Manager distribui o **RemoteInstall** pasta no ponto de distribuição com PXE ativado.  
>   
>  Para obter mais informações sobre como utilizar o PXE para implementar sistemas operativos, consulte [utilizar o PXE para implementar o Windows através da rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Para obter os passos para distribuir uma imagem de arranque, veja [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a>Modificar uma imagem de arranque  
 Pode adicionar ou remover controladores de dispositivo da imagem ou editar as propriedades associadas à imagem de arranque. Os controladores de dispositivo que adicionar ou remover podem incluir controladores de placas de rede ou de dispositivos de armazenamento de massa. Ao modificar imagens de arranque, considere os seguintes fatores:  

-   Tem de importar e ativar os controladores de dispositivos no catálogo de controladores de dispositivos antes de poder adicioná-los à imagem de arranque.  

-   Quando modifica uma imagem de arranque, esta não altera nenhum dos pacotes associados aos quais a imagem de arranque faz referência.  

-   Depois de alterar uma imagem de arranque, tem de **atualizar** a imagem de arranque nos pontos de distribuição que já têm a imagem de arranque, para que esteja disponível a versão mais atual da imagem de arranque. Para obter mais informações, veja [Gerir conteúdo que distribuiu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

 Utilize o procedimento seguinte para modificar uma imagem de arranque.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Para modificar as propriedades de uma imagem de arranque  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

3.  Selecione a imagem de arranque que pretende modificar.  

4.  No separador **Home Page**, no grupo **Propriedades**, clique em **Propriedades** para abrir a caixa de diálogo **Propriedades** da imagem de arranque.  

5.  Defina qualquer uma das seguintes definições para alterar o comportamento da imagem de arranque:  

    -   No separador **Imagens**, se tiver alterado as propriedades da imagem de arranque com uma ferramenta externa, clique em **Recarregar**.  

    -   No separador **Controladores**, adicione os controladores de dispositivo Windows que são precisos para iniciar o WinPE. Quando adicionar controladores de dispositivo, considere o seguinte:  

        -   Selecione **Ocultar controladores que não correspondem à arquitetura da imagem de arranque** para apresentar apenas os controladores para a arquitetura da imagem de arranque. A arquitetura baseia-se na arquitetura reportada no .INF do fabricante.  

        -   Selecione **Ocultar controladores fora da classe de armazenamento ou de rede (para imagens de arranque)** para apresentar apenas controladores de armazenamento e de rede, e ocultar outros controladores que normalmente não são necessários para imagens de arranque, como um controlador de vídeo ou controlador de modem.  

        -   Selecione **Ocultar controladores que não estejam assinados digitalmente** para ocultar os controladores que não estão assinados digitalmente.  

        -   Como melhor prática, adicione apenas Controladores de NIC e de Armazenamento de Massa à imagem de arranque, a não ser que seja necessário incluir outros controladores no WinPE.  

        -   Uma vez que o WinPE é fornecido com muitos controladores incorporados, adicione apenas Controladores de NIC e de Armazenamento de Massa que não sejam fornecidos pelo WinPE.  

        -   Certifique-se de que os controladores que adiciona à imagem de arranque correspondem à arquitetura da imagem de arranque.  

        > [!NOTE]  
        >  Tem de importar controladores de dispositivo para o catálogo de controladores antes de os adicionar a uma imagem de arranque. Para obter informações sobre como importar controladores de dispositivo, consulte [gerir controladores](manage-drivers.md).  

    -   No separador **Personalização**, selecione qualquer uma das seguintes definições:  

        -   Selecione a caixa de verificação **Ativar Comando de Pré-início** para especificar a execução de um comando antes da execução da sequência de tarefas. Quando os comandos de pré-início são ativados, pode especificar a linha de comandos que é executada, se são necessários ficheiros de suporte para executar o comando e a localização de origem desses ficheiros de suporte.  

            > [!WARNING]  
            >  Tem de adicionar **cmd /c** ao início da linha de comandos. Se não especificar **cmd /c**, o comando não será fechado depois de ser executado. A implementação continua a aguardar que o comando seja concluído e não irá iniciar quaisquer outros comandos ou ações configurados.  

            > [!TIP]  
            >  Durante a criação de suportes de dados de sequência de tarefas, a sequência de tarefas escreve o ID de pacote e da linha de comandos, incluindo o valor das eventuais variáveis de sequência de tarefas, para o ficheiro de registo CreateTSMedia.log no computador que executa a consola do Configuration Manager de Pré-início. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

        -   Configure as definições de **Fundo do Windows PE** para especificar se pretende utilizar o fundo predefinido do WinPE ou um fundo personalizado.  

        -   Selecione **Ativar suporte de comando (apenas teste)** para abrir uma linha de comandos com a tecla **F8** quando a imagem de arranque estiver a ser implementada. Isto é útil para resolução de problemas quando estiver a testar a implementação. Não é aconselhada a utilização desta definição numa implementação de produção.  

        -   Configure o espaço scratch do Windows PE, que é armazenamento temporário (unidade de RAM) utilizado pelo WinPE. Por exemplo, quando uma aplicação é executada no WinPE e tem de escrever ficheiros temporários, o WinPE redireciona os ficheiros para o espaço scratch na memória, para simular a presença de um disco rígido. Por predefinição, o WinPE atribui 32 megabytes (MB) de memória gravável.  

    -   No separador **Origem de Dados**, atualize qualquer uma das seguintes definições:  

        -   Defina **Caminho da imagem** e **Índice de imagens** para alterar o ficheiro de origem da imagem de arranque.  

        -   Selecione **Atualizar pontos de distribuição com base num agendamento**, para criar um agendamento para a atualização do pacote de imagem de arranque.  

        -   Selecione **Manter conteúdo na cache do cliente** se não pretender que o conteúdo deste pacote seja eliminado da cache do cliente por antiguidade para disponibilizar espaço para outro conteúdo.  

        -   Selecione **Ativar replicação de diferencial binário** para especificar que apenas os ficheiros alterados serão distribuídos quando o pacote de imagem de arranque for atualizado no ponto de distribuição. Esta definição minimiza o tráfego de rede entre sites, especialmente quando o pacote de imagem de arranque for grande e as alterações forem relativamente pequenas.  

        -   Selecione **Implementar esta imagem de arranque a partir do ponto de distribuição ativado por PXE** se a imagem de arranque for utilizada numa implementação com PXE ativado.  

            > [!NOTE]  
            >  Para obter mais informações, consulte [utilizar o PXE para implementar o Windows através da rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   No separador **Acesso a Dados**, selecione qualquer uma das seguintes definições:  

        -   Configure as **Definições de partilha de pacote** se pretender que os clientes instalem o conteúdo deste pacote a partir da rede.  

        -   Definir o **definições de atualização do pacote** para especificar como pretende que o Configuration Manager para desligar os utilizadores a partir do ponto de distribuição. O Configuration Manager poderá ser incapaz de atualizar a imagem de arranque quando os utilizadores estão ligados ao ponto de distribuição.  

    -   No separador **Definições de Distribuição**, selecione qualquer uma das seguintes definições:  

        -   No **prioridade de distribuição** lista, especifique o nível de prioridade que pretende que o Configuration Manager para utilizar quando forem distribuídos vários pacotes ao mesmo ponto de distribuição.  

        -   Selecione **Distribuir o conteúdo do pacote pelos pontos de distribuição preferenciais** se pretender ativar a distribuição de conteúdo a pedido para pontos de distribuição preferenciais. Quando esta definição está ativada, o ponto de gestão distribui o conteúdo por todos os pontos de distribuição preferenciais quando um cliente solicita o conteúdo do pacote e o conteúdo não está disponível em nenhum desses pontos de distribuição.  

        -   Configure as **Definições pré-configuradas de ponto de distribuição** para especificar como pretende que a imagem de arranque seja distribuída pelos pontos de distribuição ativados para conteúdo pré-configurado.  

            > [!NOTE]  
            >  Para obter mais informações sobre conteúdo pré-configurado, veja [Pré-configurar conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   No separador **Localizações de Conteúdo**, selecione o ponto de distribuição ou o grupo de pontos de distribuição e execute qualquer uma das seguintes ações:  

        -   Clique em **Redistribuir** para distribuir novamente a imagem de arranque para o ponto de distribuição ou grupo de pontos de distribuição selecionado.  

        -   Clique em **Validar** para verificar a integridade do pacote de imagem de arranque no ponto de distribuição ou grupo de pontos de distribuição selecionado.  

    -   No **componentes opcionais** separador, especifique os componentes que são adicionados ao Windows PE para utilização com o Configuration Manager. Para mais informações sobre os componentes opcionais disponíveis, consulte [WinPE: Adicionar pacotes (referência de componentes opcionais)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx).  

    -   No separador **Segurança**, selecione um utilizador administrativo e altere as operações que este pode realizar.  

6.  Depois de configurar as propriedades, clique em **OK**.  

##  <a name="BKMK_BootImagePXE"></a>Configurar uma imagem de arranque para implementar a partir de um ponto de distribuição com PXE ativado  
 Antes de poder utilizar uma imagem de arranque para uma implementação de sistema operativo PXE, tem de configurar a imagem de arranque para implementar a partir de um ponto de distribuição ativado por PXE.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>Para configurar uma imagem de arranque para implementar a partir de um ponto de distribuição ativado por PXE  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

3.  Selecione a imagem de arranque que pretende modificar.  

4.  No separador **Home Page**, no grupo **Propriedades**, clique em **Propriedades** para abrir a caixa de diálogo **Propriedades** da imagem de arranque.  

5.  No separador **Origem de Dados**, selecione **Implementar esta imagem de arranque a partir do ponto de distribuição ativado por PXE**.  

    > [!NOTE]  
    >  Para obter mais informações, consulte [utilizar o PXE para implementar o Windows através da rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  Depois de configurar as propriedades, clique em **OK**.  

##  <a name="BKMK_BootImageLanguage"></a>Configurar vários idiomas para implementação de imagem de arranque  
 As imagens de arranque são independentes de idiomas. Isso permite utilizar uma imagem de arranque que apresentará o texto da sequência de tarefas em vários idiomas no WinPE, se incluir o suporte de idioma apropriado dos Componentes Opcionais do Windows PE e definir a variável de sequência de tarefas apropriada para indicar o idioma que pode ser visualizado. O idioma do sistema operativo que implementar é independente do idioma que será apresentado no WinPE, independentemente da versão do Configuration Manager. O idioma que é apresentado ao utilizador é determinado do seguinte modo:  

-   Quando um utilizador executa a sequência de tarefas a partir de um sistema operativo existente, o Configuration Manager utiliza automaticamente o idioma configurado para o utilizador. Quando a sequência de tarefas é executada automaticamente em resultado de um prazo de implementação obrigatório, o Configuration Manager utiliza o idioma do sistema operativo.  

-   Para implementações do sistema operativo que utilizam o PXE ou suporte de dados, pode definir o valor do ID de idioma na variável SMSTSLanguageFolder como parte de um comando de pré-início. Quando o computador inicia o WinPE, as mensagens são apresentadas no idioma que especificou na variável. Se ocorrer um erro ao aceder ao ficheiro de recursos do idioma na pasta especificada ou se não tiver definido a variável, as mensagens serão apresentadas no idioma do WinPE.  

    > [!NOTE]  
    >  Quando o suporte de dados estiver protegido por uma palavra-passe, o texto que solicita ao utilizador a palavra-passe é sempre apresentado no idioma do WinPE.  

 Utilize o procedimento seguinte para definir o idioma do WinPE para implementações do sistema operativo iniciadas por PXE ou suportes de dados.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Para definir o idioma do Windows PE para uma implementação do sistema operativo iniciada por suportes de dados ou por PXE  

1.  Certifique-se de que o ficheiro de recursos da sequência de tarefas adequado (tsres.dll) está na pasta de idioma correspondente do servidor do site antes de atualizar a imagem de arranque. Por exemplo, o ficheiro de recursos em inglês encontra-se na seguinte localização:  <*ConfigMgrInstallationFolder*>\OSD\bin\x64\00000409\tsres.dll.  

2.  Como parte do comando de pré-início, defina a variável de ambiente SMSTSLanguageFolder no ID de idioma apropriado. O ID de idioma deve ser especificado utilizando o formato decimal e não o hexadecimal. Por exemplo, para definir o ID de idioma do inglês, especifique o valor decimal 1033 em vez do valor hexadecimal 00000409 utilizado para o nome da pasta.  
